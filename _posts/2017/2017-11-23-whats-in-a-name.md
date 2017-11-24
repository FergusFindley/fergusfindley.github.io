---
layout: post
title: "What's in a name"
date: '2017-11-23 19:26 +0100'
author: Fergus Findley
tags:
  - learning
  - DataFrame
  - pandas
  - DataCamp
description: >-
  DataCamp project.``
image: 
---
## 1. Introduction to Baby Names Data
<blockquote>
  <p>What’s in a name? That which we call a rose, By any other name would smell as sweet.</p>
</blockquote>
<p>In this project, we will explore a rich dataset of first names of babies born in the US, that spans a period of more than 100 years! This suprisingly simple dataset can help us uncover so many interesting stories, and that is exactly what we are going to be doing. </p>
<p>Let us start by reading the data.</p>


```python
# Import modules
import pandas as pd

# Read names into a dataframe: bnames
bnames = pd.read_csv('datasets/names.csv.gz')

bnames.head()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>sex</th>
      <th>births</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mary</td>
      <td>F</td>
      <td>7065</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Anna</td>
      <td>F</td>
      <td>2604</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emma</td>
      <td>F</td>
      <td>2003</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Elizabeth</td>
      <td>F</td>
      <td>1939</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Minnie</td>
      <td>F</td>
      <td>1746</td>
      <td>1880</td>
    </tr>
  </tbody>
</table>
</div>




```python
%%nose
def test_bnames_exists():
    """bnames is defined."""
    assert 'bnames' in globals(), "You should have defined a variable named bnames"
# bnames is a dataframe with 1891894 rows and 4 columns
def test_bnames_dataframe():
    """bnames is a DataFrame with 1891894 rows and 4 columns"""
    import pandas as pd
    assert isinstance(bnames, pd.DataFrame)
    assert bnames.shape[0] == 1891894, "Your  DataFrame, bnames, should contain 1891984 rows"
    assert bnames.shape[1] == 4, "Your DataFrame, bnames, should contain 4 columns"

# bnames has column names ['name', 'sex', 'births', 'year']
def test_bnames_colnames():
    """bnames has column names ['name', 'sex', 'births', 'year']"""
    colnames = ['name', 'sex', 'births', 'year']
    assert all(name in bnames for name in colnames), "Your DataFrame, bnames, should have columns named name, sex, births and year"
```






    3/3 tests passed
    



## 2. Exploring Trends in Names
<p>One of the first things we want to do is to understand naming trends. Let us start by figuring out the top five most popular male and female names for this decade (born 2011 and later). Do you want to make any guesses? Go on, be a sport!!</p>


```python
# bnames_top5: A dataframe with top 5 popular male and female names for the decade

bnames_decade = bnames[bnames['year']>=2011]
#bnames_decade.groupby(['sex','name']).agg({'births':sum}).sort_values(['births'], ascending=False)
bnames_decade_agg = bnames_decade.groupby(['sex','name'], as_index=False)['births'].sum()
bnames_top5 = bnames_decade_agg.sort_values(['sex','births'],ascending=[True,False]).groupby('sex').head()
bnames_top5
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sex</th>
      <th>name</th>
      <th>births</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9304</th>
      <td>F</td>
      <td>Emma</td>
      <td>121375</td>
    </tr>
    <tr>
      <th>26546</th>
      <td>F</td>
      <td>Sophia</td>
      <td>117352</td>
    </tr>
    <tr>
      <th>22720</th>
      <td>F</td>
      <td>Olivia</td>
      <td>111691</td>
    </tr>
    <tr>
      <th>11799</th>
      <td>F</td>
      <td>Isabella</td>
      <td>103947</td>
    </tr>
    <tr>
      <th>4124</th>
      <td>F</td>
      <td>Ava</td>
      <td>94507</td>
    </tr>
    <tr>
      <th>46014</th>
      <td>M</td>
      <td>Noah</td>
      <td>110280</td>
    </tr>
    <tr>
      <th>44593</th>
      <td>M</td>
      <td>Mason</td>
      <td>105104</td>
    </tr>
    <tr>
      <th>38946</th>
      <td>M</td>
      <td>Jacob</td>
      <td>104722</td>
    </tr>
    <tr>
      <th>43724</th>
      <td>M</td>
      <td>Liam</td>
      <td>103250</td>
    </tr>
    <tr>
      <th>51129</th>
      <td>M</td>
      <td>William</td>
      <td>99144</td>
    </tr>
  </tbody>
</table>
</div>




```python
%%nose
def test_bnames_top5_exists():
    """bnames_top5 is defined."""
    assert 'bnames_top5' in globals(), \
      "You should have defined a variable named bnames_top5."

def test_bnames_top5_df():
    """Output is a DataFrame with 10 rows and 3 columns."""
    assert bnames_top5.shape == (10, 3), \
      "Your DataFrame, bnames_top5, should have 10 rows and 3 columns."

def test_bnames_top5_df_colnames():
    """Output has column names: name, sex, births."""
    assert all(name in bnames_top5 for name in ['name', 'sex', 'births']), \
      "Your DataFrame, bnames_top5 should have columns named name, sex, births."

def test_bnames_top5_df_contains_names():
    """Output has the follwing female names: Emma, Sophia, Olivia, Isabella, Ava"""
    target_names = ['Emma', 'Sophia', 'Olivia', 'Isabella', 'Ava']
    assert set(target_names).issubset(bnames_top5['name']), \
      "Your DataFrame, bnames_top5 should contain the female names: Emma, Sophia, Olivia, Isabella, Ava"

def test_bnames_top5_df_contains_female_names():
    """Output has the following male names: Noah, Mason, Jacob, Liam, William"""
    target_names = ['Noah', 'Mason', 'Jacob', 'Liam', 'William']
    assert set(target_names).issubset(bnames_top5['name']), \
      "Your DataFrame, bnames_top5 should contain the male names: Noah, Mason, Jacob, Liam, William"
```






    5/5 tests passed
    



## 3. Proportion of Births
<p>While the number of births is a useful metric, making comparisons across years becomes difficult, as one would have to control for population effects. One way around this is to normalize the number of births by the total number of births in that year.</p>


```python
bnames2 = bnames.copy()
# Compute the proportion of births by year and add it as a new column
# -- YOUR CODE HERE --
bnames2['births_per_year'] = bnames2.groupby('year')['births'].transform(sum)
bnames2['prop_births']=bnames2['births']/bnames2['births_per_year']
bnames2 = bnames2.drop('births_per_year',axis=1)
bnames2.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>sex</th>
      <th>births</th>
      <th>year</th>
      <th>prop_births</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mary</td>
      <td>F</td>
      <td>7065</td>
      <td>1880</td>
      <td>0.035065</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Anna</td>
      <td>F</td>
      <td>2604</td>
      <td>1880</td>
      <td>0.012924</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emma</td>
      <td>F</td>
      <td>2003</td>
      <td>1880</td>
      <td>0.009941</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Elizabeth</td>
      <td>F</td>
      <td>1939</td>
      <td>1880</td>
      <td>0.009624</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Minnie</td>
      <td>F</td>
      <td>1746</td>
      <td>1880</td>
      <td>0.008666</td>
    </tr>
  </tbody>
</table>
</div>




```python
%%nose
def test_bnames2_exists():
    """bnames2 is defined."""
    assert 'bnames2' in globals(),\
      "You should have defined a variable named bnames2."
    
def test_bnames2_dataframe():
    """bnames2 is a DataFrame with 1891894 rows and 5 columns"""
    import pandas as pd
    assert isinstance(bnames2, pd.DataFrame)
    assert bnames2.shape[1] == 5,\
      "Your DataFrame, bnames2, should have 5 columns"
    assert bnames2.shape[0] == 1891894,\
      "Your DataFrame, bnames2,  should have 1891894 rows"


def test_bnames2_colnames():
    """bnames2 has column names ['name', 'sex', 'births', 'year', 'prop_births']"""
    colnames = ['name', 'sex', 'births', 'year', 'prop_births']
    assert all(name in bnames2 for name in colnames),\
      "Your DataFrame, bnames2, should have column names 'name', 'sex', 'births', 'year', 'prop_births'"
```






    3/3 tests passed
    



## 4. Popularity of Names
<p>Now that we have the proportion of births, let us plot the popularity of a name through the years. How about plotting the popularity of the female names <code>Elizabeth</code>, and <code>Deneen</code>, and inspecting the underlying trends for any interesting patterns!</p>


```python
# Set up matplotlib for plotting in the notebook.
%matplotlib inline
import matplotlib.pyplot as plt

def plot_trends(name, sex):
    # -- YOUR CODE HERE --
    temp = bnames2[(bnames2.sex==sex) & (bnames2.name==name)]
    plt.plot(temp.year, temp.prop_births, label=name)
    plt.legend()
    plt.xlabel('year')
    plt.ylabel('proportion of births')
    return


# Plot trends for Elizabeth and Deneen 
# -- YOUR CODE HERE --
plot_trends('Elizabeth', 'F')
plot_trends('Deneen', 'F')
# How many times did these female names peak?
num_peaks_elizabeth = 3
num_peaks_deneen    = 1
```


![png](2017-11-23-whats-in-a-name_files/2017-11-23-whats-in-a-name_10_0.png)



```python
%%nose
def test_peaks_elizabeth():
    """The name Elizabeth peaks 3 times."""
    assert num_peaks_elizabeth == 3, \
      "The name Elizabeth peaks 3 times"
    
def test_peaks_deneen():
    """The name Deneen peaks 1 time."""
    assert num_peaks_deneen == 1, \
      "The name Deneen peaks only once"
```






    2/2 tests passed
    



## 5. Trendy vs. Stable Names
<p>Based on the plots we created earlier, we can see that <strong>Elizabeth</strong> is a fairly stable name, while <strong>Deneen</strong> is not. An interesting question to ask would be what are the top 5 stable and top 5 trendiest names. A stable name is one whose proportion across years does not vary drastically, while a trendy name is one whose popularity peaks for a short period and then dies down. </p>
<p>There are many ways to measure trendiness. A simple measure would be to look at the maximum proportion of births for a name, normalized by the sume of proportion of births across years. For example, if the name <code>Joe</code> had the proportions <code>0.1, 0.2, 0.1, 0.1</code>, then the trendiness measure would be <code>0.2/(0.1 + 0.2 + 0.1 + 0.1)</code> which equals <code>0.5</code>.</p>
<p>Let us use this idea to figure out the top 10 trendy names in this data set, with at least a 1000 births.</p>


```python
# top10_trendy_names | A Data Frame of the top 10 most trendy names
names = pd.DataFrame()
name_and_sex_grouped = bnames2.groupby(['name','sex'])
names['total'] = name_and_sex_grouped['births'].sum()
#bnames2 = bnames2[bnames2.total>=1000]

names['max'] = name_and_sex_grouped['births'].max()

names = names[names.total >= 1000]

names['trendiness']=names['max']/names['total']
top10_trendy_names = names.sort_values('trendiness', ascending=False).head(10).reset_index()

top10_trendy_names
#bnames2['max'] = bnames2.groupby(['name','sex'])['births'].transform(max)
#bnames2['trendiness'] = bnames2['max']/bnames2['total'] 
#bnames2 = bnames2.sort_values('trendiness', ascending=False)
#bnames2.head()
#bnames_over1000 = bynames[bynames.births>=1000]
#bnames_over1000.sort_values('births')

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>sex</th>
      <th>total</th>
      <th>max</th>
      <th>trendiness</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Christop</td>
      <td>M</td>
      <td>1082</td>
      <td>1082</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Royalty</td>
      <td>F</td>
      <td>1057</td>
      <td>581</td>
      <td>0.549669</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kizzy</td>
      <td>F</td>
      <td>2325</td>
      <td>1116</td>
      <td>0.480000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aitana</td>
      <td>F</td>
      <td>1203</td>
      <td>564</td>
      <td>0.468828</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Deneen</td>
      <td>F</td>
      <td>3602</td>
      <td>1604</td>
      <td>0.445308</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Moesha</td>
      <td>F</td>
      <td>1067</td>
      <td>426</td>
      <td>0.399250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Marely</td>
      <td>F</td>
      <td>2527</td>
      <td>1004</td>
      <td>0.397309</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Kanye</td>
      <td>M</td>
      <td>1304</td>
      <td>507</td>
      <td>0.388804</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Tennille</td>
      <td>F</td>
      <td>2172</td>
      <td>769</td>
      <td>0.354052</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kadijah</td>
      <td>F</td>
      <td>1411</td>
      <td>486</td>
      <td>0.344437</td>
    </tr>
  </tbody>
</table>
</div>




```python
%%nose
def test_top10_trendy_names_exists():
    """top10_trendy_names is defined"""
    assert 'top10_trendy_names' in globals(), \
      "You should have defined a variable namedtop10_trendy_names."
def test_top10_trendy_df():
    """top10_trendy_names is a dataframe with 10 rows and 5 columns."""
    assert top10_trendy_names.shape == (10, 5), \
      "Your data frame, top10_trendy_names, should have 10 rows and 5 columns."

def test_top10_trendy_df_colnames():
    """top10_trendy_names has column names: name, sex, births, max and trendiness"""
    assert all(name in top10_trendy_names for name in ['name', 'sex', 'total', 'max', 'trendiness']), \
       "Your data frame, top10_trendy_names, should have column names: name, sex, births, max and trendiness"

def test_top10_trendy_df_contains_female_names():
    """top10_trendy_names has the follwing female names: Royalty, Kizzy, Aitana, Deneen, Moesha, Marely, Tennille, Kadijah"""
    target_names = ['Royalty', 'Kizzy', 'Aitana', 'Deneen', 'Moesha', 'Marely', 'Tennille', 'Kadijah']
    assert set(target_names).issubset(top10_trendy_names['name']), \
      "Your data frame, top10_trendy_names, should have female names: Royalty, Kizzy, Aitana, Deneen, Moesha, Marely, Tennille, Kadijah."

def test_top10_trendy_df_contains_male_names():
    """top10_trendy_names has the following male names: Christop, Kanye"""
    target_names = ['Christop', 'Kanye']
    assert set(target_names).issubset(top10_trendy_names['name']), \
      "Your data frame, top10_trendy_names, should have male names: Christop, Kanye"
```






    5/5 tests passed
    



## 6. Bring in Mortality Data
<p>So, what more is in a name? Well, with some further work, it is possible to predict the age of a person based on the name (Whoa! Really????). For this, we will need actuarial data that can tell us the chances that someone is still alive, based on when they were born. Fortunately, the <a href="https://www.ssa.gov/">SSA</a> provides detailed <a href="https://www.ssa.gov/oact/STATS/table4c6.html">actuarial life tables</a> by birth cohorts.</p>
<table>
<thead>
<tr>
<th style="text-align:right;">year</th>
<th style="text-align:right;">age</th>
<th style="text-align:right;">qx</th>
<th style="text-align:right;">lx</th>
<th style="text-align:right;">dx</th>
<th style="text-align:right;">Lx</th>
<th style="text-align:right;">Tx</th>
<th style="text-align:right;">ex</th>
<th style="text-align:left;">sex</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">39</td>
<td style="text-align:right;">0.00283</td>
<td style="text-align:right;">78275</td>
<td style="text-align:right;">222</td>
<td style="text-align:right;">78164</td>
<td style="text-align:right;">3129636</td>
<td style="text-align:right;">39.98</td>
<td style="text-align:left;">F</td>
</tr>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">40</td>
<td style="text-align:right;">0.00297</td>
<td style="text-align:right;">78053</td>
<td style="text-align:right;">232</td>
<td style="text-align:right;">77937</td>
<td style="text-align:right;">3051472</td>
<td style="text-align:right;">39.09</td>
<td style="text-align:left;">F</td>
</tr>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">41</td>
<td style="text-align:right;">0.00318</td>
<td style="text-align:right;">77821</td>
<td style="text-align:right;">248</td>
<td style="text-align:right;">77697</td>
<td style="text-align:right;">2973535</td>
<td style="text-align:right;">38.21</td>
<td style="text-align:left;">F</td>
</tr>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">42</td>
<td style="text-align:right;">0.00332</td>
<td style="text-align:right;">77573</td>
<td style="text-align:right;">257</td>
<td style="text-align:right;">77444</td>
<td style="text-align:right;">2895838</td>
<td style="text-align:right;">37.33</td>
<td style="text-align:left;">F</td>
</tr>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">43</td>
<td style="text-align:right;">0.00346</td>
<td style="text-align:right;">77316</td>
<td style="text-align:right;">268</td>
<td style="text-align:right;">77182</td>
<td style="text-align:right;">2818394</td>
<td style="text-align:right;">36.45</td>
<td style="text-align:left;">F</td>
</tr>
<tr>
<td style="text-align:right;">1910</td>
<td style="text-align:right;">44</td>
<td style="text-align:right;">0.00351</td>
<td style="text-align:right;">77048</td>
<td style="text-align:right;">270</td>
<td style="text-align:right;">76913</td>
<td style="text-align:right;">2741212</td>
<td style="text-align:right;">35.58</td>
<td style="text-align:left;">F</td>
</tr>
</tbody>
</table>
<p>You can read the <a href="https://www.ssa.gov/oact/NOTES/as120/LifeTables_Body.html">documentation for the lifetables</a> to understand what the different columns mean. The key column of interest to us is <code>lx</code>, which provides the number of people born in a <code>year</code> who live upto a given <code>age</code>. The probability of being alive can be derived as <code>lx</code> by 100,000. </p>
<p>Given that 2016 is the latest year in the baby names dataset, we are interested only in a subset of this data, that will help us answer the question, "What percentage of people born in Year X are still alive in 2016?" </p>
<p>Let us use this data and plot it to get a sense of the mortality distribution!</p>


```python
# Read lifetables from datasets/lifetables.csv
lifetables = pd.read_csv('datasets/lifetables.csv')

# Extract subset relevant to those alive in 2016

#lifetables_2016 = lifetables[lifetables['year']+lifetables['age']==2016]

lifetables['dyear']=lifetables['year']+lifetables['age']
still_alive = lifetables[lifetables.dyear==2016]
lifetables_2016 = still_alive.drop('dyear',axis=1)
#lifetables_2016
# Plot the mortality distribution: year vs. lx
#lifetables_2016.groupby('year')['lx'].sum().plot()
lifetables_2016.plot(x='year', y='lx')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f7533381048>




![png](2017-11-23-whats-in-a-name_files/2017-11-23-whats-in-a-name_16_1.png)



```python
ax = lifetables_2016[lifetables_2016.sex=='M'].plot(x='year', y='lx', label='M')
lifetables_2016[lifetables_2016.sex=='F'].plot(x='year', y='lx', label='F', ax=ax)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f753338e2b0>




![png](2017-11-23-whats-in-a-name_files/2017-11-23-whats-in-a-name_17_1.png)



```python
%%nose
def test_lifetables_2016_exists():
    """lifetables_2016 is defined"""
    assert 'lifetables_2016' in globals(), \
      "You should have defined a variable named lifetables_2016."
def test_lifetables_2016_df():
    """Output is a DataFrame with 24 rows and 9 columns."""
    assert lifetables_2016.shape == (24, 9), \
      "Your DataFrame, lifetables_2016, should have 24 rows and 9 columns."

def test_lifetables_2016_df_colnames():
    """Output has column names: year, age, qx, lx, dx, Lx, Tx, ex, sex"""
    assert all(name in lifetables_2016 for name in ['year', 'age', 'qx', 'lx', 'dx', 'Lx', 'Tx', 'ex', 'sex']), \
      "Your DataFrame, lifetables_2016, should have columns named: year, age, qx, lx, dx, Lx, Tx, ex, sex."

def test_lifetables_2016_df_year_plus_age():
    """Output has the year + age = 2016"""
    assert all(lifetables_2016.year + lifetables_2016.age - 2016 == 0), \
      "The `year` column and `age` column in `lifetables_2016` should sum up to 2016."
```






    4/4 tests passed
    



## 7. Smoothen the Curve!
<p>We are almost there. There is just one small glitch. The cohort life tables are provided only for every decade. In order to figure out the distribution of people alive, we need the probabilities for every year. One way to fill up the gaps in the data is to use some kind of interpolation. Let us keep things simple and use linear interpolation to fill out the gaps in values of <code>lx</code>, between the years <code>1900</code> and <code>2016</code>.</p>


```python
# Create smoothened lifetable_2016_s by interpolating values of lx
import numpy as np
#lifetable_2016_s = lifetables_2016.sort_values(['sex','year']).copy()
#lifetable_2016_s.interpolate(method='linear',)

year = np.arange(1900, 2016)
#year
mf = {"M": pd.DataFrame(), "F": pd.DataFrame()}
#mf
#lifetables_2016[lifetables_2016['sex'] == 'M'][["year", "lx"]].set_index('year').reindex(year).interpolate().reset_index()
for sex in ["M", "F"]:
    d = lifetables_2016[lifetables_2016['sex'] == sex][["year", "lx"]]
    mf[sex] = d.set_index('year').reindex(year).interpolate().reset_index()
    mf[sex]['sex'] = sex
#type(pd.concat(mf, ignore_index=True))
#pd.concat(mf, ignore_index=True)
lifetable_2016_s = pd.concat(mf, ignore_index = True)
lifetable_2016_s
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>lx</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1900</td>
      <td>0.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901</td>
      <td>6.1</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902</td>
      <td>12.2</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903</td>
      <td>18.3</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1904</td>
      <td>24.4</td>
      <td>F</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1905</td>
      <td>30.5</td>
      <td>F</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1906</td>
      <td>36.6</td>
      <td>F</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1907</td>
      <td>42.7</td>
      <td>F</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1908</td>
      <td>48.8</td>
      <td>F</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1909</td>
      <td>54.9</td>
      <td>F</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1910</td>
      <td>61.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1911</td>
      <td>597.7</td>
      <td>F</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1912</td>
      <td>1134.4</td>
      <td>F</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1913</td>
      <td>1671.1</td>
      <td>F</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1914</td>
      <td>2207.8</td>
      <td>F</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1915</td>
      <td>2744.5</td>
      <td>F</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1916</td>
      <td>3281.2</td>
      <td>F</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1917</td>
      <td>3817.9</td>
      <td>F</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1918</td>
      <td>4354.6</td>
      <td>F</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1919</td>
      <td>4891.3</td>
      <td>F</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1920</td>
      <td>5428.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1921</td>
      <td>8393.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1922</td>
      <td>11358.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1923</td>
      <td>14323.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1924</td>
      <td>17288.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1925</td>
      <td>20253.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1926</td>
      <td>23218.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1927</td>
      <td>26183.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1928</td>
      <td>29148.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1929</td>
      <td>32113.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>202</th>
      <td>1986</td>
      <td>96718.2</td>
      <td>M</td>
    </tr>
    <tr>
      <th>203</th>
      <td>1987</td>
      <td>96904.9</td>
      <td>M</td>
    </tr>
    <tr>
      <th>204</th>
      <td>1988</td>
      <td>97091.6</td>
      <td>M</td>
    </tr>
    <tr>
      <th>205</th>
      <td>1989</td>
      <td>97278.3</td>
      <td>M</td>
    </tr>
    <tr>
      <th>206</th>
      <td>1990</td>
      <td>97465.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>207</th>
      <td>1991</td>
      <td>97607.3</td>
      <td>M</td>
    </tr>
    <tr>
      <th>208</th>
      <td>1992</td>
      <td>97749.6</td>
      <td>M</td>
    </tr>
    <tr>
      <th>209</th>
      <td>1993</td>
      <td>97891.9</td>
      <td>M</td>
    </tr>
    <tr>
      <th>210</th>
      <td>1994</td>
      <td>98034.2</td>
      <td>M</td>
    </tr>
    <tr>
      <th>211</th>
      <td>1995</td>
      <td>98176.5</td>
      <td>M</td>
    </tr>
    <tr>
      <th>212</th>
      <td>1996</td>
      <td>98318.8</td>
      <td>M</td>
    </tr>
    <tr>
      <th>213</th>
      <td>1997</td>
      <td>98461.1</td>
      <td>M</td>
    </tr>
    <tr>
      <th>214</th>
      <td>1998</td>
      <td>98603.4</td>
      <td>M</td>
    </tr>
    <tr>
      <th>215</th>
      <td>1999</td>
      <td>98745.7</td>
      <td>M</td>
    </tr>
    <tr>
      <th>216</th>
      <td>2000</td>
      <td>98888.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>217</th>
      <td>2001</td>
      <td>98928.8</td>
      <td>M</td>
    </tr>
    <tr>
      <th>218</th>
      <td>2002</td>
      <td>98969.6</td>
      <td>M</td>
    </tr>
    <tr>
      <th>219</th>
      <td>2003</td>
      <td>99010.4</td>
      <td>M</td>
    </tr>
    <tr>
      <th>220</th>
      <td>2004</td>
      <td>99051.2</td>
      <td>M</td>
    </tr>
    <tr>
      <th>221</th>
      <td>2005</td>
      <td>99092.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>222</th>
      <td>2006</td>
      <td>99132.8</td>
      <td>M</td>
    </tr>
    <tr>
      <th>223</th>
      <td>2007</td>
      <td>99173.6</td>
      <td>M</td>
    </tr>
    <tr>
      <th>224</th>
      <td>2008</td>
      <td>99214.4</td>
      <td>M</td>
    </tr>
    <tr>
      <th>225</th>
      <td>2009</td>
      <td>99255.2</td>
      <td>M</td>
    </tr>
    <tr>
      <th>226</th>
      <td>2010</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>227</th>
      <td>2011</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>228</th>
      <td>2012</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>229</th>
      <td>2013</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>230</th>
      <td>2014</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>231</th>
      <td>2015</td>
      <td>99296.0</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
<p>232 rows × 3 columns</p>
</div>




```python
%%nose
def test_lifetable_2016_s_exists():
    """lifetable_2016_s is defined"""
    assert 'lifetable_2016_s' in globals(), \
      "You should have defined a variable named lifetable_2016_s."
def test_lifetables_2016_s_df():
    """lifetable_2016_s is a dataframe with 232 rows and 3 columns."""
    assert lifetable_2016_s.shape == (232, 3), \
      "Your DataFrame, lifetable_2016_s, should have 232 rows and 3 columns."

def test_lifetable_2016_s_df_colnames():
    """lifetable_2016_s has column names: year, lx, sex"""
    assert all(name in lifetable_2016_s for name in ['year', 'lx', 'sex']), \
      "Your DataFrame, lifetable_2016_s, should have columns named: year, lx, sex."
```






    3/3 tests passed
    



## 8. Distribution of People Alive by Name
<p>Now that we have all the required data, we need a few helper functions to help us with our analysis. </p>
<p>The first function we will write is <code>get_data</code>,which takes <code>name</code> and <code>sex</code> as inputs and returns a data frame with the distribution of number of births and number of people alive by year.</p>
<p>The second function is <code>plot_name</code> which accepts the same arguments as <code>get_data</code>, but returns a line plot of the distribution of number of births, overlaid by an area plot of the number alive by year.</p>
<p>Using these functions, we will plot the distribution of births for boys named <strong>Joseph</strong> and girls named <strong>Brittany</strong>.</p>


```python
def get_data(name, sex):
       # YOUR CODE HERE
    bnames_name_sex = bnames[(bnames.name==name)&(bnames.sex==sex)]
    lifetable_2016_s_sex = lifetable_2016_s[lifetable_2016_s.sex == sex]
    data = pd.merge(lifetable_2016_s_sex, bnames_name_sex, how='left', on='year')
    data['n_alive'] = data['lx']*data['births']/100000
    data = data.drop(['sex_y'], axis=1)
    data = data[['name', 'sex_x', 'births', 'year', 'lx', 'n_alive']]
    #print(data)
    return data

  

def plot_data(name, sex):
    # YOUR CODE HERE
    ax = get_data(name,sex).plot(x='year', y='births')
    get_data(name,sex).plot(kind='area',alpha=0.5, x='year', y='n_alive', ax=ax)
    return 
    
# Plot the distribution of births and number alive for Joseph and Brittany
plot_data('Joseph','M')
plot_data('Brittany','F')
#bnames
#lifetable_2016_s
```


![png](2017-11-23-whats-in-a-name_files/2017-11-23-whats-in-a-name_23_0.png)



![png](2017-11-23-whats-in-a-name_files/2017-11-23-whats-in-a-name_23_1.png)



```python
%%nose
joseph = get_data('Joseph', 'M')
def test_joseph_df():
    """get_data('Joseph', 'M') is a dataframe with 116 rows and 6 columns."""
    assert joseph.shape == (116, 6), \
      "Running  get_data('Joseph', 'M') should return a data frame with 116 rows and 6 columns."

def test_joseph_df_colnames():
    """get_data('Joseph', 'M') has column names: name, sex, births, year, lx, n_alive"""
    assert all(name in lifetable_2016_s for name in ['year', 'lx', 'sex']), \
      "Running  get_data('Joseph', 'M') should return a data frame with column names: name, sex, births, year, lx, n_alive"
```






    2/2 tests passed
    



## 9. Estimate Age
<p>In this section, we want to figure out the probability that a person with a certain name is alive, as well as the quantiles of their age distribution. In particular, we will estimate the age of a female named <strong>Gertrude</strong>. Any guesses on how old a person with this name is? How about a male named <strong>William</strong>?</p>


```python
# Import modules
from wquantiles import quantile

# Function to estimate age quantiles
def estimate_age(name, sex):
    # YOUR CODE HERE
    data = get_data(name,sex)
    data = data.fillna(0)
    qs = [0.25, 0.5, 0.75]
    quantiles = [2016 - int(quantile(data.year, data.n_alive, q)) for q in qs]
    p_alive = data.n_alive.sum()/data.births.sum()
    #data['age']=2016-data['year']
    result = pd.Series(index=['name','p_alive','q25','q50','q75','sex'])
    result['name']=name
    result['p_alive']=p_alive
    result['q25']=quantiles[0]
    result['q50']=quantiles[1]
    result['q75']=quantiles[2]
    result['sex']=sex

    return result

# Estimate the age of Gertrude
estimate_age('Gertrude', 'F')

#  result = dict(zip(['q25', 'q50', 'q75'], quantiles))
#  result['p_alive'] = round(data.n_alive.sum()/data.births.sum()*100, 2)
#  result['sex'] = sex
#  result['name'] = name
#  return pd.Series(result)
```




    name       Gertrude
    p_alive    0.187256
    q25              89
    q50              80
    q75              70
    sex               F
    dtype: object




```python
%%nose
gertrude = estimate_age('Gertrude', 'F')
def test_gertrude_names():
    """Series has indices name, p_alive, q25, q50 and q75"""
    expected_names = ['name', 'p_alive', 'q25', 'q50', 'q75']
    assert all(name in gertrude.index.values for name in expected_names), \
      "Your function `estimate_age` should return a series with names: name, p_alive, q25, q50 and q75"

def test_gertrude_q50():
    """50th Percentile of age for Gertrude is between 75 and 85"""
    assert ((75 < gertrude['q50']) and (gertrude['q50'] < 85)), \
      "The estimated median age for the name Gertrude should be between 75 and 85."
```






    2/2 tests passed
    



## 10. Median Age of Top 10 Female Names
<p>In the previous section, we estimated the age of a female named Gertrude. Let's go one step further this time, and compute the 25th, 50th and 75th percentiles of age, and the probability of being alive for the top 10 most common female names of all time. This should give us some interesting insights on how these names stack up in terms of median ages!</p>


```python
# Create median_ages: DataFrame with Top 10 Female names, 
#    age percentiles and probability of being alive
# -- YOUR CODE HERE --

#sex='F'
#bnames_agg = bnames.groupby(['sex', 'name'], as_index=False)['births'].sum()
#top_ten_female = bnames_agg.sort_values(['sex','births'], ascending=[True, False]).head(10).name
#top_ten_female

#for name in top_ten_female:
    #estimate_age(name, sex)
#    print(name, sex)
    
    
top_10_female_names = bnames.\
    groupby(['sex', 'name'], as_index = False).\
    agg({'births': np.sum}).\
    sort_values('births', ascending = False).\
    query('sex == "F"').\
    head(10).\
    reset_index(drop = True)
estimates = pd.concat([estimate_age(name, 'F') for name in top_10_female_names.name], axis = 1)
median_ages = estimates.T.sort_values('q50').reset_index(drop = True)
median_ages
```


```python
#estimate_age('Jennifer','F')
```


```python
%%nose
def test_median_ages_exists():
    """median_ages is defined"""
    assert 'median_ages' in globals(), \
      "You should have a variable named median_ages defined."
def test_median_ages_df():
    """median_ages is a dataframe with 10 rows and 6 columns."""
    assert median_ages.shape == (10, 6), \
      "Your DataFrame, median_ages, should have 10 rows and 6 columns"

def test_median_ages_df_colnames():
    """median_ages has column names: name, p_alive, q25, q50, q75 and sex"""
    assert all(name in median_ages for name in ['name', 'p_alive', 'q25', 'q50', 'q75', 'sex']), \
      "Your DataFrame, median_ages, should have columns named: name, p_alive, q25, q50, q75 and sex"
```
