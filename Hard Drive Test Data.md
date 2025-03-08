---
title: "Hard Drive Test Data"
source: "https://www.backblaze.com/cloud-storage/resources/hard-drive-test-data"
author:
published:
created: 2025-02-16
description: "Hard Drive test data from the Backblaze data center. Backblaze is affordable, easy-to-use cloud storage."
tags:
  - "clippings"
---
Since 2013, Backblaze has collected, curated, and published the annualized failure rates (AFR) and related statistics from the hard disk drives (HDDs) and solid state drives (SSDs) in our data centers. This collection is the Backblaze Drive Stats dataset. Each quarter we publish updates to the dataset which is open source and can be downloaded using the links in the “**Downloading the Drive Stats Dataset**” section below.

## Drive Stats Q4 2024 Snapshot

### Drive count

#### 300,633

### Drive failures

#### 994

### Drive days

#### 26,926,070

### Drive population by manufacturer

#### HGST

#### Seagate

#### Toshiba

#### WDC

### Drive reliability: annualized failure rates (AFR)

Drives failed

Drives failed

## Drive Stats quarterly reports and related articles

We publish our analyses, observations, and insights based on the Drive Stats dataset on a regular basis on the Backblaze Blog which includes the quarterly Hard Drive Stats reports and SSD reports, and related topics such as the cost of storage, bathtub curve and hard drives, and more.

[

Learn More

](https://www.backblaze.com/blog/category/cloud-storage/hard-drive-stats/)

## Overview of the Drive Stats dataset

**How we collect the data**

Each day at each Backblaze data center, we take a snapshot of each operational drive. This snapshot includes basic drive information along with the S.M.A.R.T. statistics reported by that drive. The daily snapshot of one drive is one record or row of data. All of the drive snapshots for a given day are collected into a file consisting of a row for each active drive. The format of this file is a ".csv" (Comma Separated Values) file. Each day this file is named in the format YYYY-MM-DD.csv, for example, 2024-03-25.csv.

‍

**How the data is organized**

The Drive Stats schema is comprised of fields Backblaze includes for each drive record and the raw and normalized S.M.A.R.T. attributes reported by each drive.

- Download a .csv file of the current Drive Stats schema: [https://f001.backblazeb2.com/file/Backblaze-Hard-Drive-Data/Drive\_Stats\_Schema\_Current.csv](https://f001.backblazeb2.com/file/Backblaze-Hard-Drive-Data/Drive_Stats_Schema_Current.csv)
- Download a .csv file of the Drive Stats schema changes from Q1 2018 onward: [https://f001.backblazeb2.com/file/Backblaze-Hard-Drive-Data/Drive\_Stats\_Schema\_2018\_Onward.csv](https://f001.backblazeb2.com/file/Backblaze-Hard-Drive-Data/Drive_Stats_Schema_2018_Onward.csv)

Please note, schema changes from quarter to quarter do occur, so you should always check for such changes each quarter and align the data to reflect any changes.

‍

**How you can use the data**

The Drive Stats dataset is open source and available for you to download below, all we ask is is the following:

1. you cite Backblaze as the source if you use the data,
2. you accept that you are solely responsible for how you use the data,
3. you may sell derivative works based on the data, but
4. you can not sell the data itself to anyone, it is free.

## Downloading the Drive Stats dataset

Beginning in 2016 we uploaded the Drive Stats dataset for a given quarter. Prior to 2016 the datasets uploaded were annual (2013, 2014, and 2015). Each item listed below is a ZIP file of containing the .csv files for the named quarter or year. 

All

![arrow](https://cdn.prod.website-files.com/63d32de856f6323a43a277f2/643594d64c934cd60ae50d04_dropdown-arrow.svg)