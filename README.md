
# Creating Sankey diagram with 3 different data


```python
import json, urllib
import chart_studio.plotly as py
import pandas as pd
import numpy as np
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
```

## List of cities I visited.


```python
import plotly.graph_objects as go

fig = go.Figure(data=[go.Sankey(
    node = dict(
      pad = 15,
      thickness = 20,
      line = dict(color = "black", width = 0.5),
      label = ["City1", "City2", "City3", "City4", "City6","City7","City8","City9"],
      color = "blue"
    ),
    link = dict(
      source = [0,1,2,3,2,4,2,5,2,2], # indices correspond to labels, eg A1, A2, A1, B1, ...
      target = [1,2,3,2,4,2,5,2,6,7],
      value =  [1,1,1,1,1,1,1,1,1,1]
  ))])

fig.update_layout(title_text="List of cities I visited.", font_size=10)
plot(fig,
     image_filename='sankey_plot_1', 
     image='png', 
     image_width=1000, 
     image_height=600
)
fig.show()
```

![1](1.png)

##  Sankey from csv


```python
df = pd.read_csv ('ulkes.csv')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Source</th>
      <th>Target</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>Portugal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Brazil</td>
      <td>France</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brazil</td>
      <td>Spain</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Brazil</td>
      <td>England</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Canada</td>
      <td>Portugal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Canada</td>
      <td>France</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Canada</td>
      <td>England</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Mexico</td>
      <td>Portugal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Mexico</td>
      <td>France</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mexico</td>
      <td>Spain</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Mexico</td>
      <td>England</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>USA</td>
      <td>Portugal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>USA</td>
      <td>France</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>USA</td>
      <td>Spain</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>USA</td>
      <td>England</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Portugal</td>
      <td>Angola</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Portugal</td>
      <td>Senegal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Portugal</td>
      <td>Morocco</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Portugal</td>
      <td>SouthAfrica</td>
      <td>1</td>
    </tr>
    <tr>
      <th>19</th>
      <td>France</td>
      <td>Angola</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>France</td>
      <td>Senegal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>France</td>
      <td>Mali</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>France</td>
      <td>Morocco</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>France</td>
      <td>SouthAfrica</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Spain</td>
      <td>Senegal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Spain</td>
      <td>Morocco</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Spain</td>
      <td>SouthAfrica</td>
      <td>1</td>
    </tr>
    <tr>
      <th>27</th>
      <td>England</td>
      <td>Angola</td>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>England</td>
      <td>Senegal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>England</td>
      <td>Morocco</td>
      <td>1</td>
    </tr>
    <tr>
      <th>30</th>
      <td>England</td>
      <td>SouthAfrica</td>
      <td>1</td>
    </tr>
    <tr>
      <th>31</th>
      <td>SouthAfrica</td>
      <td>China</td>
      <td>1</td>
    </tr>
    <tr>
      <th>32</th>
      <td>SouthAfrica</td>
      <td>India</td>
      <td>1</td>
    </tr>
    <tr>
      <th>33</th>
      <td>SouthAfrica</td>
      <td>Japan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Angola</td>
      <td>China</td>
      <td>1</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Angola</td>
      <td>India</td>
      <td>1</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Angola</td>
      <td>Japan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Senegal</td>
      <td>China</td>
      <td>1</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Senegal</td>
      <td>India</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Senegal</td>
      <td>Japan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Mali</td>
      <td>China</td>
      <td>1</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Mali</td>
      <td>India</td>
      <td>1</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Mali</td>
      <td>Japan</td>
      <td>1</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Morocco</td>
      <td>China</td>
      <td>1</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Morocco</td>
      <td>India</td>
      <td>1</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Morocco</td>
      <td>Japan</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
c=df
del c["Value"]
```


```python
c=c.values

```


```python
node_label=[]
for i in c:
    for ii in i:
        if ii not in node_label:
            node_label.append(ii)
        
```


```python
node_label
```




    ['Brazil',
     'Portugal',
     'France',
     'Spain',
     'England',
     'Canada',
     'Mexico',
     'USA',
     'Angola',
     'Senegal',
     'Morocco',
     'SouthAfrica',
     'Mali',
     'China',
     'India',
     'Japan']




```python
#node_label = ["A1", "A2", "B1", "B2","B3", "C1", "C2"]
node_dict = {y:x for x, y in enumerate(node_label)}
node_dict
# {'A1': 0, 'A2': 1, 'B1': 2, 'B2': 3, 'B3': 4, 'C1': 5, 'C2': 6}
```




    {'Angola': 8,
     'Brazil': 0,
     'Canada': 5,
     'China': 13,
     'England': 4,
     'France': 2,
     'India': 14,
     'Japan': 15,
     'Mali': 12,
     'Mexico': 6,
     'Morocco': 10,
     'Portugal': 1,
     'Senegal': 9,
     'SouthAfrica': 11,
     'Spain': 3,
     'USA': 7}




```python

df = pd.read_csv ('ulkes.csv')

source = df["Source"]
target = df["Target"]
values = df["Value"]
source_node = [node_dict[x] for x in source]
target_node = [node_dict[x] for x in target]

```


```python
import plotly.graph_objects as go # Import the graphical object

fig = go.Figure( 
    data=[go.Sankey( # The plot we are interest
        # This part is for the node information
        node = dict( 
            label = node_label
        ),
        # This part is for the link information
        link = dict(
            source = source_node,
            target = target_node,
            value = values
        ))])

# With this save the plots 
plot(fig,
     image_filename='sankey_plot_1', 
     image='png', 
     image_width=1000, 
     image_height=600
)
# And shows the plot
fig.show()
```

![2](2.png)

## Display of Syrian refugee numbers with Sankey diagram


```python
df = pd.read_csv ('suria.csv')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Source</th>
      <th>Target</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Syria</td>
      <td>Turkey</td>
      <td>3643700</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Syria</td>
      <td>Switzerland</td>
      <td>12931</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Syria</td>
      <td>Algeria</td>
      <td>43000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Syria</td>
      <td>Argentina</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Syria</td>
      <td>Armenia</td>
      <td>22000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Syria</td>
      <td>Australia</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Syria</td>
      <td>Austria</td>
      <td>45827</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Syria</td>
      <td>Bahrain</td>
      <td>3500</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Syria</td>
      <td>Belgium</td>
      <td>16986</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Syria</td>
      <td>Brazil</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Syria</td>
      <td>Bulgaria</td>
      <td>17527</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Syria</td>
      <td>Canada</td>
      <td>62000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Syria</td>
      <td>Croatia</td>
      <td>55000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Syria</td>
      <td>Cyprus</td>
      <td>3527</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Syria</td>
      <td>Denmark</td>
      <td>19433</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Syria</td>
      <td>Egypt</td>
      <td>130074</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Syria</td>
      <td>Finland</td>
      <td>6232</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Syria</td>
      <td>France</td>
      <td>11694</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Syria</td>
      <td>Germany</td>
      <td>770000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Syria</td>
      <td>Greece</td>
      <td>54574</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Syria</td>
      <td>Hungary</td>
      <td>72505</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Syria</td>
      <td>Iraq</td>
      <td>247440</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Syria</td>
      <td>Italy</td>
      <td>2538</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Syria</td>
      <td>Jordan</td>
      <td>1265000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Syria</td>
      <td>Lebanon</td>
      <td>2200000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Syria</td>
      <td>Libya</td>
      <td>26672</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Syria</td>
      <td>Malaysia</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Syria</td>
      <td>Malta</td>
      <td>1222</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Syria</td>
      <td>Montenegro</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Syria</td>
      <td>Netherlands</td>
      <td>31963</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Syria</td>
      <td>NorthMacedonia</td>
      <td>2150</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Syria</td>
      <td>Norway</td>
      <td>13993</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Syria</td>
      <td>Qatar</td>
      <td>54000</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Syria</td>
      <td>Romania</td>
      <td>2525</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Syria</td>
      <td>Russia</td>
      <td>7096</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Syria</td>
      <td>Serbia</td>
      <td>11831</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Syria</td>
      <td>Singapore</td>
      <td>13856</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Syria</td>
      <td>Somalia</td>
      <td>1312</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Syria</td>
      <td>Spain</td>
      <td>8365</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Syria</td>
      <td>Sudan</td>
      <td>250,000</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Syria</td>
      <td>Sweden</td>
      <td>122087</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Syria</td>
      <td>Tunisia</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Syria</td>
      <td>UAE</td>
      <td>100000</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Syria</td>
      <td>UnitedKingdom</td>
      <td>10,583</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Syria</td>
      <td>UnitedStates</td>
      <td>16218</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Syria</td>
      <td>Yemen</td>
      <td>100,000</td>
    </tr>
  </tbody>
</table>
</div>




```python
c=df
del c["Value"]
c=c.values
node_label=[]
for i in c:
    for ii in i:
        if ii not in node_label:
            node_label.append(ii)
node_label
```




    ['Syria',
     'Turkey',
     'Switzerland',
     'Algeria',
     'Argentina',
     'Armenia',
     'Australia',
     'Austria',
     'Bahrain',
     'Belgium',
     'Brazil',
     'Bulgaria',
     'Canada',
     'Croatia',
     'Cyprus',
     'Denmark',
     'Egypt',
     'Finland',
     'France',
     'Germany',
     'Greece',
     'Hungary',
     'Iraq',
     'Italy',
     'Jordan',
     'Lebanon',
     'Libya',
     'Malaysia',
     'Malta',
     'Montenegro',
     'Netherlands',
     'NorthMacedonia',
     'Norway',
     'Qatar',
     'Romania',
     'Russia',
     'Serbia',
     'Singapore',
     'Somalia',
     'Spain',
     'Sudan',
     'Sweden',
     'Tunisia',
     'UAE',
     'UnitedKingdom',
     'UnitedStates',
     'Yemen']




```python
node_dict = {y:x for x, y in enumerate(node_label)}
node_dict
```




    {'Algeria': 3,
     'Argentina': 4,
     'Armenia': 5,
     'Australia': 6,
     'Austria': 7,
     'Bahrain': 8,
     'Belgium': 9,
     'Brazil': 10,
     'Bulgaria': 11,
     'Canada': 12,
     'Croatia': 13,
     'Cyprus': 14,
     'Denmark': 15,
     'Egypt': 16,
     'Finland': 17,
     'France': 18,
     'Germany': 19,
     'Greece': 20,
     'Hungary': 21,
     'Iraq': 22,
     'Italy': 23,
     'Jordan': 24,
     'Lebanon': 25,
     'Libya': 26,
     'Malaysia': 27,
     'Malta': 28,
     'Montenegro': 29,
     'Netherlands': 30,
     'NorthMacedonia': 31,
     'Norway': 32,
     'Qatar': 33,
     'Romania': 34,
     'Russia': 35,
     'Serbia': 36,
     'Singapore': 37,
     'Somalia': 38,
     'Spain': 39,
     'Sudan': 40,
     'Sweden': 41,
     'Switzerland': 2,
     'Syria': 0,
     'Tunisia': 42,
     'Turkey': 1,
     'UAE': 43,
     'UnitedKingdom': 44,
     'UnitedStates': 45,
     'Yemen': 46}




```python
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
df = pd.read_csv ('suria.csv')

source = df["Source"]
target = df["Target"]
values = df["Value"]
source_node = [node_dict[x] for x in source]
target_node = [node_dict[x] for x in target]

```


```python
import plotly.graph_objects as go 

fig = go.Figure( 
    data=[go.Sankey(
        node = dict( 
            label = node_label
        ),
     
        link = dict(
            source = source_node,
            target = target_node,
            value = values
        ))])


plot(fig,
     image_filename='sankey_plot_1', 
     image='png', 
     image_width=1000, 
     image_height=600
)
# And shows the plot
fig.show()
```

![3](3.png)
