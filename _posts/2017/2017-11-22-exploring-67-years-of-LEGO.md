---
layout: post
title: "Exploring 67 years of LEGO"
date: '2017-11-22 20:26 +0100'
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


```python
%%nose
def test_default():
  assert True
```






    1/1 tests passed
    



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




```python
%%nose
def test_colors_exists():
    assert 'colors' in globals(), "You should read the data into a variable named `colors`"
```






    1/1 tests passed
    



## 3. Exploring Colors
<p>Now that we have read the <code>colors</code> data, we can start exploring it! Let us start by understanding the number of colors available.</p>


```python
# How many distinct colors are available?
# -- YOUR CODE FOR TASK 3 --
num_colors = len(colors.name.unique())
num_colors
```




    135




```python
%%nose
def test_num_colors():
    assert num_colors == 135, "The variable num_colors should equal 135"
```






    1/1 tests passed
    



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




```python
%%nose
def test_colors_summary_exists():
    assert 'colors_summary' in globals(), "You should have defined a variable named `colors_summary`"
def test_colors_summary():
    assert colors_summary.shape == (2, 3), "The DataFrame colors_summary should contain 2 rows and 3 columns"
```






    1/2 tests passed; 1 failed
    ========
    __main__.test_colors_summary
    ========
    Traceback (most recent call last):
      File "/usr/lib/python3.5/unittest/case.py", line 58, in testPartExecutor
        yield
      File "/usr/lib/python3.5/unittest/case.py", line 600, in run
        testMethod()
      File "/usr/local/lib/python3.5/dist-packages/nose/case.py", line 198, in runTest
        self.test(*self.arg)
      File "<string>", line 4, in test_colors_summary
    AssertionError: The DataFrame colors_summary should contain 2 rows and 3 columns
    
    



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
parts_by_year.plot()

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fdde00d6080>




![png](Exploring67YearsOfLEGO_files/Exploring67YearsOfLEGO_13_1.png)



```python
%%nose
def test_sets_exists():
    assert 'sets' in globals(), "You should read the data into a variable named `sets`"
def test_parts_by_year_exists():
    assert 'parts_by_year' in globals(), "You should have defined a variable named `parts_by_year`"
```






    2/2 tests passed
    



## 6. Lego Themes Over Years
<p>Lego blocks ship under multiple <a href="https://shop.lego.com/en-US/Themes">themes</a>. Let us try to get a sense of how the number of themes shipped has varied over the years.</p>


```python
sets[['year', 'theme_id']].groupby('year').count()
```




<div>
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
    <tr>
      <th>1957</th>
      <td>21</td>
    </tr>
    <tr>
      <th>1958</th>
      <td>42</td>
    </tr>
    <tr>
      <th>1959</th>
      <td>4</td>
    </tr>
    <tr>
      <th>1960</th>
      <td>3</td>
    </tr>
    <tr>
      <th>1961</th>
      <td>17</td>
    </tr>
    <tr>
      <th>1962</th>
      <td>40</td>
    </tr>
    <tr>
      <th>1963</th>
      <td>18</td>
    </tr>
    <tr>
      <th>1964</th>
      <td>11</td>
    </tr>
    <tr>
      <th>1965</th>
      <td>10</td>
    </tr>
    <tr>
      <th>1966</th>
      <td>89</td>
    </tr>
    <tr>
      <th>1967</th>
      <td>21</td>
    </tr>
    <tr>
      <th>1968</th>
      <td>25</td>
    </tr>
    <tr>
      <th>1969</th>
      <td>69</td>
    </tr>
    <tr>
      <th>1970</th>
      <td>29</td>
    </tr>
    <tr>
      <th>1971</th>
      <td>45</td>
    </tr>
    <tr>
      <th>1972</th>
      <td>38</td>
    </tr>
    <tr>
      <th>1973</th>
      <td>68</td>
    </tr>
    <tr>
      <th>1974</th>
      <td>39</td>
    </tr>
    <tr>
      <th>1975</th>
      <td>31</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>68</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>92</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>73</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>82</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>88</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>79</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>68</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>114</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>85</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>106</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>115</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>111</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>128</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>128</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>144</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>194</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>325</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>300</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>327</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>339</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>447</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>415</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>371</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>330</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>283</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>319</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>349</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>403</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>444</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>502</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>615</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>593</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>715</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>670</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>609</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>470</td>
    </tr>
  </tbody>
</table>
<p>66 rows × 1 columns</p>
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




```python
%%nose
def test_themes_by_year_exists():
    assert 'themes_by_year' in globals(), "You should have defined a variable named `themes_by_year`"
def test_themes_by_year():
    assert themes_by_year.shape == (66, 2), "The DataFrame themes_by_year should contain 66 rows and 2 columns"
def test_themes_by_year_names():
    colnames = ['year', 'theme_id']
    assert all(name in themes_by_year for name in colnames), "Your DataFrame, bnames, should have columns named: year, theme_id"
```






    3/3 tests passed
    



## 7. Wrapping It All Up!
<p>Lego blocks offer an unlimited amount of fun across ages. We explored some interesting trends around colors, parts, and themes. </p>


```python
# Nothing to do here
```


```python
%%nose
def test_default():
  assert True
```






    1/1 tests passed
    


