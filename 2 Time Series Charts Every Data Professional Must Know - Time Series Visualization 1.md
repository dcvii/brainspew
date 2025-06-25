---
title: "2 Time Series Charts Every Data Professional Must Know - Time Series Visualization #1"
source: "https://darioradecic.substack.com/p/time-series-data-visualization"
author:
  - "[[Dario Radecic]]"
published: 2024-09-06
created: 2025-03-24
description: "Make stunning line charts and area plots for one or multiple time series datasets."
tags:
  - "clippings"
---
### Make stunning line charts and area plots for one or multiple time series datasets.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0dc02fdf-615b-48d7-9099-7004d6e8ea6c_1500x1000.png)

Article thumbnail (image by author)

Do you know what’s the most common type of data companies collect?

They have it in all databases. They use it to create reports. They make forecasts and decisions based on it. Surprise, surprise - it’s time series data. In other words, it’s any type of data that’s **stored with a timestamp at regular intervals**.

As a data professional, you must know how to work with time series datasets. No way around it. Visualization is the best first step because it uncovers more insight than your typical skim of tabular data would.

This article will teach you the ins and outs of visualizing time series with Python and Matplotlib.

## Where to Get the Data?

I’m using the Light Weight Vehicle Sales dataset from [FRED](https://fred.stlouisfed.org/series/LTOTALNSA), and loading it to Python with the following command:

```markup
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv("../data/LTOTALNSA.csv", index_col="DATE", parse_dates=True)
data.head()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8611f10f-68ad-4927-b075-a3f3b961afc1_536x466.heic)

Image 1 - Light weight vehicle sales dataset (image by author)

The dataset has dates for an index and float values for the only attribute.

In other words, it’s fully prepared for visualization.

## Everything You Need to Know About Time Series Data Visualization

This section goes through line and area charts but also discusses essential chart elements - title, axis labels, legends, and so on.

To make your charts visually appealing, I recommend following my [3 Things You Must Change to Make Your Charts Stand Out](https://open.substack.com/pub/darioradecic/p/you-need-to-fix-these-3-things-right?r=48ma0u&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true) article.

### Title and Axis Labels

Without a title and axis labels, the reader doesn’t know what they’re looking at.

It can be sales data. It could be stock price. It could your heart rate throughout the day. Without these elements, you’re only guessing. There’s no way to be certain.

Luckily, adding a title and axis labels is straightforward:

```markup
plt.plot(data, color="#1C3041")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff4fabb85-fac1-4719-a847-2b19d47466f2_2504x1634.heic)

Image 2 - Adding title and axis labels (image by author)

You could leave the title center aligned, but I prefer it on the left. It’s more natural and has better flow.

### Subsetting Time Series Plots

The time series chart we have so far is a bit crammed.

To mitigate, you could change the `figsize()`, or you could focus on an area of interest. Let’s go with the latter.

The dataset uses a date column for the index, which means you can zoom into a certain part by using Python’s slicing notation. Just pass in dates as strings and you’ll be good to go.

Everything else remains unchanged:

```markup
subset = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
plt.plot(subset, color="#1C3041")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff168a8f8-45a7-4244-994b-f8a90155bdb6_2556x1646.heic)

Image 3 - Plotting a subset (image by author)

Getting there.

### Line Width and Style

The default line width might be too thin for some folk. Others might think a regular line is too boring.

Whichever the case might be, you have options. The `linewidth` and `linestyle` parameters can be tweaked to spice things up. The prior controls the width of the line, and the latter is used to change the [style](https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html), for example, to dots, dashes, or something else.

The following code snippet tweaks both:

```markup
subset = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
plt.plot(subset, color="#1C3041", linewidth=3, linestyle="dashdot")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4bc97c9f-312e-4fa7-a31d-cef246273315_2492x1640.heic)

Image 4 - Changing line width and style

I prefer my line charts solid and a bit thinner. You do you.

### Area Charts

There are cases when a line chart feels too boring.

Filling the area between the line to the bottom of the y-axis (0) is a good way to spice things up. Use the `plt.fll_between()` function to do so. It’s a good practice to specify color and opacity (alpha), so you’re not surprised with Matplotlib’s default blue color.

Let’s stick to the line color, but reduce the opacity way down:

```markup
subset = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
plt.plot(subset, color="#1C3041")
plt.fill_between(subset.index, subset.values, color="#1C3041", alpha=0.3)

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3718e074-c51d-4ab6-a620-b2b47463c1ea_2438x1640.heic)

Image 5 - Area chart in Matplotlib (image by author)

Another cool party trick with area plots is custom [hatches](https://matplotlib.org/stable/gallery/shapes_and_collections/hatch_style_reference.html).

These will essentially add a pattern to the filled area. It’s worth noting that the pattern can be difficult to spot when the `alpha` parameter is set too low, or when you’re using a color that blends in with the pattern.

The overall effect is cool, so it’s worth playing around with it for a while:

```markup
subset = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
plt.plot(subset, color="#1C3041")
plt.fill_between(subset.index, subset.values, color="#1C3041", alpha=0.6, hatch="//", edgecolor="black")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6add8a83-92c0-4211-8b1a-5d0d2f0d1465_2446x1640.heic)

Image 6 - Adding a hatch pattern to area plots (image by author)

There are [10 patterns](https://matplotlib.org/stable/gallery/shapes_and_collections/hatch_style_reference.html) to choose from. You can combine them and increase their density to match your preference.

### Splines - Make Your Line Plots Smooth

Ever noticed how line/area charts on most dashboards are smooth?

That has nothing to do with the underlying data. It has everything to do with fitting a spline to your X and Y values and adding more data points (linearly spaced) to make the curve smoother.

Implementing a spline in Python requires you to extract X and Y features and ditch the date component in favor of a range. It’s worth the effort if you ask me.

You can always manually tweak axis ticks if needed:

```markup
import numpy as np
from scipy.interpolate import make_interp_spline

subset = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
# We need a list of integers now instead of dates
x = np.arange(len(subset))
y = subset.values

# Make a spline with 500 points
spline = make_interp_spline(x, y)
x_plot = np.linspace(0, len(x), 500)
y_plot = spline(x_plot)

plt.plot(x_plot, y_plot, color="#1C3041")
plt.fill_between(x_plot, y_plot, color="#1C3041", alpha=0.6, hatch="//", edgecolor="black")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb6c584b5-cf32-4ad3-a502-2f4c5890850b_2474x1634.heic)

Image 7 - Making a plot line smooth (image by author)

One more thing to cover and then you’ll be good to go.

### Multiple Line Plots

Let’s say you want to plot history data and predictions. How can you go about it?

Simple add multiple calls to `plt.plot()`. The example below pretends you’re plotting history data and predictions, when in reality, it plots different subsets of the same dataset. But you get the point.

It’s useful to add labels to individual plots and then call `plt.legend()` at the end. This way, you know which line represents what:

```markup
history = data["LTOTALNSA"]["1990-01-01":"1999-12-01"]
prediction = data["LTOTALNSA"]["2000-01-01":"2001-12-01"]

plt.plot(history, color="#1C3041", label="History")
plt.plot(prediction, color="#BA5E09", label="Prediction")

plt.title("Light Weight Vehicle Sales in Thousands of Units", loc="left", fontdict={"weight": "bold"}, y=1.06)
plt.xlabel("Time Period")
plt.ylabel("Sales in 000")
plt.legend()

plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Faa848d4f-36d0-4d47-94b2-26d193811af4_2538x1636.heic)

Image 8 - Plotting multiple series (image by author)

And that’s about all you need to know. Let’s make a recap next.

## Summing up Time Series Data Visualization

Time series data visualization is straightforward.

Line and area charts are typically all you need. There are some specific use cases, sure, but we’ll cross that bridge when we get there.

Right now, you have the fundamentals covered. You know what time series data represents, how to work with it in Pandas, and how to plot it with Matplotlib.

**Download today’s notebook:**

Notebook Timeseriesvisualization800KB ∙ PDF file [Download](https://darioradecic.substack.com/api/v1/file/83e0982b-eb08-46b4-b8ed-a2918760c5f8.pdf) [Download](https://darioradecic.substack.com/api/v1/file/83e0982b-eb08-46b4-b8ed-a2918760c5f8.pdf)