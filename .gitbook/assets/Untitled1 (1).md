```python
import numpy as np
import pandas as pd
```


```python
import os
print("Current Directory: {0:s}".format(os.getcwd()))
```

    Current Directory: C:\Users\User
    


```python
train = pd.read_csv('train.csv')
```


```python
train.tail()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1455</th>
      <td>1456</td>
      <td>60</td>
      <td>RL</td>
      <td>62.0</td>
      <td>7917</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>8</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>175000</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>1457</td>
      <td>20</td>
      <td>RL</td>
      <td>85.0</td>
      <td>13175</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>210000</td>
    </tr>
    <tr>
      <th>1457</th>
      <td>1458</td>
      <td>70</td>
      <td>RL</td>
      <td>66.0</td>
      <td>9042</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>GdPrv</td>
      <td>Shed</td>
      <td>2500</td>
      <td>5</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>266500</td>
    </tr>
    <tr>
      <th>1458</th>
      <td>1459</td>
      <td>20</td>
      <td>RL</td>
      <td>68.0</td>
      <td>9717</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>4</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>142125</td>
    </tr>
    <tr>
      <th>1459</th>
      <td>1460</td>
      <td>20</td>
      <td>RL</td>
      <td>75.0</td>
      <td>9937</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>147500</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 81 columns</p>
</div>




```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1460 entries, 0 to 1459
    Data columns (total 81 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   Id             1460 non-null   int64  
     1   MSSubClass     1460 non-null   int64  
     2   MSZoning       1460 non-null   object 
     3   LotFrontage    1201 non-null   float64
     4   LotArea        1460 non-null   int64  
     5   Street         1460 non-null   object 
     6   Alley          91 non-null     object 
     7   LotShape       1460 non-null   object 
     8   LandContour    1460 non-null   object 
     9   Utilities      1460 non-null   object 
     10  LotConfig      1460 non-null   object 
     11  LandSlope      1460 non-null   object 
     12  Neighborhood   1460 non-null   object 
     13  Condition1     1460 non-null   object 
     14  Condition2     1460 non-null   object 
     15  BldgType       1460 non-null   object 
     16  HouseStyle     1460 non-null   object 
     17  OverallQual    1460 non-null   int64  
     18  OverallCond    1460 non-null   int64  
     19  YearBuilt      1460 non-null   int64  
     20  YearRemodAdd   1460 non-null   int64  
     21  RoofStyle      1460 non-null   object 
     22  RoofMatl       1460 non-null   object 
     23  Exterior1st    1460 non-null   object 
     24  Exterior2nd    1460 non-null   object 
     25  MasVnrType     1452 non-null   object 
     26  MasVnrArea     1452 non-null   float64
     27  ExterQual      1460 non-null   object 
     28  ExterCond      1460 non-null   object 
     29  Foundation     1460 non-null   object 
     30  BsmtQual       1423 non-null   object 
     31  BsmtCond       1423 non-null   object 
     32  BsmtExposure   1422 non-null   object 
     33  BsmtFinType1   1423 non-null   object 
     34  BsmtFinSF1     1460 non-null   int64  
     35  BsmtFinType2   1422 non-null   object 
     36  BsmtFinSF2     1460 non-null   int64  
     37  BsmtUnfSF      1460 non-null   int64  
     38  TotalBsmtSF    1460 non-null   int64  
     39  Heating        1460 non-null   object 
     40  HeatingQC      1460 non-null   object 
     41  CentralAir     1460 non-null   object 
     42  Electrical     1459 non-null   object 
     43  1stFlrSF       1460 non-null   int64  
     44  2ndFlrSF       1460 non-null   int64  
     45  LowQualFinSF   1460 non-null   int64  
     46  GrLivArea      1460 non-null   int64  
     47  BsmtFullBath   1460 non-null   int64  
     48  BsmtHalfBath   1460 non-null   int64  
     49  FullBath       1460 non-null   int64  
     50  HalfBath       1460 non-null   int64  
     51  BedroomAbvGr   1460 non-null   int64  
     52  KitchenAbvGr   1460 non-null   int64  
     53  KitchenQual    1460 non-null   object 
     54  TotRmsAbvGrd   1460 non-null   int64  
     55  Functional     1460 non-null   object 
     56  Fireplaces     1460 non-null   int64  
     57  FireplaceQu    770 non-null    object 
     58  GarageType     1379 non-null   object 
     59  GarageYrBlt    1379 non-null   float64
     60  GarageFinish   1379 non-null   object 
     61  GarageCars     1460 non-null   int64  
     62  GarageArea     1460 non-null   int64  
     63  GarageQual     1379 non-null   object 
     64  GarageCond     1379 non-null   object 
     65  PavedDrive     1460 non-null   object 
     66  WoodDeckSF     1460 non-null   int64  
     67  OpenPorchSF    1460 non-null   int64  
     68  EnclosedPorch  1460 non-null   int64  
     69  3SsnPorch      1460 non-null   int64  
     70  ScreenPorch    1460 non-null   int64  
     71  PoolArea       1460 non-null   int64  
     72  PoolQC         7 non-null      object 
     73  Fence          281 non-null    object 
     74  MiscFeature    54 non-null     object 
     75  MiscVal        1460 non-null   int64  
     76  MoSold         1460 non-null   int64  
     77  YrSold         1460 non-null   int64  
     78  SaleType       1460 non-null   object 
     79  SaleCondition  1460 non-null   object 
     80  SalePrice      1460 non-null   int64  
    dtypes: float64(3), int64(35), object(43)
    memory usage: 924.0+ KB
    


```python
train.shape
```




    (1460, 81)




```python
train['SaleCondition'].dtype
```




    dtype('O')




```python
import matplotlib.pyplot as plt
```


```python
pip install matplot
```

    Note: you may need to restart the kernel to use updated packages.Collecting matplot
      Downloading matplot-0.1.9-py2.py3-none-any.whl (5.0 kB)
    Collecting matplotlib>=3.1.1
      Downloading matplotlib-3.6.1-cp39-cp39-win_amd64.whl (7.2 MB)
         ---------------------------------------- 7.2/7.2 MB 5.2 MB/s eta 0:00:00
    Collecting pyloco>=0.0.134
      Downloading pyloco-0.0.139-py2.py3-none-any.whl (60 kB)
         ---------------------------------------- 60.2/60.2 kB ? eta 0:00:00
    Requirement already satisfied: python-dateutil>=2.7 in c:\python39\lib\site-packages (from matplotlib>=3.1.1->matplot) (2.8.2)
    Collecting cycler>=0.10
      Downloading cycler-0.11.0-py3-none-any.whl (6.4 kB)
    Collecting kiwisolver>=1.0.1
      Downloading kiwisolver-1.4.4-cp39-cp39-win_amd64.whl (55 kB)
         ---------------------------------------- 55.4/55.4 kB 3.0 MB/s eta 0:00:00
    Requirement already satisfied: numpy>=1.19 in c:\python39\lib\site-packages (from matplotlib>=3.1.1->matplot) (1.23.2)
    Collecting fonttools>=4.22.0
      Downloading fonttools-4.37.4-py3-none-any.whl (960 kB)
         -------------------------------------- 960.8/960.8 kB 6.7 MB/s eta 0:00:00
    Requirement already satisfied: pillow>=6.2.0 in c:\python39\lib\site-packages (from matplotlib>=3.1.1->matplot) (9.2.0)
    Requirement already satisfied: pyparsing>=2.2.1 in c:\python39\lib\site-packages (from matplotlib>=3.1.1->matplot) (3.0.9)
    Collecting contourpy>=1.0.1
      Downloading contourpy-1.0.5-cp39-cp39-win_amd64.whl (161 kB)
         -------------------------------------- 162.0/162.0 kB 9.5 MB/s eta 0:00:00
    Requirement already satisfied: packaging>=20.0 in c:\python39\lib\site-packages (from matplotlib>=3.1.1->matplot) (21.3)
    Collecting twine
      Downloading twine-4.0.1-py3-none-any.whl (36 kB)
    Collecting websocket-client
      Downloading websocket_client-1.4.1-py3-none-any.whl (55 kB)
         ---------------------------------------- 55.0/55.0 kB 3.0 MB/s eta 0:00:00
    Collecting SimpleWebSocketServer
      Downloading SimpleWebSocketServer-0.1.2.tar.gz (10 kB)
      Preparing metadata (setup.py): started
      Preparing metadata (setup.py): finished with status 'done'
    Collecting ushlex
      Downloading ushlex-0.99.1.tar.gz (4.7 kB)
      Preparing metadata (setup.py): started
      Preparing metadata (setup.py): finished with status 'done'
    Collecting typing
      Downloading typing-3.7.4.3.tar.gz (78 kB)
         ---------------------------------------- 78.6/78.6 kB 4.3 MB/s eta 0:00:00
      Preparing metadata (setup.py): started
      Preparing metadata (setup.py): finished with status 'done'
    Requirement already satisfied: six>=1.5 in c:\python39\lib\site-packages (from python-dateutil>=2.7->matplotlib>=3.1.1->matplot) (1.16.0)
    Collecting rich>=12.0.0
      Downloading rich-12.6.0-py3-none-any.whl (237 kB)
         -------------------------------------- 237.5/237.5 kB 3.7 MB/s eta 0:00:00
    Collecting requests-toolbelt!=0.9.0,>=0.8.0
      Downloading requests_toolbelt-0.10.0-py2.py3-none-any.whl (54 kB)
         ---------------------------------------- 54.4/54.4 kB 2.8 MB/s eta 0:00:00
    Collecting readme-renderer>=35.0
      Downloading readme_renderer-37.2-py3-none-any.whl (14 kB)
    Requirement already satisfied: requests>=2.20 in c:\python39\lib\site-packages (from twine->pyloco>=0.0.134->matplot) (2.28.1)
    Collecting pkginfo>=1.8.1
      Downloading pkginfo-1.8.3-py2.py3-none-any.whl (26 kB)
    Collecting keyring>=15.1
      Downloading keyring-23.9.3-py3-none-any.whl (35 kB)
    Collecting rfc3986>=1.4.0
      Downloading rfc3986-2.0.0-py2.py3-none-any.whl (31 kB)
    Requirement already satisfied: importlib-metadata>=3.6 in c:\python39\lib\site-packages (from twine->pyloco>=0.0.134->matplot) (4.12.0)
    Requirement already satisfied: urllib3>=1.26.0 in c:\python39\lib\site-packages (from twine->pyloco>=0.0.134->matplot) (1.26.12)
    Requirement already satisfied: zipp>=0.5 in c:\python39\lib\site-packages (from importlib-metadata>=3.6->twine->pyloco>=0.0.134->matplot) (3.8.1)
    Collecting pywin32-ctypes!=0.1.0,!=0.1.1
      Downloading pywin32_ctypes-0.2.0-py2.py3-none-any.whl (28 kB)
    Collecting jaraco.classes
      Downloading jaraco.classes-3.2.3-py3-none-any.whl (6.0 kB)
    Collecting docutils>=0.13.1
      Downloading docutils-0.19-py3-none-any.whl (570 kB)
         -------------------------------------- 570.5/570.5 kB 8.9 MB/s eta 0:00:00
    Requirement already satisfied: Pygments>=2.5.1 in c:\python39\lib\site-packages (from readme-renderer>=35.0->twine->pyloco>=0.0.134->matplot) (2.13.0)
    Requirement already satisfied: bleach>=2.1.0 in c:\python39\lib\site-packages (from readme-renderer>=35.0->twine->pyloco>=0.0.134->matplot) (5.0.1)
    Requirement already satisfied: charset-normalizer<3,>=2 in c:\python39\lib\site-packages (from requests>=2.20->twine->pyloco>=0.0.134->matplot) (2.1.1)
    Requirement already satisfied: idna<4,>=2.5 in c:\python39\lib\site-packages (from requests>=2.20->twine->pyloco>=0.0.134->matplot) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in c:\python39\lib\site-packages (from requests>=2.20->twine->pyloco>=0.0.134->matplot) (2022.6.15)
    Collecting commonmark<0.10.0,>=0.9.0
      Downloading commonmark-0.9.1-py2.py3-none-any.whl (51 kB)
         ---------------------------------------- 51.1/51.1 kB ? eta 0:00:00
    Requirement already satisfied: webencodings in c:\python39\lib\site-packages (from bleach>=2.1.0->readme-renderer>=35.0->twine->pyloco>=0.0.134->matplot) (0.5.1)
    Collecting more-itertools
      Downloading more_itertools-9.0.0-py3-none-any.whl (52 kB)
         ---------------------------------------- 52.8/52.8 kB ? eta 0:00:00
    Building wheels for collected packages: SimpleWebSocketServer, typing, ushlex
      Building wheel for SimpleWebSocketServer (setup.py): started
      Building wheel for SimpleWebSocketServer (setup.py): finished with status 'done'
      Created wheel for SimpleWebSocketServer: filename=SimpleWebSocketServer-0.1.2-py3-none-any.whl size=9684 sha256=ca5c56fd056e0da1dd7eed76a8eb57a1dc1f0b700d8e682290ab1a71f8787423
      Stored in directory: c:\users\user\appdata\local\pip\cache\wheels\54\20\6b\a4ce68b72f26f10cdd3280976de363886c9172be1374666c3d
      Building wheel for typing (setup.py): started
      Building wheel for typing (setup.py): finished with status 'done'
      Created wheel for typing: filename=typing-3.7.4.3-py3-none-any.whl size=26325 sha256=415259368156efc7c4697920acd52f0cdfd804697916bbee6b918e610b2051b2
      Stored in directory: c:\users\user\appdata\local\pip\cache\wheels\fa\17\1f\332799f975d1b2d7f9b3f33bbccf65031e794717d24432caee
      Building wheel for ushlex (setup.py): started
      Building wheel for ushlex (setup.py): finished with status 'done'
      Created wheel for ushlex: filename=ushlex-0.99.1-py3-none-any.whl size=4416 sha256=abed4760c14d94a49c9749e7e27b6bffd3d22489efd67f776f9211662f2e6cd6
      Stored in directory: c:\users\user\appdata\local\pip\cache\wheels\30\e7\e6\d3f198618450ea67a8950ebbefbcddffee32b034187ed8c3f9
    Successfully built SimpleWebSocketServer typing ushlex
    Installing collected packages: ushlex, SimpleWebSocketServer, pywin32-ctypes, commonmark, websocket-client, typing, rich, rfc3986, pkginfo, more-itertools, kiwisolver, fonttools, docutils, cycler, contourpy, requests-toolbelt, readme-renderer, matplotlib, jaraco.classes, keyring, twine, pyloco, matplot
    Successfully installed SimpleWebSocketServer-0.1.2 commonmark-0.9.1 contourpy-1.0.5 cycler-0.11.0 docutils-0.19 fonttools-4.37.4 jaraco.classes-3.2.3 keyring-23.9.3 kiwisolver-1.4.4 matplot-0.1.9 matplotlib-3.6.1 more-itertools-9.0.0 pkginfo-1.8.3 pyloco-0.0.139 pywin32-ctypes-0.2.0 readme-renderer-37.2 requests-toolbelt-0.10.0 rfc3986-2.0.0 rich-12.6.0 twine-4.0.1 typing-3.7.4.3 ushlex-0.99.1 websocket-client-1.4.1
    
    

    
    [notice] A new release of pip available: 22.2.2 -> 22.3
    [notice] To update, run: python.exe -m pip install --upgrade pip
    


```python
plt.hist(train['SaleCondition'])
```




    (array([1198.,    0.,  101.,    0.,  125.,    0.,    4.,    0.,   12.,
              20.]),
     array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. , 4.5, 5. ]),
     <BarContainer object of 10 artists>)




    
![png](output_9_1.png)
    



```python

```


```python

```


```python

```


```python

```
