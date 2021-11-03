---
title: visualization
date: 2021-11-03 11:58:05
tags: phython
---
# visualization
### 객체지향 fig,ax 사용하기(많은 데이터를 처리하기 용이)
### 세가지 방법으로 데이터 시각화 가능

```python
import matplotlib.pyplot as plt

dates = [
    '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05',
    '2021-01-06', '2021-01-07', '2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7, 17.9, 18.8, 14.6, 15.8, 15.8, 15.8, 17.4, 21.8, 20.0]
max_temperature = [34.7, 28.9, 31.8, 25.6, 28.8, 21.8, 22.8, 28.4, 30.8, 32.0]

fig, ax = plt.subplots()
ax.plot(dates, min_temperature, label = "Min Temp")
ax.plot(dates, max_temperature, label = "Max Temp")
ax.legend()
plt.show()
```
plot(x,y)의 x,y는 각각 x축과 y축값이 된다.

    
![output_1_0](/img/output_1_0.png)
    



```python
import matplotlib.pyplot as plt

dates = [
    '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05',
    '2021-01-06', '2021-01-07', '2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7, 17.9, 18.8, 14.6, 15.8, 15.8, 15.8, 17.4, 21.8, 20.0]
max_temperature = [34.7, 28.9, 31.8, 25.6, 28.8, 21.8, 22.8, 28.4, 30.8, 32.0]

fig, axes = plt.subplots(nrows=1, ncols=1, figsize=(10,6))
axes.plot(dates, min_temperature, label = 'Min Temperature')
axes.plot(dates, max_temperature, label = 'Max Temperature')
axes.legend()
plt.show()
```


    
![output_2_0](/img/output_2_0.png)
    



```python
print(fig)
print(axes)
```

    Figure(720x432)
    AxesSubplot(0.125,0.125;0.775x0.755)
    

## Matplotlib

### 선 그래프
- 흐름 변화 확인 용도

#### 방법 1. Pyplot API
- 코드 변경됨
- 참조: https://pypi.org/project/fix-yahoo-finance/


```python
!pip install yfinance --upgrade --no-cache-dir
```
설치
   

```python
import yfinance as yf
data = yf.download('AAPL', '2019-08-01', '2020-08-01')
data.info()
```

```python
ts = data['Open']
print(ts.head())
```


#### 방법 2. 객체지향 API



```python
from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
from matplotlib.figure import Figure
import matplotlib.pyplot as plt

fig = Figure()

import numpy as np
np.random.seed(6)
x = np.random.randn(20000)

ax = fig.add_subplot(111)
ax.hist(x, 100)
ax.set_title('Artist Layer Histogram')
# fig.savefig('Matplotlib_histogram.png')
plt.show()
```

### 방법 3. Pyplot API + 객체지향 API

- ax.set_title("제목")
- ax.set_xlabel("x축 이름")
- ax.set_ylabel("y축 이름")
- as.legend([]) -> 범례

```python
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL','2019-08-01','2020-08-01')
ts = data['Open']

fig, ax=plt.subplots(figsize=(10,6))
ax.plot(ts)
ax.set_title('Stock Market Fluctuation of AAPL')
ax.legend(labels=['Price'], loc='best')
ax.set_xlabel('Date')
ax.set_ylabel('Stock Market Open Price')
plt.show()
```

    [*********************100%***********************]  1 of 1 completed
    


    
![output_15_1](/img/output_15_1.png)
    



```python
# import fix_yahoo_finance as yf
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL', '2019-08-01', '2020-08-01')
ts = data['Open']

fig, ax = plt.subplots(figsize=(10, 6)) # 직접 Figure 객체 생성
# ax= fig.subplots() # 직접 axes를 생성
ax.plot(ts) # 생성된 axes 에 대한 plot() 멤버 직접 호출 
ax.set_title('Stock Market fluctuation of AAPL')
ax.legend(labels=['Price'], loc='best')
ax.set_xlabel('Date')
ax.set_ylabel('Stock Market Open Price')
plt.show()
```

    [*********************100%***********************]  1 of 1 completed
    


    
![output_16_1](/img/output_16_1.png)
    


### 막대 그래프
카테고리 별로 수치 비교 확인용

```python
import matplotlib.pyplot as plt
import numpy as np
import calendar

month_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
sold_list = [300, 400, 550, 900, 600, 960, 900, 910, 800, 700, 550, 450]

fig, ax = plt.subplots(figsize=(10,6))
plt.xticks(month_list, calendar.month_name[1:13], rotation=90)
plot = ax.bar(month_list, sold_list)
for rect in plot:
  print("graph:", rect) 
  height = rect.get_height()
  ax.text(rect.get_x() + rect.get_width()/2., 1.002*height,'%d' % 
  int(height), ha='center', va='bottom')

plt.show()
```
    
![output_18_1](/img/output_18_1.png)
    


### 산점도 그래프
- 두개의 연속형 변수 (키, 몸무게 등)
- 상관관계 != 인과관계
- 산점도 (Scatter plot)는 두 변수의 상관 관계를 직교 좌표계의 평면에 점으로 표현하는 그래프


```python
import matplotlib.pyplot as plt
import seaborn as sns

# 내장 데이터
tips = sns.load_dataset("tips")
x = tips['total_bill']
y = tips['tip']

fig, ax = plt.subplots(figsize=(10, 6))
ax.scatter(x, y)
ax.set_xlabel('Total Bill')
ax.set_ylabel('Tip')
ax.set_title('Tip ~ Total Bill')

fig.show()
```


    
![output_20_0](/img/output_20_0.png)
    



```python
label, data = tips.groupby('sex')
```


```python
tips['sex_color'] = tips['sex'].map({"Female" : "#0000FF", "Male" : "#00FF00"})

fig, ax = plt.subplots(figsize=(10, 6))
for label, data in tips.groupby('sex'):
  ax.scatter(data['total_bill'], data['tip'], label=label, 
             color=data['sex_color'], alpha=0.5)
  ax.set_xlabel('Total Bill')
  ax.set_ylabel('Tip')
  ax.set_title('Tip ~ Total Bill by Gender')

ax.legend()
fig.show()
```


    
![output_22_0](/img/output_22_0.png)
    


### 히스토그램
- 수치형 변수 1개
- 막대그래프와 비슷하지만 구간 지정 그래프화


```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

# 내장 데이터 
titanic = sns.load_dataset('titanic')
age = titanic['age']

nbins = 21
fig, ax = plt.subplots(figsize=(10, 6))
ax.hist(age, bins = nbins)
ax.set_xlabel("Age")
ax.set_ylabel("Frequency")
ax.set_title("Distribution of Aae in Titanic")
ax.axvline(x = age.mean(), linewidth = 2, color = 'r')
fig.show()
```


    
![output_24_0](/img/output_24_0.png)
    


### 박스플롯
- x축 변수: 범주형 변수, 그룹과 관련있는 변수, 문자열
- y축 변수: 수치형 변수 
- 박스형태로 그래프화 하여 최소,최대 구간을 표시하여 박스크기와 위치에 따라 데이터를 분석가능

```python
import matplotlib.pyplot as plt
import seaborn as sns

iris = sns.load_dataset('iris')

data = [iris[iris['species']=="setosa"]['petal_width'], 
        iris[iris['species']=="versicolor"]['petal_width'],
        iris[iris['species']=="virginica"]['petal_width']]

fig, ax = plt.subplots(figsize=(10, 6))
ax.boxplot(data, labels=['setosa', 'versicolor', 'virginica'])

fig.show()
```


    
![output_26_0](/img/output_26_0.png)
    


### 히트맵

```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

# 내장 데이터
flights = sns.load_dataset("flights")
flights = flights.pivot("month", "year", "passengers")

fig, ax = plt.subplots(figsize=(12, 6))
im = ax.imshow(flights, cmap = 'YlGnBu')
ax.set_xticklabels(flights.columns, rotation = 20)
ax.set_yticklabels(flights.index, rotation = 10)
fig.colorbar(im)

fig.show()
```
    
![output_28_1](/img/output_28_1.png)
    


## Seaborn

### 산점도와 회귀선이 있는 산점도
- seaborn 참고 url:https://jjeongil.tistory.com/775

```python
%matplotlib inline 

import matplotlib.pyplot as plt
import seaborn as sns

tips = sns.load_dataset("tips")
sns.scatterplot(x = "total_bill", y = "tip", data = tips)
plt.show()
```


    
![output_31_0](/img/output_31_0.png)
    



```python
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(15, 5))
sns.regplot(x = "total_bill", 
            y = "tip", 
            data = tips, 
            ax = ax[0], 
            fit_reg = True)

sns.regplot(x = "total_bill", 
            y = "tip", 
            data = tips, 
            ax = ax[1], 
            fit_reg = False)

plt.show()
```


    
![output_32_0](/img/output_32_0.png)
    


### 히스토그램/커널 밀도 그래프



```python
import matplotlib.pyplot as plt
import seaborn as sns

tips = sns.load_dataset("tips")

sns.displot(x = "tip", data = tips)
plt.figure(figsize=(10, 6))
plt.show()
```


    
![output_34_0](/img/output_34_0.png)
    



    <Figure size 720x432 with 0 Axes>



```python
sns.displot(x="tip", kind="kde", data=tips)
plt.show()
```


    
![output_35_0](/img/output_35_0.png)
    



```python
sns.displot(x="tip", kde=True, data=tips)
plt.show()
```


    
![output_36_0](/img/output_36_0.png)
    


### 박스플롯


```python
sns.boxplot(x = "day", y = "total_bill", data = tips)
sns.swarmplot(x = "day", y = "total_bill", data = tips, alpha = .25)
plt.show()
```


    
![output_38_0](/img/output_38_0.png)
    


### 막대 그래프


```python
sns.countplot(x = "day", data = tips)
plt.show()
```


    
![output_40_0](/img/output_40_0.png)
    



```python
print(tips['day'].value_counts())
print("index: ", tips['day'].value_counts().index)
print("values: ", tips['day'].value_counts().values)
```

    Sat     87
    Sun     76
    Thur    62
    Fri     19
    Name: day, dtype: int64
    index:  CategoricalIndex(['Sat', 'Sun', 'Thur', 'Fri'], categories=['Thur', 'Fri', 'Sat', 'Sun'], ordered=False, dtype='category')
    values:  [87 76 62 19]
    


```python
print(tips['day'].value_counts(ascending=True))
```

    Fri     19
    Thur    62
    Sun     76
    Sat     87
    Name: day, dtype: int64
    


```python
plt.show()
```


```python
ax = sns.countplot(x = "day", data = tips, order = tips['day'].value_counts().index)
for p in ax.patches:
  height = p.get_height()
  ax.text(p.get_x() + p.get_width()/2., height+3, height, ha = 'center', size=9)
ax.set_ylim(-5, 100)
plt.show()
```


    
![output_44_0](/img/output_44_0.png)
    



```python
ax = sns.countplot(x = "day", data = tips, hue = "sex", dodge = True,
              order = tips['day'].value_counts().index)
for p in ax.patches:
  height = p.get_height()
  ax.text(p.get_x() + p.get_width()/2., height+3, height, ha = 'center', size=9)
ax.set_ylim(-5, 100)

plt.show()
```


    
![output_45_0](/img/output_45_0.png)
    


### 상관관계 그래프


```python
import pandas as pd 
import numpy as np 
import seaborn as sns
import matplotlib.pyplot as plt

mpg = sns.load_dataset("mpg")
print(mpg.shape) # 398 행, 9개 열

num_mpg = mpg.select_dtypes(include = np.number)
print(num_mpg.shape) # 398 행, 7개 열
```

    (398, 9)
    (398, 7)
    


```python
num_mpg.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 398 entries, 0 to 397
    Data columns (total 7 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   mpg           398 non-null    float64
     1   cylinders     398 non-null    int64  
     2   displacement  398 non-null    float64
     3   horsepower    392 non-null    float64
     4   weight        398 non-null    int64  
     5   acceleration  398 non-null    float64
     6   model_year    398 non-null    int64  
    dtypes: float64(4), int64(3)
    memory usage: 21.9 KB
    


```python
num_mpg.corr()
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mpg</th>
      <td>1.000000</td>
      <td>-0.775396</td>
      <td>-0.804203</td>
      <td>-0.778427</td>
      <td>-0.831741</td>
      <td>0.420289</td>
      <td>0.579267</td>
    </tr>
    <tr>
      <th>cylinders</th>
      <td>-0.775396</td>
      <td>1.000000</td>
      <td>0.950721</td>
      <td>0.842983</td>
      <td>0.896017</td>
      <td>-0.505419</td>
      <td>-0.348746</td>
    </tr>
    <tr>
      <th>displacement</th>
      <td>-0.804203</td>
      <td>0.950721</td>
      <td>1.000000</td>
      <td>0.897257</td>
      <td>0.932824</td>
      <td>-0.543684</td>
      <td>-0.370164</td>
    </tr>
    <tr>
      <th>horsepower</th>
      <td>-0.778427</td>
      <td>0.842983</td>
      <td>0.897257</td>
      <td>1.000000</td>
      <td>0.864538</td>
      <td>-0.689196</td>
      <td>-0.416361</td>
    </tr>
    <tr>
      <th>weight</th>
      <td>-0.831741</td>
      <td>0.896017</td>
      <td>0.932824</td>
      <td>0.864538</td>
      <td>1.000000</td>
      <td>-0.417457</td>
      <td>-0.306564</td>
    </tr>
    <tr>
      <th>acceleration</th>
      <td>0.420289</td>
      <td>-0.505419</td>
      <td>-0.543684</td>
      <td>-0.689196</td>
      <td>-0.417457</td>
      <td>1.000000</td>
      <td>0.288137</td>
    </tr>
    <tr>
      <th>model_year</th>
      <td>0.579267</td>
      <td>-0.348746</td>
      <td>-0.370164</td>
      <td>-0.416361</td>
      <td>-0.306564</td>
      <td>0.288137</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

#  기본 그래프 [Basic Correlation Heatmap]
sns.heatmap(num_mpg.corr(), ax=ax[0])
ax[0].set_title('Basic Correlation Heatmap', pad = 12)

# 상관관계 수치 그래프 [Correlation Heatmap with Number]
sns.heatmap(num_mpg.corr(), vmin=-1, vmax=1, annot=True, ax=ax[1])
ax[1].set_title('Correlation Heatmap with Number', pad = 12)

plt.show()
```


    
![output_50_0](/img/output_50_0.png)
    



```python
print(int(True))
np.triu(np.ones_like(num_mpg.corr()))
```

    1
    




    array([[1., 1., 1., 1., 1., 1., 1.],
           [0., 1., 1., 1., 1., 1., 1.],
           [0., 0., 1., 1., 1., 1., 1.],
           [0., 0., 0., 1., 1., 1., 1.],
           [0., 0., 0., 0., 1., 1., 1.],
           [0., 0., 0., 0., 0., 1., 1.],
           [0., 0., 0., 0., 0., 0., 1.]])




```python
mask = np.triu(np.ones_like(num_mpg.corr(), dtype=np.bool))
print(mask)
```

    [[ True  True  True  True  True  True  True]
     [False  True  True  True  True  True  True]
     [False False  True  True  True  True  True]
     [False False False  True  True  True  True]
     [False False False False  True  True  True]
     [False False False False False  True  True]
     [False False False False False False  True]]
    


```python
fig, ax = plt.subplots(figsize=(16, 5))

#  기본 그래프 [Basic Correlation Heatmap]
ax = sns.heatmap(num_mpg.corr(), mask=mask, 
                 vmin=-1, vmax = 1, 
                 annot=True, 
                 cmap="BrBG", cbar = True)
ax.set_title('Triangle Correlation Heatmap', pad = 16, size = 16)
fig.show()
```


    
![output_53_0](/img/output_53_0.png)
    

## Intermediate

### 페가블로그 코드
- https://jehyunlee.github.io/2020/08/27/Python-DS-28-mpl_spines_grids/

