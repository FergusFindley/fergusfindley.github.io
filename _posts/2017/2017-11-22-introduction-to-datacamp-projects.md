---
layout: post
title: "Introduction to DataCamp projects"
date: '2017-11-22 19:26 +0100'
author: Fergus Findley
tags:
  - learning
  - DataCamp
description: >-
  DataCamp project.``
image: 
---

## 1. This is a Jupyter notebook!
<p>A <em>Jupyter notebook</em> is a document that contains text cells (what you're reading right now) and code cells. What is special with a notebook is that it's <em>interactive</em>: You can change or add code cells, and then <em>run</em> a cell by first selecting it and then clicking the <em>run cell</em> button above ( <strong>▶|</strong> Run ) or hitting <code>ctrl + enter</code>. </p>
<p><img src="https://s3.amazonaws.com/assets.datacamp.com/production/project_33/datasets/run_code_cell_image.png" alt=""></p>
<p>The result will be displayed directly in the notebook. You <em>could</em> use a notebook as a simple calculator. For example, it's estimated that on average 256 children were born every minute in 2016. The code cell below calculates how many children were born on average on a day. </p>


```python
# I'm a code cell, click me, then run me!
256 * 60 * 24 # Children × minutes × hours
```


```python
%%nose
# No tests
```

## 2. Put _any_ code in code cells
<p>But a code cell can contain much more than a simple one-liner! This is a notebook running python and you can put <em>any</em> python code in a code cell (but notebooks can run other languages too, like R). Below is a code cell where we define a whole new function (<code>greet</code>). To show the output of <code>greet</code> we run it last in the code cell as the last value is always printed out. </p>


```python
def greet(first_name, last_name):
    greeting = 'My name is ' + last_name + ', ' + first_name + ' ' + last_name + '!'
    return greeting

# Replace with your first and last name.
# That is, unless your name is already James Bond.
greet('James', 'Bond')
```




    'My name is Bond, James Bond!'




```python
%%nose
# No tests
```

## 3. Jupyter notebooks ♡ data
<p>We've seen that notebooks can display basic objects such as numbers and strings. But notebooks also support the objects used in data science, which makes them great for interactive data analysis!</p>
<p>For example, below we create a <code>pandas</code> DataFrame by reading in a <code>csv</code>-file with the average global temperature for the years 1850 to 2016. If we look at the <code>head</code> of this DataFrame the notebook will render it as a nice-looking table.</p>


```python
# Importing the pandas module
import pandas as pd

# Reading in the global temperature data,data
global_temp = pd.read_csv('datasets/global_temperature.csv')

# Take a look at the first datapoints
# ... YOUR CODE FOR TASK 3 ...
global_temp.head()
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
      <th>degrees_celsius</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1850</td>
      <td>7.74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1851</td>
      <td>8.09</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1852</td>
      <td>7.97</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1853</td>
      <td>7.93</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1854</td>
      <td>8.19</td>
    </tr>
  </tbody>
</table>
</div>




```python
%%nose
# No tests
```

## 4. Jupyter notebooks ♡ plots
<p>Tables are nice but — as the saying goes — <em>"a plot can show a thousand data points"</em>. Notebooks handle plots as well, but it requires a bit of magic. Here <em>magic</em> does not refer to any arcane rituals but to so-called "magic commands" that affect how the Jupyter notebook works. Magic commands start with either <code>%</code> or <code>%%</code> and the command we need to nicely display plots inline is <code>%matplotlib inline</code>. With this <em>magic</em> in place, all plots created in code cells will automatically be displayed inline. </p>
<p>Let's take a look at the global temperature for the last 150 years.</p>


```python
# Setting up inline plotting using jupyter notebook "magic"
%matplotlib inline

import matplotlib.pyplot as plt

# Plotting global temperature in degrees celsius by year.
plt.plot(global_temp['year'], global_temp['degrees_celsius'])

# Adding some nice labels 
plt.xlabel('...') 
plt.ylabel('...') 
```




    <matplotlib.text.Text at 0x7f7276e52438>




![png](2017-11-22-introduction-to-data-camp-projects_files/2017-11-22-introduction-to-data-camp-projects_10_1.png)



```python
%%nose
# No tests
```

## 5. Jupyter notebooks ♡ a lot more
<p>Tables and plots are the most common outputs when doing data analysis, but Jupyter notebooks can render many more types of outputs such as sound, animation, video, etc. Yes, almost anything that can be shown in a modern web browser. This also makes it possible to include <em>interactive widgets</em> directly in the notebook!</p>
<p>For example, this (slightly complicated) code will create an interactive map showing the locations of the three largest smartphone companies in 2016. You can move and zoom the map, and you can click the markers for more info! </p>


```python
# Making a map using the folium module
import folium
phone_map = folium.Map()

# Top three smart phone companies by market share in 2016.
companies = [
    {'loc': [37.4970,  127.0266], 'label': 'Samsung: ...%'},
    {'loc': [37.3318, -122.0311], 'label': 'Apple: ...%'},
    {'loc': [22.5431,  114.0579], 'label': 'Huawei: ...%'}] 

# Adding markers to the map.
for company in companies:
    marker = folium.Marker(location=company['loc'], popup=company['label'])
    marker.add_to(phone_map)

# The last object in the cell always gets shown in the notebook
phone_map
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIgLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC5taW4uY3NzIiAvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiIC8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIgLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuY3NzIiAvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhd2dpdC5jb20vcHl0aG9uLXZpc3VhbGl6YXRpb24vZm9saXVtL21hc3Rlci9mb2xpdW0vdGVtcGxhdGVzL2xlYWZsZXQuYXdlc29tZS5yb3RhdGUuY3NzIiAvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfNzNjNzQ0YTE4ZWIzNDcxMGE4MGQ0NGQzYjJlZGIyYTQgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzczYzc0NGExOGViMzQ3MTBhODBkNDRkM2IyZWRiMmE0IiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF83M2M3NDRhMThlYjM0NzEwYTgwZDQ0ZDNiMmVkYjJhNCA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF83M2M3NDRhMThlYjM0NzEwYTgwZDQ0ZDNiMmVkYjJhNCcsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbMCwwXSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHpvb206IDEsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBtYXhCb3VuZHM6IGJvdW5kcywKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGxheWVyczogW10sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB3b3JsZENvcHlKdW1wOiBmYWxzZSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgfSk7CiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyX2U1ODFkM2Y3OGViNjQ2NzE4MjdhODdmNjA1NmZiYWUzID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAnaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmcnLAogICAgICAgICAgICAgICAgewogICJhdHRyaWJ1dGlvbiI6IG51bGwsCiAgImRldGVjdFJldGluYSI6IGZhbHNlLAogICJtYXhab29tIjogMTgsCiAgIm1pblpvb20iOiAxLAogICJub1dyYXAiOiBmYWxzZSwKICAic3ViZG9tYWlucyI6ICJhYmMiCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzczYzc0NGExOGViMzQ3MTBhODBkNDRkM2IyZWRiMmE0KTsKICAgICAgICAKICAgIAoKICAgICAgICAgICAgdmFyIG1hcmtlcl9kNDAyYWNkNWQzNGE0OWY5YjkzYzUyZjBiMWZkYWFjMiA9IEwubWFya2VyKAogICAgICAgICAgICAgICAgWzM3LjQ5NywxMjcuMDI2Nl0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgaWNvbjogbmV3IEwuSWNvbi5EZWZhdWx0KCkKICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICApCiAgICAgICAgICAgICAgICAuYWRkVG8obWFwXzczYzc0NGExOGViMzQ3MTBhODBkNDRkM2IyZWRiMmE0KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzJhZDMxYTE4MTI0NDQ5MmU4ZjQ1YjdkYjQ5YWRlZDZiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2U5MjhlMTVmYzVhZjRmNGU4MTA0NzQzYmZlNWZjYjM0ID0gJCgnPGRpdiBpZD0iaHRtbF9lOTI4ZTE1ZmM1YWY0ZjRlODEwNDc0M2JmZTVmY2IzNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U2Ftc3VuZzogLi4uJTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMmFkMzFhMTgxMjQ0NDkyZThmNDViN2RiNDlhZGVkNmIuc2V0Q29udGVudChodG1sX2U5MjhlMTVmYzVhZjRmNGU4MTA0NzQzYmZlNWZjYjM0KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBtYXJrZXJfZDQwMmFjZDVkMzRhNDlmOWI5M2M1MmYwYjFmZGFhYzIuYmluZFBvcHVwKHBvcHVwXzJhZDMxYTE4MTI0NDQ5MmU4ZjQ1YjdkYjQ5YWRlZDZiKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCgogICAgICAgICAgICB2YXIgbWFya2VyXzcwY2ZlMTg0M2VhNzQzMzE5ZGU1NGFmMmIxZjNmOWI1ID0gTC5tYXJrZXIoCiAgICAgICAgICAgICAgICBbMzcuMzMxOCwtMTIyLjAzMTFdLAogICAgICAgICAgICAgICAgewogICAgICAgICAgICAgICAgICAgIGljb246IG5ldyBMLkljb24uRGVmYXVsdCgpCiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgKQogICAgICAgICAgICAgICAgLmFkZFRvKG1hcF83M2M3NDRhMThlYjM0NzEwYTgwZDQ0ZDNiMmVkYjJhNCk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9hNDY3MTIzZjFiZmU0MGYzOWY2MjRjOGFlMmFhYWU0OCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9mMzQ4Yjc4NDhlMjg0ZjQ0OWYwM2VjMGMyYTczMjAxMyA9ICQoJzxkaXYgaWQ9Imh0bWxfZjM0OGI3ODQ4ZTI4NGY0NDlmMDNlYzBjMmE3MzIwMTMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkFwcGxlOiAuLi4lPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9hNDY3MTIzZjFiZmU0MGYzOWY2MjRjOGFlMmFhYWU0OC5zZXRDb250ZW50KGh0bWxfZjM0OGI3ODQ4ZTI4NGY0NDlmMDNlYzBjMmE3MzIwMTMpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIG1hcmtlcl83MGNmZTE4NDNlYTc0MzMxOWRlNTRhZjJiMWYzZjliNS5iaW5kUG9wdXAocG9wdXBfYTQ2NzEyM2YxYmZlNDBmMzlmNjI0YzhhZTJhYWFlNDgpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKCiAgICAgICAgICAgIHZhciBtYXJrZXJfYTlkNjdmMGUzMGI4NDk4ZDliZTA1ZjgxZjFjZmE3MmQgPSBMLm1hcmtlcigKICAgICAgICAgICAgICAgIFsyMi41NDMxLDExNC4wNTc5XSwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBpY29uOiBuZXcgTC5JY29uLkRlZmF1bHQoKQogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgICkKICAgICAgICAgICAgICAgIC5hZGRUbyhtYXBfNzNjNzQ0YTE4ZWIzNDcxMGE4MGQ0NGQzYjJlZGIyYTQpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNmMzMjM5ZjczZjFiNGM3NmFmYWM2ZjEzMWU0Njc4YjQgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfYTI5ZWFhOWVlNWVmNGIyMmJmZWJjZDIwYWU4NDVmYjAgPSAkKCc8ZGl2IGlkPSJodG1sX2EyOWVhYTllZTVlZjRiMjJiZmViY2QyMGFlODQ1ZmIwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IdWF3ZWk6IC4uLiU8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzZjMzIzOWY3M2YxYjRjNzZhZmFjNmYxMzFlNDY3OGI0LnNldENvbnRlbnQoaHRtbF9hMjllYWE5ZWU1ZWY0YjIyYmZlYmNkMjBhZTg0NWZiMCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgbWFya2VyX2E5ZDY3ZjBlMzBiODQ5OGQ5YmUwNWY4MWYxY2ZhNzJkLmJpbmRQb3B1cChwb3B1cF82YzMyMzlmNzNmMWI0Yzc2YWZhYzZmMTMxZTQ2NzhiNCk7CgogICAgICAgICAgICAKICAgICAgICAKPC9zY3JpcHQ+" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python
%%nose

def test_market_share_of_samsung():
    assert '20.5' in companies[0]['label'], \
        "The market share of Samsung should be 20.5%"
        
def test_market_share_of_apple():
    assert '14.4' in companies[1]['label'], \
        "The market share of Apple should be 14.4%"

def test_market_share_of_huawei():
    assert '8.9' in companies[2]['label'], \
        "The market share of Huawei should be 8.9%"
```

## 6. Goodbye for now!
<p>This was just a short introduction to Jupyter notebooks, an open source technology that is increasingly used for data science and analysis. I hope you enjoyed it! :)</p>


```python
# Are you ready to get started with  DataCamp projects?
I_am_ready = False

# Ps. 
# Feel free to try out any other stuff in this notebook. 
# It's all yours!
```


```python
%%nose

def test_if_ready():
    assert I_am_ready, \
        "I_am_ready should be set to True, if you are ready to get started with DataCamp projects, that is."
```
