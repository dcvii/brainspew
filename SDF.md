---
title: SDF
source: https://davidsj.substack.com/p/sdf
author:
  - "[[David Jayatillake]]"
published: 2025-02-12
created: 2025-02-12
description: Is it better than SQLMesh?
tags:
  - clippings
  - dbt
---
Recently, dbt Labs announced its [acquisition](https://www.getdbt.com/blog/dbt-labs-acquires-sdf-labs) of SDF Labs. The week after this, Tobiko Labs announced its [acquisition](https://tobikodata.com/tobiko-acquires-quary.html) of Quary. SDF and Quary were two exciting alternatives to DBT, written in Rust. They were both very early products - in some senses, it’s a bit of a shame that we didn’t see how far they could go on their own in their early innovative arcs, which have been curtailed. Some of the changes that SQLMesh introduced during their own early innovative arc have been game-changing.

Perhaps it also shows that it doesn’t make sense for there to be many different data transformation framework standards. For years, most people have been happy with dbt as **the** standard without any real competition (other than large legacy incumbents). This has allowed the industry to converge on expressing data transformations in a modular, composable framework that others, like SQLMesh, SDF, Quary, LEA, and Yato, also subscribe to.

The question isn’t whether this kind of framework, stored procedures, Airflow string-manipulation, Informatica, Alteryx or Azure Data Factory is the future. The question is **which** of these frameworks is the best and can be widely and easily adopted. Both SDF and [SQLMesh](https://davidsj.substack.com/p/sqlmesh-init-t-dbt) offer varying[1](https://davidsj.substack.com/p/sdf#footnote-1-156780520) backwards compatibility with dbt (SQLMesh is actually better in this regard), meaning they can be easily adopted, so then it’s a question of which is best[2](https://davidsj.substack.com/p/sdf#footnote-2-156780520).

I have covered SQLMesh in great detail already! I think it’s the best tool out there for this purpose, so how does SDF compare? A Cube customer who reads my blog mentioned that I should check out SDF just a week before the dbt acquisition was announced, having seen my SQLMesh series. So this blog was always going to happen; there is now more impetus than before!

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3f192471-44e7-4bec-a7dd-30ca84b2d32b_784x692.png)

sdf.com

> *SDF is a multi-dialect SQL compiler, transformation framework, and analytical database engine packaged into a single CLI. Unlike other data transformation tools like DBT, SDF extracts SQL compilers from their clouds, understanding proprietary dialects of SQL (like Snowflake) so deeply that it can ultimately execute them.*
> 
> *When working locally, SDF is both the Database, and Transformation layer, ensuring validity. Regardless of which Database you work with - at any point, the entirety of the Data Warehouse defined in your workspace is fully defined and statically analyzed as code. This makes SDF more like the build system for TypeScript or Rust than a traditional data development tool.*

On the face of the comparison with dbt that I shared above, there seem to be many similarities with SQLMesh. One difference is quite material, though: SDF includes an integral database in the form of Apache DataFusion. Apache DataFusion is not the kind of database you could use on its own to replace a typical data warehouse in the way possible with DuckDB. It is meant to be a high-performance cache used inside another application, much like it is used within Cube’s [cache and pre-aggregation layer](https://cube.dev/blog/why-cube-store-is-the-best-choice-for-storing-pre-aggregated-data).

The qualification in the second paragraph of the quote above is key: “**When working locally…**”. SDF is not saying that it is trying to replace your existing data warehouse, but it is using DataFusion to allow you to have a **local** data warehouse to develop on. This reduces the need to test queries against your cloud data warehouse and to incur the cost and lag associated with doing this. It is common in all other forms of engineering than data/analytics engineering to have a fully local environment to develop in, to increase iteration speed and reduce lag and costs during development.

While SQLMesh doesn’t have a query engine baked into the framework, like SDF, it is very easy to use DuckDB for this purpose when working with a SQLMesh project, as SQLMesh can transpile SQL used in models to other SQL dialects. One benefit to using DuckDB over having DataFusion baked into SDF is that it will probably make it easier to look at the data directly and debug things by simply querying the DuckDB database. I am unsure how you would directly query the SDF DataFusion cache (I may be wrong); it’s not its purpose. It’s there to provide a complete development environment.

Both SDF and SQLMesh support column-level lineage out of the box; it’s hard to say if they have exact parity in what they support. For example, I know that SQLMesh(SQLGlot) can support lineage via CTEs and all kinds of complex SQL patterns because of its [AST walk](https://tobikodata.com/ast_journey.html) method in parsing SQL. I’m unsure if this is exactly the same in SDF or close enough not to be an interesting point of comparison. SDF’s column-level lineage is not as polished as SQLMesh’s from a front-end UI perspective; it is shown in the terminal as below:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8ec43dab-225b-4f52-9fe2-367699acaff2_787x478.png)

https://docs.sdf.com/tutorials/debugging

However, one advantage SDF has is that it seems to explicitly show where a column is modified in its lineage, in addition to which column/s it is derived from. This is helpful, as it’s rare for a copy operation to cause an issue other than if you rename the column and break references. It’s much more common for mutation and changes to mutation logic to cause issues. When debugging, you would first check for any change to mutation logic from recently changed code.

The main point of column-level lineage is not to have pretty diagrams; it is to prevent bugs being shipped into prod from development. If you read this [part](https://docs.sdf.com/tutorials/debugging) of the SDF docs, it has clearly become easier to use CLL to do this with SDF in a way that isn’t possible with dbt Core today. However, it isn’t particularly automated. It involves rooting around the exposed lineage and doing some eye-balling.

The SQLMesh plan/apply workflow is far superior in this regard; you make your changes, then plan them to see if they cause breaking downstream changes. The output of the plan command explicitly shows you which change broke something downstream and in which column, so you don't have to hunt around manually. This is a much better developer experience and more akin to other mature software engineering toolchains. It is better to automatically gain CLL's benefits without thinking about using something else.

I’m not saying SDF isn’t a substantial improvement on dbt; it definitely is. Rather than the `compile` command simply generating SQL text, SDF `compile` tests whether the model code will actually run, and if not, why.

SDF does have a `build` command that tries to implement the Write Audit Publish workflow. However, the audit only functions on tests that you have specified for your models. It doesn’t seem to include an understanding of breaking downstream changes, where you might change a model that doesn’t break that model itself but does break downstream ones.

I believe this is SQLMesh's single greatest advantage over dbt. During my December series, I spent considerable time explaining Virtual Data Environments. They enable you to effortlessly create a new environment based on your production data, develop it, and implement blue/green deployment. This, in conjunction with the plan/apply workflow with CLL applied automatically, is the fundamental reason why SQLMesh is my preferred data transformation framework.

SDF does not have this concept; you would have to do it like you do today with dbt: to create a dev schema, etc. This lack alone means that SQLMesh is a better tool than SDF.

SQLMesh also has other strengths over SDF. For example, storing model state to avoid re-running the same data and incremental models' extra configurability could greatly benefit organisations that manage large amounts of data[3](https://davidsj.substack.com/p/sdf#footnote-3-156780520). You can have Python macros in SQLMesh, but not in SDF. However, none of the other advantages are as categorical as Virtual Data Environments and the Plan/Apply workflow with CLL automatically applied.

If you use dbt now, you should be happy about the SDF acquisition; you will benefit if and when SDF features trickle down into Core or Cloud. It has already been stated that not all of SDF’s benefits will come to Core, as dbt Labs will use this as an incentive to upgrade to Cloud,[4](https://davidsj.substack.com/p/sdf#footnote-4-156780520) so I’m interested in which features make it and which don’t. SDF gets dbt users some of the benefits that SQLMesh offers, improving the dbt toolchain, but it lacks many - in particular, the crucial two I mention above.

Before the acquisition, one could argue that SDF might catch up with Tobiko, since they do not possess as mature a product, nor do they have as many companies employing it in production, as far as I know. Generally, smaller, more agile companies tend to outpace and outmanoeuvre larger, established ones – that is essentially the philosophy of venture capital. However, Tobiko remains quite small and nimble.

With the acquisition, SDF are now set to spend most of this year integrating features into dbt Core and Cloud, facing the challenge of dividing features between the two. Integrations are consistently difficult, and dbt Labs have already encountered this with the Transform acquisition. In theory, this time should be easier as it is not attempting to add an ancillary product; it directly replaces their core functionality, making go-to-market and sales strategy change considerably simpler.

It would have been easier to simply replace dbt Core with SDF and label it ‘dbt v2.0’, allowing companies a year to transition. This approach would enable the incoming SDF team to concentrate on developing any features that dbt Core and Cloud possessed but that SDF was missing, in addition to catching up with SQLMesh. While Virtual Data Environments and the Plan/Apply workflow are excellent features, it would not have been insurmountably challenging for SDF to release them within the next 12 months had they chosen to remain independent, or to prioritise innovation rather than integration and migration at dbt.

Tobiko now has the advantage of being able to innovate and release features faster than anyone else in the space. If they decide to put the afterburner on, it will be really hard for dbt and SDF to catch up or even keep the gap as it is today. I’m almost certain that by this time next year, the SDF team at dbt Labs will release few or no new innovations above what SDF can do today (certainly not to dbt Core), but there will be a lot from Tobiko.

I wonder if the relationship between dbt Labs and Tobiko had been less [acrimonious](https://www.linkedin.com/posts/toby-mao_although-dbt-labs-banned-us-from-coalesce-activity-7241483143730319360-XBsP/), whether they would have bought Tobiko instead… It’s not the first time we’ve seen the wrong company get bought in the space, and there is a lot of talk of [acquisitions](https://www.crn.com/news/cloud/2025/snowflake-eying-purchase-of-software-startup-redpanda-report) in data stack companies at this point in time.

All of this talk about which product is better is probably academic, though. dbt Labs is now past [$100m ARR](https://www.getdbt.com/blog/dbt-labs-100m-arr-milestone)[5](https://davidsj.substack.com/p/sdf#footnote-5-156780520) (not far from the IPO zone); even if they hadn’t acquired SDF, their momentum is past the point of no return. There isn’t really a chance that Tobiko could derail their momentum, even with a much better product. Having a better product doesn’t really matter from a commercial and GTM POV when one product is a data household name and one has more of a cult following and is preferred by data nerds like me; Microsoft is the proof of this.