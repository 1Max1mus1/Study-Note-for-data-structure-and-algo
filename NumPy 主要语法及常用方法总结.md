# NumPy 主要语法及常用方法总结

## 1. 数组创建

### 基本创建方法

```python
import numpy as np

# 从列表创建
arr = np.array([1, 2, 3, 4])
arr2d = np.array([[1, 2], [3, 4]])

# 创建特殊数组
np.zeros((3, 4))        # 全0数组
np.ones((2, 3))         # 全1数组
np.empty((2, 2))        # 空数组（未初始化）
np.full((2, 3), 7)      # 填充指定值

# 创建序列
np.arange(0, 10, 2)     # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)    # 在0到1之间生成5个等间距的数

# 创建单位矩阵
np.eye(3)               # 3x3单位矩阵
np.identity(4)          # 4x4单位矩阵
```

## 2. 数组属性

```python
arr.shape      # 数组形状
arr.ndim       # 数组维度
arr.size       # 元素总数
arr.dtype      # 数据类型
arr.itemsize   # 每个元素的字节大小
```

## 3. 数组索引与切片

```python
# 一维数组
arr[0]         # 第一个元素
arr[-1]        # 最后一个元素
arr[1:4]       # 切片

# 多维数组
arr2d[0, 1]    # 第0行第1列
arr2d[0]       # 第0行
arr2d[:, 1]    # 第1列
arr2d[0:2, 1:3]  # 切片

# 布尔索引
arr[arr > 5]   # 选择大于5的元素

# 花式索引
arr[[0, 2, 4]] # 选择指定索引的元素
```

## 4. 数组形状操作

```python
arr.reshape(3, 4)      # 改变形状
arr.flatten()          # 展平为一维
arr.ravel()            # 展平（返回视图）
arr.T                  # 转置
arr.transpose()        # 转置

np.concatenate([arr1, arr2], axis=0)  # 连接数组
np.vstack([arr1, arr2])               # 垂直堆叠
np.hstack([arr1, arr2])               # 水平堆叠
np.split(arr, 3)                      # 分割数组
```

## 5. 数学运算

### 基本运算（元素级）

```python
arr + 5        # 加法
arr - 3        # 减法
arr * 2        # 乘法
arr / 2        # 除法
arr ** 2       # 幂运算
arr % 2        # 取模

# 数组间运算
arr1 + arr2
arr1 * arr2    # 对应元素相乘
```

### 矩阵运算

```python
np.dot(arr1, arr2)     # 矩阵乘法
arr1 @ arr2            # 矩阵乘法（Python 3.5+）
np.matmul(arr1, arr2)  # 矩阵乘法
```

### 统计函数

```python
arr.sum()          # 求和
arr.sum(axis=0)    # 按列求和
arr.mean()         # 平均值
arr.std()          # 标准差
arr.var()          # 方差
arr.min()          # 最小值
arr.max()          # 最大值
arr.argmin()       # 最小值索引
arr.argmax()       # 最大值索引
arr.cumsum()       # 累积和
arr.cumprod()      # 累积积
```

## 6. 数学函数

```python
# 三角函数
np.sin(arr)
np.cos(arr)
np.tan(arr)

# 指数和对数
np.exp(arr)        # e^x
np.log(arr)        # 自然对数
np.log10(arr)      # 以10为底的对数
np.sqrt(arr)       # 平方根

# 取整
np.round(arr)      # 四舍五入
np.floor(arr)      # 向下取整
np.ceil(arr)       # 向上取整
np.abs(arr)        # 绝对值
```

## 7. 逻辑运算

```python
# 比较运算
arr > 5
arr == 5
arr != 5

# 逻辑运算
np.logical_and(arr > 0, arr < 10)
np.logical_or(arr < 0, arr > 10)
np.logical_not(arr)

# 条件函数
np.where(arr > 5, 1, 0)    # 条件选择
```

## 8. 随机数生成

```python
np.random.rand(3, 4)           # [0,1)均匀分布
np.random.randn(3, 4)          # 标准正态分布
np.random.randint(0, 10, (3,4)) # 随机整数
np.random.random((3, 4))       # [0,1)随机数
np.random.choice(arr, 5)       # 随机抽取
np.random.shuffle(arr)         # 打乱顺序
```

## 9. 广播机制

NumPy允许不同形状的数组进行运算：

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
arr + np.array([10, 20, 30])  # 自动广播
```

## 10. 常用技巧

```python
# 数组去重
np.unique(arr)

# 排序
np.sort(arr)
arr.sort()  # 就地排序

# 保存和加载
np.save('array.npy', arr)
arr = np.load('array.npy')
np.savetxt('array.txt', arr)
arr = np.loadtxt('array.txt')
```

## 学习建议

1. **多维数组是核心**：理解shape、轴（axis）的概念
2. **广播机制**：掌握不同形状数组的运算规则
3. **向量化操作**：避免使用Python循环，用NumPy的向量化操作提高效率
4. **实践为主**：多动手练习各种数组操作

有什么具体的NumPy操作需要我详细解释吗？