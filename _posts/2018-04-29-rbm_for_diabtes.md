---
title: "Restricted Boltzmann Machine for Diabetes Prediction"
layout: post
date: 2018-04-29 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- RBM
- Diabetes
star: true
category: blog
author: Mustapha
description: Restricted Boltzmann Machine for Diabetes Prediction
---

<h3>Restricted Boltzmann machine (RBM)</h3>
A restricted Boltzmann machine (RBM) is a generative stochastic artificial neural network that can learn a probability distribution over its set of inputs.It has seen wide applications in
different areas of supervised/unsupervised machine learning such as feature learning,
dimensionality reduction, classification, collaborative filtering, and topic modeling.
<a href='https://en.wikipedia.org/wiki/Restricted_Boltzmann_machine'>Source</a>

<h3> Bernoulli RBM</h3>
we will use Berrnoulli RBM in scikit learn with Logistic regression.The BernoulliRBM is an unsupervised method so it is mostly used for non-linear feature extraction that can be feed to a classifier (in this case Logistic Regression).

<h3>Objective</h3>
To train a calssifier for predicting Diabetes

<h3>Data source</h3>
diabetes data set is included in scikit learn and can also be downloded from the <a href='https://www.kaggle.com/mariuszwilk/diabetes'>kaggle</a>

<h3>The Notebook</h3>
The notebook for this work can be found at <a href="https://github.com/alaniomotosho2/machine_learning/blob/master/rbm_4_diabtes.ipynb">[Restricted Boltzmann machine (RBM)]</a>

```python
import pandas as pd
import seaborn as sns
import random
from sklearn.model_selection import train_test_split
%matplotlib inline
import matplotlib
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler
from sklearn.preprocessing import StandardScaler
from numpy import set_printoptions
from sklearn.model_selection import KFold
from sklearn.model_selection import cross_val_score
from sklearn.pipeline import Pipeline
from sklearn.neural_network import BernoulliRBM
from sklearn import metrics
from sklearn.linear_model import LogisticRegression
from sklearn.grid_search import GridSearchCV
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix
from sklearn.metrics import classification_report
from sklearn.metrics import classification_report
```


```python
data = pd.read_csv('Diabetes.csv')
```

### Dimensions of Your Data


```python
shape = data.shape
print(shape)
```

    (768, 9)



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
      <th>preg_count</th>
      <th>glucose_concentration</th>
      <th>blood_pressure</th>
      <th>skin_thickness</th>
      <th>serum_insulin</th>
      <th>bmi</th>
      <th>pedigree_function</th>
      <th>age</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>148</td>
      <td>72</td>
      <td>35</td>
      <td>0</td>
      <td>33.6</td>
      <td>0.627</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>85</td>
      <td>66</td>
      <td>29</td>
      <td>0</td>
      <td>26.6</td>
      <td>0.351</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>183</td>
      <td>64</td>
      <td>0</td>
      <td>0</td>
      <td>23.3</td>
      <td>0.672</td>
      <td>32</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>89</td>
      <td>66</td>
      <td>23</td>
      <td>94</td>
      <td>28.1</td>
      <td>0.167</td>
      <td>21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>137</td>
      <td>40</td>
      <td>35</td>
      <td>168</td>
      <td>43.1</td>
      <td>2.288</td>
      <td>33</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Descriptive Statistics


```python
# Statistical Summary
from pandas import set_option
set_option('display.width', 100)
set_option('precision', 3)
description = data.describe()
(description)
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
      <th>preg_count</th>
      <th>glucose_concentration</th>
      <th>blood_pressure</th>
      <th>skin_thickness</th>
      <th>serum_insulin</th>
      <th>bmi</th>
      <th>pedigree_function</th>
      <th>age</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
      <td>768.000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.845</td>
      <td>120.895</td>
      <td>69.105</td>
      <td>20.536</td>
      <td>79.799</td>
      <td>31.993</td>
      <td>0.472</td>
      <td>33.241</td>
      <td>0.349</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.370</td>
      <td>31.973</td>
      <td>19.356</td>
      <td>15.952</td>
      <td>115.244</td>
      <td>7.884</td>
      <td>0.331</td>
      <td>11.760</td>
      <td>0.477</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.078</td>
      <td>21.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000</td>
      <td>99.000</td>
      <td>62.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>27.300</td>
      <td>0.244</td>
      <td>24.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.000</td>
      <td>117.000</td>
      <td>72.000</td>
      <td>23.000</td>
      <td>30.500</td>
      <td>32.000</td>
      <td>0.372</td>
      <td>29.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.000</td>
      <td>140.250</td>
      <td>80.000</td>
      <td>32.000</td>
      <td>127.250</td>
      <td>36.600</td>
      <td>0.626</td>
      <td>41.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>17.000</td>
      <td>199.000</td>
      <td>122.000</td>
      <td>99.000</td>
      <td>846.000</td>
      <td>67.100</td>
      <td>2.420</td>
      <td>81.000</td>
      <td>1.000</td>
    </tr>
  </tbody>
</table>
</div>



#### check if data is balanced


```python
class_counts = data.groupby('class').size()
print(class_counts)
```

    class
    0    500
    1    268
    dtype: int64


#### Correlations Between Attributes


```python
correlations = data.corr(method='pearson')
(correlations)
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
      <th>preg_count</th>
      <th>glucose_concentration</th>
      <th>blood_pressure</th>
      <th>skin_thickness</th>
      <th>serum_insulin</th>
      <th>bmi</th>
      <th>pedigree_function</th>
      <th>age</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>preg_count</th>
      <td>1.000</td>
      <td>0.129</td>
      <td>0.141</td>
      <td>-0.082</td>
      <td>-0.074</td>
      <td>0.018</td>
      <td>-0.034</td>
      <td>0.544</td>
      <td>0.222</td>
    </tr>
    <tr>
      <th>glucose_concentration</th>
      <td>0.129</td>
      <td>1.000</td>
      <td>0.153</td>
      <td>0.057</td>
      <td>0.331</td>
      <td>0.221</td>
      <td>0.137</td>
      <td>0.264</td>
      <td>0.467</td>
    </tr>
    <tr>
      <th>blood_pressure</th>
      <td>0.141</td>
      <td>0.153</td>
      <td>1.000</td>
      <td>0.207</td>
      <td>0.089</td>
      <td>0.282</td>
      <td>0.041</td>
      <td>0.240</td>
      <td>0.065</td>
    </tr>
    <tr>
      <th>skin_thickness</th>
      <td>-0.082</td>
      <td>0.057</td>
      <td>0.207</td>
      <td>1.000</td>
      <td>0.437</td>
      <td>0.393</td>
      <td>0.184</td>
      <td>-0.114</td>
      <td>0.075</td>
    </tr>
    <tr>
      <th>serum_insulin</th>
      <td>-0.074</td>
      <td>0.331</td>
      <td>0.089</td>
      <td>0.437</td>
      <td>1.000</td>
      <td>0.198</td>
      <td>0.185</td>
      <td>-0.042</td>
      <td>0.131</td>
    </tr>
    <tr>
      <th>bmi</th>
      <td>0.018</td>
      <td>0.221</td>
      <td>0.282</td>
      <td>0.393</td>
      <td>0.198</td>
      <td>1.000</td>
      <td>0.141</td>
      <td>0.036</td>
      <td>0.293</td>
    </tr>
    <tr>
      <th>pedigree_function</th>
      <td>-0.034</td>
      <td>0.137</td>
      <td>0.041</td>
      <td>0.184</td>
      <td>0.185</td>
      <td>0.141</td>
      <td>1.000</td>
      <td>0.034</td>
      <td>0.174</td>
    </tr>
    <tr>
      <th>age</th>
      <td>0.544</td>
      <td>0.264</td>
      <td>0.240</td>
      <td>-0.114</td>
      <td>-0.042</td>
      <td>0.036</td>
      <td>0.034</td>
      <td>1.000</td>
      <td>0.238</td>
    </tr>
    <tr>
      <th>class</th>
      <td>0.222</td>
      <td>0.467</td>
      <td>0.065</td>
      <td>0.075</td>
      <td>0.131</td>
      <td>0.293</td>
      <td>0.174</td>
      <td>0.238</td>
      <td>1.000</td>
    </tr>
  </tbody>
</table>
</div>



#### skew  and Kurtosis of univeraite data


```python
print(data.skew())

```

    preg_count               0.902
    glucose_concentration    0.174
    blood_pressure          -1.844
    skin_thickness           0.109
    serum_insulin            2.272
    bmi                     -0.429
    pedigree_function        1.920
    age                      1.130
    class                    0.635
    dtype: float64



```python
data.kurtosis()
```




    preg_count               0.159
    glucose_concentration    0.641
    blood_pressure           5.180
    skin_thickness          -0.520
    serum_insulin            7.214
    bmi                      3.290
    pedigree_function        5.595
    age                      0.643
    class                   -1.601
    dtype: float64



#### Univariate Visualization


```python
data.hist(figsize=(16,7))
```




    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1f381750>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1f2de9d0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1f306250>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1ea21dd0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1f2d5b50>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e94ee50>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e91e290>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e8df990>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e89ef90>]],
          dtype=object)




![png]({{site.baseurl}}/assets/images/rbm/output_16_1.png)

#### Density Curve to inspect shape of each distribution clearly


```python
data.plot(kind='density', subplots=True, layout=(3,3), sharex=False,figsize=(15,6))
```




    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e69d390>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e63f790>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e600410>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e5a7350>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e5889d0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e543a90>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e48d6d0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e45c190>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x7fcb1e419d10>]],
          dtype=object)




![png]({{site.baseurl}}/assets/images/rbm/output_18_1.png)

#### Multivariate Plots


```python
import numpy
correlations = data.corr()
# plot correlation matrix
fig = plt.figure(figsize=(15,7))
ax = fig.add_subplot(111)
cax = ax.matshow(correlations, vmin=-1, vmax=1)
fig.colorbar(cax)
ticks = numpy.arange(0,9,1)
ax.set_xticks(ticks)
ax.set_yticks(ticks)
ax.set_xticklabels(data.columns)
ax.set_yticklabels(data.columns)
plt.show()
```

![png]({{site.baseurl}}/assets/images/rbm/output_20_0.png)


####  Data standardization


```python
# Standardize data (0 mean, 1 stdev)
data_array = data.values
# separate array into input and output components
X = data_array[:,0:8]
Y = data_array[:,8]
scaler = StandardScaler()
scaledX = scaler.fit_transform(X)
# summarize transformed data
set_printoptions(precision=3)
print(scaledX[0:8,:])
```

    [[ 0.64   0.848  0.15   0.907 -0.693  0.204  0.468  1.426]
     [-0.845 -1.123 -0.161  0.531 -0.693 -0.684 -0.365 -0.191]
     [ 1.234  1.944 -0.264 -1.288 -0.693 -1.103  0.604 -0.106]
     [-0.845 -0.998 -0.161  0.155  0.123 -0.494 -0.921 -1.042]
     [-1.142  0.504 -1.505  0.907  0.766  1.41   5.485 -0.02 ]
     [ 0.343 -0.153  0.253 -1.288 -0.693 -0.811 -0.818 -0.276]
     [-0.251 -1.342 -0.988  0.719  0.071 -0.126 -0.676 -0.616]
     [ 1.828 -0.184 -3.573 -1.288 -0.693  0.42  -1.02  -0.361]]



```python
X = data_array[:,0:8]
y = data_array[:,8]

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)


X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2, random_state=2017)

print X.shape
print y.shape
```

    (768, 8)
    (768,)



```python
X_train[0]
```




    array([ 0.64 , -0.059, -0.988,  0.092,  0.835, -0.621,  2.555, -0.02 ])



####  Building Machine Learning Pipelines


```python
# initialize the RBM + Logistic Regression pipeline
rbm = BernoulliRBM()
logistic = LogisticRegression()
classifier = Pipeline([("rbm", rbm), ("logistic", logistic)])

params = {
    "rbm__learning_rate": [0.1, 0.01, 0.001,0.05,0.005],
    "rbm__n_iter": [20, 40,50, 80,90,100],
    "rbm__n_components": [20,30,50, 100,80, 200],
    "logistic__C": [1.0,5.0 ,10.0,20.0,30.0,100.0]}

# perform a grid search over the parameter
gs = GridSearchCV(classifier, params, n_jobs = -1, verbose = 1)
gs.fit(X_train, y_train)

print "Best Score: %0.3f" % (gs.best_score_)

print "RBM + Logistic Regression parameters"
bestParams = gs.best_estimator_.get_params()

# loop over the parameters and print each of them out
# so they can be manually set
for p in sorted(params.keys()):
    print "\t %s: %f" % (p, bestParams[p])
```

    Fitting 3 folds for each of 1080 candidates, totalling 3240 fits


    [Parallel(n_jobs=-1)]: Done  73 tasks      | elapsed:   21.2s
    [Parallel(n_jobs=-1)]: Done 223 tasks      | elapsed:  1.3min
    [Parallel(n_jobs=-1)]: Done 473 tasks      | elapsed:  2.8min
    [Parallel(n_jobs=-1)]: Done 823 tasks      | elapsed:  4.9min
    [Parallel(n_jobs=-1)]: Done 1273 tasks      | elapsed:  7.7min
    [Parallel(n_jobs=-1)]: Done 1823 tasks      | elapsed: 11.1min
    [Parallel(n_jobs=-1)]: Done 2473 tasks      | elapsed: 15.0min
    [Parallel(n_jobs=-1)]: Done 3223 tasks      | elapsed: 19.6min
    [Parallel(n_jobs=-1)]: Done 3240 out of 3240 | elapsed: 19.8min finished


    Best Score: 0.762
    RBM + Logistic Regression parameters
    	 logistic__C: 100.000000
    	 rbm__learning_rate: 0.001000
    	 rbm__n_components: 100.000000
    	 rbm__n_iter: 90.000000



```python
# initialize the RBM + Logistic Regression classifier with
# the cross-validated parameters
rbm = BernoulliRBM(n_components = 200, n_iter = 80, learning_rate = 0.001000,  verbose = False)
logistic = LogisticRegression(C = 100)

# train the classifier and show an evaluation report
classifier = Pipeline([("rbm", rbm), ("logistic", logistic)])
classifier.fit(X_train, y_train)

print metrics.accuracy_score(y_train, classifier.predict(X_train))
print metrics.accuracy_score(y_test, classifier.predict(X_test))
```

    0.7768729641693811
    0.8051948051948052


####  Confusion Matrix


```python
matrix = confusion_matrix(y_test, classifier.predict(X_test))
matrix= pd.DataFrame(matrix,index=['Positive','Negative'],columns=['True Posutive','False Negative'])
matrix
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
      <th>True Posutive</th>
      <th>False Negative</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Positive</th>
      <td>91</td>
      <td>12</td>
    </tr>
    <tr>
      <th>Negative</th>
      <td>18</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>



####  Classification report


```python

report = classification_report(y_test, classifier.predict(X_test))
print(report)



```

                 precision    recall  f1-score   support
    
            0.0       0.83      0.88      0.86       103
            1.0       0.73      0.65      0.69        51
    
    avg / total       0.80      0.81      0.80       154
    


#### Firstfive Actual class VS predicted class


```python
print "\tACTUAL class (1-5) "
print y_test[1:10]
```

    	ACTUAL class (1-5) 
    [1. 1. 1. 1. 0. 0. 0. 0. 0.]



```python
print "\tPREDICTED class( 1-5) "
print classifier.predict(X_test)[1:10]
```

    	PREDICTED class( 1-5) 
    [1. 1. 1. 1. 0. 0. 0. 0. 0.]

