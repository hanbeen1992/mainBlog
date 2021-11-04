---
title: Yfinance_laod
date: 2021-11-04 09:00:00
categories:
- python
- Yfinance
tags:
- python
- Yfinance
---
# 한 종목 주가 데이터 받아오기 (삼성전자)


```python
!pip install yfinance --upgrade --no-cache-dir
#데이터를 다운받음
```


```python
#블로그에 올라온 자료
import pandas as pd
import yfinance as yf # yfinance 를 임포트 한다.

tic = '005930.KS' #삼성전자
df = yf.download(tic, start='2020-01-01', end='2020-12-31',progress=False)
df.info()
#tic에 받고자 하는 종목 정보를 넣는다
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 248 entries, 2020-01-02 to 2020-12-30
    Data columns (total 6 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   Open       248 non-null    float64
     1   High       248 non-null    float64
     2   Low        248 non-null    float64
     3   Close      248 non-null    float64
     4   Adj Close  248 non-null    float64
     5   Volume     248 non-null    int64  
    dtypes: float64(5), int64(1)
    memory usage: 13.6 KB
    


```python
df.head(5) # 5개의 정보를 불러왔다.
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-02</th>
      <td>55500.0</td>
      <td>56000.0</td>
      <td>55000.0</td>
      <td>55200.0</td>
      <td>52058.132812</td>
      <td>12993228</td>
    </tr>
    <tr>
      <th>2020-01-03</th>
      <td>56000.0</td>
      <td>56600.0</td>
      <td>54900.0</td>
      <td>55500.0</td>
      <td>52341.058594</td>
      <td>15422255</td>
    </tr>
    <tr>
      <th>2020-01-06</th>
      <td>54900.0</td>
      <td>55600.0</td>
      <td>54600.0</td>
      <td>55500.0</td>
      <td>52341.058594</td>
      <td>10278951</td>
    </tr>
    <tr>
      <th>2020-01-07</th>
      <td>55700.0</td>
      <td>56400.0</td>
      <td>55600.0</td>
      <td>55800.0</td>
      <td>52623.980469</td>
      <td>10009778</td>
    </tr>
    <tr>
      <th>2020-01-08</th>
      <td>56200.0</td>
      <td>57400.0</td>
      <td>55900.0</td>
      <td>56800.0</td>
      <td>53567.058594</td>
      <td>23501171</td>
    </tr>
  </tbody>
</table>
</div>




```python
#import fix_yahoo_finance as yf
import yfinance as yf
import matplotlib.pyplot as plt

tic = '005930.KS' #삼성전자
df = yf.download(tic, start='2020-01-01', end='2021-11-01',progress=False)
ts1 = df['Open']
fig, ax = plt.subplots(figsize=(10,6))# 직접 Figure 객체 생성
# ax = fig.subplots() # 직접 axes를 생성
ax.plot(ts1) #생성된 axes에 대한 plot() 멤버 직접 호출
ax.set_title('Stock Market fluctuation of Samsung Electronics')
ax.legend(labels=['Price'],loc='best')
ax.set_xlabel('Data')
ax.set_ylabel('Stock Market Open Price')
plt.show()
```

![](/images/yfinance_load/output_4_0.png)

    



```python
# 수업시간에 했던 자료
import yfinance as yf
data = yf.download('AAPL','2019-08-01','2020-08-01')
data.info()
#다운받은 데이터의 정보를 볼러온다. 
```

    [*********************100%***********************]  1 of 1 completed
    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 253 entries, 2019-08-01 to 2020-07-31
    Data columns (total 6 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   Open       253 non-null    float64
     1   High       253 non-null    float64
     2   Low        253 non-null    float64
     3   Close      253 non-null    float64
     4   Adj Close  253 non-null    float64
     5   Volume     253 non-null    int64  
    dtypes: float64(5), int64(1)
    memory usage: 13.8 KB
    
