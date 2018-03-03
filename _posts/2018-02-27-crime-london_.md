---
title: "Exploratory analysis of London street level crime 2015-2017"
layout: post
date: 2018-02-27 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- crime
- london
star: true
category: blog
author: Mustapha
description: Exploratory analysis of London street level crime 2015-2017
---

![crime]({{site.baseurl}}/assets/images/london_crime/crime.jpg)

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
plt.style.use('ggplot')
```


```python
%matplotlib inline
```

<h3>Lets load the dataset </h3>
data source : https://data.police.uk/data/archive/


```python
data = pd.read_csv('crime.csv')
```

<h3>check the number of rows in the dataset</h3>


```python
data.shape
```




    (18000, 13)



the dataset has 18,000 rows and 13 columns

lets check the first five rows


```python
data.iloc[:5,:]
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
      <th>Unnamed: 0</th>
      <th>Crime ID</th>
      <th>Month</th>
      <th>Reported by</th>
      <th>Falls within</th>
      <th>Longitude</th>
      <th>Latitude</th>
      <th>Location</th>
      <th>LSOA code</th>
      <th>LSOA name</th>
      <th>Crime type</th>
      <th>Last outcome category</th>
      <th>Context</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>80e07583f4bd74b85e457d92eef5d014e4e8d7b0eab0dc...</td>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.106453</td>
      <td>51.518207</td>
      <td>On or near Charterhouse Street</td>
      <td>E01000916</td>
      <td>Camden 027B</td>
      <td>Bicycle theft</td>
      <td>Unable to prosecute suspect</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>6589894ebc515f501527628eb650d52a6f031116eb0ada...</td>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.111497</td>
      <td>51.518226</td>
      <td>On or near Pedestrian Subway</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Burglary</td>
      <td>Investigation complete; no suspect identified</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>e6dc6a4a33ed886c7c72beaff0c5de92cc35cd2f76c6e5...</td>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.111497</td>
      <td>51.518226</td>
      <td>On or near Pedestrian Subway</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Burglary</td>
      <td>Unable to prosecute suspect</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>b6e6462d45d0d7f4258d57628cab4c8988dc41ac675b63...</td>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.111497</td>
      <td>51.518226</td>
      <td>On or near Pedestrian Subway</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Other theft</td>
      <td>Investigation complete; no suspect identified</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>769e1aa86e62b5f3c4c08c8c140147a275ca721d0801ba...</td>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.113767</td>
      <td>51.517372</td>
      <td>On or near Stone Buildings</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Theft from the person</td>
      <td>Investigation complete; no suspect identified</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



lets remove the crime Id  and unamed 0 columns


```python
del data['Crime ID']
```


```python
del data['Unnamed: 0']
```


```python
data.head(3)
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
      <th>Month</th>
      <th>Reported by</th>
      <th>Falls within</th>
      <th>Longitude</th>
      <th>Latitude</th>
      <th>Location</th>
      <th>LSOA code</th>
      <th>LSOA name</th>
      <th>Crime type</th>
      <th>Last outcome category</th>
      <th>Context</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.106453</td>
      <td>51.518207</td>
      <td>On or near Charterhouse Street</td>
      <td>E01000916</td>
      <td>Camden 027B</td>
      <td>Bicycle theft</td>
      <td>Unable to prosecute suspect</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.111497</td>
      <td>51.518226</td>
      <td>On or near Pedestrian Subway</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Burglary</td>
      <td>Investigation complete; no suspect identified</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-01</td>
      <td>City of London Police</td>
      <td>City of London Police</td>
      <td>-0.111497</td>
      <td>51.518226</td>
      <td>On or near Pedestrian Subway</td>
      <td>E01000914</td>
      <td>Camden 028B</td>
      <td>Burglary</td>
      <td>Unable to prosecute suspect</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



lets check the month datatype


```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 18000 entries, 0 to 17999
    Data columns (total 11 columns):
    Month                    18000 non-null object
    Reported by              18000 non-null object
    Falls within             18000 non-null object
    Longitude                17129 non-null float64
    Latitude                 17129 non-null float64
    Location                 18000 non-null object
    LSOA code                17129 non-null object
    LSOA name                17129 non-null object
    Crime type               18000 non-null object
    Last outcome category    14801 non-null object
    Context                  0 non-null float64
    dtypes: float64(3), object(8)
    memory usage: 984.4+ KB


it appears the month datatype is object, we need to convert it to datetime to be able to manipulate it


```python
import datetime
```


```python
data['Month'] = pd.to_datetime(data['Month'],yearfirst=True)
```


```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 18000 entries, 0 to 17999
    Data columns (total 11 columns):
    Month                    18000 non-null datetime64[ns]
    Reported by              18000 non-null object
    Falls within             18000 non-null object
    Longitude                17129 non-null float64
    Latitude                 17129 non-null float64
    Location                 18000 non-null object
    LSOA code                17129 non-null object
    LSOA name                17129 non-null object
    Crime type               18000 non-null object
    Last outcome category    14801 non-null object
    Context                  0 non-null float64
    dtypes: datetime64[ns](1), float64(3), object(7)
    memory usage: 1.0+ MB


lest check location based on incicence of crime


```python
data.Location.value_counts()
```




    No Location                                871
    On or near Police Station                  607
    On or near Pedestrian Subway               607
    On or near Supermarket                     532
    On or near Parking Area                    487
    On or near Great St Helen'S                354
    On or near Conference/Exhibition Centre    318
    On or near Nightclub                       316
    On or near Blomfield Street                304
    On or near Queen Victoria Street           297
    On or near St Martin'S Le Grand            296
    On or near Bride Lane                      296
    On or near New Change                      284
    On or near Shopping Area                   274
    On or near Fish Street Hill                269
    On or near Clement'S Lane                  235
    On or near Gracechurch Street              204
    On or near Fleet Street                    194
    On or near Artillery Lane                  172
    On or near Leadenhall Street               166
    On or near Fetter Lane                     158
    On or near Finch Lane                      149
    On or near Philpot Lane                    149
    On or near Bow Lane                        141
    On or near Cheapside                       139
    On or near Bell Inn Yard                   138
    On or near Bishopsgate                     133
    On or near Bear Alley                      132
    On or near Primrose Street                 130
    On or near Eastcheap                       129
                                              ... 
    On or near St Dunstan'S Lane                 3
    On or near Mount Pleasant                    3
    On or near Old Buildings                     2
    On or near Dysart Street                     2
    On or near Amen Court                        2
    On or near Sandy Lane                        2
    On or near Tooley Street                     2
    On or near Shadwell Gardens                  2
    On or near Goswell Place                     2
    On or near Mark Street                       1
    On or near Milk Street                       1
    On or near Little Essex Street               1
    On or near Farringdon Street                 1
    On or near Cripplegate Street                1
    On or near Timber Street                     1
    On or near Goldsmith Street                  1
    On or near Stoney Lane                       1
    On or near Fournier Street                   1
    On or near Nelson Terrace                    1
    On or near Whiskin Street                    1
    On or near Queen Street Place                1
    On or near Tower Royal                       1
    On or near Mucking Wharf Road                1
    On or near Folgate Street                    1
    On or near Holywell Row                      1
    On or near Banner Street                     1
    On or near Upper Ground                      1
    On or near Haven Quays                       1
    On or near Weaver'S Lane                     1
    On or near Bartlett Court                    1
    Name: Location, Length: 335, dtype: int64



lets visualize top ten crime location


```python
data.Location.value_counts().head(10).plot(kind='bar',figsize=(15,6),title='Crime Location in London city')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa812488c>




![crime]({{site.baseurl}}/assets/images/london_crime/blog_24_1.png)

it turned out location was unknown for 871 times.Aside from No location, most crime happnede very close to police station!!!

##### lets visualize the 5 least crime location


```python
data.Location.value_counts().tail(5).plot(kind='bar',figsize=(13,5))
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa7e2ed2c>



![crime]({{site.baseurl}}/assets/images/london_crime/blog_27_1.png)


we found that the most crime free location are Banner Street,Upper Ground,Weaver's Lane

### lets check crime type


```python
data['Crime type'].value_counts()
```




    Other theft                     4081
    Anti-social behaviour           3199
    Violence and sexual offences    2536
    Shoplifting                     1911
    Theft from the person           1270
    Drugs                            996
    Bicycle theft                    934
    Burglary                         665
    Public order                     661
    Criminal damage and arson        659
    Other crime                      470
    Vehicle crime                    402
    Possession of weapons            111
    Robbery                          105
    Name: Crime type, dtype: int64



other theft, Anti Social behaviour and Sexual behavoiurs is the most prevalent


```python
data['Crime type'].value_counts().plot(kind='bar',figsize=(15,6),title='Crime type in Londo--2015-2017')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa7f3baac>




![crime]({{site.baseurl}}/assets/images/london_crime/blog_32_1.png)

##### Location in which Violence and Sexual offences occur the most


```python

data[data['Crime type'] == 'Violence and sexual offences']['Location'].value_counts()
```




    No Location                                178
    On or near Great St Helen'S                104
    On or near Police Station                  101
    On or near Supermarket                      78
    On or near Pedestrian Subway                75
    On or near Nightclub                        65
    On or near Parking Area                     64
    On or near Conference/Exhibition Centre     55
    On or near Blomfield Street                 53
    On or near Queen Victoria Street            51
    On or near Leadenhall Street                50
    On or near Fish Street Hill                 43
    On or near Shopping Area                    34
    On or near Philpot Lane                     33
    On or near Moorgate                         32
    On or near Wormwood Street                  30
    On or near Gracechurch Street               30
    On or near St Martin'S Le Grand             29
    On or near Finch Lane                       29
    On or near Bride Lane                       29
    On or near Watling Court                    28
    On or near St Swithin'S Lane                27
    On or near New Broad Street                 25
    On or near New Change                       23
    On or near Wood Street                      23
    On or near Mark Lane                        21
    On or near Moor Lane                        20
    On or near Camomile Street                  20
    On or near Distaff Lane                     20
    On or near Creed Lane                       19
                                              ... 
    On or near Arthur Street                     1
    On or near Fournier Street                   1
    On or near Cloth Street                      1
    On or near Old Seacoal Lane                  1
    On or near Lloyd'S Avenue                    1
    On or near Bell Yard                         1
    On or near Sandy'S Row                       1
    On or near Cursitor Street                   1
    On or near Amen Corner                       1
    On or near Norton Folgate                    1
    On or near St Dunstan'S Hill                 1
    On or near St Mary Axe                       1
    On or near Copthall Avenue                   1
    On or near Leadenhall Place                  1
    On or near Monkwell Square                   1
    On or near Tudor Street                      1
    On or near Lombard Lane                      1
    On or near Portsoken Street                  1
    On or near Pilgrim Street                    1
    On or near Nun Court                         1
    On or near Temple Lane                       1
    On or near South Place Mews                  1
    On or near John Carpenter Street             1
    On or near Basinghall Street                 1
    On or near King'S Arms Yard                  1
    On or near Charterhouse Street               1
    On or near Moorgate Place                    1
    On or near Old Square                        1
    On or near Billiter Street                   1
    On or near Charterhouse Mews                 1
    Name: Location, Length: 256, dtype: int64




```python
sex_crime = data[data['Crime type'] == 'Violence and sexual offences']['Location'].value_counts()
```


```python
sex_crime.head().plot(kind='bar',figsize=(15,6),title='Location of Violence and Sexual Offence')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa67ce90c>




![crime]({{site.baseurl}}/assets/images/london_crime/blog_36_1.png)

##### analysis of crime based on Last outcome category


```python
data['Last outcome category'].value_counts()
```




    Investigation complete; no suspect identified          7568
    Unable to prosecute suspect                            1644
    Status update unavailable                              1613
    Court result unavailable                                783
    Offender given a caution                                591
    Under investigation                                     531
    Offender sent to prison                                 443
    Offender given a drugs possession warning               249
    Local resolution                                        245
    Offender fined                                          198
    Offender given suspended prison sentence                143
    Offender given community sentence                       138
    Formal action is not in the public interest             129
    Defendant found not guilty                              116
    Awaiting court outcome                                  104
    Offender given penalty notice                            85
    Offender given conditional discharge                     81
    Court case unable to proceed                             42
    Offender otherwise dealt with                            27
    Suspect charged as part of another case                  22
    Further investigation is not in the public interest      21
    Offender deprived of property                            12
    Action to be taken by another organisation                7
    Offender ordered to pay compensation                      5
    Defendant sent to Crown Court                             3
    Offender given absolute discharge                         1
    Name: Last outcome category, dtype: int64




```python
data['Last outcome category'].value_counts().head(10).plot(kind='bar',figsize=(16,7),title='Crime Outome')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa6798c2c>



![crime]({{site.baseurl}}/assets/images/london_crime/blog_39_1.png)

turned out that most time suspect was unable to be indentified 

## Time series analysis of the crime


```python
crime_time = data['Month']
```


```python
crime_time.head()
```




    0   2015-01-01
    1   2015-01-01
    2   2015-01-01
    3   2015-01-01
    4   2015-01-01
    Name: Month, dtype: datetime64[ns]




```python
crime_time = pd.DataFrame(crime_time)
```


```python
#pd.to_datetime(crime_time['Month'],yearfirst=True)
#crime_time['Month'] = pd.to_datetime(crime_time['Month'],yearfirst=True)
crime_time.head()
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
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-01-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-01-01</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-01-01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-01-01</td>
    </tr>
  </tbody>
</table>
</div>




```python
crime_time['value'] = 0
```


```python
crime_time['Month'] = pd.to_datetime(crime_time['Month'],yearfirst=True)
```


```python
crime_time.set_index(crime_time.Month,inplace=True)
```


```python
del crime_time['Month']
```


```python
crime_time.head()
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
      <th>value</th>
    </tr>
    <tr>
      <th>Month</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-01-01</th>
      <td>0</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>0</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>0</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>0</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
crime_t = crime_time.resample('M')
```


```python
crime_t
```




    DatetimeIndexResampler [freq=<MonthEnd>, axis=0, closed=right, label=right, convention=start, base=0]




```python
#
```


```python
crime_per_month = crime_t.count()
```


```python
crime_per_month.plot(kind='line',figsize=(16,7),title='Monthly Times seties (2015-2017)')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa80ecb4c>




![crime]({{site.baseurl}}/assets/images/london_crime/blog_55_1.png)

the above show crime was high around march of 2017


```python
crime_w = crime_time.resample('Y')
```


```python
crime_w = crime_w.count()
```


```python
crime_w.index.name = 'Year'
```


```python
crime_w.head()
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
      <th>value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-12-31</th>
      <td>6185</td>
    </tr>
    <tr>
      <th>2016-12-31</th>
      <td>6586</td>
    </tr>
    <tr>
      <th>2017-12-31</th>
      <td>5229</td>
    </tr>
  </tbody>
</table>
</div>




```python
crime_w.plot(figsize=(17,6),title='Yearly Time series of crime per year')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa5de6e2c>




![crime]({{site.baseurl}}/assets/images/london_crime/blog_61_1.png)

there was more crime in 2016 than 2015 and 2017 but there was a particular month in 2017 that recorded highest crime which was around march

we also learnt that through out 2015 crime rate was on the increase


```python

```
