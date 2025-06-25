---
title: "Introduction to ECDFs in Python: A Robust Histogram Replacement"
source: "https://darioradecic.substack.com/p/introduction-to-ecdfs-in-python-a"
author:
  - "[[Dario Radecic]]"
published: 2024-08-13
created: 2025-03-24
description: "Ditch the Binning bias once and for all with ECDFs"
tags:
  - "clippings"
---
### Ditch the Binning bias once and for all with ECDFs

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F97b64a28-5498-44b8-9b5a-9ef29d036b2c_1500x1000.png)

Article thumbnail (image by author)

Charts shouldn’t be open to interpretation.

And unfortunately, that’s rarely the case, especially with histograms. Today you’ll see how histogram’s *binning bias* can mislead you in the analysis and how to prevent this issue with the power of ECDF plots.

After reading, you’ll know:

- What’s wrong with histograms — and when should you avoid them
- How to replace histograms with ECDFs — a more robust method for examining data distributions
- How to use and interpret multiple ECDFs in a single chart — to compare distributions among different data segments

Let’s dig in!

If you’re a paid subscriber, you can skip the reading and [download the notebook](https://github.com/darioradecic/Data-Doodles-with-Python/tree/main/021_ecdf) instead.

## What’s Wrong with Histograms?

As Justin Bois from [DataCamp](https://learn.datacamp.com/courses/statistical-thinking-in-python-part-1) said — binning bias — and I can’t agree more. What this means is that using different bin sizes on a histogram makes data distribution look different. Don’t take my word for it — the example below speaks for itself.

To start, I’ll import a couple of libraries for data analysis and visualization, and load the [Titanic](https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv) dataset straight from the web:

```markup
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
plt.style.use("custom_light.mplstyle")

df = pd.read_csv("https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv")
df.sample(5)
```

I’m using my `custom-light` theme to change the look of the visualizations. If you’re interested, you can learn how to create a Matplotlib theme from scratch in this article:

If you are unfamiliar with the dataset, here’s what the first couple of rows look like:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b17c457-26e1-4abf-8941-ad8c9a641acf_2398x360.png)

Image 1 - Titanic dataset sample (image by author)

Missing values can’t be visualized, so I’ll drop them for the purpose of the article:

```markup
df = df.dropna(subset=["Age"])
```

Next, I’ll declare a function for visualizing histograms. It takes a bunch of parameters, but the most important ones in our case are:

- `x` – a single attribute for which you want to make a histogram
- `nbins` – how many bins the histogram should have
```markup
def plot_histogram(x, nbins=10, title="Histogram", xlab="Age", ylab="Count"):
    plt.hist(x, bins=nbins, color="#895884", ec="#000000", linewidth=1)
    plt.title(title, size=20, y=1.04)
    plt.xlabel(xlab, size=14)
    plt.ylabel(ylab, size=14)
```

I’ll use the mentioned function twice, the first to make a histogram with 10 bins, and the second to make a histogram with 30 bins. Here are the results:

Histogram with 10 bins:

```markup
plot_histogram(df["Age"], title="Histogram of passenger ages")
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa26b4fe3-5a17-4a79-a382-5ac70e4623ac_2214x1472.png)

Image 2 - Histogram with 10 bins (image by author)

Histogram with 30 bins:

```markup
plot_histogram(df["Age"], nbins=30, title="Histogram of passenger ages")
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0ad52d51-14a0-46ab-9959-7e5ed126dd91_2214x1452.png)

Image 3 - Histogram with 30 bins (image by author)

The data is identical, but different bin sizes can lead to *binning bias* — perceiving the same data differently, due to a slight change in the visual representations.

What can you do to address this issue? **ECDF plots** are here to save the day.

## ECDFs: A Robust Histogram Replacement

ECDF stands for the *Empirical Cumulative Distribution Function*. In reality, it’s way less fancy than it sounds and is also relatively easy to interpret.

Like histograms, ECDFs show a single variable distribution, but in a more efficient way. You’ve seen previously how histograms can be misleading due to different bin sizing options. That’s not the case with ECDFs. ECDFs show every data point, and the plot can be interpreted only in one way.

Think of ECDFs as scatter plots because they also have points along X and Y axes. To be more precise, here’s what ECDFs show on both axes:

- X-axis — a quantity you’re measuring ( *Age* in the example above)
- Y-axis — the percentage of data points that have a smaller value than the respective X value (at each point X, Y% of the values are smaller or identical to X)

To make this sort of visualization, you need to do a bit of calculation first. Two arrays are required:

- X — sorted data (sorting the *Age* column from lowest to highest)
- Y — list of evenly spaced data points where the maximum is 1 (as in 100%)

Use the following snippet to calculate *X* and *Y* values for a single column in a Pandas DataFrame:

```markup
def ecdf(df, column):
    x = np.sort(df[column])
    y = np.arange(1, len(x) + 1) / len(x)
    return x, y
```

And to plot ECDF, use the following:

```markup
def plot_ecdf(x, y, title="ECDF", xlab="Age", ylab="Percentage", color="#895884"):
    plt.scatter(x, y, color=color)
    plt.title(title, size=20, y=1.04)
    plt.xlabel(xlab, size=14)
    plt.ylabel(ylab, size=14)
```

Let’s use this function to make an ECDF plot of the `Age` attribute:

```markup
x, y = ecdf(df, "Age")

plot_ecdf(x, y, title="ECDF of passenger ages")
plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe1709b34-d4b3-4972-84ea-baa449bde581_2206x1470.png)

Image 4 - Age ECDF plot (image by author)

**To interpret:**

- Around 25% of the passengers are 20 years old or younger
- Around 80% of the passengers are 40 years old or younger
- Around 5% of the passengers are 60 years old or older (1 — the percentage)

The true power lies in plotting multiple ECDFs. Let’s see what that’s all about.

## Multiple ECDF Plots

In the Titanic dataset, you have the `Pclass` attribute, which indicates the passenger class. This sort of class organization is typical in travel even today, as the first class is reserved for wealthier individuals, and the other classes are where the rest of the folk is located.

With the power of ECDFs, you can explore how the passenger age was distributed among classes. You’ll need to call the `ecdf()` function 3 times, as there were three classes on the ship. The rest of the code boils down to data visualization, which is self-explanatory:

```markup
x1, y1 = ecdf(df[df["Pclass"] == 1], "Age")
x2, y2 = ecdf(df[df["Pclass"] == 2], "Age")
x3, y3 = ecdf(df[df["Pclass"] == 3], "Age")

plt.scatter(x1, y1, color="#F07605", label="Pclass = 1")
plt.scatter(x2, y2, color="#0B6E4F", label="Pclass = 2")
plt.scatter(x3, y3, color="#9B1D20", label="Pclass = 3")
plt.title("ECDF of ages across passenger classes", size=20, y=1.04)
plt.xlabel("Age", size=14)
plt.ylabel("Percentage", size=14)
plt.legend(loc="lower right")
plt.show()
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa658bb26-e362-4578-9b18-332eaca20a86_2256x1492.png)

Image 5 - ECDFs across passenger classes (image by author)

As you can see, the third class (red) had a lot of children on board, which isn’t the case with the first class (orange). The population in the first class is quite older, too:

- Only 20% of the first-class passengers are older than 50 years
- Only 20% of the second-class passengers are older than 40 years
- Only 20% of the third-class passengers are older than 34 years

## Wrapping Up

In data visualization, don’t leave anything open to interpretation.

Just because you prefer to see 15 bins in a histogram doesn’t mean your coworker does too. These differences might lead to different data interpretations if interpreted visually.

That’s not the case with ECDFs. You now know enough about them so you can include them in the next data analysis project. They might look strange, but they’re dead easy to explain and interpret.

Until next time.

\-Dario