---
title: "LETSQL - Using DataFusion’s UDAFs to do ML Training: A Exploration"
source: https://www.letsql.com/posts/xgboost-udaf-ibis/
author:
  - "[[LETSQL]]"
published: 
created: 2025-03-04
description: Using DataFusion’s UDAFs to do pandas’s style groupby-apply for XGBoost model training
tags:
  - clippings
  - LETSQL
---
Welcome back to LETSQL’s exploration series! Today, we’re tackling a common yet complex challenge in data science workflows: enabling efficient groupby-apply operations, akin to pandas, within [DataFusion](https://arrow.apache.org/datafusion/). This capability is a key enabler for applying machine learning models, directly within our data processing pipelines leveraging database compute machinery. In this second blog post, we’ll teach DataFusion to do pandas style `groupby-apply` aggregation rather than accumulation. To demonstrate the capability, we use a simple XGBoost model that gets trained on each group and outputs top features for the trained model. Then we’ll demonstrate how we’re able to use the same underlying python aggregation function in both pandas and DataFusion, towards the goal of a multi-engine DataFrame API.

You can find the complete code on [GitHub](https://github.com/letsql/xgboost-udaf-ibis).

## Introduction

![split-apply-combine](https://www.letsql.com/posts/xgboost-udaf-ibis/images/groupby-apply-udaf.png) User-Defined Aggregate Functions (`udaf`) are emerging as essential tools for sophisticated data analytics on a subset of data. In this post, we use XGboost model training as an example of a complex operation that is well-suited for the UDAFs computation. However, there are two challenges:

1. Creating a UDAF often involves hardcoding the aggregation computation process.
2. UDAF’s operations are generally not fully transparent to the query processor, limiting the system’s ability to optimize queries effectively. These challenges underscore the need for a more flexible and efficient approach to aggregating data, which we aim to address through our work with DataFusion.

Many systems provide `udaf` functionality via [accumulators](https://en.wikipedia.org/wiki/Accumulator_\(computing\)) which receive incremental subsets of the data rather than all of it once. This can be more efficient if your operation is expressible as an accumulation (think of something like a [sufficient statistic](https://en.wikipedia.org/wiki/Sufficient_statistic)). However, for many modeling use cases, we need simultaneous access to all of the data to be processed. Our use case is gradient boosting via XGBoost, which does indeed need all the data at once.

## Problem Statement

We have some loan data and want to find how the most salient features for predicting a target vary over time: training one XGBoost model per year to get the `n` “best features” per year.

We’d like the user experience to look as close as possible to pandas. Below is our pseudo-code target for how we might do it in pure pandas, how it changes when we do it in pandas via Ibis, and how we’d like to be able to do it in DataFusion via Ibis. We’ll use this as a guide to build our library.

```python
# pure pandas
from_pandas = (
    pd.read_parquet(path)[cols]
    .groupby(by)
    .apply(calc_best_features)
)

# pandas-via-ibis
pandas_t = ibis.pandas.connect().read_parquet(path, "t")[cols]
pandas_udaf = make_pandas_udf(
    pandas_t,
    calc_best_features,
    ibis_output_type,
)
pandas_expr = (
    pandas_t
    .group_by(by)
    .agg(pandas_udaf(pandas_t).name("best_features"))
)
from_pandas_ibis = pandas_expr.execute()

# datafusion-via-ibis
datafusion_t = ibis.datafusion.connect().read_parquet(path, "t")[cols]
datafusion_udaf = make_datafusion_udaf(
    datafusion_t,
    calc_best_features,
    PyArrowType.from_ibis(ibis_output_type),
)
datafusion_expr = (
    datafusion_t
    .group_by(by)
    .agg(datafusion_udaf(datafusion_t).name("best_features"))
)
from_datafusion_ibs = datafusion_expr.execute()
```

And here’s code for a toy model that fleshes out the pure pandas pseudo code[<sup>1</sup>](https://www.letsql.com/posts/xgboost-udaf-ibis/#fn1)

toy model code

```python
def train_xgboost_model(df, features, target, seed=0):
    if "rownum" in df:
        df = df.sort_values("rownum", ignore_index=True)
    param = {"max_depth": 2, "eta": 1, "objective": "binary:logistic", "seed": seed}
    num_round = 10
    X = df[list(features)]
    y = df[target]
    dtrain = xgb.DMatrix(X, y)
    bst = xgb.train(param, dtrain, num_boost_round=num_round)
    return bst

def calc_best_features(df, candidates, target, n):
    return (
        pd.Series(
            train_xgboost_model(df, candidates, target)
            .get_score()
        )
        .tail(n)
        .pipe(lambda s: tuple(
            {"feature": k, "score": v}
            for k, v in s.items()
        ))
    )

curried_calc_best_features = toolz.curry(
    calc_best_features, candidates=candidates, target=target, n=n,
)
from_pandas = (
    pd.read_parquet(path)[cols]
    .groupby(by)
    .apply(curried_calc_best_features)
)
```

Our goal is to teach DataFusion how to use the same `curried_calc_best_features` function for DataFusion.

## Interlude

![ibis-datafusion](https://www.letsql.com/posts/xgboost-udaf-ibis/images/ibis-datafusion.png) We’ll use Ibis to target both pandas and DataFusion. Ibis aims to be [**the** portable Python dataframe library](https://ibis-project.org/posts/why-voda-supports-ibis/), allowing you to specify your computation once and target multiple engines, including query engines like DataFusion, and pandas. It is designed to be a high-level API for data manipulation and analysis, and can be used to build complex data processing pipelines.

In our case, we are using Ibis to register UDAFs with DataFusion and pandas, generate a deferred expression in a similar API to pandas and execute them on multiple backends. This requires us to register a `udaf` with Ibis for each backend.

For the pandas backend, we can automate `udaf` registration for a function with a known input table like this

pandas udaf registration

```python
def make_pandas_udf(t, f, output_type):
    schema = t.schema()
    input_type = [schema[c] for c in t.columns]

    @reduction(
        input_type=input_type,
        output_type=output_type,
    )
    def f_on_series(*args):
        df = pd.DataFrame({series.name: series for series in args})
        return f(df)

    def udf_on_t(t):
        return f_on_series(*(t[col] for col in schema))

    return udf_on_t
```

We’d like to be able to create the `udaf` and invoke Ibis with the DataFusion backend in a similar way.

## Implementation

We know what we want the user experience to feel like, but what is the DataFusion baseline?

Per the [DataFusion example](https://arrow.apache.org/datafusion-python/user-guide/common-operations/udf-and-udfa.html) of a `udaf`, first, you define a class that inherits from `Accumulator`

DataFusion example: class definition

```python
class MyAccumulator(Accumulator):
    """
    Interface of a user-defined accumulation.
    """
    def __init__(self):
        self._sum = pyarrow.scalar(0.0)

    def update(self, values: pyarrow.Array) -> None:
        # not nice since pyarrow scalars can't be summed yet. This breaks on \`None\`
        self._sum = pyarrow.scalar(self._sum.as_py() + pyarrow.compute.sum(values).as_py())

    def merge(self, states: pyarrow.Array) -> None:
        # not nice since pyarrow scalars can't be summed yet. This breaks on \`None\`
        self._sum = pyarrow.scalar(self._sum.as_py() + pyarrow.compute.sum(states).as_py())

    def state(self) -> pyarrow.Array:
        return pyarrow.array([self._sum.as_py()])

    def evaluate(self) -> pyarrow.Scalar:
        return self._sum
```

You then register this class with DataFusion, specifying additional information (some types and volatility)

DataFusion example: class registration

```python
my_udaf = udaf(
    MyAccumulator,
    pyarrow.float64(),
    pyarrow.float64(),
    [pyarrow.float64()],
    'stable',
)
```

We can’t / don’t want to `update` and `merge` models, so what’s to be done? We could try to accumulate the rows into a `ListArray<Struct>`, but this would be computationally costly (think of it like doing a transpose, only worse). Instead, we’ll accumulate the data as serialized `RecordBatch`s. This is surprisingly cheap because of the underlying `Arrow` representation.

A first pass at our Accumulator might look something like this

Accumulator first pass

```python
class BestFeatureCalculator(Accumulator, ABC):

    def __init__(self):
        self._states = []

    def pystate(self):
        struct_arr = pa.concat_arrays(map(pickle.loads, self._states))
        df = pa.Table.from_batches(
            [pa.RecordBatch.from_struct_array(struct_arr)]
        ).to_pandas()
        return df

    def state(self):
        value = pa.array(
            [self._states],
        )
        return value

    def pyevaluate(self):
        return curried_calc_best_features(
            self.pystate()
        )

    def evaluate(self):
        return pa.scalar(
            self.pyevaluate(),
            type=pa.list_(
                pa.struct(
                    (
                        ("feature", pa.string()),
                        ("score", pa.float64()),
                    )
                )
            ),
        )

    def update(self, *arrays) -> None:
        state = pa.StructArray.from_arrays(
            arrays,
            names=column_names,
        )
        self._states.append(pickle.dumps(state))

    def merge(self, states: pa.Array) -> None:
        for state in states.to_pylist():
            self._states.extend(state)
```

What’s happening here?

- `_states` is a list of serialized `StructArray`
- `state` simply returns the accumulator’s list of serialized `StructArray`, `_states`, cast into its `pyarrow` type
- `update` combines the columns’ `RecordBatch`s into a single `StructArray`, serializes it with python’s `pickle` and extends `_states`
- `merge` simply extends `_states` with other `Accumulator`s’ `_states`
- `pystate` converts all the data in `_states` into a single pandas DataFrame
- `pyevaluate` is where the computation **actually happens**: invoke our pure pandas style function on the DataFrame returned by `pystate`
- `evaluate` invokes `pyevaluate` and casts it’s return value to `return_type`

## Stay [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), my friendsNote that almost everything here is boiler-plate with exception of

- Our aggregation function: `curried_calc_best_features`
- The `pyarrow` type used to cast in `evaluate`
- The variable `column_names` used by `update`

Note also that we have to coordinate names and types between the Ibis table, `udaf` definition, and `udaf` invocation.

Let’s combine all of this into a single function that dynamically generates a class and registers it with both DataFusion and Ibis.

The Datafusion related section of our final library code will look like this

DataFusion related library code

```python
class PyAggregator(Accumulator, ABC):
    """Variadic aggregator for udafs"""

    def __init__(self):
        self._states = []

    def pystate(self):
        struct_arr = pa.concat_arrays(map(pickle.loads, self._states))
        df = pa.Table.from_batches(
            [pa.RecordBatch.from_struct_array(struct_arr)]
        ).to_pandas()
        return df

    def state(self):
        value = pa.array(
            [self._states],
            type=self.state_type,
        )
        return value

    @abstractmethod
    def pyevaluate(self):
        pass

    def evaluate(self):
        return pa.scalar(
            self.pyevaluate(),
            type=self.return_type,
        )

    def update(self, *arrays) -> None:
        state = pa.StructArray.from_arrays(
            arrays,
            names=self.names,
        )
        self._states.append(pickle.dumps(state))

    def merge(self, states: pa.Array) -> None:
        for state in states.to_pylist():
            self._states.extend(state)

    def supports_retract_batch(self):
        return False

    @classmethod
    @property
    def names(cls):
        return tuple(field.name for field in cls.struct_type)

    @classmethod
    @property
    def input_type(cls):
        return list(field.type for field in cls.struct_type)

    @classmethod
    @property
    @abstractmethod
    def return_type(cls):
        pass

    @classmethod
    @property
    @abstractmethod
    def struct_type(cls):
        return pa.struct(())

    @classmethod
    @property
    def state_type(cls):
        return pa.list_(pa.binary())

    @classmethod
    @property
    def volatility(cls):
        return "stable"

    @classmethod
    @property
    def name(cls):
        return cls.__name__.lower()

    @classmethod
    def register_udaf(cls, ctx):
        if not isinstance(cls.input_type, Iterable) or not all(
            isinstance(el, pa.DataType) for el in cls.input_type
        ):
            raise ValueError(
                f"{cls.__name__}.input_type must be iterable of pa.DataType"
            )

        def register_ibis_reduction_f(cls):
            @translate_val.register(ReductionVectorizedUDF)
            def _fmt(op, **kw):
                return F[op.func.__name__](*kw["func_args"])

            class Klass(ReductionVectorizedUDF):
                pass

            @reduction(
                input_type=[dt.core.from_pyarrow(el) for el in cls.input_type],
                output_type=dt.core.from_pyarrow(cls.return_type),
            )
            def ibis_reduction_f(*args, where=None):
                return Klass(*args, where=where).to_expr()

            ibis_reduction_f.func.__name__ = cls.name

            def udf_on_t(t):
                return ibis_reduction_f(*(t[col] for col in cls.names))

            return udf_on_t

        ctx.register_udaf(
            udaf(
                cls,
                cls.input_type,
                cls.return_type,
                [cls.state_type],
                cls.volatility,
                cls.name,
            )
        )
        ibis_reduction_f = register_ibis_reduction_f(cls)

        return ibis_reduction_f

def make_struct_type(t):
    return pa.struct(
        (
            pa.field(
                field_name,
                t[field_name].type().to_pyarrow(),
            )
            for field_name in t.columns
        )
    )

def make_tokenized_name(*args, prefix="my_udaf_", length=8):
    return f"{prefix}{dask.base.tokenize(*args)[:length]}"

def make_datafusion_udaf(
    t, df_to_value, return_type, name=None,
):
    struct_type = make_struct_type(t)
    if name is None:
        name = make_tokenized_name(df_to_value, return_type, struct_type)

    class MyAggregator(PyAggregator):

        def pyevaluate(self):
            return df_to_value(self.pystate())

        @classmethod
        @property
        def return_type(cls):
            return return_type

        @classmethod
        @property
        def struct_type(cls):
            return struct_type

        @classmethod
        @property
        def name(cls):
            return name

    udaf = MyAggregator.register_udaf(t._find_backend().con)

    return udaf
```

Now, via `make_datafusion_udaf`, we only need to provide

- the Ibis table the `udaf` will be invoked on (used to extract names and types)
- the function to invoke on each group’s pandas DataFrame
- the return type of the function

We can optionally provide a name for the `udaf` that DataFusion uses internally and Ibis will use for the `SQL` string it generates for the DataFusion backend.

## But, does it work?

Ok, let’s invoke this on some real data! We’ll use the LendingClub data from [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club/download?datasetVersionNumber=3) and try to determine which features are predictive of a loan not being “Fully Paid” by the end of its standard term (which we’ve already massaged into the data our target variable called `event_occurred` as well as some other derived variables like `dti` and `cr_age_days`).

Code

```python
import warnings

import ibis
import ibis.expr.datatypes as dt
import pandas as pd
import toolz
from ibis.formats.pyarrow import PyArrowType

from letsql.examples.pyaggregator import (
    calc_best_features,
    make_datafusion_udaf,
    make_pandas_udf,
)

def join_splat(df, col):
    return (
        df
        .drop(col, axis=1)
        .join(
            df
            [col]
            .apply(lambda x: pd.Series({
                f"{k}{i}": v
                for (i, dct) in enumerate(x)
                for k, v in dct.items()
            }))
        )
    )

path = "data.rownum.parquet"
candidates = (
    "emp_length",
    "dti",
    "annual_inc",
    "loan_amnt",
    "fico_range_high",
    "cr_age_days",
)
by = "issue_y"
target = "event_occurred"
cols = list(candidates) + [by, target, "rownum"]
curried_calc_best_features = toolz.curry(
    calc_best_features, candidates=candidates, target=target, n=2
)
ibis_output_type = dt.infer(({"feature": "feature", "score": 0.},))

pandas_t = ibis.pandas.connect().read_parquet(path, "t")[cols]
pandas_udaf = make_pandas_udf(
    pandas_t,
    curried_calc_best_features,
    ibis_output_type,
)
pandas_expr = (
    pandas_t
    .group_by(by)
    .agg(pandas_udaf(pandas_t).name("best_features"))
)

datafusion_t = ibis.datafusion.connect().read_parquet(path, "t")[cols]
datafusion_udaf = make_datafusion_udaf(
    datafusion_t,
    curried_calc_best_features,
    PyArrowType.from_ibis(ibis_output_type),
)
datafusion_expr = (
    datafusion_t
    .group_by(by)
    .agg(datafusion_udaf(datafusion_t).name("best_features"))
)

with warnings.catch_warnings():
    warnings.simplefilter("ignore")
    from_pandas_ibis = (
        pandas_expr
        .execute()
        .sort_values(by, ignore_index=True)
        .pipe(join_splat, "best_features")
    )
    from_datafusion_ibis = (
        datafusion_expr
        .execute()
        .sort_values(by, ignore_index=True)
        .pipe(join_splat, "best_features")
    )
    from_pandas = (
        pd.read_parquet(path)[cols]
        .groupby(by)
        .apply(curried_calc_best_features)
        .rename("best_features").reset_index()
        .pipe(join_splat, "best_features")
    )

assert from_pandas.equals(from_pandas_ibis)
assert from_pandas.equals(from_datafusion_ibis)
print(from_pandas)
```

```python
   issue_y         feature0  score0     feature1  score1
0     2007  fico_range_high    12.0  cr_age_days    23.0
1     2008  fico_range_high    18.0  cr_age_days    29.0
2     2009  fico_range_high    17.0  cr_age_days    31.0
3     2010  fico_range_high    15.0  cr_age_days    29.0
4     2011  fico_range_high    21.0  cr_age_days    22.0
5     2012  fico_range_high    26.0  cr_age_days    24.0
6     2013  fico_range_high    23.0  cr_age_days    28.0
7     2014  fico_range_high    21.0  cr_age_days    28.0
8     2015  fico_range_high    27.0  cr_age_days    26.0
```

### New Possibilities

Now that we have the infrastructure to create scalar values that are in fact multiple rows, we could conceivably create rows that represent all the data from a group, allowing us to run analytic window functions over time periods: a rolling regression that outputs one model per month with the trailing 12 months as training data. Moreover, now that the UDAF is part of the DataFusion’s planning layer, it opens the possibilities for optimization by rewriting the plan with a specialized operator. But we’ll leave this digression for another time.

### Conclusion

We’ve taught DataFusion how to do pandas style aggregation[<sup>2</sup>](https://www.letsql.com/posts/xgboost-udaf-ibis/#fn2), we’ve demonstrated the ability to use the same function for both a pandas groupby-apply and datafusion-python’s groupby-apply (by way of Ibis) and we’ve laid the groundwork for doing windows-over-groups.

**Why DataFusion**: DataFusion’s UDF capabilities offer a game-changing advantage in the world of data science. By enabling SQL users to tap into powerful ML pipelines, we bridge the gap between data manipulation and data analysis. This is a huge win for data scientists and data analysts who can now use their existing SQL skills to build and deploy ML pipelines. Moreover, DataFusion provides the building blocks and primitives to be able to utilize the optimizations without diving too deep into database internals or recreating the foundations for a new database. In LETSQL’s case, we are extending DataFusion to add ML focused UDFs and new DataTypes that are amenable to Tensor processing, necessary for performing ML.

**The Power of SQL in Data Science**: SQL’s declarative nature and widespread adoption make it an indispensable tool in the data science toolkit. Our efforts aim to simplify the integration of complex data processes into SQL, enhancing accessibility and efficiency across data workflows.

### Future work: LETSQL

As we continue to refine our DataFrame API, future explorations will delve into end-to-end optimization of machine learning pipelines, leveraging the insights gained from this and our recent post on [XGBoost scoring with UDFs](https://letsql.dev/posts/xgboost-scoring-pipeline/). Stay tuned for our next installment, where we’ll unveil new advancements in making data science more accessible, efficient, and powerful than ever before.

Your thoughts and feedback are invaluable as we navigate this journey. Share your experiences, questions, or suggestions in the comments below or on our community forum. Together, let’s redefine the boundaries of data science and machine learning integration.

To subscribe to our newsletter, visit [letsql.dev](https://letsql.dev/).

1. XGBoost can give you deterministic results for the same input with seed control. One wrinkle is that DataFusion’s accumulation process results in a different ordering of the data than in pandas. To get the same results, we add a column, `rownum` that we can sort by to ensure the same XGBoost input order.[↩︎](https://www.letsql.com/posts/xgboost-udaf-ibis/#fnref1)
2. Along the way, we also had to teach DataFusion how to [build a struct with non-uniform field types](https://github.com/apache/arrow-datafusion/pull/8463) and how to [accept `udf`s with multiple column input](https://github.com/apache/arrow-datafusion-python/pull/546)[↩︎](https://www.letsql.com/posts/xgboost-udaf-ibis/#fnref2)