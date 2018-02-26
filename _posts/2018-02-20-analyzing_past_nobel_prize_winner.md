---
title: "Noble Prize Winners"
layout: post
date: 2018-02-20 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- prize
- noble
star: true
category: blog
author: Mustapha
description: Content Analysis of Past Nobel prize winners
---


![png]({{site.baseurl}}/assets/images/noble/blog1_1_0.jpeg)





```python
import pandas as pd
```


```python
HTML("<h4>we import the dataset which is in csv format</h4>")
```




<h4>we import the dataset which is in csv format</h4>




```python
data_set = pd.read_csv('archive.csv')
```


```python
HTML("<h4>lets check the length of the dataset</h4>")
```




<h4>lets check the length of the dataset</h4>




```python
len(data_set)
```




    969




```python
HTML("<h4>display the first five rows</h4>")
```




<h4>display the first five rows</h4>




```python
data_set.head()
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
      <th>Year</th>
      <th>Category</th>
      <th>Prize</th>
      <th>Motivation</th>
      <th>Prize Share</th>
      <th>Laureate ID</th>
      <th>Laureate Type</th>
      <th>Full Name</th>
      <th>Birth Date</th>
      <th>Birth City</th>
      <th>Birth Country</th>
      <th>Sex</th>
      <th>Organization Name</th>
      <th>Organization City</th>
      <th>Organization Country</th>
      <th>Death Date</th>
      <th>Death City</th>
      <th>Death Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1901</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>160</td>
      <td>Individual</td>
      <td>Jacobus Henricus van 't Hoff</td>
      <td>1852-08-30</td>
      <td>Rotterdam</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Berlin University</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>1911-03-01</td>
      <td>Berlin</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1901</td>
      <td>"in special recognition of his poetic composit...</td>
      <td>1/1</td>
      <td>569</td>
      <td>Individual</td>
      <td>Sully Prudhomme</td>
      <td>1839-03-16</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1907-09-07</td>
      <td>Châtenay</td>
      <td>France</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1901</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1901</td>
      <td>"for his work on serum therapy, especially its...</td>
      <td>1/1</td>
      <td>293</td>
      <td>Individual</td>
      <td>Emil Adolf von Behring</td>
      <td>1854-03-15</td>
      <td>Hansdorf (Lawice)</td>
      <td>Prussia (Poland)</td>
      <td>Male</td>
      <td>Marburg University</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>1917-03-31</td>
      <td>Marburg</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>462</td>
      <td>Individual</td>
      <td>Jean Henry Dunant</td>
      <td>1828-05-08</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1910-10-30</td>
      <td>Heiden</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>463</td>
      <td>Individual</td>
      <td>Frédéric Passy</td>
      <td>1822-05-20</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1912-06-12</td>
      <td>Paris</td>
      <td>France</td>
    </tr>
  </tbody>
</table>
</div>




```python
HTML("<h4>display the last five rows</h4>")
```




<h4>display the last five rows</h4>




```python
data_set.tail(5)
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
      <th>Year</th>
      <th>Category</th>
      <th>Prize</th>
      <th>Motivation</th>
      <th>Prize Share</th>
      <th>Laureate ID</th>
      <th>Laureate Type</th>
      <th>Full Name</th>
      <th>Birth Date</th>
      <th>Birth City</th>
      <th>Birth Country</th>
      <th>Sex</th>
      <th>Organization Name</th>
      <th>Organization City</th>
      <th>Organization Country</th>
      <th>Death Date</th>
      <th>Death City</th>
      <th>Death Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>964</th>
      <td>2016</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 2016</td>
      <td>"for his discoveries of mechanisms for autophagy"</td>
      <td>1/1</td>
      <td>927</td>
      <td>Individual</td>
      <td>Yoshinori Ohsumi</td>
      <td>1945-02-09</td>
      <td>Fukuoka</td>
      <td>Japan</td>
      <td>Male</td>
      <td>Tokyo Institute of Technology</td>
      <td>Tokyo</td>
      <td>Japan</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>965</th>
      <td>2016</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2016</td>
      <td>"for his resolute efforts to bring the country...</td>
      <td>1/1</td>
      <td>934</td>
      <td>Individual</td>
      <td>Juan Manuel Santos</td>
      <td>1951-08-10</td>
      <td>Bogotá</td>
      <td>Colombia</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>966</th>
      <td>2016</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/2</td>
      <td>928</td>
      <td>Individual</td>
      <td>David J. Thouless</td>
      <td>1934-09-21</td>
      <td>Bearsden</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>University of Washington</td>
      <td>Seattle, WA</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>967</th>
      <td>2016</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/4</td>
      <td>929</td>
      <td>Individual</td>
      <td>F. Duncan M. Haldane</td>
      <td>1951-09-14</td>
      <td>London</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>Princeton University</td>
      <td>Princeton, NJ</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>968</th>
      <td>2016</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/4</td>
      <td>930</td>
      <td>Individual</td>
      <td>J. Michael Kosterlitz</td>
      <td>1943-06-22</td>
      <td>Aberdeen</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>Brown University</td>
      <td>Providence, RI</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
HTML("<h4> 10 Countries with the most awards</h4>")
```




<h4>Countries with the most awards</h4>




```python
data_set['Birth Country'].value_counts().head(10)
```




    United States of America    276
    United Kingdom               88
    Germany                      70
    France                       53
    Sweden                       30
    Japan                        29
    Russia                       20
    Netherlands                  19
    Italy                        18
    Canada                       18
    Name: Birth Country, dtype: int64




```python
HTML("<h4> 10 Countries with the least awards</h4>")
```




<h4> 10 Countries with the least awards</h4>




```python
data_set['Birth Country'].value_counts().tail(10)
```




    Poland (Lithuania)                          1
    British West Indies (Saint Lucia)           1
    Venezuela                                   1
    Free City of Danzig (Poland)                1
    Austria-Hungary (Bosnia and Herzegovina)    1
    Austrian Empire (Italy)                     1
    Bavaria (Germany)                           1
    Ottoman Empire (Turkey)                     1
    W&uuml;rttemberg (Germany)                  1
    Gold Coast (Ghana)                          1
    Name: Birth Country, dtype: int64




```python
HTML("<h4>lets visualize top ten countries with the most awards</h4>")
```




<h4>lets visualize top ten countries with the most awards</h4>




```python
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
plt.style.use('ggplot')
```


```python
top10.plot.bar(figsize=(17,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xab693f8c>




![png]({{site.baseurl}}/assets/images/noble/blog1_18_1.png)



```python
HTML("<h4>lets see the awards in terms of category</h4>")
```




<h4>lets see the awards in terms of category</h4>




```python
data_set.Category.value_counts()
```




    Medicine      227
    Physics       222
    Chemistry     194
    Peace         130
    Literature    113
    Economics      83
    Name: Category, dtype: int64




```python
HTML("<h4>lets visualize the awards in terms of category</h4>")
```




<h4>lets visualize the awards in terms of category</h4>




```python
cat = data_set.Category.value_counts()
```


```python
cat.plot(kind='barh',figsize=(16,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xab64362c>



![png]({{site.baseurl}}/assets/images/noble/blog1_23_1.png)




```python
HTML("<h4>lets count the awards in terms of gender</h4>")
```




<h4>lets count the awards in terms of gender</h4>




```python
data_set.Sex.value_counts()
```




    Male      893
    Female     50
    Name: Sex, dtype: int64




```python
HTML("<h4>lets visualize the awards in terms of gender</h4>")
```




<h4>lets visualize the awards in terms of gender</h4>




```python
gender = data_set.Sex.value_counts()
```


```python
gender.plot(kind='pie',figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xaa0dc0ec>





![png]({{site.baseurl}}/assets/images/noble/blog1_28_1.png)


```python
HTML("<h4>lets check the number of female that have won it from united states</h4>")
```




<h4>lets check the number of female that have won it from united states</h4>




```python
us = data_set[data_set['Birth Country'] == 'United States of America']
```


```python
us.Sex.value_counts()
```




    Male      264
    Female     12
    Name: Sex, dtype: int64




```python
us_v = us.Sex.value_counts()
```


```python
us_v.plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xaa0660cc>





![png]({{site.baseurl}}/assets/images/noble/blog1_33_1.png)



```python
HTML("<h4>lets analyze the awards in terms of continent</h4>")
```




<h4>lets analyze the awards in terms of continent</h4>




```python
contries = data_set['Birth Country'].unique()
```


```python
contries
```




    array(['Netherlands', 'France', 'Prussia (Poland)', 'Switzerland',
           'Prussia (Germany)', 'Schleswig (Germany)', 'India', 'Sweden',
           'Norway', 'Faroe Islands (Denmark)', 'United Kingdom',
           'Russian Empire (Poland)', 'Scotland', 'Spain', 'Russia', nan,
           'Poland', 'Germany', 'Austrian Empire (Czech Republic)',
           'Hungary (Slovakia)', 'Tuscany (Italy)', 'Italy',
           'United States of America', 'Bavaria (Germany)',
           'British India (India)', 'Austrian Empire (Italy)', 'New Zealand',
           'East Friesland (Germany)', 'Russian Empire (Ukraine)', 'Denmark',
           'Luxembourg', 'Russian Empire (Latvia)', 'Belgium',
           'Hesse-Kassel (Germany)', 'Germany (Russia)',
           'Mecklenburg (Germany)', 'Austria', 'Prussia (Russia)',
           'Australia', 'Austria-Hungary (Slovenia)', 'Ireland', 'Canada',
           'Java, Dutch East Indies (Indonesia)', 'Austrian Empire (Austria)',
           'Germany (Poland)', 'W&uuml;rttemberg (Germany)', 'Argentina',
           'Austria-Hungary (Hungary)', 'Austria-Hungary (Austria)',
           'Austria-Hungary (Croatia)', 'Russian Empire (Finland)',
           'Austria-Hungary (Poland)', 'Chile',
           'Austria-Hungary (Czech Republic)', 'Portugal', 'Japan',
           'South Africa', 'Germany (France)', 'Iceland', 'China',
           'French Algeria (Algeria)', 'Guadeloupe Island', 'Brazil',
           'Southern Rhodesia (Zimbabwe)', 'Bosnia (Bosnia and Herzegovina)',
           'Hungary', 'Russian Empire (Azerbaijan)',
           'Ottoman Empire (Turkey)', 'Egypt',
           'Union of Soviet Socialist Republics (Russia)',
           'Austria-Hungary (Ukraine)', 'Guatemala',
           'Russian Empire (Belarus)', 'Vietnam', 'Romania',
           'Austria-Hungary (Bosnia and Herzegovina)',
           'Russian Empire (Russia)', 'Northern Ireland',
           'Poland (Lithuania)', 'British West Indies (Saint Lucia)',
           'Crete (Greece)', 'Ottoman Empire (Republic of Macedonia)',
           'India (Pakistan)', 'Russian Empire (Lithuania)', 'Venezuela',
           'Poland (Ukraine)', 'Bulgaria', 'Lithuania', 'Colombia', 'Mexico',
           'Madagascar', 'German-occupied Poland (Poland)', 'Taiwan',
           'Nigeria', 'West Germany (Germany)', 'Korea (South Korea)',
           'Costa Rica', "Tibet (People's Republic of China)",
           'Burma (Myanmar)', 'Saint Lucia', 'Poland (Belarus)',
           'British Mandate of Palestine (Israel)', 'East Timor',
           'Free City of Danzig (Poland)',
           'Union of Soviet Socialist Republics (Belarus)', 'Trinidad',
           'Gold Coast (Ghana)', 'Iran',
           'British Protectorate of Palestine (Israel)', 'Kenya', 'Turkey',
           'British India (Bangladesh)', 'Persia (Iran)',
           'Czechoslovakia (Czech Republic)', 'Finland', 'Cyprus', 'Peru',
           'Liberia', 'Yemen', 'Morocco', 'Pakistan', 'Ukraine'], dtype=object)




```python
n_america = ['United States of America','Canada','Costa Rica','Guatemala','Mexico',]
europe = ['Netherlands', 'France', 'Prussia (Poland)', 'Switzerland',
       'Prussia (Germany)', 'Schleswig (Germany)','Sweden'
        'Norway', 'Faroe Islands (Denmark)', 'United Kingdom',
       'Russian Empire (Poland)', 'Scotland', 'Spain', 'Russia',
       'Poland', 'Germany', 'Austrian Empire (Czech Republic)',
       'Hungary (Slovakia)', 'Tuscany (Italy)', 'Italy', 'Bavaria (Germany)',
       'Austrian Empire (Italy)',
       'East Friesland (Germany)', 'Russian Empire (Ukraine)', 'Denmark',
       'Luxembourg', 'Russian Empire (Latvia)', 'Belgium',
       'Hesse-Kassel (Germany)', 'Germany (Russia)',
       'Mecklenburg (Germany)', 'Austria', 'Prussia (Russia)',
       'Austria-Hungary (Slovenia)', 'Ireland', 
        'Austrian Empire (Austria)','Germany (Poland)', 'W&uuml;rttemberg (Germany)', 
       'Austria-Hungary (Hungary)', 'Austria-Hungary (Austria)',
       'Austria-Hungary (Croatia)', 'Russian Empire (Finland)',
       'Austria-Hungary (Poland)', 'Chile',
       'Austria-Hungary (Czech Republic)', 'Portugal', 
        'Germany (France)', 'Iceland','Guadeloupe Island','Bosnia (Bosnia and Herzegovina)',
       'Hungary', 'Russian Empire (Azerbaijan)',
       'Ottoman Empire (Turkey)', 
       'Union of Soviet Socialist Republics (Russia)',
       'Austria-Hungary (Ukraine)', 
       'Russian Empire (Belarus)', 'Romania',
       'Austria-Hungary (Bosnia and Herzegovina)',
       'Russian Empire (Russia)', 'Northern Ireland',
       'Poland (Lithuania)', 'British West Indies (Saint Lucia)',
       'Crete (Greece)', 'Ottoman Empire (Republic of Macedonia)',
        'Russian Empire (Lithuania)',
       'Poland (Ukraine)', 'Bulgaria', 'Lithuania', 
       'Madagascar', 'German-occupied Poland (Poland)','West Germany (Germany)', 
       'Saint Lucia', 'Poland (Belarus)', 'East Timor',
       'Free City of Danzig (Poland)','Union of Soviet Socialist Republics (Belarus)',
       'British Protectorate of Palestine (Israel)', 'Turkey',
        'Czechoslovakia (Czech Republic)', 'Finland', 'Cyprus',
         'Pakistan', 'Ukraine']
africa = ['Egypt','South Africa','Morocco','Liberia','Southern Rhodesia (Zimbabwe)',
          'Gold Coast (Ghana)', 'Kenya','Nigeria','French Algeria (Algeria)',]
asia = ['Japan','China','India','British Mandate of Palestine (Israel)'
        'British India (Bangladesh)','Korea (South Korea)','Iran','India (Pakistan)',
        'British India (India)','Yemen',"Tibet (People's Republic of China)",
        'Java, Dutch East Indies (Indonesia)','Taiwan','Persia (Iran)','Burma (Myanmar)',
         'Vietnam',]
s_america = ['Trinidad','Venezuela','Brazil', 'Argentina','Peru','Colombia']
oceania = ['New Zealand', 'Australia']
```


```python
continent = {
    "n_america":n_america,
    "africa":africa,
    "asia":asia,
    "s_america":s_america,
    "europe":europe,
    "oceania":oceania
}
```


```python
def cont(val):
    if val in continent['n_america']:
        return 'North Anmerica'
    if val in continent['africa']:
        return 'Africa'
    if val in continent['asia']:
        return 'Asia'
    if val in continent['oceania']:
        return 'Oceania'
    if val in continent['s_america']:
        return 'South America'
    return 'Europe' ## this is for europe
```


```python
data_set['contNumber'] = data_set['Birth Country'].apply(cont)
```


```python
cotin = data_set.contNumber.value_counts()
```


```python
cotin.plot(kind='bar',figsize=(15,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa671ddec>





![png]({{site.baseurl}}/assets/images/noble/blog1_42_1.png)
