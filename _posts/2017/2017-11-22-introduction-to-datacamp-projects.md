---
layout: post
title: "Introduction to DataCamp projects"
date: '2017-11-22 18:26 +0100'
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




    368640



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




    Text(0,0.5,'...')




![png]({{ site.url }}/imgs/2017-11-22-introduction-to-datacamp-projects_files/2017-11-22-introduction-to-datacamp-projects_7_1.png)


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




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;base64,CiAgICAgICAgPCFET0NUWVBFIGh0bWw+CiAgICAgICAgPGhlYWQ+CiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgICAgICA8bWV0YSBodHRwLWVxdWl2PSJjb250ZW50LXR5cGUiIGNvbnRlbnQ9InRleHQvaHRtbDsgY2hhcnNldD1VVEYtOCIgLz4KICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9sZWFmbGV0LzAuNy4zL2xlYWZsZXQuanMiPjwvc2NyaXB0PgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vYWpheC5nb29nbGVhcGlzLmNvbS9hamF4L2xpYnMvanF1ZXJ5LzEuMTEuMS9qcXVlcnkubWluLmpzIj48L3NjcmlwdD4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxzY3JpcHQgc3JjPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9qcy9ib290c3RyYXAubWluLmpzIj48L3NjcmlwdD4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5taW4uanMiPjwvc2NyaXB0PgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY2RuanMuY2xvdWRmbGFyZS5jb20vYWpheC9saWJzL2xlYWZsZXQubWFya2VyY2x1c3Rlci8wLjQuMC9sZWFmbGV0Lm1hcmtlcmNsdXN0ZXItc3JjLmpzIj48L3NjcmlwdD4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9sZWFmbGV0Lm1hcmtlcmNsdXN0ZXIvMC40LjAvbGVhZmxldC5tYXJrZXJjbHVzdGVyLmpzIj48L3NjcmlwdD4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvbGVhZmxldC8wLjcuMy9sZWFmbGV0LmNzcyIgLz4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC5taW4uY3NzIiAvPgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiIC8+CiAgICAgICAgCiAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgICAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuMS4wL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIgLz4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuY3NzIiAvPgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9sZWFmbGV0Lm1hcmtlcmNsdXN0ZXIvMC40LjAvTWFya2VyQ2x1c3Rlci5EZWZhdWx0LmNzcyIgLz4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvbGVhZmxldC5tYXJrZXJjbHVzdGVyLzAuNC4wL01hcmtlckNsdXN0ZXIuY3NzIiAvPgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhdy5naXRodWJ1c2VyY29udGVudC5jb20vcHl0aG9uLXZpc3VhbGl6YXRpb24vZm9saXVtL21hc3Rlci9mb2xpdW0vdGVtcGxhdGVzL2xlYWZsZXQuYXdlc29tZS5yb3RhdGUuY3NzIiAvPgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAgICAgPHN0eWxlPgoKICAgICAgICAgICAgaHRtbCwgYm9keSB7CiAgICAgICAgICAgICAgICB3aWR0aDogMTAwJTsKICAgICAgICAgICAgICAgIGhlaWdodDogMTAwJTsKICAgICAgICAgICAgICAgIG1hcmdpbjogMDsKICAgICAgICAgICAgICAgIHBhZGRpbmc6IDA7CiAgICAgICAgICAgICAgICB9CgogICAgICAgICAgICAjbWFwIHsKICAgICAgICAgICAgICAgIHBvc2l0aW9uOmFic29sdXRlOwogICAgICAgICAgICAgICAgdG9wOjA7CiAgICAgICAgICAgICAgICBib3R0b206MDsKICAgICAgICAgICAgICAgIHJpZ2h0OjA7CiAgICAgICAgICAgICAgICBsZWZ0OjA7CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIDwvc3R5bGU+CiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAgICAgPHN0eWxlPiAjbWFwX2NmNDc0OTllZWU4YTQ3NGRiMmIwYjgzMzhiMjc1YmVjIHsKICAgICAgICAgICAgICAgIHBvc2l0aW9uIDogcmVsYXRpdmU7CiAgICAgICAgICAgICAgICB3aWR0aCA6IDEwMC4wJTsKICAgICAgICAgICAgICAgIGhlaWdodDogMTAwLjAlOwogICAgICAgICAgICAgICAgbGVmdDogMC4wJTsKICAgICAgICAgICAgICAgIHRvcDogMC4wJTsKICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgPC9zdHlsZT4KICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICA8L2hlYWQ+CiAgICAgICAgPGJvZHk+CiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAgICAgPGRpdiBjbGFzcz0iZm9saXVtLW1hcCIgaWQ9Im1hcF9jZjQ3NDk5ZWVlOGE0NzRkYjJiMGI4MzM4YjI3NWJlYyIgPjwvZGl2PgogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgIDwvYm9keT4KICAgICAgICA8c2NyaXB0PgogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCgogICAgICAgICAgICB2YXIgc291dGhXZXN0ID0gTC5sYXRMbmcoLTkwLCAtMTgwKTsKICAgICAgICAgICAgdmFyIG5vcnRoRWFzdCA9IEwubGF0TG5nKDkwLCAxODApOwogICAgICAgICAgICB2YXIgYm91bmRzID0gTC5sYXRMbmdCb3VuZHMoc291dGhXZXN0LCBub3J0aEVhc3QpOwoKICAgICAgICAgICAgdmFyIG1hcF9jZjQ3NDk5ZWVlOGE0NzRkYjJiMGI4MzM4YjI3NWJlYyA9IEwubWFwKCdtYXBfY2Y0NzQ5OWVlZThhNDc0ZGIyYjBiODMzOGIyNzViZWMnLCB7CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBjZW50ZXI6WzAsMF0sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB6b29tOiAxLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbWF4Qm91bmRzOiBib3VuZHMsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBsYXllcnM6IFtdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgY3JzOiBMLkNSUy5FUFNHMzg1NwogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIH0pOwogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzM5YjU0YjJmYTcxNTRhMzNhMjYyNmRmODI2MmM4MGIxID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAnaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmcnLAogICAgICAgICAgICAgICAgewogICAgICAgICAgICAgICAgICAgIG1heFpvb206IDE4LAogICAgICAgICAgICAgICAgICAgIG1pblpvb206IDEsCiAgICAgICAgICAgICAgICAgICAgYXR0cmlidXRpb246ICdEYXRhIGJ5IDxhIGhyZWY9Imh0dHA6Ly9vcGVuc3RyZWV0bWFwLm9yZyI+T3BlblN0cmVldE1hcDwvYT4sIHVuZGVyIDxhIGhyZWY9Imh0dHA6Ly93d3cub3BlbnN0cmVldG1hcC5vcmcvY29weXJpZ2h0Ij5PRGJMPC9hPi4nLAogICAgICAgICAgICAgICAgICAgIGRldGVjdFJldGluYTogZmFsc2UKICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF9jZjQ3NDk5ZWVlOGE0NzRkYjJiMGI4MzM4YjI3NWJlYyk7CgogICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKCiAgICAgICAgICAgIHZhciBtYXJrZXJfZDVkMjJkZjQzYjdjNDllNjlkZmQxOWY4MDc3MTRjMTcgPSBMLm1hcmtlcigKICAgICAgICAgICAgICAgIFszNy40OTcsMTI3LjAyNjZdLAogICAgICAgICAgICAgICAgewogICAgICAgICAgICAgICAgICAgIGljb246IG5ldyBMLkljb24uRGVmYXVsdCgpCiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgKQogICAgICAgICAgICAgICAgLmFkZFRvKG1hcF9jZjQ3NDk5ZWVlOGE0NzRkYjJiMGI4MzM4YjI3NWJlYyk7CiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgICAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzFhNmRmNjYwYzAxYjQwODNhOTBjZTMwY2FlYzI3NDhkID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzQ1NmViM2NkNTE4MDQwNWE5MDc5YWQzYTc2NmUzZTEzID0gJCgnICAgICAgICAgPGRpdiBpZD0iaHRtbF80NTZlYjNjZDUxODA0MDVhOTA3OWFkM2E3NjZlM2UxMyIgICAgICAgICAgICAgICAgIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPiAgICAgICAgICAgICAgICAgU2Ftc3VuZzogLi4uJTwvZGl2PiAgICAgICAgICAgICAgICAgJylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8xYTZkZjY2MGMwMWI0MDgzYTkwY2UzMGNhZWMyNzQ4ZC5zZXRDb250ZW50KGh0bWxfNDU2ZWIzY2Q1MTgwNDA1YTkwNzlhZDNhNzY2ZTNlMTMpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIG1hcmtlcl9kNWQyMmRmNDNiN2M0OWU2OWRmZDE5ZjgwNzcxNGMxNy5iaW5kUG9wdXAocG9wdXBfMWE2ZGY2NjBjMDFiNDA4M2E5MGNlMzBjYWVjMjc0OGQpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcmtlcl82OGFlZWQyOTg2OTU0NWI3YjhlZGZhYjJiODQ3MWQ2ZSA9IEwubWFya2VyKAogICAgICAgICAgICAgICAgWzM3LjMzMTgsLTEyMi4wMzExXSwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBpY29uOiBuZXcgTC5JY29uLkRlZmF1bHQoKQogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgICkKICAgICAgICAgICAgICAgIC5hZGRUbyhtYXBfY2Y0NzQ5OWVlZThhNDc0ZGIyYjBiODMzOGIyNzViZWMpOwogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kNzM1MzA5MDc4Nzk0ZDQwOWYwM2VhYmYzNzA5NTM0NSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8yY2I0YjdkMmRlNDg0MDk3OGRlYzIzNDIzMGJhOWQ2OSA9ICQoJyAgICAgICAgIDxkaXYgaWQ9Imh0bWxfMmNiNGI3ZDJkZTQ4NDA5NzhkZWMyMzQyMzBiYTlkNjkiICAgICAgICAgICAgICAgICBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij4gICAgICAgICAgICAgICAgIEFwcGxlOiAuLi4lPC9kaXY+ICAgICAgICAgICAgICAgICAnKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2Q3MzUzMDkwNzg3OTRkNDA5ZjAzZWFiZjM3MDk1MzQ1LnNldENvbnRlbnQoaHRtbF8yY2I0YjdkMmRlNDg0MDk3OGRlYzIzNDIzMGJhOWQ2OSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgbWFya2VyXzY4YWVlZDI5ODY5NTQ1YjdiOGVkZmFiMmI4NDcxZDZlLmJpbmRQb3B1cChwb3B1cF9kNzM1MzA5MDc4Nzk0ZDQwOWYwM2VhYmYzNzA5NTM0NSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgICAgICAKICAgICAgICAgICAgCgogICAgICAgICAgICB2YXIgbWFya2VyXzQ1ZWQ3YzYyZTE1MDRlNTI4Zjc3Y2EwNjU0YjVkZDNjID0gTC5tYXJrZXIoCiAgICAgICAgICAgICAgICBbMjIuNTQzMSwxMTQuMDU3OV0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgaWNvbjogbmV3IEwuSWNvbi5EZWZhdWx0KCkKICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICApCiAgICAgICAgICAgICAgICAuYWRkVG8obWFwX2NmNDc0OTllZWU4YTQ3NGRiMmIwYjgzMzhiMjc1YmVjKTsKICAgICAgICAgICAgCiAgICAgICAgCiAgICAgICAgICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNjYxNzQ1ODQ0MTg4NGYyZWI0Yjk3MjdmNTE5NDIxNGUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfM2E0YjgyNjdjNjA0NDdmNTlkMWY1OTI2OGQ5ZGNmZjAgPSAkKCcgICAgICAgICA8ZGl2IGlkPSJodG1sXzNhNGI4MjY3YzYwNDQ3ZjU5ZDFmNTkyNjhkOWRjZmYwIiAgICAgICAgICAgICAgICAgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+ICAgICAgICAgICAgICAgICBIdWF3ZWk6IC4uLiU8L2Rpdj4gICAgICAgICAgICAgICAgICcpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNjYxNzQ1ODQ0MTg4NGYyZWI0Yjk3MjdmNTE5NDIxNGUuc2V0Q29udGVudChodG1sXzNhNGI4MjY3YzYwNDQ3ZjU5ZDFmNTkyNjhkOWRjZmYwKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBtYXJrZXJfNDVlZDdjNjJlMTUwNGU1MjhmNzdjYTA2NTRiNWRkM2MuYmluZFBvcHVwKHBvcHVwXzY2MTc0NTg0NDE4ODRmMmViNGI5NzI3ZjUxOTQyMTRlKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgIAogICAgICAgIDwvc2NyaXB0PgogICAgICAgIA==" style="position:absolute;width:100%;height:100%;left:0;top:0;"></iframe></div></div>



## 6. Goodbye for now!
<p>This was just a short introduction to Jupyter notebooks, an open source technology that is increasingly used for data science and analysis. I hope you enjoyed it! :)</p>


```python
# Are you ready to get started with  DataCamp projects?
I_am_ready = False

# Ps. 
# Feel free to try out any other stuff in this notebook. 
# It's all yours!
```
