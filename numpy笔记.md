# numpy简单应用

## 一、创建数组（ndarray）

1. 创建方式：
    * 用`np.array([1,2,3])`
    * 用`np.array(range(10))` == `np.arange(10)`
    * 这里的`arange`和python中的`range`类似，可以使用`star`、`stop`、`step`属性
    * 比如： `np.arange(4,10,2)`

2. 对数组使用`dtype`方法，可以查看数据的类型
    * 再创建数组时使用`dtype`属性可以修改创建出的数组的数据类型
    * 例如：`np.array(range(1,4),dtype="int64")`
    * 数据类型也可以改成`bool`类型,这种修改数据应该只有0,1
    * 同时，也可以对数组使用`astype("类型")`方法来修改数据类型
    * 例如：`x.astype("int8")`

3. 对数组中的所有数据取n位小数
    * 方法：`np.round(a,n)`
    * a是数组，n是要保留的位数，可以取负值

4. 创建一个全为0的数组：
    * 方法：`np.zeros((x,y))`
    * 形成一个x行y列的全为0的数组

5. 获取每行或者每列最大值和最小值的位置
    * 最大值：`np.argmax(x,axis=0)`
    * 最小值：`np.argmin(x,axis=1)`
    * axis是用来控制行或者列的，0是行，1是列

6. 创建一个对角线为1的正方形数组(n阶单位阵):
    * `np.eye(n)`

7. `linspace`函数生成等差数列
    * `def linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None):`
    * 指定初始值、终止值、数量、是否包含终止值，默认为包含。
8. logspace函数生成等比数列
    * `def logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None):`
    * 指定初始值、终止值、数量、是否包含终止值，默认为包含。

## 二、数组的形状

1. 如果是二维数组，就会形成矩阵形式
    * 使用`shape`方法可以查看他的维度，有多少个值就是多少维数组
    * 例如：`a.shape`

2. 修改数组形状的方法
    * 方法：`reshape`
    * 例子：`x.reshape(a,b)`
    * 将x修改成a行b列的数组
    * `a.reshape(2,3,4)`将数组x分成两块，每块是3×4的矩阵
    * 使用`reshape`方法会产生新的数组，而不是在原来的数组上进行改动

3. 将多维数组展开成一维数组
    * 方法：`flatten()`
    * 例子: `a.flatten()`
    * 将数组a按行展开成一维数组

4. 与数字计算时会对数组中的每一个数字进行运算（四则运算）

5. 两个数组形状一模一样时，两个数组运算会对对应的数字进行运算

6. 两个数组在某个维度相同时也是对应数相运算
    * 比如：4x3的数组与4x1的数组运算时，4x1的数组会与4x3数组的第一列的四行进行运算
    * 并非所有维度不相同的数组都能进行运算

## 四、轴（axis）

1. 在numpy中可以理解为方向，使用0,1,2，...数字表示，对于一个以为数组，只有一个0轴，对于二维数组，有0轴和1轴，对于三维数组，有0,1,2轴

## 五、numpy读取数据

1. 方法：`np.loadtxt(frame,dtpe=np.float,delimiter=None,skiprows=0,usecols=None, unpack=False)`
    * frame： 文件、字符串或产生器，尅一时.gz或者.bz2压缩文件
    * dtype： 数据类型可选，csv的字符串一神秘数据类型读入数组中,默认np.float
    * delimiter： 分割字符串，默认是任何空格，改为逗号
    * skiprows： 跳过前x行，一般跳过第一行表头
    * usecole： 读取指定的列，索引，元组类型
    * unpack： 如果为True，则对原来读取出来的数据进行转置，默认False为正常读取
    * 虽然是loadtxt并非只能读取txt文件，也能读取csv文件

2. 对数组进行转置
    * 方法：`transpose()`、`T`
    * 例子：`x.transpose()`、`x.T`
    * 将数组x进行转置，生成新数组，不是在原来的数组上进行改动

## 六、numpy索引和切片

1. 取一行：`x[n]`
    * 取x数组的第n行

2. 取连续多行：`x[n:]`
    * 从第n行开始一直取到数据末尾

3. 取指定的多个行：`x[[a,b,c]]`  
    * 取出第a第b第c行，这里使用了列表做参数，也可以使用元组做参数

4. 取一列：`tx[:,n]`
    * 取出所有数据的第n列的数据形成一个一维数组

5. 取连续多列：`x[:,2:]`
    * 从第二列开始一直取到低

6. 取不连续多了：`x[:,[0,2]]`
    * 取第一列和第三列

7. 取指定位置数据：`x[2,3]`
    * 取第三行第四列

8. 取多行多列：`x[2:5,1:4]`
    * 取3行到5行的2列到4列
    * 取的是行和列交叉点的位置

9. 取多个不相邻的点：`x[[0,2,2],[0,1,3]]`
    * 选出点(0,0),(2,1),(2,3)

10. numpy的数值修改：`t[:,2:4] = 0`
    * 将t数组中的第三列和第4列全部修改成0

## 七、numpy中的布尔索引

1. 对满足True的数值进行修改:`x[x>10] = 0`
    * 对x数组中大于10的数据，在对应位置修改成0

## 八、numpy中的三元运算符

1. 对满足True的数值修改成a，满足False的修改成b：`np.where(t<10,a,b)`
2. `np.where()`括号中可以输入判断条件，比如`np.where(x = x.min)`这时他会返回x的最小值的全部索引

## 九、numpy中的clip（裁剪）

1. 将x数组中小于a的替换成a，大于b的替换成b：`x.clip(a,b)`

2. 给数值赋值为nan:`x[3,3] = np.nan`
    * 这里的nan是一个float类型，如果你的x数组为整形时，需要使用astype方法进行转换才能赋值

## 十、数组的拼接

1. 竖直拼接数组x,y:`np.vstack((x,y))`
    * 形成一个数组，上方是x数组的数据，下方是y数组的数据

2. 水平拼接x,y:`np.hstack((x,y))`
    * 形成一个数组，左边是x数组的数据，右边是y数组的数据

3. 形成的都是一个新的数组，不是在原来的数组上进行修改

4. 要实现拼接在对应的维数要相同，比如在数值上拼接，那么他们的列数要相同，如果在水平上拼接，那么的行数要相同

5. 传入的是一个元组

## 十一、数组的行列交换

1. 第n+1行与第m+1行进行交换：`t[[n,m],:] = t[[m,n],:]`

2. 第n+1列与第m+1列进性交换：`t:[[n,m]] = t[:[m,n]]`

## 十二、numpy生成随机数

1. `.rand(d0,d1,...,dn)`：创建d0~dn维度的均匀分布的随机数数组，浮点数，范围从0~1

2. `.randn(d0,d1,..,dn)`: 创建d0~dn维度的正态分布的随机数，浮点数，平均值0，标准差1

3. `.randint(low,high,(size))`:从给定上下限方位选取随机数，范围是low,high。size是形状

4. `.normal(loc,scale,(size))`：从指定正太分布中速记抽取样本，分布中心是loc(概率分布的均值)，标准差是scale，形状是size

5. `.seed(s)`：随机数种子，s是给定的种子值。因为计算机生成的是伪随机数，所以通过设置相同的随机数种子，可以每次生成相同的随机数

## 十三、numpy的注意点copy和view

1. a = b完全不复制，a和b相互影响
2. a = b[:]视图的操作，一种切片，会创建新的对象a，但是a的数据完全有b保管，他们两个的数据变化是一致的
3. a = b.copy()复制，a和b互不影响
4. 为了避免出现多个变量表示同一个数组，我们可以每次都赋值给同一个变量

## 十四、numpy中常用的统计函数

1. 求和：`t.sum(axis=None)`
2. 均值：`t.mean(a,axis=None)`受离群点的影响较大
3. 中值：`np.median(t.axis=None)`
4. 最大值：`t.max(axis =None)`
5. 最大值：`t.min(axis =None)`
6. 极差：`np.pyp(t.axis=None)`即最大值和最小值之差
7. 标准差：`t.std(axis=None)`(方差开根号)
8. `axis`参数用来表示计算方式,None表示全部都计算（默认）,0表示计算结果与行的维数相同（即对每列进行计算），1同理
9. 在numpy中的nan和inf不是一个数字，但是属于float类型，nan != nan、inf != inf

## 十五、numpy中的线性运算

1. 矩阵相乘
    * a*b是指两个矩阵对应的每个数分别相乘
    * `a.dot(b)`是指a x b
    * `b.dot(a)`是指b x a
2. 矩阵求逆
    * `np.linalg.inv(a)`对a进行求逆运算
    * `np.linalg.pinv(a)`求a的伪逆，a的行列式为0时
3. `a,b=np.linalg.eig(x)`提取矩阵x的特征值（放入a）和特征向量（放入b）
4. `np.identity(n)`创建n阶的单位矩阵
5. `np.linalg.det(a)`求a的行列式
6. 要创建一个列向量只需先创建一个行向量，然后在创建语句的结尾加个.T
7. 使用`np.size`（矩阵，行或列）函数用来判断矩阵是几乘几阶的
    * 第二个参数只能是0（行）或1（列），如果不输入第二个参数他会输出nxm的结果
8. `np.vdot()`求两个向量的点积
9. `np.pi` 是一个常数表示圆周率π，2×np.pi就相当于2π啦