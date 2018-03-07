---
title: "Analysis of conflicts in Africa 1997 - 2017"
layout: post
date: 2018-03-06 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- conflicts
- Africa
star: true
category: blog
author: Mustapha
description: Analysis of conflict in Africa
---

```python
import pandas as pd
import pandas
```

<h2>Context</h2>
The <a href='https://www.acleddata.com/about-acled/'>Armed Conflict Location and Event Data Project</a> is designed for disaggregated conflict analysis and crisis mapping. This dataset codes the dates and locations of all reported political violence and protest events in dozens of developing countries in Africa. Political violence and protest includes events that occur within civil wars and periods of instability, public protest and regime breakdown. The project covers all African countries from 1997 to 2017.

<h3>Content</h3>
These data contain information on:
<ul>
<li>Dates and locations of conflict events;</li>
<li>Specific types of events including battles, civilian killings, riots, protests and</li>
<li>recruitment activities;</li>
<li>Events by a range of actors, including rebels, governments, militias, armed groups, protesters and civilians;</li>
<li>Changes in territorial control; and Reported fatalities.</li>
</ul>
Event data are derived from a variety of sources including reports from developing countries and local media, humanitarian agencies, and research publications. Please review the codebook and user guide for additional information: the codebook is for coders and users of ACLED, whereas the brief guide for users reviews important information for downloading, reviewing and using ACLED data. A specific user guide for development and humanitarian practitioners is also available, as is a guide to our sourcing materials.

<h3>Acknowledgements:</h3>
ACLED is directed by Prof. Clionadh Raleigh (University of Sussex). It is operated by senior research manager Andrea Carboni (University of Sussex) for Africa and Hillary Tanoff for South and South-East Asia. The data collection involves several research analysts, including Charles Vannice, James Moody, Daniel Wigmore-Shepherd, Andrea Carboni, Matt Batten-Carew, Margaux Pinaud, Roudabeh Kishi, Helen Morris, Braden Fuller, Daniel Moody and others. Please cite:
Raleigh, Clionadh, Andrew Linke, Håvard Hegre and Joakim Karlsen. 2010. Introducing ACLED-Armed Conflict Location and Event Data. Journal of Peace Research 47(5) 651-660.

<h3>Data Source</h3>
The Dataset for this analysis can be gotten on <a href='https://www.kaggle.com/jboysen/african-conflicts/data'>Kaggle Website</a>

<h3>About The Dataset</h3>
<ul>
<li>ACTOR1: Name of first actor</li>
<li>ACTOR1_ID: Unique numerical ID for first actor</li>
<li>ACTOR2: Name of second actor</li>
<li>ACTOR2_ID: Unique numerical ID for second actor</li>
<li>ACTOR_DYAD_ID: Join of first two actor IDs in format (ACTOR1_ID - ACTOR2_ID)</li>
<li>ADMIN1: The largest sub-national administrative region in which the event took place</li>
<li>ADMIN2: The second-largest sub-national administrative region in which the event took place</li>
<li>ADMIN3: The third-largest sub-national administrative region in which the event took place</li>
<li>ALLY_ACTOR_1: Allied parties to Actor1</li>
<li>ALLY_ACTOR_2: Allied parties to Actor2</li>
<li>COUNTRY: country of conflict</li>
<li>EVENT_DATE: date of conflict, DD/MM/YYYY</li>
<li>EVENT_ID_CNTY: An individual identifier by number and country acronym</li>
<li>EVENT_ID_NO_CNTY: An individual numeric identifier</li>
<li>EVENT_TYPE: Event occurrence, string eg “Riots against police”</li>
<li>FATALITIES: Integer value of fatalities that occurred, as reported by source</li>
<li>GEO_PRECISION: A numeric code indicating the level of certainty of the geocode for the event</li>
<li>GWNO: Gleditsch & Ward (2007) country code</li>
<li>INTER1: A numeric code indicating the type of ACTOR1</li>
<li>INTER2: A numeric code indicating the type of ACTOR2</li>
<li>INTERACTION: A numeric code indicating the interaction between types of ACTOR1 and ACTOR2</li>
<li>LOCATION: The location where event occurred</li>
<li>NOTES: additional notes, string</li>
<li>SOURCE: Source of conflict information</li>
<li>TIME_PRECISION: A numeric code indicating the level of certainty of the date coded for the event</li>
<li>YEAR: Year event occurred</li>
</ul>


```python
data = pd.read_csv('african_conflicts.csv')
```

    /home/anaconda/.conda/envs/py27/lib/python2.7/site-packages/IPython/core/interactiveshell.py:2717: DtypeWarning: Columns (21,23) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)


####  numbers of rows and columns in the dataset


```python
data.shape
```




    (165808, 28)



#### First five rows in the dataset


```python
pandas.set_option('display.max_columns', None)
```


```python
data.head()
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
      <th>ACTOR1</th>
      <th>ACTOR1_ID</th>
      <th>ACTOR2</th>
      <th>ACTOR2_ID</th>
      <th>ACTOR_DYAD_ID</th>
      <th>ADMIN1</th>
      <th>ADMIN2</th>
      <th>ADMIN3</th>
      <th>ALLY_ACTOR_1</th>
      <th>ALLY_ACTOR_2</th>
      <th>COUNTRY</th>
      <th>EVENT_DATE</th>
      <th>EVENT_ID_CNTY</th>
      <th>EVENT_ID_NO_CNTY</th>
      <th>EVENT_TYPE</th>
      <th>FATALITIES</th>
      <th>GEO_PRECISION</th>
      <th>GWNO</th>
      <th>INTER1</th>
      <th>INTER2</th>
      <th>INTERACTION</th>
      <th>LATITUDE</th>
      <th>LOCATION</th>
      <th>LONGITUDE</th>
      <th>NOTES</th>
      <th>SOURCE</th>
      <th>TIME_PRECISION</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>Civilians (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>Algeria</td>
      <td>18/04/2001</td>
      <td>1416RTA</td>
      <td>NaN</td>
      <td>Violence against civilians</td>
      <td>1</td>
      <td>1</td>
      <td>615</td>
      <td>1</td>
      <td>7</td>
      <td>17</td>
      <td>36.61954</td>
      <td>Beni Douala</td>
      <td>4.08282</td>
      <td>A Berber student was shot while in police cust...</td>
      <td>Associated Press Online</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Tizi Ouzou</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>19/04/2001</td>
      <td>2229RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>3</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.71183</td>
      <td>Tizi Ouzou</td>
      <td>4.04591</td>
      <td>Riots were reported in numerous villages in Ka...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>20/04/2001</td>
      <td>2230RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.64022</td>
      <td>Amizour</td>
      <td>4.90131</td>
      <td>Students protested in the Amizour area. At lea...</td>
      <td>Crisis Group</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>2231RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.64022</td>
      <td>Amizour</td>
      <td>4.90131</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rioters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Beni-Douala</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>2232RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>5</td>
      <td>1</td>
      <td>15</td>
      <td>36.61954</td>
      <td>Beni Douala</td>
      <td>4.08282</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
  </tbody>
</table>
</div>



the dataset contains more than 165 thousands rows and 28 columns. we will extract columns of interest for this analysis

#### we extract columns of interests


```python
cols = ['ACTOR1','ACTOR2','ALLY_ACTOR_1','ALLY_ACTOR_2','COUNTRY','EVENT_DATE','EVENT_TYPE','LOCATION','NOTES','SOURCE']
```


```python
len(cols) ### we will extract ten columns for analysis
```




    10




```python
data = data[cols]
```


```python
data.columns ## now we have 10 columns to work with
```




    Index([u'ACTOR1', u'ACTOR2', u'ALLY_ACTOR_1', u'ALLY_ACTOR_2', u'COUNTRY',
           u'EVENT_DATE', u'EVENT_TYPE', u'LOCATION', u'NOTES', u'SOURCE'],
          dtype='object')



#### we display firts five rows again


```python
data.head()
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
      <th>ACTOR1</th>
      <th>ACTOR2</th>
      <th>ALLY_ACTOR_1</th>
      <th>ALLY_ACTOR_2</th>
      <th>COUNTRY</th>
      <th>EVENT_DATE</th>
      <th>EVENT_TYPE</th>
      <th>LOCATION</th>
      <th>NOTES</th>
      <th>SOURCE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Civilians (Algeria)</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>Algeria</td>
      <td>18/04/2001</td>
      <td>Violence against civilians</td>
      <td>Beni Douala</td>
      <td>A Berber student was shot while in police cust...</td>
      <td>Associated Press Online</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>19/04/2001</td>
      <td>Riots/Protests</td>
      <td>Tizi Ouzou</td>
      <td>Riots were reported in numerous villages in Ka...</td>
      <td>Kabylie report</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>20/04/2001</td>
      <td>Riots/Protests</td>
      <td>Amizour</td>
      <td>Students protested in the Amizour area. At lea...</td>
      <td>Crisis Group</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>Riots/Protests</td>
      <td>Amizour</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rioters (Algeria)</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>Berber Ethnic Group (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>21/04/2001</td>
      <td>Riots/Protests</td>
      <td>Beni Douala</td>
      <td>Rioters threw molotov cocktails, rocks and bur...</td>
      <td>Kabylie report</td>
    </tr>
  </tbody>
</table>
</div>



#### lets first check the number of countries embroiled in conflict across Africa


```python
num_conflict = data.COUNTRY.value_counts()
```


```python
num_conflict.count()
```




    50



#### we check how each countries are affected


```python
num_conflict
```




    Somalia                         25232
    Democratic Republic of Congo    12294
    Nigeria                         12253
    Sudan                           12018
    South Africa                    10887
    Egypt                            9290
    Burundi                          7396
    Libya                            6532
    Zimbabwe                         6001
    Kenya                            5812
    Algeria                          5309
    Uganda                           5185
    South Sudan                      5144
    Ethiopia                         5035
    Sierra Leone                     4669
    Tunisia                          4493
    Central African Republic         3973
    Angola                           3181
    Ivory Coast                      1804
    Mali                             1753
    Liberia                          1369
    Morocco                          1355
    Zambia                           1289
    Senegal                          1132
    Madagascar                       1064
    Burkina Faso                     1032
    Cameroon                          937
    Guinea                            894
    Mozambique                        886
    Namibia                           754
    Tanzania                          746
    Chad                              732
    Ghana                             671
    Niger                             660
    Rwanda                            633
    Republic of Congo                 473
    Mauritania                        467
    Malawi                            434
    Eritrea                           408
    Togo                              258
    Guinea-Bissau                     233
    Gabon                             215
    Swaziland                         198
    Gambia                            190
    Benin                             187
    Lesotho                           118
    Djibouti                          112
    Botswana                           53
    Equatorial Guinea                  46
    Mozambique                          1
    Name: COUNTRY, dtype: int64




```python
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
ax = num_conflict.plot(kind='bar',figsize=(35,17),fontsize=(30))
plt.title("conflicts in Africa (1997-2017)", fontname='Ubuntu', fontsize=38,
          fontstyle='italic', fontweight='normal',color='green')
```




    <matplotlib.text.Text at 0xac7b90ec>



![image]({{site.baseurl}}/assets/images/afr_files/afr_26_1.png)


##### we inspect event type to see kind of conflict that is common


```python
cm_conflict = data.EVENT_TYPE.value_counts()
```


```python
cm_conflict
```




    Riots/Protests                                47224
    Violence against civilians                    45021
    Battle-No change of territory                 44005
    Strategic development                         10923
    Remote violence                               10456
    Battle-Government regains territory            2632
    Non-violent transfer of territory              2566
    Battle-Non-state actor overtakes territory     2135
    Headquarters or base established                771
    Remote Violence                                  30
    Violence Against Civilians                       21
    Battle-no change of territory                    16
    Strategic Development                             7
    Strategic development                             1
    Name: EVENT_TYPE, dtype: int64



Some event type are not unique!!! <h4> lets convert the whole string to lower and then count again, we will also strip white space as well to avoid duplicate</h4>


```python
import string
```


```python
a = data.EVENT_TYPE.apply(string.lower).apply(string.strip).value_counts()
```


```python
a
```




    riots/protests                                47224
    violence against civilians                    45042
    battle-no change of territory                 44021
    strategic development                         10931
    remote violence                               10486
    battle-government regains territory            2632
    non-violent transfer of territory              2566
    battle-non-state actor overtakes territory     2135
    headquarters or base established                771
    Name: EVENT_TYPE, dtype: int64



#### now we can visualize event type


```python
ax = a.plot(kind='bar',figsize=(16,6),fontsize=(20))
plt.xticks(rotation=70,fontsize=(17))
plt.title("conflicts Type in Africa (1997-2017)", fontname='Ubuntu', fontsize=20,
          fontstyle='italic', fontweight='normal',color='green')
```




    <matplotlib.text.Text at 0xac53ac8c>



![image]({{site.baseurl}}/assets/images/afr_files/afr_35_1.png)


## which year recorded highest conflict



```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 165808 entries, 0 to 165807
    Data columns (total 10 columns):
    ACTOR1          165808 non-null object
    ACTOR2          122255 non-null object
    ALLY_ACTOR_1    28144 non-null object
    ALLY_ACTOR_2    19651 non-null object
    COUNTRY         165808 non-null object
    EVENT_DATE      165808 non-null object
    EVENT_TYPE      165808 non-null object
    LOCATION        165805 non-null object
    NOTES           155581 non-null object
    SOURCE          165635 non-null object
    dtypes: object(10)
    memory usage: 6.3+ MB


###### we first convert the date and year to datatime


```python
import datetime
```


```python
data['EVENT_DATE'] = pd.to_datetime(data['EVENT_DATE'],dayfirst=True)
```


```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 165808 entries, 0 to 165807
    Data columns (total 10 columns):
    ACTOR1          165808 non-null object
    ACTOR2          122255 non-null object
    ALLY_ACTOR_1    28144 non-null object
    ALLY_ACTOR_2    19651 non-null object
    COUNTRY         165808 non-null object
    EVENT_DATE      165808 non-null datetime64[ns]
    EVENT_TYPE      165808 non-null object
    LOCATION        165805 non-null object
    NOTES           155581 non-null object
    SOURCE          165635 non-null object
    dtypes: datetime64[ns](1), object(9)
    memory usage: 7.0+ MB



```python
data_n = data.set_index(data.EVENT_DATE)
```


```python
data_n['counter'] = 0 #### we create new column to hold number of conflict per year
```


```python
data_n = data_n['counter']
```


```python
data_n = pd.DataFrame(data_n)
```


```python
con_yr = data_n.resample('Y').count()
```


```python
t = (range(1997,2018))
```


```python
t = tuple(t)
```


```python
ax = con_yr.plot(kind='bar',figsize=(15,6),fontsize=(18))
plt.title('Annual conflict 1997-2017',fontsize=(16))
ax.set_xticklabels(t,rotation=30)
ax.grid()
```

![image]({{site.baseurl}}/assets/images/afr_files/afr_49_0.png)


###### 2016 was the most troubled year

## Conflict according to region of Africa


```python
data.COUNTRY.unique()
```




    array(['Algeria', 'Angola', 'Benin', 'Burkina Faso', 'Burundi',
           'Cameroon', 'Central African Republic', 'Chad',
           'Democratic Republic of Congo', 'Egypt', 'Equatorial Guinea',
           'Eritrea', 'Ethiopia', 'Gabon', 'Gambia', 'Ghana', 'Guinea',
           'Guinea-Bissau', 'Ivory Coast', 'Kenya', 'Lesotho', 'Liberia',
           'Libya', 'Madagascar', 'Malawi', 'Mali', 'Mauritania', 'Morocco',
           'Mozambique', 'Namibia', 'Niger', 'Nigeria', 'Republic of Congo',
           'Rwanda', 'Senegal', 'Sierra Leone', 'Somalia', 'South Africa',
           'South Sudan', 'Sudan', 'Swaziland', 'Tanzania', 'Togo', 'Tunisia',
           'Uganda', 'Zambia', 'Zimbabwe', 'Botswana', 'Djibouti',
           'Mozambique '], dtype=object)




```python
region = {
    'north':['Algeria','Egypt','Morocco','Sudan','Tunisia','Western Sahara','Libya','Mauritania'],
    'east':['Burundi','Comoros','Djibouti','Eritrea','Ethiopia','Kenya','Zambia',
            'Madagascar','Malawi','Mauritius','Mayotte','Mozambique','Uganda',
            'Reunion','Rwanda','Seychelles','Somalia','South Sudan','Tanzania','Zimbabwe'],
    'west':['Benin','Burkina Faso','Cape Verde','Ivory Coast','Gambia',
            'Ghana','Guinea','Guinea-Bissau','Liberia','Mali',
            'Mauritania','Niger','Nigeria','Saint Helena','Senegal','Sierra Leone',
            'Togo'],
    'central':['Angola','Cameroon','Central African Republic','Chad',
               'Democratic Republic of Congo','Republic of Congo',
               'Equatorial Guinea','Gabon'],

    'south':['Botswana','Lesotho','Namibia','South Africa''Swaziland','Angola','Zambia']
}
```


```python
def mapper(country):
    if string.strip(country) in region['north'] or string.capitalize(country) in region['north']:
        return 1
    if string.strip(country) in region['east'] or string.capitalize(country) in region['east']:
        return 2
    if string.strip(country) in region['west'] or string.capitalize(country) in region['west']:
        return 3
    if string.strip(country) in region['central'] or string.capitalize(country) in region['central']:
        return 4
    if string.strip(country) in region['south'] or string.capitalize(country) in region['south']:
        return 5
    return 5 ### South africa and Swaziland here too
```


```python
data_region = data
```


```python
data_region.COUNTRY = data.COUNTRY.apply(mapper)
```


```python
data_region = data_region.COUNTRY.value_counts()
```


```python
data_region
```




    2    65378
    1    39464
    3    27105
    4    21851
    5    12010
    Name: COUNTRY, dtype: int64






```python
data_region = pd.DataFrame(data_region)
```


```python
data_region['val'] = [2,1,3,4,5]
```


```python
def mapper(val):
    if val == 1:
        return 'North Africa'
    if val == 2:
        return 'East Africa'
    if val == 3:
        return 'West Africa'
    if val == 4 :
        return 'Central Africa'
    return 'South Africa' 
```


```python
data_region.val = data_region.val.apply(mapper)
```


```python
data_region
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
      <th>COUNTRY</th>
      <th>val</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>65378</td>
      <td>East Africa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>39464</td>
      <td>North Africa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>27105</td>
      <td>West Africa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21851</td>
      <td>Central Africa</td>
    </tr>
    <tr>
      <th>5</th>
      <td>12010</td>
      <td>South Africa</td>
    </tr>
  </tbody>
</table>
</div>



## we visulize conflicts in terms of region


```python
data_region.set_index(data_region.val,inplace=True)
```


```python
del data_region['val']
```


```python
data_region
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
      <th>COUNTRY</th>
    </tr>
    <tr>
      <th>val</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>East Africa</th>
      <td>65378</td>
    </tr>
    <tr>
      <th>North Africa</th>
      <td>39464</td>
    </tr>
    <tr>
      <th>West Africa</th>
      <td>27105</td>
    </tr>
    <tr>
      <th>Central Africa</th>
      <td>21851</td>
    </tr>
    <tr>
      <th>South Africa</th>
      <td>12010</td>
    </tr>
  </tbody>
</table>
</div>




```python
ax = data_region.COUNTRY.plot(kind='bar',figsize=(16,6))
plt.xticks(fontsize=(24),rotation=30)
plt.tight_layout()
plt.yticks(fontsize=(20))
plt.title('Conflicts in Africa according to region',fontsize=(28))
plt.legend()
plt.grid()
```

![image]({{site.baseurl}}/assets/images/afr_files/afr_69_0.png)



```python
import mpl_toolkits
```


```python
mpl_toolkits.__path__.append('/usr/lib/python2.7/dist-packages/mpl_toolkits/')
```

## Analysis of conflicts that has something to do with Students

we will inspect column Note and we extract any rows that mention student


```python
data = pd.read_csv('african_conflicts.csv')
```


```python
stud_con = data[(data.NOTES.str.find('students') >=0 ) | (data.NOTES.str.find('Students') >=0 )]
```

#### lets count the number of rows returned


```python
stud_con.shape
```




    (5474, 28)




```python
## more than five thousand

```


```python
stud_con.head()
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
      <th>ACTOR1</th>
      <th>ACTOR1_ID</th>
      <th>ACTOR2</th>
      <th>ACTOR2_ID</th>
      <th>ACTOR_DYAD_ID</th>
      <th>ADMIN1</th>
      <th>ADMIN2</th>
      <th>ADMIN3</th>
      <th>ALLY_ACTOR_1</th>
      <th>ALLY_ACTOR_2</th>
      <th>COUNTRY</th>
      <th>EVENT_DATE</th>
      <th>EVENT_ID_CNTY</th>
      <th>EVENT_ID_NO_CNTY</th>
      <th>EVENT_TYPE</th>
      <th>FATALITIES</th>
      <th>GEO_PRECISION</th>
      <th>GWNO</th>
      <th>INTER1</th>
      <th>INTER2</th>
      <th>INTERACTION</th>
      <th>LATITUDE</th>
      <th>LOCATION</th>
      <th>LONGITUDE</th>
      <th>NOTES</th>
      <th>SOURCE</th>
      <th>TIME_PRECISION</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Amizour</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>20/04/2001</td>
      <td>2230RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.64022</td>
      <td>Amizour</td>
      <td>4.90131</td>
      <td>Students protested in the Amizour area. At lea...</td>
      <td>Crisis Group</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Oran</td>
      <td>Oran</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>3/05/2001</td>
      <td>2243RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>1</td>
      <td>16</td>
      <td>35.6911</td>
      <td>Oran</td>
      <td>-0.6417</td>
      <td>Students demonstrated in Oran despite signific...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Alger</td>
      <td>Sidi MHamed</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>4/05/2001</td>
      <td>2244RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.7525</td>
      <td>Algiers</td>
      <td>3.04197</td>
      <td>As many as 10,000 students protested at the go...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Alger</td>
      <td>Sidi MHamed</td>
      <td>NaN</td>
      <td>Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>29/05/2001</td>
      <td>1450RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.7525</td>
      <td>Algiers</td>
      <td>3.04197</td>
      <td>Students protested in the Algerian capital to ...</td>
      <td>Associated Press Online</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>155</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tizi Ouzou</td>
      <td>Tizi Ouzou</td>
      <td>NaN</td>
      <td>Berber Ethnic Group (Algeria); Students (Algeria)</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>15/04/2002</td>
      <td>2622RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>3</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.71183</td>
      <td>Tizi Ouzou</td>
      <td>4.04591</td>
      <td>Students protested and boycotted classes to de...</td>
      <td>Kabylie report</td>
      <td>3</td>
      <td>2002</td>
    </tr>
  </tbody>
</table>
</div>



##### which country has highest number of student conflict?



```python
stud_con.COUNTRY.value_counts()
```




    South Africa                    1167
    Egypt                            521
    Ethiopia                         497
    Sudan                            481
    Nigeria                          461
    Kenya                            318
    Uganda                           202
    Tunisia                          177
    Democratic Republic of Congo     140
    Algeria                          126
    Burkina Faso                     115
    Burundi                          106
    Senegal                          102
    Zambia                            96
    Zimbabwe                          80
    Ivory Coast                       79
    Somalia                           75
    Malawi                            71
    Madagascar                        66
    Morocco                           61
    Liberia                           60
    Central African Republic          53
    Niger                             41
    Guinea                            32
    Gabon                             32
    Swaziland                         31
    South Sudan                       31
    Namibia                           29
    Togo                              29
    Chad                              27
    Sierra Leone                      23
    Libya                             18
    Ghana                             17
    Tanzania                          17
    Mauritania                        15
    Gambia                             9
    Rwanda                             9
    Cameroon                           9
    Mali                               8
    Benin                              8
    Republic of Congo                  8
    Angola                             7
    Botswana                           7
    Mozambique                         4
    Guinea-Bissau                      3
    Equatorial Guinea                  2
    Djibouti                           2
    Eritrea                            1
    Lesotho                            1
    Name: COUNTRY, dtype: int64




```python
## south africa has the highest number of student conflict or conflict that has something to
## do with student
```


```python
std_con = stud_con.COUNTRY.value_counts()
```


```python
ax = std_con.plot(kind='bar',figsize=(25,10),fontsize=(30))
plt.title('student conflict---countries wise',fontsize=(30))
```




    <matplotlib.text.Text at 0xa7fde38c>



![image]({{site.baseurl}}/assets/images/afr_files/afr_84_1.png)


## conflict involving women 


```python
wn = data[(data.NOTES.str.find('women') >=0 ) | (data.NOTES.str.find('Women') >=0 )|(data.NOTES.str.find('Woman') >=0 )|(data.NOTES.str.find('woman') >=0 )]
```


```python
len(wn) # it return more than 3000 rows
```




    3944




```python
wn.head(2)
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
      <th>ACTOR1</th>
      <th>ACTOR1_ID</th>
      <th>ACTOR2</th>
      <th>ACTOR2_ID</th>
      <th>ACTOR_DYAD_ID</th>
      <th>ADMIN1</th>
      <th>ADMIN2</th>
      <th>ADMIN3</th>
      <th>ALLY_ACTOR_1</th>
      <th>ALLY_ACTOR_2</th>
      <th>COUNTRY</th>
      <th>EVENT_DATE</th>
      <th>EVENT_ID_CNTY</th>
      <th>EVENT_ID_NO_CNTY</th>
      <th>EVENT_TYPE</th>
      <th>FATALITIES</th>
      <th>GEO_PRECISION</th>
      <th>GWNO</th>
      <th>INTER1</th>
      <th>INTER2</th>
      <th>INTERACTION</th>
      <th>LATITUDE</th>
      <th>LOCATION</th>
      <th>LONGITUDE</th>
      <th>NOTES</th>
      <th>SOURCE</th>
      <th>TIME_PRECISION</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>78</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Alger</td>
      <td>Cheraga</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>19/06/2001</td>
      <td>2601RTA</td>
      <td>NaN</td>
      <td>Riots/Protests</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>0</td>
      <td>60</td>
      <td>36.80277</td>
      <td>Ain Benian</td>
      <td>2.92185</td>
      <td>100 women gathered in Ain Benian, west of Algi...</td>
      <td>Kabylie report</td>
      <td>1</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>410</th>
      <td>Protesters (Algeria)</td>
      <td>NaN</td>
      <td>Police Forces of Algeria (1999-)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bejaia</td>
      <td>Bejaia</td>
      <td>NaN</td>
      <td>SNATEGZ: National Autonomous Union of Sonelgaz...</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>22/03/2017</td>
      <td>3605RTA</td>
      <td>NaN</td>
      <td>Violence against civilians</td>
      <td>0</td>
      <td>1</td>
      <td>615</td>
      <td>6</td>
      <td>1</td>
      <td>16</td>
      <td>36.75</td>
      <td>Bejaia</td>
      <td>5.0833</td>
      <td>Security forces attacked the participants of t...</td>
      <td>Arab Trade Union Confederation; El Watan</td>
      <td>1</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
wn.COUNTRY.value_counts()
```




    Sudan                           651
    Somalia                         492
    Democratic Republic of Congo    416
    Nigeria                         318
    South Africa                    289
    South Sudan                     223
    Central African Republic        179
    Burundi                         160
    Egypt                           140
    Kenya                           138
    Zimbabwe                        137
    Tunisia                         112
    Uganda                           88
    Algeria                          87
    Libya                            70
    Morocco                          44
    Ivory Coast                      32
    Ghana                            31
    Ethiopia                         26
    Senegal                          25
    Namibia                          24
    Mali                             21
    Cameroon                         20
    Liberia                          18
    Angola                           17
    Guinea                           17
    Mauritania                       16
    Mozambique                       16
    Zambia                           16
    Burkina Faso                     15
    Madagascar                       14
    Rwanda                           13
    Malawi                           12
    Sierra Leone                     10
    Tanzania                         10
    Niger                             9
    Republic of Congo                 7
    Swaziland                         6
    Chad                              5
    Eritrea                           4
    Togo                              4
    Botswana                          4
    Djibouti                          2
    Gambia                            2
    Lesotho                           1
    Gabon                             1
    Guinea-Bissau                     1
    Equatorial Guinea                 1
    Name: COUNTRY, dtype: int64




```python
ax = wn.COUNTRY.value_counts().plot(kind='bar',figsize=(20,8),fontsize=(20))
```

![image]({{site.baseurl}}/assets/images/afr_files/afr_90_0.png)


## SUMMARIES BASED ON THE DATASET
<ul>
<li>the dataset contains more than 165,000 rows</li>
<li>East Africa is the most volatile region in Africa</li>
<li>South Africa is the least voltile region in Africa</li>
<li>Somalia is the most affected countries by conflict according to this report</li>
<li>Mozambique is the most peaceful country in Africa</li>
<li>2016 is the most troubled Year in Africa within the period of 1997 to 2017</li>
<li>Student involvement in conflict is most common in South Africa</li>
</ul>


```python

```
