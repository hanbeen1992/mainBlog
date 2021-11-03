# python Visualization

# Matplotlib
<li>matplotlib.pyplot / 각 pyplot()함수는 figure를 변형시킨다. 예를들어 figure생성, figure에 플롯 영역 생성, 플롯영역에 일부 선그리기, 레이블로 플롯 꾸미기 등이 있다.</li>
<li>pyplot는 시각화를 매우 빠르게 만들 수있다.</li>


```python
import matplotlib.pyplot as plt

dates = [
         '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05'
         ,'2021-01-06', '2021-01-07' ,'2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7,17.9,18.8,14.6,15.8,15.8,15.8,17.4,21.8,20.0]
max_temperature = [34.7,28.9,31.8,25.6,28.8,21.8,22.8,28.4,30.8,32.0]

fig, ax = plt.subplots()
ax. plot(dates, min_temperature, label = 'Min Temp')
ax. plot(dates, max_temperature, label = 'Max Temp')
ax.legend()
plt.show



```




    <function matplotlib.pyplot.show>




    
![png](output_2_1.png)
    


## 선 그래프


```python
!pip install yfinance --upgrade --no-cache-dir
#데이터를 다운받음
```


```python
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
    


```python
ts = data['Open']
print(ts.head())
```

    Date
    2019-08-01    53.474998
    2019-08-02    51.382500
    2019-08-05    49.497501
    2019-08-06    49.077499
    2019-08-07    48.852501
    Name: Open, dtype: float64
    

##  PyPlot API + 객체지향 API


```python
#import fix_yahoo_finance as yf
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL','2019-08-01','2020-08-01')
ts = data['Open']
fig, ax = plt.subplots(figsize=(10,6))# 직접 Figure 객체 생성
# ax = fig.subplots() # 직접 axes를 생성
ax.plot(ts) #생성된 axes에 대한 plot() 멤버 직접 호출
ax.set_title('Stock Market fluctuation of AAPL')
ax.legend(labels=['Price'],loc='best')
ax.set_xlabel('Data')
ax.set_ylabel('Stock Market Open Price')
plt.show()
```

    [*********************100%***********************]  1 of 1 completed
    


    
![png](output_8_1.png)
    


### 막대그래프


```python
import matplotlib.pyplot as plt 
import numpy as np #Numpy
import calendar #해당월 의 달력 출력하기

month_list = [1,2,3,4,5,6,7,8,9,10,11,12]
sold_list = [300,400,550,900,600,960,900,910,800,700,550,450]

fig, ax = plt.subplots(figsize=(10,6))
# fig = figure : 데이터가 담기는 프레임, 크기, 모양을 변형할수 있지만 실제로 프레임 위에 글씨를 쓸수 없다. 즉 여러 그래프가 담길 수 있는 액자 같은 역활을 한다.
# ax = axes : 실제 데이터가 그려지는 캔버스. 그렇기에 모든 plot은 axes위에서 이루어져야 하는 것이다.
plt.xticks(month_list, calendar.month_name[1:13], rotation=90)
plot = ax.bar(month_list, sold_list)
for rect in plot:
  print("graph : ",rect)
  height = rect.get_height()
  ax.text(rect.get_x() + rect.get_width()/2.,1.002*height,'%d' % int(height), ha='center', va='bottom')
  
  plt.show


```

    graph :  Rectangle(xy=(0.6, 0), width=0.8, height=300, angle=0)
    graph :  Rectangle(xy=(1.6, 0), width=0.8, height=400, angle=0)
    graph :  Rectangle(xy=(2.6, 0), width=0.8, height=550, angle=0)
    graph :  Rectangle(xy=(3.6, 0), width=0.8, height=900, angle=0)
    graph :  Rectangle(xy=(4.6, 0), width=0.8, height=600, angle=0)
    graph :  Rectangle(xy=(5.6, 0), width=0.8, height=960, angle=0)
    graph :  Rectangle(xy=(6.6, 0), width=0.8, height=900, angle=0)
    graph :  Rectangle(xy=(7.6, 0), width=0.8, height=910, angle=0)
    graph :  Rectangle(xy=(8.6, 0), width=0.8, height=800, angle=0)
    graph :  Rectangle(xy=(9.6, 0), width=0.8, height=700, angle=0)
    graph :  Rectangle(xy=(10.6, 0), width=0.8, height=550, angle=0)
    graph :  Rectangle(xy=(11.6, 0), width=0.8, height=450, angle=0)
    


    
![png](output_10_1.png)
    

