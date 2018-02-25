

```python
from IPython.core.display import HTML
HTML("<iframe src=http://pandas.pydata.org width=800 height=350></iframe>")
```




<iframe src=http://pandas.pydata.org width=800 height=350></iframe>




```python
a = HTML()
```


```python
HTML("<h1>Finacial analysis</h1>")
```




<h1>Finacial analysis</h1>




```python
HTML("<img src='download.jpeg'>")
```




<img src='download.jpeg'>




```python
import IPython.core.display as disp
```


```python
disp.Math('22/3')
```




$$22/3$$




```python
import datetime

import pandas as pd
from pandas import Series, DataFrame
pd.__version__
```




    '0.22.0'




```python
import matplotlib.pyplot as plt
import matplotlib as mpl
mpl.rc('figure', figsize=(8, 7))
mpl.__version__
```




    '2.0.2'




```python
labels = ['a', 'b', 'c', 'd', 'e']
s = Series([1, 2, 3, 4, 5], index=labels)
s
```




    a    1
    b    2
    c    3
    d    4
    e    5
    dtype: int64




```python
'b' in s
```




    True




```python
HTML("<h4>It can be converted to dict</h4>")
```




<h4>It can be converted to dict</h4>




```python
mapping = s.to_dict()
mapping
```




    {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}




```python
Series(mapping)  ### series can accept dictionary
```




    a    1
    b    2
    c    3
    d    4
    e    5
    dtype: int64




```python
HTML("<h3>From Google finance</h3>")
```




<h3>From Google finance</h3>




```python
import pandas_datareader.data as web
```


```python
import datetime
```


```python
start = datetime.datetime(2010, 1, 1)
```


```python
end = datetime.datetime(2013, 1, 27)
```


```python
####### note how we do it
```


```python
f = web.DataReader('F', 'google', start, end)
```

    /home/anaconda/.local/lib/python3.6/site-packages/pandas_datareader/google/daily.py:40: UnstableAPIWarning: 
    The Google Finance API has not been stable since late 2017. Requests seem
    to fail at random. Failure is especially common when bulk downloading.
    
      warnings.warn(UNSTABLE_WARNING, UnstableAPIWarning)



```python
f.ix['2010-01-04']
```

    /opt/anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





    Open            10.17
    High            10.28
    Low             10.05
    Close           10.28
    Volume    60855796.00
    Name: 2010-01-04 00:00:00, dtype: float64




```python
############## wordld bank
```


```python
from pandas_datareader import wb
```


```python
mathces = wb.search('gdp.*capita.*const')
```


```python
dat = wb.download(indicator='NY.GDP.PCAP.KD', country=['US', 'CA', 'MX'], start=2005, end=2008)
```


```python
dat2  = wb.get_countries()
```


```python
len(dat2)
```




    304




```python
type(dat2)
```




    pandas.core.frame.DataFrame




```python
dat2.head()
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>Oranjestad</td>
      <td>ABW</td>
      <td>High income</td>
      <td>AW</td>
      <td>12.51670</td>
      <td>Not classified</td>
      <td>-70.0167</td>
      <td>Aruba</td>
      <td>Latin America &amp; Caribbean</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Asia</td>
      <td>Kabul</td>
      <td>AFG</td>
      <td>Low income</td>
      <td>AF</td>
      <td>34.52280</td>
      <td>IDA</td>
      <td>69.1761</td>
      <td>Afghanistan</td>
      <td>South Asia</td>
    </tr>
    <tr>
      <th>2</th>
      <td></td>
      <td></td>
      <td>AFR</td>
      <td>Aggregates</td>
      <td>A9</td>
      <td>NaN</td>
      <td>Aggregates</td>
      <td>NaN</td>
      <td>Africa</td>
      <td>Aggregates</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>Luanda</td>
      <td>AGO</td>
      <td>Lower middle income</td>
      <td>AO</td>
      <td>-8.81155</td>
      <td>IBRD</td>
      <td>13.2420</td>
      <td>Angola</td>
      <td>Sub-Saharan Africa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>Tirane</td>
      <td>ALB</td>
      <td>Upper middle income</td>
      <td>AL</td>
      <td>41.33170</td>
      <td>IBRD</td>
      <td>19.8172</td>
      <td>Albania</td>
      <td>Europe &amp; Central Asia</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['name'] == 'Nigeria']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>203</th>
      <td>Sub-Saharan Africa (excluding high income)</td>
      <td>Abuja</td>
      <td>NGA</td>
      <td>Lower middle income</td>
      <td>NG</td>
      <td>9.05804</td>
      <td>Blend</td>
      <td>7.48906</td>
      <td>Nigeria</td>
      <td>Sub-Saharan Africa</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['name'] == 'India']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>134</th>
      <td>South Asia</td>
      <td>New Delhi</td>
      <td>IND</td>
      <td>Lower middle income</td>
      <td>IN</td>
      <td>28.6353</td>
      <td>IBRD</td>
      <td>77.225</td>
      <td>India</td>
      <td>South Asia</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['name'] == 'China']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>49</th>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>Beijing</td>
      <td>CHN</td>
      <td>Upper middle income</td>
      <td>CN</td>
      <td>40.0495</td>
      <td>IBRD</td>
      <td>116.286</td>
      <td>China</td>
      <td>East Asia &amp; Pacific</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['name'] == 'France']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>100</th>
      <td></td>
      <td>Paris</td>
      <td>FRA</td>
      <td>High income</td>
      <td>FR</td>
      <td>48.8566</td>
      <td>Not classified</td>
      <td>2.35097</td>
      <td>France</td>
      <td>Europe &amp; Central Asia</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['name'] == 'United States']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>288</th>
      <td></td>
      <td>Washington D.C.</td>
      <td>USA</td>
      <td>High income</td>
      <td>US</td>
      <td>38.8895</td>
      <td>Not classified</td>
      <td>-77.032</td>
      <td>United States</td>
      <td>North America</td>
    </tr>
  </tbody>
</table>
</div>




```python
dat2[dat2['capitalCity'] == 'Moscow']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>236</th>
      <td>Europe &amp; Central Asia (excluding high income)</td>
      <td>Moscow</td>
      <td>RUS</td>
      <td>Upper middle income</td>
      <td>RU</td>
      <td>55.7558</td>
      <td>IBRD</td>
      <td>37.6176</td>
      <td>Russian Federation</td>
      <td>Europe &amp; Central Asia</td>
    </tr>
  </tbody>
</table>
</div>




```python
tt = dat2['incomeLevel']
```


```python
tt.unique()
```




    array(['High income', 'Low income', 'Aggregates', 'Lower middle income',
           'Upper middle income'], dtype=object)




```python
#import pandas_datareader as pdr
```


```python
tt.unique()
```




    array(['High income', 'Low income', 'Aggregates', 'Lower middle income',
           'Upper middle income'], dtype=object)




```python
def chenge(x):
    if x == 'High income':
        return 1
    elif x == 'Upper middle income':
        return 2
    elif x == 'Lower middle income':
        return 3
    elif x == 'Low income':
        return 4
    else:
        return 5
```


```python
chenge('High income')
```




    1




```python
att = tt.apply(chenge)
```


```python
len(att)
```




    304




```python
type(att)
```




    pandas.core.series.Series




```python
att[0]
```




    1




```python
att[90]
```




    3




```python
att.plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa96a272c>




```python
%matplotlib inline
```


```python
att3 = att.value_counts()
```


```python
len(att3)
```




    5




```python
att3.plot(kind='bar',figsize=(15,5))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xabba942c>




![png](financial_analysis_files/financial_analysis_50_1.png)



```python
dat2[dat2['name'] == 'Cambodia']
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
      <th>adminregion</th>
      <th>capitalCity</th>
      <th>iso3c</th>
      <th>incomeLevel</th>
      <th>iso2c</th>
      <th>latitude</th>
      <th>lendingType</th>
      <th>longitude</th>
      <th>name</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>148</th>
      <td>East Asia &amp; Pacific (excluding high income)</td>
      <td>Phnom Penh</td>
      <td>KHM</td>
      <td>Lower middle income</td>
      <td>KH</td>
      <td>11.5556</td>
      <td>IDA</td>
      <td>104.874</td>
      <td>Cambodia</td>
      <td>East Asia &amp; Pacific</td>
    </tr>
  </tbody>
</table>
</div>




```python
import os
```


```python
import pandas_datareader as pdr
```


