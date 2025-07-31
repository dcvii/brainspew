---
title: Matplotlib Has 28 Built-In Themes - These 5 Are The Best
source: https://darioradecic.substack.com/p/matplotlib-has-28-built-in-themes
author:
  - "[[Dario Radecic]]"
published: 2024-08-13
created: 2025-03-24
description: Changing a Matplotlib theme is one line of code away - but which themes deserve your effort?
tags:
  - jupyter
---
### Changing a Matplotlib theme is one line of code away - but which themes deserve your effort?

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F768a574c-2413-4ba0-9f8b-a8f0e5fc2bea_1500x1000.heic)

Article thumbnail (image by author)

You can be lazy and still get a decent-looking Matplotlib chart.

It won’t make it to the New York Times, but at least you won’t spend hours [creating a custom theme from scratch](https://darioradecic.substack.com/p/how-to-create-a-custom-matplotlib). That said, making your own theme is worth it in the long run. It’s the only way to have **full control**.

This article is for people in a hurry.

Matplotlib comes with 28 stylesheets, and switching between them takes just one line of code. Today, you’ll learn what that line is and how to compare your chart using all the stylesheets. I’ll also share my top 5 theme picks at the end and guide you on what to do next.

If you’re a paid subscriber, you can skip reading and [download the notebook](https://github.com/darioradecic/Data-Doodles-with-Python/tree/main/017_built_in_matplotlib_themes) instead.

## How to Change a Theme in Matplotlib

If you’re working in a notebook environment and have Numpy and Matplotlib installed, use the code below to import the libraries you’ll need:

```markup
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
import matplotlib_inline
matplotlib_inline.backend_inline.set_matplotlib_formats("svg")
```

You can list all available stylesheets with this command:

```markup
plt.style.available
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F041d6a5a-c1c0-4b0e-988f-6574186bd151_914x336.heic)

Image 1 - Available matplotlib themes (image by author)

Keep in mind, `custom-style` is a theme I created in a [previous article](https://darioradecic.substack.com/p/how-to-create-a-custom-matplotlib) and is not included in the default Matplotlib installation.

**To change the theme, just run this:**

```markup
plt.style.use("<theme-name>")
```

It’s that easy!

You’ll see it in action in the next section.

## How to Find the Best Built-in Matplotlib Theme for Yourself

The easiest way is to try them all.

Consider the following function:

```markup
def bar_chart(theme: str):
    x = np.array(["New York", "San Francisco", "Los Angeles", "Chicago", "Miami"])
    y1 = np.array([50, 63, 40, 68, 35])
    y2 = np.array([77, 85, 62, 89, 58])
    y3 = np.array([50, 35, 79, 43, 67])
    y4 = np.array([59, 62, 33, 77, 72])

    plt.style.use(theme)

    plt.figure(figsize=(10, 6))
    plt.bar(x, y1, label="HR")
    plt.bar(x, y2, bottom=y1, label="Engineering")
    plt.bar(x, y3, bottom=y1 + y2, label="Marketing")
    plt.bar(x, y4, bottom=y1 + y2 + y3, label="Sales")

    plt.title(f"Theme: {theme}", fontweight="bold", loc="left")
    plt.xlabel("Office Location")
    plt.ylabel("Count")

    plt.legend()
    plt.show()
```

It will plot a bar chart with the theme you specify through the `theme` parameter.

Then, use a simple loop to go through all available themes and call the function:

```markup
for theme in plt.style.available:
    bar_chart(theme=theme)
```

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F99933e10-01c7-4952-98f0-af496f7c2992_1934x1712.heic)

Image 2 - Going through all available themes (image by author)

You’ll get 28 plots stacked one below the other, so it will only take a minute to review them.

From there, just pick your favorite and tweak it if needed.

## My Top 5 Built-in Matplotlib Themes

From the 28 available themes, here are my top 5 (in no particular order):

### dark\_background

This theme works great if your code editor has a dark mode turned on and you want a color palette that is easy on the eyes.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2f1c0f82-2601-416f-a6d6-bfac9ebc4d64_2164x1328.heic)

Image 3 - Matplotlib’s dark\_background theme (image by author)

### grayscale

It gives your charts an old-school textbook look and ensures they work well in black-and-white situations.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F615f4309-48a3-473c-ae18-fc6319175297_2164x1328.heic)

Image 4 - Matpotlib’s grayscale theme (image by author)

### seaborn-v0\_8

The vibrant colors in this theme really stand out, especially when compared to charts using other themes.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3de96f97-96b6-4087-8702-c18d5cca7ff3_2164x1328.heic)

Image 5 - Matplotlib’s seaborn-v0\_8 theme (image by author)

### seaborn-v0\_8-pastel

In 2024, pastel colors are very trendy. This theme offers a modern pastel palette.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4cb5386c-0949-40dd-9856-ec5905d612f1_2164x1328.heic)

Image 6 - Matplotlib’s seaborn-v0\_8-pastel theme (image by author)

### tableau-colorblind10

This theme is a reliable choice. It’s vibrant even with many gray shades and is designed to be [colorblind-friendly](https://darioradecic.substack.com/p/5-crucial-tweaks-that-will-make-your?r=48ma0u).

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcef7408a-5adb-4854-8db4-e5b745b0798c_2164x1328.heic)

Image 7 - Matplotlib’s tableau-colorblind10 theme (image by author)

## Where to Go From Here?

If you’re short on time, any of these five themes will look better than the default one.

**But use them as a starting point.** Find what you like about each theme and use that to create your own [custom theme](https://darioradecic.substack.com/p/how-to-create-a-custom-matplotlib). This is the best way to make your charts truly *yours*.

Just copy the contents of the `mplstyle` file from a theme you like and start customizing! There’s always something to adjust, so choose the one that fits your preferences best. Aim for a stylesheet that gets you about 70% there, so you don’t have to start from scratch.

*What’s your favorite built-in Matplotlib theme?* Let me know in the comments below.