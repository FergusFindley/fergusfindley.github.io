---
layout: post
title: "Exploring 67 years of LEGO"
date: '2017-11-22 19:26 +0100'
author: Fergus Findley
tags:
  - learning
  - DataFrame
  - pandas
  - DataCamp
description: >-
  DataCamp project.``
image: https://s3.amazonaws.com/assets.datacamp.com/production/project_10/datasets/lego-bricks.jpeg
---

## 1. Introduction
<p>Everyone loves Lego (unless you ever stepped on one). Did you know by the way that "Lego" was derived from the Danish phrase leg godt, which means "play well"? Unless you speak Danish, probably not. </p>
<p>In this project, we will analyze a fascinating dataset on every single lego block that has ever been built!</p>
<p><img src="https://s3.amazonaws.com/assets.datacamp.com/production/project_10/datasets/lego-bricks.jpeg" alt="lego"></p>


```python
# Nothing to do here
```

## 2. Reading Data
<p>A comprehensive database of lego blocks is provided by <a href="https://rebrickable.com/downloads/">Rebrickable</a>. The data is available as csv files and the schema is shown below.</p>
<p><img src="https://s3.amazonaws.com/assets.datacamp.com/production/project_10/datasets/downloads_schema.png" alt="schema"></p>
<p>Let us start by reading in the colors data to get a sense of the diversity of lego sets!</p>


```python
# Import modules
import pandas as pd

# Read colors data
colors = pd.read_csv('datasets/colors.csv')

# Print the first few rows
colors.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>rgb</th>
      <th>is_trans</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1</td>
      <td>Unknown</td>
      <td>0033B2</td>
      <td>f</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Black</td>
      <td>05131D</td>
      <td>f</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Blue</td>
      <td>0055BF</td>
      <td>f</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Green</td>
      <td>237841</td>
      <td>f</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>Dark Turquoise</td>
      <td>008F9B</td>
      <td>f</td>
    </tr>
  </tbody>
</table>
</div>



## 3. Exploring Colors
<p>Now that we have read the <code>colors</code> data, we can start exploring it! Let us start by understanding the number of colors available.</p>


```python
# How many distinct colors are available?
# -- YOUR CODE FOR TASK 3 --
num_colors = len(colors.name.unique())
num_colors
```




    135



## 4. Transparent Colors in Lego Sets
<p>The <code>colors</code> data has a column named <code>is_trans</code> that indicates whether a color is transparent or not. It would be interesting to explore the distribution of transparent vs. non-transparent colors.</p>


```python
# colors_summary: Distribution of colors based on transparency
# -- YOUR CODE FOR TASK 4 --
#colors_summary = colors.is_trans.value_counts()
#colors.is_trans.count()
colors_summary = colors.groupby('is_trans').count()

colors_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>rgb</th>
    </tr>
    <tr>
      <th>is_trans</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>f</th>
      <td>107</td>
      <td>107</td>
      <td>107</td>
    </tr>
    <tr>
      <th>t</th>
      <td>28</td>
      <td>28</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>



## 5. Explore Lego Sets
<p>Another interesting dataset available in this database is the <code>sets</code> data. It contains a comprehensive list of sets over the years and the number of parts that each of these sets contained. </p>
<p><img src="https://imgur.com/1k4PoXs.png" alt="sets_data"></p>
<p>Let us use this data to explore how the average number of parts in Lego sets has varied over the years.</p>


```python
%matplotlib inline
# Read sets data as `sets`
sets = pd.read_csv('datasets/sets.csv')
# Create a summary of average number of parts by year: `parts_by_year`
parts_by_year = sets.pivot_table(columns='year', values='num_parts')
# Plot trends in average number of parts by year
parts_by_year.T.plot()

```




    <matplotlib.axes._subplots.AxesSubplot at 0xc32eb00>




![png](Exploring67YearsOfLEGO_files/Exploring67YearsOfLEGO_9_1.png)


## 6. Lego Themes Over Years
<p>Lego blocks ship under multiple <a href="https://shop.lego.com/en-US/Themes">themes</a>. Let us try to get a sense of how the number of themes shipped has varied over the years.</p>


```python
sets[['year', 'theme_id']].groupby('year').count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>theme_id</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1950</th>
      <td>7</td>
    </tr>
    <tr>
      <th>1953</th>
      <td>4</td>
    </tr>
    <tr>
      <th>1954</th>
      <td>14</td>
    </tr>
    <tr>
      <th>1955</th>
      <td>28</td>
    </tr>
    <tr>
      <th>1956</th>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
# themes_by_year: Number of themes shipped by year
# -- YOUR CODE HERE --

themes_by_year = sets[['year', 'theme_id']].groupby(by='year', as_index=False).agg({'theme_id': pd.Series.count})

#themes_by_year = sets[[___, ___]].\
 # ___(___, as_index = False).\
  #agg({"theme_id": pd.Series.___})
themes_by_year.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>theme_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1950</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1953</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1954</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1955</td>
      <td>28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1956</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



## 7. Wrapping It All Up!
<p>Lego blocks offer an unlimited amount of fun across ages. We explored some interesting trends around colors, parts, and themes. </p>


```python
# Nothing to do here
```
