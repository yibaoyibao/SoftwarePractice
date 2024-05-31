快速排序


```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        # 找到从i到n中最小的元素的索引
        min_idx = i
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        # 将找到的最小元素交换到它的位置
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
def test():
    # 执行数据输入
    arr = [64, 25, 12, 22, 11]
    print("原始数组:", arr)
    
    # 调用 selection_sort 函数进行排序
    selection_sort(arr)
    
    # 输出结果
    print("排序后的数组:", arr)

# 调用 test 函数进行测试
test()
```

    原始数组: [64, 25, 12, 22, 11]
    排序后的数组: [11, 12, 22, 25, 64]
    

试着输入一行代码，查看执行效果：


```python
print('Hello World!')
```

    Hello World!
    


```python
import numpy as np
def square(x):
    return x * x

```


```python
x = np.random.randint(1, 10)
y = square(x)
print('%d squared is %d' % (x, y))

```

    5 squared is 25
    


```python
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

```

使用pandas


```python
df = pd.read_csv('fortune500.csv')#读取文件
```


```python
df.head()#查看前5行
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
      <th>Year</th>
      <th>Rank</th>
      <th>Company</th>
      <th>Revenue (in millions)</th>
      <th>Profit (in millions)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1955</td>
      <td>1</td>
      <td>General Motors</td>
      <td>9823.5</td>
      <td>806</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1955</td>
      <td>2</td>
      <td>Exxon Mobil</td>
      <td>5661.4</td>
      <td>584.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1955</td>
      <td>3</td>
      <td>U.S. Steel</td>
      <td>3250.4</td>
      <td>195.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1955</td>
      <td>4</td>
      <td>General Electric</td>
      <td>2959.1</td>
      <td>212.6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1955</td>
      <td>5</td>
      <td>Esmark</td>
      <td>2510.8</td>
      <td>19.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail()#查看最后5行
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
      <th>Year</th>
      <th>Rank</th>
      <th>Company</th>
      <th>Revenue (in millions)</th>
      <th>Profit (in millions)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>25495</th>
      <td>2005</td>
      <td>496</td>
      <td>Wm. Wrigley Jr.</td>
      <td>3648.6</td>
      <td>493</td>
    </tr>
    <tr>
      <th>25496</th>
      <td>2005</td>
      <td>497</td>
      <td>Peabody Energy</td>
      <td>3631.6</td>
      <td>175.4</td>
    </tr>
    <tr>
      <th>25497</th>
      <td>2005</td>
      <td>498</td>
      <td>Wendy's International</td>
      <td>3630.4</td>
      <td>57.8</td>
    </tr>
    <tr>
      <th>25498</th>
      <td>2005</td>
      <td>499</td>
      <td>Kindred Healthcare</td>
      <td>3616.6</td>
      <td>70.6</td>
    </tr>
    <tr>
      <th>25499</th>
      <td>2005</td>
      <td>500</td>
      <td>Cincinnati Financial</td>
      <td>3614.0</td>
      <td>584</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.columns = ['year', 'rank', 'company', 'revenue', 'profit']#设置列名
```


```python
len(df)#查看条目数
```




    25500




```python
df.dtypes#查看不同列的数据类型,profit存在异常
```




    year         int64
    rank         int64
    company     object
    revenue    float64
    profit      object
    dtype: object




```python
non_numberic_profits = df.profit.str.contains('[^0-9.-]')#检查非数字的列情况
df.loc[non_numberic_profits].head()
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
      <th>year</th>
      <th>rank</th>
      <th>company</th>
      <th>revenue</th>
      <th>profit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>228</th>
      <td>1955</td>
      <td>229</td>
      <td>Norton</td>
      <td>135.0</td>
      <td>N.A.</td>
    </tr>
    <tr>
      <th>290</th>
      <td>1955</td>
      <td>291</td>
      <td>Schlitz Brewing</td>
      <td>100.0</td>
      <td>N.A.</td>
    </tr>
    <tr>
      <th>294</th>
      <td>1955</td>
      <td>295</td>
      <td>Pacific Vegetable Oil</td>
      <td>97.9</td>
      <td>N.A.</td>
    </tr>
    <tr>
      <th>296</th>
      <td>1955</td>
      <td>297</td>
      <td>Liebmann Breweries</td>
      <td>96.0</td>
      <td>N.A.</td>
    </tr>
    <tr>
      <th>352</th>
      <td>1955</td>
      <td>353</td>
      <td>Minneapolis-Moline</td>
      <td>77.4</td>
      <td>N.A.</td>
    </tr>
  </tbody>
</table>
</div>




```python
len(df.profit[non_numberic_profits])#查看总共有多少非数字的收益
```




    369




```python
bin_sizes, _, _ = plt.hist(df.year[non_numberic_profits], bins=range(1955, 2006))#用直方图查看非数字收益的大体情况
```


    
![png](output_16_0.png)
    



```python
df = df.loc[~non_numberic_profits]#删除这些非法记录
df.profit = df.profit.apply(pd.to_numeric)
```


```python
len(df)#删除后查看条目数
```




    25131




```python
df.dtypes#重新查看数据类型,现在正常
```




    year         int64
    rank         int64
    company     object
    revenue    float64
    profit     float64
    dtype: object



matplotlib使用


```python
group_by_year = df.loc[:, ['year', 'revenue', 'profit']].groupby('year')#以年分组绘制平均利润和收入
avgs = group_by_year.mean()
x = avgs.index
y1 = avgs.profit
def plot(x, y, ax, title, y_label):
    ax.set_title(title)
    ax.set_ylabel(y_label)
    ax.plot(x, y)
    ax.margins(x=0, y=0)

```


```python
fig, ax = plt.subplots()#1990年类似指数增长,但之后急剧下降
plot(x, y1, ax, 'Increase in mean Fortune 500 company profits from 1955 to 2005', 'Profit (millions)')
```


    
![png](output_22_0.png)
    



```python
y2 = avgs.revenue#查看平均收入曲线
fig, ax = plt.subplots()
plot(x, y2, ax, 'Increase in mean Fortune 500 company revenues from 1955 to 2005', 'Revenue (millions)')
```


    
![png](output_23_0.png)
    



```python
def plot_with_std(x, y, stds, ax, title, y_label):
    ax.fill_between(x, y - stds, y + stds, alpha=0.2)
    plot(x, y, ax, title, y_label)
fig, (ax1, ax2) = plt.subplots(ncols=2)
title = 'Increase in mean and std Fortune 500 company %s from 1955 to 2005'
stds1 = group_by_year.std().profit.values
stds2 = group_by_year.std().revenue.values
plot_with_std(x, y1.values, stds1, ax1, title % 'profits', 'Profit (millions)')
plot_with_std(x, y2.values, stds2, ax2, title % 'revenues', 'Revenue (millions)')
fig.set_size_inches(14, 4)
fig.tight_layout()
```


    
![png](output_24_0.png)
    



```python
根据标准差来查看前10%和后10%谁的波动更大
```


```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# 加载数据集
df = pd.read_csv('fortune500.csv')

# 重命名列
df.columns = ['year', 'rank', 'company', 'revenue', 'profit']

# 清洗数据，删除无效的利润记录
non_numberic_profits = df.profit.str.contains('[^0-9.-]')
df = df.loc[~non_numberic_profits]
df.profit = df.profit.apply(pd.to_numeric)

# 按年份分组
group_by_year = df.groupby('year')

# 准备存储标准差的DataFrame
std_devs = pd.DataFrame()

# 计算每一年前10%和后10%公司的收入和利润的标准差
for year, group in group_by_year:
    revenue_std = group.revenue.std()
    profit_std = group.profit.std()
    top_revenue_std = group.revenue.nlargest(int(len(group) * 0.1)).std()
    top_profit_std = group.profit.nlargest(int(len(group) * 0.1)).std()
    bottom_revenue_std = group.revenue.nsmallest(int(len(group) * 0.1)).std()
    bottom_profit_std = group.profit.nsmallest(int(len(group) * 0.1)).std()
    std_devs = pd.concat([std_devs, pd.DataFrame({
        'year': [year],
        'revenue_std': [revenue_std],
        'profit_std': [profit_std],
        'top_revenue_std': [top_revenue_std],
        'top_profit_std': [top_profit_std],
        'bottom_revenue_std': [bottom_revenue_std],
        'bottom_profit_std': [bottom_profit_std]
    })], ignore_index=True)

# 绘制结果
plt.figure(figsize=(10, 6))
for column in std_devs.columns[1:]:
    plt.plot(std_devs['year'], std_devs[column], label=column)

plt.xlabel('Year')
plt.ylabel('Standard Deviation')
plt.title('Standard Deviation of Revenue and Profit for Top 10% and Bottom 10% Companies')
plt.legend()
plt.show()

```


    
![png](output_26_0.png)
    



```python
很明显年份的影响更大
```
