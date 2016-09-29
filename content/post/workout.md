+++
date = "2016-09-07T00:10:10-04:00"
description = "Using Python's pandas and ggplot packages to analyze and plot our workouts."
draft = true
title = "Analyzing Our Workout History"
tags = [ "python", "visualization", "ggplot", "pandas"]
categories = [ "data" ]

+++

# Setup

```sh
# Create a virtual environment with Python3 as default
mkproject -p python3 workout_post

# Within the virtualenv, install some packages
pip install pandas
```

Follow [the instructions](https://developers.google.com/sheets/quickstart/python)
to get set up to use the Google Sheets API.  This is only if you want to read
your data in from Google Sheets obviously.


# Reading in the Data and Cleaning it Up

```python
import pandas as pd

# Read in our Google Spreadsheet with Pandas
# Note: the spreadsheet has to be 
sheet_url = ('https://docs.google.com/spreadsheets/d/'
             '19Nl8qft7kv1cZt2VUneql0OgUsSmO4OE3yTbfaR9_o4/'
             'export?gid=0&format=csv')
workout_data = pd.read_csv(sheet_url, parse_dates=['date'])
```

# Summarize our Workout Dedication

```python
# Let's rename our data frame to make it a bit easier to work with
wd = workout_data

# And rename our columns for easier reference as well
wd.columns = ['date', 'alex_ex', 'alex_desc', 'laur_ex', 'laur_desc']

# Look at the top 5 rows to make sure it looks alright
wd.head()

# See how many rows we're dealing with
len(wd)

# Or get both dimensions of the data
wd.shape

# Get a summary of the [numerical] data.  Hmm, why the 'NaN's?
wd.describe()
# /Users/alexscott/virtualenvs/workout_post/lib/python3.5/site-packages/numpy/lib/function_base.py:3834: RuntimeWarning: Invalid value encountered in percentile
# RuntimeWarning)
#        alex_exercised  babe_exercised
# count      490.000000      487.000000
# mean         0.511224        0.575975
# std          0.489539        0.482596
# min          0.000000        0.000000
# 25%          0.000000             NaN
# 50%          0.500000             NaN
# 75%          1.000000             NaN
# max          1.000000        1.000000

# Looks like Laur forgot to fill in some dates!  Let's fix that real quick
# and just give her zeros.
wd['laur_ex'].fillna(0, inplace=True)
wd.describe()  # much better

# Look at counts of the data
wd.alex_ex.value_counts()
# 1.0    240
# 0.0    229
# 0.5     21

wd.laur_ex.value_counts()
# 1.0    269
# 0.0    198
# 0.5     23

```