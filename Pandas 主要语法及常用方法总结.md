我很乐意帮你总结pandas的主要语法和常用方法！我会按照实际使用场景来组织这些内容。

## 一、基础导入与数据结构

```python
import pandas as pd
import numpy as np

# 两种核心数据结构
# Series: 一维数组
s = pd.Series([1, 2, 3, 4])

# DataFrame: 二维表格
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
})
```

## 二、数据读取与保存

```python
# 读取数据
df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
df = pd.read_json('file.json')
df = pd.read_sql(query, connection)

# 保存数据
df.to_csv('file.csv', index=False)
df.to_excel('file.xlsx', index=False)
df.to_json('file.json')
```

## 三、数据查看与基本信息

```python
df.head()          # 查看前5行
df.tail()          # 查看后5行
df.shape           # 查看形状(行数, 列数)
df.info()          # 查看数据类型和非空值
df.describe()      # 统计描述
df.columns         # 列名
df.dtypes          # 各列数据类型
df.isnull().sum()  # 每列缺失值数量
```

## 四、数据选择与索引

```python
# 按列选择
df['A']            # 单列,返回Series
df[['A', 'B']]     # 多列,返回DataFrame

# 按行选择
df[0:3]            # 切片选择行

# loc: 按标签索引
df.loc[0]          # 选择第0行
df.loc[0:2, 'A']   # 选择0-2行的A列
df.loc[df['A'] > 2, ['A', 'B']]  # 条件选择

# iloc: 按位置索引
df.iloc[0]         # 第0行
df.iloc[0:3, 0:2]  # 前3行,前2列
df.iloc[[0, 2], [1, 3]]  # 指定行列

# 条件筛选
df[df['A'] > 2]    # 单条件
df[(df['A'] > 2) & (df['B'] < 5)]  # 多条件用&(与)
df[(df['A'] > 2) | (df['B'] < 5)]  # 或用|
```

## 五、数据清洗

```python
# 缺失值处理
df.dropna()                    # 删除含缺失值的行
df.dropna(axis=1)              # 删除含缺失值的列
df.fillna(0)                   # 填充缺失值
df.fillna(df.mean())           # 用均值填充
df.fillna(method='ffill')      # 前向填充

# 删除重复值
df.drop_duplicates()           # 删除重复行
df.drop_duplicates(['A'])      # 基于某列删除重复

# 重命名
df.rename(columns={'A': 'a'})  # 重命名列
df.columns = ['a', 'b', 'c']   # 直接赋值列名

# 删除行列
df.drop('A', axis=1)           # 删除列
df.drop([0, 1], axis=0)        # 删除行

# 替换值
df.replace(0, np.nan)          # 替换单个值
df.replace({0: np.nan, 1: 2})  # 替换多个值
```

## 六、数据操作

```python
# 新增列
df['C'] = df['A'] + df['B']    # 计算列
df['D'] = 100                   # 常数列

# 排序
df.sort_values('A')             # 按列排序
df.sort_values(['A', 'B'], ascending=[True, False])  # 多列排序
df.sort_index()                 # 按索引排序

# 应用函数
df['A'].apply(lambda x: x * 2)  # 对Series应用函数
df.apply(lambda x: x.max() - x.min())  # 对DataFrame应用

# 数据类型转换
df['A'].astype(int)             # 转换数据类型
pd.to_datetime(df['date'])      # 转换为日期类型
```

## 七、分组与聚合

```python
# groupby分组
df.groupby('A').sum()           # 分组求和
df.groupby('A').mean()          # 分组求均值
df.groupby('A')['B'].sum()      # 特定列分组聚合
df.groupby(['A', 'B']).agg(['sum', 'mean'])  # 多列分组,多种聚合

# 常用聚合函数
df['A'].sum()       # 求和
df['A'].mean()      # 均值
df['A'].median()    # 中位数
df['A'].std()       # 标准差
df['A'].min()       # 最小值
df['A'].max()       # 最大值
df['A'].count()     # 计数
df['A'].nunique()   # 唯一值数量
```

## 八、数据合并

```python
# concat: 拼接
pd.concat([df1, df2])              # 纵向拼接
pd.concat([df1, df2], axis=1)      # 横向拼接

# merge: 类似SQL的join
pd.merge(df1, df2, on='key')       # 基于共同列合并
pd.merge(df1, df2, how='left')     # 左连接
pd.merge(df1, df2, how='right')    # 右连接
pd.merge(df1, df2, how='outer')    # 外连接
pd.merge(df1, df2, how='inner')    # 内连接(默认)

# join: 基于索引合并
df1.join(df2)
```

## 九、透视表与交叉表

```python
# 透视表
df.pivot_table(
    values='D',        # 值列
    index='A',         # 行索引
    columns='B',       # 列索引
    aggfunc='mean'     # 聚合函数
)

# 交叉表
pd.crosstab(df['A'], df['B'])  # 频数统计
```

## 十、字符串操作

```python
# str访问器
df['A'].str.lower()         # 转小写
df['A'].str.upper()         # 转大写
df['A'].str.strip()         # 去空格
df['A'].str.contains('abc') # 包含判断
df['A'].str.replace('a', 'b')  # 替换
df['A'].str.split(',')      # 分割
df['A'].str[0:3]            # 切片
```

## 十一、日期时间操作

```python
# 转换为日期类型
df['date'] = pd.to_datetime(df['date'])

# 提取日期部分
df['date'].dt.year          # 年
df['date'].dt.month         # 月
df['date'].dt.day           # 日
df['date'].dt.dayofweek     # 星期几
df['date'].dt.hour          # 小时
```

## 十二、重塑数据

```python
# 宽转长
df.melt(id_vars=['A'], value_vars=['B', 'C'])

# 长转宽
df.pivot(index='A', columns='B', values='C')

# 重置索引
df.reset_index()            # 重置索引
df.set_index('A')           # 设置索引
```

这些是pandas最常用的语法和方法。建议你在实践中逐步掌握，遇到具体问题时可以随时问我！