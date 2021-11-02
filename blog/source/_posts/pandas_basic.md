---
title : python pandas 정리
date : 21-11-01-15:00
tags  : python
categories  : python
---

판다스는 파이썬에서 데이터 처리를 위해 존재하는 가장 인기 있는 라이브러리이다. 일반적으로 대부분의 데이터 세트는 <strong>2차원 데이터</strong>입니다. **행(Row)** X **열(column)**로 구성되어 있다.

판다스의 핵심객체는 DataFrame.
여러 개의 행가 열로 이뤄진 2차원 데이터를  담는 데이터 구조체이다.

라이브러리 불러오기


```python
import pandas as pd
print(pd.__version__)
```

    1.1.5
    

테스트


```python
df = pd.DataFrame({'col1':[1,2],'col2': [3,4]})
print(type(df))
```

    <class 'pandas.core.frame.DataFrame'>
    

구글 드라이브 연동


```python
from google.colab import drive
drive.mount('/content/drive')
```

    Mounted at /content/drive
    


```python
# DATA_PATH = '경로를 입력하세요'
# 경로는 다음과 같이 설정한다.
DATA_PATH = '/content/drive/MyDrive/Colab Notebooks/lectures_210923/PART_I_Intro/data/Lemonade2016.csv'
lemonade = pd.read_csv(DATA_PATH)
lemonade.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 32 entries, 0 to 31
    Data columns (total 7 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   Date         31 non-null     object 
     1   Location     32 non-null     object 
     2   Lemon        32 non-null     int64  
     3   Orange       32 non-null     int64  
     4   Temperature  32 non-null     int64  
     5   Leaflets     31 non-null     float64
     6   Price        32 non-null     float64
    dtypes: float64(2), int64(3), object(2)
    memory usage: 1.9+ KB
    

# 데이터 불러오기


```python
lemonade.head(5)
#앞에서부터 5개의 데이터 값을 불러온다
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
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
lemonade.tail(3)
#뒤에서부터 3개의 데이터 값을 불러온다
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
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>7/29/2016</td>
      <td>Park</td>
      <td>100</td>
      <td>66</td>
      <td>81</td>
      <td>95.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7/30/2016</td>
      <td>Beach</td>
      <td>88</td>
      <td>57</td>
      <td>82</td>
      <td>81.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/31/2016</td>
      <td>Beach</td>
      <td>76</td>
      <td>47</td>
      <td>82</td>
      <td>68.0</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(lemonade.info())
#데이터 정보를 출력한다.
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 32 entries, 0 to 31
    Data columns (total 7 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   Date         31 non-null     object 
     1   Location     32 non-null     object 
     2   Lemon        32 non-null     int64  
     3   Orange       32 non-null     int64  
     4   Temperature  32 non-null     int64  
     5   Leaflets     31 non-null     float64
     6   Price        32 non-null     float64
    dtypes: float64(2), int64(3), object(2)
    memory usage: 1.9+ KB
    None
    


```python
lemonade.describe()
# describe() 함수를 사용하면 수치형 변수만을 기준으로 카운트, 평균, 표준편차, 최소/최대값, 4분의 수를 기준으로 25%, 50%, 75% 에 해당하는 값들을 테이블로 출력한다.
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
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>31.000000</td>
      <td>32.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>116.156250</td>
      <td>80.000000</td>
      <td>78.968750</td>
      <td>108.548387</td>
      <td>0.354687</td>
    </tr>
    <tr>
      <th>std</th>
      <td>25.823357</td>
      <td>21.863211</td>
      <td>4.067847</td>
      <td>20.117718</td>
      <td>0.113137</td>
    </tr>
    <tr>
      <th>min</th>
      <td>71.000000</td>
      <td>42.000000</td>
      <td>70.000000</td>
      <td>68.000000</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>98.000000</td>
      <td>66.750000</td>
      <td>77.000000</td>
      <td>90.000000</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>113.500000</td>
      <td>76.500000</td>
      <td>80.500000</td>
      <td>108.000000</td>
      <td>0.350000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>131.750000</td>
      <td>95.000000</td>
      <td>82.000000</td>
      <td>124.000000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>176.000000</td>
      <td>129.000000</td>
      <td>84.000000</td>
      <td>158.000000</td>
      <td>0.500000</td>
    </tr>
  </tbody>
</table>
</div>



<li>count</li>
행 내에 null(빈값, numpy의 NaN과 같은 취급)이 아닌 row의 개수를 센다. 
<li>mean</li>
모든 row에 있어 각 colum들의 값에 대한 평균값을 나타낸다. null값은 아예 없는 값으로 취급하여 분모에 들어가지 않는다. 즉 sum(모든 row의 값)/count 가 된다고 생각하면 된다.
<li>std</li>
해당 column들의 값을에 대한 표준편차를 나타낸다. 역시 null값은 없는 값으로 취급한다.
<li>min, 25%, 50%, 75%, max</li>
해당 column들의 값 중 최솟값, 사분위수, 최대값을 의미한다.


```python
lemonade['Location'].value_counts()
해당열의 정보 갯수를 나타낸다.
```




    Beach    17
    Park     15
    Name: Location, dtype: int64



# 데이터 다뤄보기


```python
lemonade['Sold'] = 0
print(lemonade.head(3))
#데이터에 sold 행을 추가함
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  sold  Sold
    0  7/1/2016     Park     97      67           70      90.0   0.25     0     0
    1  7/2/2016     Park     98      67           72      90.0   0.25     0     0
    2  7/3/2016     Park    110      77           71     104.0   0.25     0     0
    


```python
lemonade['Sold'] = lemonade['Lemon'] + lemonade['Orange']
print(lemonade.head(3))
# sold 행에 데이터 값을 지정함. (레몬과 오렌지 값을 더한 값)
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  sold  Sold
    0  7/1/2016     Park     97      67           70      90.0   0.25     0   164
    1  7/2/2016     Park     98      67           72      90.0   0.25     0   165
    2  7/3/2016     Park    110      77           71     104.0   0.25     0   187
    


```python
lemonade['Revenue'] = lemonade['Price'] * lemonade['Sold']
print(lemonade.head(3))
# 새 행을 추가함과 동시에 값을 지정해줌.
```

           Date Location  Lemon  Orange  ...  Price  sold  Sold  Revenue
    0  7/1/2016     Park     97      67  ...   0.25     0   164    41.00
    1  7/2/2016     Park     98      67  ...   0.25     0   165    41.25
    2  7/3/2016     Park    110      77  ...   0.25     0   187    46.75
    
    [3 rows x 10 columns]
    


```python
pd.set_option('display.max_columns', None)

lemonade['Revenue'] = lemonade['Price'] * lemonade['Sold']
print(lemonade.head(3))

```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  sold  Sold  \
    0  7/1/2016     Park     97      67           70      90.0   0.25     0   164   
    1  7/2/2016     Park     98      67           72      90.0   0.25     0   165   
    2  7/3/2016     Park    110      77           71     104.0   0.25     0   187   
    
       Revenue  
    0    41.00  
    1    41.25  
    2    46.75  
    


```python
pd.set_option('display.max_columns', 0)

lemonade['Revenue'] = lemonade['Price'] * lemonade['Sold']
print(lemonade.head(3))
```

           Date Location  Lemon  Orange  ...  Price  sold  Sold  Revenue
    0  7/1/2016     Park     97      67  ...   0.25     0   164    41.00
    1  7/2/2016     Park     98      67  ...   0.25     0   165    41.25
    2  7/3/2016     Park    110      77  ...   0.25     0   187    46.75
    
    [3 rows x 10 columns]
    


```python
lemonade_column_drop = lemonade.drop('Sold', axis=1)
print(lemonade_column_drop.head(3))
```

           Date Location  Lemon  Orange  ...  Leaflets  Price  sold  Revenue
    0  7/1/2016     Park     97      67  ...      90.0   0.25     0    41.00
    1  7/2/2016     Park     98      67  ...      90.0   0.25     0    41.25
    2  7/3/2016     Park    110      77  ...     104.0   0.25     0    46.75
    
    [3 rows x 9 columns]
    


```python
lemonade_row_drop = lemonade_column_drop.drop(0, axis=0)
print(lemonade_row_drop.head(3))
```

           Date Location  Lemon  Orange  ...  Leaflets  Price  sold  Revenue
    1  7/2/2016     Park     98      67  ...      90.0   0.25     0    41.25
    2  7/3/2016     Park    110      77  ...     104.0   0.25     0    46.75
    3  7/4/2016    Beach    134      99  ...      98.0   0.25     0    58.25
    
    [3 rows x 9 columns]
    

# 데이터 인덱싱


```python
print(lemonade[0:5])
# 0부터 5개의 값을 가져옴
```

           Date Location  Lemon  Orange  ...  Price  sold  Sold  Revenue
    0  7/1/2016     Park     97      67  ...   0.25     0   164    41.00
    1  7/2/2016     Park     98      67  ...   0.25     0   165    41.25
    2  7/3/2016     Park    110      77  ...   0.25     0   187    46.75
    3  7/4/2016    Beach    134      99  ...   0.25     0   233    58.25
    4  7/5/2016    Beach    159     118  ...   0.25     0   277    69.25
    
    [5 rows x 10 columns]
    


```python
lemonade['Location'] == 'Beach'
```




    0     False
    1     False
    2     False
    3      True
    4      True
    5      True
    6      True
    7      True
    8      True
    9      True
    10     True
    11     True
    12     True
    13     True
    14     True
    15     True
    16     True
    17     True
    18    False
    19    False
    20    False
    21    False
    22    False
    23    False
    24    False
    25    False
    26    False
    27    False
    28    False
    29    False
    30     True
    31     True
    Name: Location, dtype: bool




```python
print(lemonade[lemonade['Location']=='Beach'].head(3)) 
# Beach인 데이터를 앞에서 3개 출력한다.
```

           Date Location  Lemon  Orange  ...  Price  sold  Sold  Revenue
    3  7/4/2016    Beach    134      99  ...   0.25     0   233    58.25
    4  7/5/2016    Beach    159     118  ...   0.25     0   277    69.25
    5  7/6/2016    Beach    103      69  ...   0.25     0   172    43.00
    
    [3 rows x 10 columns]
    


```python
print(lemonade.iloc[0:3,0:2])
# 0 부터 3개의 열 / 0부터 2개의 행을 출력한다
```

           Date Location
    0  7/1/2016     Park
    1  7/2/2016     Park
    2  7/3/2016     Park
    


```python
print(lemonade.loc[0:2,['Date','Location']])
# 0부터 2개의 열 / date와 location 의 값을 출력한다.
```

           Date Location
    0  7/1/2016     Park
    1  7/2/2016     Park
    2  7/3/2016     Park
    

# 기본 데이터 전처리


```python
print(lemonade.sort_values(by=['Temperature']).head(5))
```

             Date Location  Lemon  Orange  ...  Price  sold  Sold  Revenue
    0    7/1/2016     Park     97      67  ...   0.25     0   164    41.00
    20  7/20/2016     Park     71      42  ...   0.50     0   113    56.50
    2    7/3/2016     Park    110      77  ...   0.25     0   187    46.75
    1    7/2/2016     Park     98      67  ...   0.25     0   165    41.25
    16  7/16/2016    Beach     81      50  ...   0.50     0   131    65.50
    
    [5 rows x 10 columns]
    


```python
lemonade.sort_values(by=['Temperature','Revenue'], ascending = False, inplace = True)
print(lemonade.loc[:,['Date','Temperature','Revenue']].head(5))
```

             Date  Temperature  Revenue
    25  7/25/2016           84   134.50
    12  7/12/2016           84    56.25
    26  7/26/2016           83   106.75
    11  7/11/2016           83    70.50
    24  7/24/2016           82   101.50
    


```python
print(lemonade.groupby(by='Location').count())
```

              Date  Lemon  Orange  Temperature  ...  Price  sold  Sold  Revenue
    Location                                    ...                            
    Beach       16     17      17           17  ...     17    17    17       17
    Park        15     15      15           15  ...     15    15    15       15
    
    [2 rows x 9 columns]
    


```python
print(lemonade.groupby('Location')['Revenue'].agg([max,min]))
```

                max   min
    Location             
    Beach      95.5  43.0
    Park      134.5  41.0
    


```python
print(lemonade.groupby('Location')[['Revenue','Sold']].agg([max,min]))
```

             Revenue       Sold     
                 max   min  max  min
    Location                        
    Beach       95.5  43.0  282  123
    Park       134.5  41.0  305  113
    
