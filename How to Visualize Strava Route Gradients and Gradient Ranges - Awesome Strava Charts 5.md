---
title: "How to Visualize Strava Route Gradients and Gradient Ranges - Awesome Strava Charts #5"
source: "https://darioradecic.substack.com/p/how-to-visualize-strava-route-gradients"
author:
  - "[[Dario Radecic]]"
published: 2024-08-13
created: 2025-03-24
description: "Steep and short climbs don't show well on Strava - Use gradient ranges to paint a full picture."
tags:
  - "clippings"
---
### Steep and short climbs don't show well on Strava - Use gradient ranges to paint a full picture.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc2a13351-3d3d-4364-8fab-ba59eb2909bd_1500x1000.heic)

Article thumbnail (image by author)

You might think your last ride was tough, but how can you prove it?

One way is by looking at total elevation gain. It’s a good measure - the more climbing you do, the more effort you have to put out. But what about those pesky short bursts at an **uncomfortable gradient level**? What about that 1-kilometer-long 16% average climb that doesn’t show well on Strava?

That’s where gradient ranges come in. In today’s article, you’ll learn what they are, how to calculate them in Python, and how to visualize them with Plotly.

[If you want to access all articles with data and code right now, download the eBook and level up your data visualization skills in one afternoon:](https://radecic.gumroad.com/l/yermz)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fce9dd5fb-f2a8-4f6a-9c5e-47d048435855_1200x600.heic)

[https://radecic.gumroad.com/l/yermz](https://radecic.gumroad.com/l/yermz)

If you’re a paid subscriber, you can download the notebook [here](https://github.com/darioradecic/Data-Doodles-with-Python/tree/main/012_strava_5_gradients).

## Strava Gradient Visualization with Plotly

This section will show you two ways to plot gradients in Python.

The first, incorrect way, shows what happens when you don’t address for GPS errors. **Your cycling computer can fail** and misread your elevation data. When this happens, you might see gradient differences of several hundred percent between points that are just meters apart.

The second, correct way, accounts for possible errors made by cycling computers. It limits the gradient to a set maximum and smooths out any suspicious data points.

Before you start, make sure to import the following Python libraries:

```markup
import numpy as np
import pandas as pd
import plotly
import plotly.express as px
import plotly.graph_objects as go
import plotly.offline as pyo
```

Also, read the parsed CSV file:

```markup
df = pd.read_csv("../data/strava_parsed.csv")
df.head(10)
```

![](https://substackcdn.com/image/fetch/w_2400,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa6b4d7a4-d182-4cec-b8ba-f98c15aeafb8_3308x606.heic)

Image 1 - Strava GPX route in CSV format (image by author)

You will use the following function to plot the gradient with Plotly.

It returns a line plot styled as explained in [previous articles](https://open.substack.com/pub/darioradecic/p/how-to-visualize-strava-activity?r=48ma0u&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true), so I won’t go into detail here.

```markup
def plot_gradient(
        x: pd.Series, 
        y: pd.Series, 
        color: str,
        name: str = "Gradient", 
        title: str = "Strava Route Gradient Profile", 
        xaxis_title: str = "Distance (km)", 
        yaxis_title: str = "Gradient (%)",
    ) -> go.Figure:
    plot_data = go.Scatter(
        x=x,
        y=y,
        mode="lines",
        line=dict(
            width=2,
            color=color
        ),
        name=name,
        hovertemplate=(
            "<b>Gradient:</b> %{y:.2f}%<br>"
            "<extra></extra>"
        )
    )

    plot_layout = go.Layout(
        title=dict(
            text=f"<b>{title}</b>",
            font=dict(
                size=24,
                weight="bold"
            )
        ),
        xaxis=dict(
            title=xaxis_title,
            showgrid=True,
            gridcolor="#D3D3D3",
            gridwidth=0.5,
            griddash="dot"
        ),
        yaxis=dict(
            title=yaxis_title,
            showgrid=True,
            gridcolor="#D3D3D3",
            gridwidth=0.5,
            griddash="dot"
        ),
        width=1200,
        height=450,
        paper_bgcolor="rgba(0,0,0,0)",
        plot_bgcolor="rgba(0,0,0,0)",
        hovermode="x",
        font=dict(
            family="Roboto Condensed, sans-serif",
            size=16,
            color="#000000"
        )
    )

    return go.Figure(data=plot_data, layout=plot_layout)
```

Now, let’s see how a naive approach to visualizing gradients can go wrong.

### The Incorrect Way to Calculate and Plot Gradient

Start by selecting only the columns you need: distance from the start, distance from the previous point, and elevation.

```markup
df_grade = df[["distance_from_start", "elevation", "distance_in_meters_from_prev"]]
df_grade.head()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc97e0a24-bb2e-4970-8d10-ce245d531dc4_1096x354.heic)

Image 2 - Subset for gradient calculation (image by author)

To get the gradient (percentage), you’ll want to divide two values - **change in elevation** by the **change in distance** \- both of which you’ll have to calculate first.

You can call either the `diff()` or `shift()` functions on the respective columns, and then multiply the division result by 100 to get a percentage:

```markup
# Change in elevation between the current and the previous row
df_grade["elevation_change"] = df_grade["elevation"].diff()

# Shift the column up by one position - get distance to the next row
df_grade["distance_change"] = df_grade["distance_in_meters_from_prev"].shift(-1)

# Calcualte gradient percentage as ((change in elevation / change in distance) * 100)
df_grade["gradient_pct"] = (df_grade["elevation_change"] / df_grade["distance_change"]) * 100

# Drop missing values
df_grade = df_grade.dropna(subset=["gradient_pct"])
df_grade[:10]
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F694a6be0-6cb1-4de4-91f3-ccff28c0f9e4_1906x622.heic)

Image 3 - Calculated gradient results (image by author)

Everything seems fine, **but appearances can be deceiving**.

The summary statistics tell a different story:

```markup
df_grade["gradient_pct"].describe()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6ccd6986-025a-4d9c-8431-715689fff589_632x402.heic)

Image 4 - Gradient statistics (image by author)

Important values are missing, which means there’s something wrong with how we’re calculating the gradient.

Let’s plot it to understand better:

```markup
plot_grade = plot_gradient(x=df_grade["distance_from_start"], y=df_grade["gradient_pct"], color="#000000")
pyo.iplot(figure_or_data=plot_grade)
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F22abe942-6e2a-45f0-94c3-b019b62a817a_2800x1032.heic)

Image 5 - Gradient plot (image by author)

A gradient of -600% would mean you’re descending 6 meters for every meter traveled. It’s not a completely vertical drop, but you get the point - **you would die**.

Since I’m still here, there’s clearly an issue with the data.

### The Correct Way to Calculate and Plot Gradient

The “issue” comes from the unavoidable errors in measuring devices.

Cycling computers are generally accurate, but they struggle when you focus on smaller segments.

To fix this, we’ll divide the data into **100-meter bins** and calculate the gradient for each bin. While this gives an average over 100 meters and may not be perfect, it’s much more reliable.

```markup
df_grade = df[["distance_from_start", "elevation", "distance_in_meters_from_prev"]]

# Create bins in 100 meter intervals
bin_edges = np.arange(df_grade["distance_from_start"].min(), df_grade["distance_from_start"].max() + 100, 100)
df_grade["bin"] = pd.cut(df_grade["distance_from_start"], bins=bin_edges, right=False)

# Create a new DF and compute some aggregate statistics
df_grade_binned = df_grade.groupby("bin").agg({
    "elevation": "mean",
    "distance_from_start": ["min", "max", "mean"]
}).reset_index()
df_grade_binned.columns = ["bin", "avg_elevation", "start_distance", "end_distance", "avg_distance"]

# Calculate what"s needed for gradient calculation
df_grade_binned["elevation_change"] = df_grade_binned["avg_elevation"].diff()
df_grade_binned["distance_change"] = df_grade_binned["end_distance"].diff()

# Calculate the gradient and drop missing values
df_grade_binned["gradient_pct"] = (df_grade_binned["elevation_change"] / df_grade_binned["distance_change"]) * 100
df_grade_binned = df_grade_binned.dropna(subset=["gradient_pct"])
df_grade_binned.head(10)
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F116ba9cf-489d-4825-82f3-d35addc37aa5_2194x620.heic)

Image 6 - Correct approach to gradient calculation (image by author)

You can see the improvement by plotting the gradient:

```markup
plot_grade = plot_gradient(x=df_grade_binned["avg_distance"], y=df_grade_binned["gradient_pct"], color="#000000")
pyo.iplot(figure_or_data=plot_grade)
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F173080db-4169-4e10-b7b5-52306ed60937_2774x1010.heic)

Image 7 - Gradient plot (2) (image by author)

Or by examining the statistics:

```markup
df_grade_binned["gradient_pct"].describe()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F468e06bb-5865-4baf-9172-fd3b1ec2dfb5_662x408.heic)

Image 8 - Gradient statistics (2) (image by author)

There are no more missing or infinite values, and the numbers make sense.

In short, you can see how the first ~ 18km of the course was a constant uphill (gradient averaging around 5%), followed by a brief ~ 7km downhill. The rest of the route gradient was mix and match, going up and down more times than I can count.

But remember, the gradient only tells part of the story.

## Gradient Ranges - Implementation and Visualization

If you want to make an ultimate climbing/descending analysis of your Strava routes, gradient ranges are where it’s at.

It’s a metric you won’t see often, not even in Strava’s premium plan.

In plain English, the gradient range metric splits the gradient into bins, each having a range of a couple of percent, and then calculates **bin-wise statistics** to see how much distance you’ve covered in a given range.

In other words, it makes you say: I rode 8.5km in a gradient range from 7 to 10%. That’s tough.

### Calculate Gradient Ranges with Plotly

The process is simple but quite involved.

First, you need to create the bins. In this example, I’m making 14 bins to cover 14 gradient ranges. Then, you can use the `pd.cut()` function to add these bins to the data, based on the previously calculated gradient.

```markup
# Arbitrary bins for gradient ranges (individual bars on a plot)
gradient_range_bins = pd.IntervalIndex.from_tuples([
    (-15, -12),
    (-12, -10),
    (-10, -7),
    (-7, -5),
    (-5, -3),
    (-3, -1),
    (-1, 0),
    (0, 1),
    (1, 3),
    (3, 5),
    (5, 7),
    (7, 10),
    (10, 12),
    (12, 15)
], closed="left")

df_grade_binned["gradient_range"] = pd.cut(df_grade_binned["gradient_pct"], bins=gradient_range_bins)
df_grade_binned.sample(10)
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F712716df-d44c-46c3-906d-d4ba81832137_2546x616.heic)

Image 9 - Gradient range attribute (image by author)

Now onto the statistics.

The following snippet calculates the total distance traveled in each gradient range bin:

```markup
# Extract gradient statistics for each bin - only total distance in km is needed
gradient_details = []

for gr_range in df_grade_binned["gradient_range"].unique():
    subset = df_grade_binned[df_grade_binned["gradient_range"] == gr_range]

    total_distance = np.round(subset["distance_change"].sum() / 1000, 2)

    gradient_details.append({
        "gradient_range": gr_range,
        "total_distance": total_distance
    })
```

Finally, the last snippet assigns a HEX color code to each gradient range. It uses a diverging palette, with blue shades for descending (negative gradient) and red shades for climbing (positive gradient).

The `select_middle_color_values()` function allows you to have fewer gradient ranges, as it will only extract HEX color codes from the middle:

```markup
def select_middle_color_values(colors, n):
    if n > len(colors):
        return colors

    total_len = len(colors)
    start_index = (total_len - n) // 2
    end_index = start_index + n
    return colors[start_index:end_index]

colors = ["#1C3041", "#29465F", "#396284", "#5389B5", "#80A8C8", "#A8C3D9", "#CADBE8", 
          "#F3BFC0", "#EB9497", "#E26469", "#D83136", "#9F1E22", "#741619", "#4D0E11"]

gradient_ranges = pd.DataFrame(gradient_details).dropna()
gradient_ranges.sort_values(by="gradient_range", inplace=True)
gradient_ranges.reset_index(drop=True, inplace=True)

gradient_ranges["xticks"] = gradient_ranges["gradient_range"].apply(lambda x: " - ".join(str(x).replace("[", "").replace(")", "").split(", ")))
gradient_ranges["color"] = select_middle_color_values(colors=colors, n=len(gradient_ranges.index))

gradient_ranges
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F33b01d07-56ed-4758-ab65-2f5d34f140e9_1108x988.heic)

Image 10 - Gradient range plot data (image by author)

You now have everything needed to visualize gradient ranges!

### Visualize Gradient Ranges with Plotly

A bar chart is the perfect candidate for the job.

The following code snippet plots a bar chart with the gradient ranges on the X-axis and the total distance covered in each range on the Y-axis. The distance is also displayed as text above each bar, and more details are shown when you hover over the bars.

```markup
plot_data = go.Bar(
    x=gradient_ranges["gradient_range"].astype("str"),
    y=gradient_ranges["total_distance"],
    text=gradient_ranges["total_distance"],
    textposition="outside",
    marker_color=gradient_ranges["color"],
    hovertemplate=(
        "<b>Gradient range: %{x}%<br>"
        "<b>Distance: %{y:.2f}km<br>"
        "<extra></extra>"
    ),
    hoverlabel=dict(
        bgcolor="#ffffff",
        font=dict(
            color="#000000",
            size=14
        )
    )
)

plot_layout = go.Layout(
    title=dict(
        text=f"<b>Gradient Range Plot</b>",
        font=dict(
            size=24,
            weight="bold"
        )
    ),
    xaxis=dict(
        title="Gradient Range",
        showgrid=True,
        gridcolor="#D3D3D3",
        gridwidth=0.5,
        griddash="dot",
        tickvals=list(range(len(gradient_ranges))),
        ticktext=gradient_ranges["xticks"]
    ),
    yaxis=dict(
        title="Distance (km)",
        showgrid=True,
        gridcolor="#D3D3D3",
        gridwidth=0.5,
        griddash="dot"
    ),
    width=1200,
    height=700,
    paper_bgcolor="rgba(0,0,0,0)",
    plot_bgcolor="rgba(0,0,0,0)",
    hovermode="x",
    font=dict(
        family="Roboto Condensed, sans-serif",
        size=16,
        color="#000000"
    )
)

fig = go.Figure(data=plot_data, layout=plot_layout)
pyo.iplot(figure_or_data=fig)
```

![](https://substackcdn.com/image/fetch/w_2400,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbd03b2a5-1119-47f2-b4c2-c0d0e1af787d_2838x1688.heic)

Image 11 - Gradient range plot (image by author)

To interpret, **it wasn’t a flat day**.

Aside from the relatively flat section (-1 to +1 gradient), I spent nearly 28km climbing and about 18km descending. It’s just the kind of insight you can’t extract by looking at a basic [elevation chart](https://open.substack.com/pub/darioradecic/p/how-to-visualize-strava-activity?r=48ma0u&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true).

## Wrapping up

The gradient range plot is easily my favorite.

It gives you much more insight than a simple gradient or elevation chart, letting you focus on specific areas of interest. You can see exactly how much distance you’ve covered in each gradient range. For a cyclist and data enthusiast, it **fills the gap** left by Strava and other platforms.

If you’ve made it through this article—congratulations! You now have everything you need to create an interactive dashboard for analyzing Strava workouts. We won’t add any more charts here since there are plenty of new concepts coming with the dashboard.

The next article will be the longest, but it’s the one you’ll want to read because it brings everything together.