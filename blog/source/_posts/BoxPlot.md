---
title: boxplot 
date: 2021-11-03 15:00:00
categories:
- python
- boxplot
tags:
- python
- boxplot
---

# 박스플롯이란??
출처 : https://dschloe.github.io/python/python_edu/03_datavisualisation/ch_boxplot/

## 박스플롯 그래프
박스플롯 그래프는 범주형 데이터 기준으로 수치형 데이터의 분포를 파악하는데  적합하다.

박스플롯을 보면 최솟값, 1분위, 중간값, 3분위 값, 최대값을 제공한다.
![boxplot.webp](data:image/webp;base64,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)

### 1)라이브러리 불러오기
필요한 모듈을 불러온다.

### 2)데이터 생성
seaborn 패키지 내 iris 데이터를 활용한다.


```python
import matplotlib.pyplot as plt
import numpy as np 
import seaborn as sns
iris = sns.load_dataset('iris')
iris
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
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 5 columns</p>
</div>




```python
#위 데이터에서 species 변수 내 데이터를 확인해보자.
iris['species'].unique()
```




    array(['setosa', 'versicolor', 'virginica'], dtype=object)



박스플롯으로 그래프를 구현할 때에는 위 3개의 데이터를 List 안에 담아야 한다.


```python
data = [iris[iris['species']=="setosa"]['sepal_length'],
        iris[iris['species']=="versicolor"]['sepal_length'],
        iris[iris['species']=="virginica"]['sepal_length']]
```

### 3) 그래프 구현
각각의 데이터를 기준으로 박스플롯을 작성한다. 데이터의 평균을 표시하는 **showmeans**를 추가해 본다.


```python
plt.boxplot(data, labels=['setosa','versicolor','virginica'],
showmeans = True)
plt.show
```




    <function matplotlib.pyplot.show>



![](/images/BoxPlot/output_9_1.png)

    



```python
이번에는 옵션 vert=False 를 추가한다.
```


```python
plt.boxplot(data, labels=['setosa', 'versicolor', 'virginica'], showmeans=True, vert = False)
plt.show()
```


    
![](/images/BoxPlot/output_11_0.png)
