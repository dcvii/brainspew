---
title: "Benchmarking Vortex File Format ... vs Parquet, CSV, and Lance ... vs DuckDB, Polars, Datafusion."
source: "https://dataengineeringcentral.substack.com/p/benchmarking-vortex-file-format-vs?publication_id=1224799&post_id=199213160&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2026-05-24
created: 2026-05-25
description: "just because we want to make em' mad"
tags:
  - "brain_spew"
---
![](https://substackcdn.com/image/fetch/$s_!rCLU!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F035d92dc-992c-43b6-a683-b0aa4ab8a43d_1200x700.png)

If we had a dollar for every time someone came along to become the Apache Parquet killer, we would all be living on the side of a mountain tending to our alpacas. A boy can dream, can’t he?

Because it’s a holiday Monday, and I’ve been up since dawn running amok on the river, and now I’m lying on the porch with a cool breeze, it’s time we put our hand to the plow and turn up something interesting.

> Today, that will be the [Vortex file format](https://docs.vortex.dev/).

![](https://substackcdn.com/image/fetch/$s_!sCW9!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F92d76888-b172-433a-a1a8-e413c5b9413a_1916x596.png)

At this point, half of you probably know more about Vortex than I. I’ve heard the name rattle around here and there, but never touched it. So, I don’t expect much today, really just a little poke here and there, a little benchmark to bring the craizes out of the swap, ya know, the usual stuff.

---

## Vortex file format for ninnies.

It isn’t really apparent to me, on a simple poking around in the docs, what niche is being chased down by Vortex. I mean, if you read between the lines, and not hard to find lines, seeing worlds like “ *… vs Parquet* ” or “ *compressed columnar data,*” heck, even a “ *unlike Arrow …* ” makes me sit up and take note.

- **Seems like these little buggers are taking potshots at everyone worth anything today.**

![](https://substackcdn.com/image/fetch/$s_!RVm2!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe909476b-37e7-4c1b-ac0f-c037672ec20c_1600x564.png)

The GitHub page actually brings it home a little better.

> “ *Vortex is a next-generation columnar file format and toolkit designed for high-performance data processing. It is the fastest and most extensible format for building data systems backed by object storage.*”  
> \- [GitHub](https://github.com/vortex-data/vortex)

It also boasts some impressive features that stand out to me beyond what has already been mentioned.

- appears to be written in Rust
- “Zero-copy compatibility with Apache Arrow”
- Arrow, DataFusion, DuckDB, Spark, Pandas, Polars, & more
- Modeled after Apache DataFusion’s extensible approach

So, we shall see, eh?

---

### Python + Vortex and benchmarking performance.

Well, if any tool worth its salt wants to make a go of the data community, it must have first-class Python support; otherwise, all is for naught. Rustaceans might cringe, but that’s simply the way of the world.

Let us kill those two birds with one stone.

- Try out the Python integrations with DuckDB, Polars, and Datafusion.
- Benchmark those against each other, plus vs CSV, Parquet, maybe Lance?

> *We can see what it’s like to use Vortex inside Python code, and see if there is any indication its performance is a thing or not.*

Remember, if you leave me nasty comments about scientific benchmarking, there is a high probability that I will make fun of you in front of 35,000 people who follow me on this platform. Just saying. Take your chances.

![](https://substackcdn.com/image/fetch/$s_!NTOC!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F684c1550-f267-4917-8ebc-4f0af91c678d_1400x484.png)

Next, let us grab some data to use. We will use the Backblaze open-source hard drive dataset about failure rates.

![](https://substackcdn.com/image/fetch/$s_!j_5f!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F551f0eb6-d14e-4036-b650-6f3e70c37359_1706x292.png)

Let’s take these two zip files, each containing two quarters of data, totaling about **23.91 GB on disk**.

![](https://substackcdn.com/image/fetch/$s_!ga_7!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fec0e9c8d-026f-4b9c-88aa-71a51ce41b14_1364x342.png)

- This should be enough for our purposes.

First, let’s run a simple DuckDB query on these raw CSV files to get a baseline, then we will convert to Vortex and test again.

- [All this code is on GitHub, you hobbit.](https://github.com/danielbeach/benchmarkingVortex)

![](https://substackcdn.com/image/fetch/$s_!-2US!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3ced6f2d-b930-4b37-bdee-3140648ecf74_1400x1266.png)

```markup
Total failure days: 181
Runtime: 25.465s
```

Ok, longer than I thought. Let’s run the exact same code on raw CSV with both Polars and DataFusion before we switch to Vortex, and then test Parquet and Lance as well.

![](https://substackcdn.com/image/fetch/$s_!3eNd!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fadd5fe06-4fe5-4472-8807-dd041418e4ca_1400x1228.png)

> Oh … what do you flipping know, another one of those mysterious Polars failures that doesn’t exist, and you are anathema and a heretic for even saying it.

![](https://substackcdn.com/image/fetch/$s_!JfDm!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc5a44f04-7028-4565-92d9-91bde77ab3e6_1934x1314.png)

I highly suggest [you go read this.](https://dataengineeringcentral.substack.com/p/why-im-replacing-polars-with-duckdb) And also, I encourage you to go to Google OOM Polars issues yourself, don’t let that powerful and slinking Nazgul scare you away, you will find enough evidence yourself. ***You can only hide the pea for so long.***

- This is why I had to rip Polars out of production: simply unpredictable and unreliable in an unacceptable way, for tasks that other tools handle with ease.

![](https://substackcdn.com/image/fetch/$s_!Y2md!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F08e76509-56e1-405f-9baa-f90796ec5848_1884x590.png)

Anyway, stick Polars in the ditch, let’s move on to DataFusion.

![](https://substackcdn.com/image/fetch/$s_!WDx_!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fad3e5363-3d8b-40b8-a08f-bce9dae717ad_1400x1564.png)

Oh dang, Datafusion is fast.

```markup
Total failure days: 181
Runtime: 5.106s
```

---

## Ok, let’s move to Parquet files.

So, let’s convert all the CSV files to Parquet and re-run those scripts with DuckDB, Polars, and Datafusion on them. See what’s cracken.

- 184 CSVs → 20 Parquet files (*10 per quarter, last batch 2 files each*).

[Again, all the code is on GitHub](https://github.com/danielbeach/benchmarkingVortex), and we converted all our previous scripts to just read Parquet instead of raw CSV. You can go look at the scripts if you please. I’m just going to show results here.

```markup
- failures_by_day_duckdb.py — 0.125s
- failures_by_day_datafusion.py — 0.370s
- failures_by_day_polars.py — 0.193s
```

Well, that is quite the difference, eh.

---

## Ok, let’s move to Vortex files.

So, let’s finally get to what we’ve been waiting for this whole time: will these packages really integrate well with Vortex, and will the performance be noticeably faster than Parquet?

- First, let’s convert from Parquet to Vortex with DuckDB.

![](https://substackcdn.com/image/fetch/$s_!zFMi!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffd284c16-7a41-4866-8573-2e572731f88c_1400x1228.png)

With that done, let’s run the benchmarks with the same set of tools again for DuckDB, Polars, and Datafusion on Vortex. I will put the DuckDB example in; you can check the rest in GitHub, and print the results only here.

```markup
- vortex_scripts/failures_by_day_vortex.py — pure vortex scan with filter pushdown, 0.111s
- vortex_scripts/failures_by_day_duckdb.py — DuckDB querying VortexDataset (PyArrow interface), Runtime: 0.201s
- vortex_scripts/failures_by_day_polars.py — VortexFile.to_polars() LazyFrame, Runtime: 0.114s
```

FYI, the integrations aren't as solid as they claim. The DuckDB vortex extension blows up with memory errors. **OOM like Polars on CSV files.**

![](https://substackcdn.com/image/fetch/$s_!8VGS!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe3c789ce-4136-488a-8ff6-5bf1d1c726e3_1400x1526.png)

![](https://substackcdn.com/image/fetch/$s_!WDD0!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa66d805e-da4b-445b-ab70-a02d7b462b3c_1938x1426.png)

Polars only seems to support per-file-type code; I couldn't get any globbing patterns to work. On top of that, we convert to PyArrow and Polars right away in that code.

![](https://substackcdn.com/image/fetch/$s_!mB61!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F179c5efe-dd59-4e91-94bd-2c3a2be4b8c8_1400x1750.png)

Heck, maybe I’m doing stuff wrong, but the farther I get into the weeds with Vortex, the more I realize this might be early days yet. Seems there are still some problems to solve and wrinkles to iron out in the Python ecosystem.

- We could probably make DuckDB work with Vortex by doing what we did with Polars, convert to Arrow right away?

![](https://substackcdn.com/image/fetch/$s_!gFGW!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1d50de8e-05ed-4f08-a066-02926a35e15e_1400x2010.png)

Blah, performance is fine, but that is some nasty-looking code. No fault of these third-party tools, just a little early in the lifecycle methinks.

---

Anywho, here ya go.

![](https://substackcdn.com/image/fetch/$s_!zvdY!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa240e3b7-163e-4f12-8946-4be09f3a9937_1200x700.png)

I didn’t learn a ton. Maybe the lift over Parquet is larger on massive datasets, but I'm not sure it’s worth the hassle of subpar Python framework integrations and ugly code, along with OOM issues when you try to read directories of Vortex files.