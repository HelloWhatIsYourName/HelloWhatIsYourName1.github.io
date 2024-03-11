# Python 刷题感悟

## 1 向右对齐输出

读入三个整数，按每个整数占 88 个字符的宽度，右对齐输出它们，按照格式要求依次输出三个整数，之间以一个空格分开。

使用f字符串格式化输出, `{变量:>8}` 表示右对齐,宽度为8字符

```python
a, b, c = map(int, input().split())

print(f'{a:>8} {b:>8} {c:>8}')
```

在Python中,有几种方法可以实现向右对齐输出:

1. 使用字符串的 rjust() 方法:

   ```python
   a.rjust(8)
   ```

   会将a向右补充空格直到总长度为8。

2. 使用格式化字符串,指定右对齐和宽度:

   ```
   f'{a:>8}'
   ```

3. 使用格式化字符串,指定左对齐的是宽度,而省略符号表示右对齐:

   ```
   f'{a:<8}'
   ```

4. 使用format()方法和字符串填充:

   ```
   '{:8}'.format(a)
   ```

5. 使用旧式字符串格式化语法:

   ```
   '%8s' % a
   ```

6. 使用字符串的ljust()方法左对齐,结合切片右对齐:

   ```python
   a.ljust(8)[:8]
   ```

所以在Python中实现右对齐输出,主要就是利用字符串填充、格式化以及对齐方法,来控制输出的宽度和对齐方向。

上述几种方法可以灵活运用于字符串的右对齐格式化输出。

## 2 动态规划问题

```python
lenth = int(input())
lst = list(map(int, input().split()))

def L(lst, i):
    max_list = 1
    
    if i == len(lst):
        return 1
    
    for j in range(i, len(lst)):
        if lst[j] > lst[i]:
            max_list = max(max_list, L(lst, j+1) + 1)
    
    return max_list

print(max(L(lst, i) for _ in range(lenth)))
```

## 3 浮点数保留类问题

这里是用Python输出分数的双精度浮点数值(保留小数点后99位)的代码:

```python
import math

a, b = map(int, input().split())  

result = a / b

print("{:.99f}".format(result))
```

主要步骤是:

1. 输入并读取a和b为整数

2. 计算a/b的值

3. 打印结果,保留9位小数

   - {:.9f}表示打印时保留99位小数

   - format(result)将result变量插入格式化字符串中

Python默认的浮点数精度只有17位数字,为了获得99位的完整双精度精度,需要引入math模块并使用{:.99f}的格式化语法。

以此可以打印出分数a/b的最准确的双精度浮点数值,保留小数点后99位。

```python
pi = 3.14159
r = float(input())

d = 2 * r
c = 2 * pi * r
a = pi * r ** 2
print('{:.4f} {:.4f} {:.4f}'.format(d, c, a))
```

## 4 元组的排序和enumerate

`enumerate()` 是python的内置函数,它的作用是在一个可迭代的对象(列表,元组等)上添加一个计数器,使其成为一个enumerate对象,遍历这个对象能够获取元素的索引和值。

主要的好处是在迭代一个列表时能够同时得到索引位置和元素值。

例如在这个排序选手的程序中:

```
for i, (votes, name) in enumerate(contestants):
    print(f"{i+1}. {name}: {votes} votes")
```

使用`enumerate`的效果是:

- `i` 会获得索引值
- `(votes, name)` 能得到元素本身的值

这样就可以打印出像“1. Mary: 315 votes”这样的带有名次的结果。

如果不用`enumerate`,代码会更复杂,可能需要额外变量来维护排名计数。

所以,简单来说,`enumerate` 的作用就是在迭代时自动获取索引,使代码更简洁。这在处理需要访问元素索引的列表时非常有用。

元组虽然内容不可变,但是可以对包含元组的可变序列(比如列表)进行排序。

之所以列表中包含的元组可以进行排序,是因为在 python 中,排序操作是在元素的层面进行的。也就是说,会利用元素之间可以比较的特点来排序。

对于列表中的元组来说,具体排序逻辑是:

1. 按照元组的第一个元素进行第一次比较和排序
2. 如果第一个元素相等,再按照第二个元素进行比较和排序
3. 以此类推,直到比较完元组中的所有元素

我们在代码中构造的 `contestants` 列表中,每个元素是一个只有两个元素的元组 `(votes, name)`。 在排序时,会首先比较两个元组的第一个元素 `votes`,也就是选手获得的票数。

`votes` 都是整数,所以可以很好地比较大小。如果第一个元素相等,才会进行第二个字符串元素 `name` 的比较。这样就实现了整个列表的排序。

所以,通过上述逻辑,我们就可以方便地基于元组内的第一个元素来实现整个列表的排序,这使得元组这样一个不可变类型也可以排序。

这就是 python 中,列表中的元组为什么也可以进行排序的原因。

## 5 isdigit函数

好的,我用中文来解释一下isdigit()函数的作用:

isdigit() 是Python中的一个字符串方法,中文名称叫“是否全部是数字”。

所谓字符串方法,就是可以在字符串对象上直接调用的函数。例如:

```
str = "123"
print(str.isdigit()) # 输出True
```

这个方法的作用就是检查一个字符串是否全部由数字0-9组成。它会逐个去检查字符串中的每一个字符:

1. 如果所有字符都是数字,它会返回True
2. 只要有任何一个字符不是数字,它就会返回False

举几个例子:

```
"123".isdigit() 的结果是 True  (全部是数字)

"123abc".isdigit() 的结果是 False (含有字母)  

"一二三".isdigit() 的结果是 False (含有中文)

"".isdigit() 的结果是 False (空字符串)
```

所以在这个身份证校验码代码里,我们利用 isdigit() 来判断前17位是不是全部由数字组成:

```
id_num[:-1].isdigit()  
# 切掉最后一位校验码,判断前17位是否全是数字
```

这样就避免了使用正则表达式来判断数字,利用语言内置的isdigit()简化了代码逻辑。

## 6 lambda函数

lambda是Python中一个非常有用的小工具,它可以创建简单的匿名函数。

基本语法是:

```
lambda 参数: 返回值
```

举几个例子:

**求两个数的和**

```
adder = lambda x, y: x + y

print(adder(3, 5)) # 输出8
```

**转换为摄氏温度**

```
to_celsius = lambda f: (f - 32) * 5/9

print(to_celsius(100)) # 输出37.77777777777778
```

**过滤出列表中的偶数**

```
nums = [1, 2, 3, 4, 5, 6]

evens = filter(lambda x: x%2 == 0, nums)
print(list(evens)) # 输出 [2, 4, 6]
```

所以lambda的主要作用就是创建短小的内联函数,这在需要传入函数作为参数的场景下非常有用。

与定义普通函数相比,lambda可以避免申明和命名一个完整的函数,让代码更加精简和优雅。

在上面的例子中,filter函数需要传入一个判断函数对nums里的元素进行过滤。这时候用lambda就很方便,没有必要单独定义一个is_even之类的函数。

可以的,lambda函数并不限制只能在print语句中使用,它可以在代码的任何地方作为一个正常的函数去调用。



```
double = lambda x: x * 2

# 与print结合使用
print(double(5))

# 作为map函数的参数
doubled = map(double, [1, 2, 3]) 
print(list(doubled))

# 作为 sorted的key函数
points = [(1,2), (3,1), (2,3)]
sorted_points = sorted(points, key=lambda x: x[1]) 
print(sorted_points)

# 作为递归函数
fib = lambda n: n if n <= 1 else (fib(n-1) + fib(n-2))
print(fib(6))
```

上面例子中lambda被用在:

1. print语句中进行输出
2. map函数的参数中处理列表元素
3. sorted的key函数对元组列表排序
4. 递归fibonacci数字的定义

可以看出,lambda可以在任何需要函数参数或需要自定义函数的地方很灵活地使用。

## 7 Fraction类

Python中的Fraction类实现了有理数(分数)的数学运算。 Fraction类的主要作用包括:

1. 表示分数的值
2. 分数与分数、整数之间的数学运算
3. 分数的化简

例如:

```
from fractions import Fraction

# 创建分数 
a = Fraction(1, 3)  

# 分数与整数运算
b = a * 3  
print(b) # 1

# 分数与分数运算 
c = Fraction(1, 2)
d = b + c  
print(d) # 3/2

# 自动化简
e = Fraction(2, 4)
print(e) # 1/2
```

主要功能有:

- 支持直接创建分数对象,如 `Fraction(numerator, denominator)`
- 对分数自动化简,如 2/4 会被化简为 1/2
- 支持分数与整数、分数与分数之间的数学运算
- 提供限制分母的方法来返回化简结果

所以Fraction类非常适合处理分数相关的运算和计算。它封装了大量实现分数计算的细节。

在本题中,使用Fraction就可以简化代码,不需要自己实现化简、运算等逻辑。

## 



## 8 矩阵

这里是使用Python来解决矩阵寻找鞍点的问题:

```python
matrix = []
for _ in range(5):
    matrix.append(list(map(int, input().split())))

r_max = {i: max(row) for i, row in enumerate(matrix)}
c_min = {j: min(col) for j, col in enumerate(zip(*matrix))}

saddle_point = None
for i in range(5):
    for j in range(5):
        if r_max[i] == matrix[i][j] and c_min[j] == matrix[i][j]:
            saddle_point = (i+1, j+1, matrix[i][j])
            break 
    if saddle_point: break
        
if saddle_point:
    print(*saddle_point)
else:
    print("not found")
```

主要思路:

- 创建行最大值字典 r_max
- 创建列最小值字典 c_min
- 遍历查找符合条件的鞍点

时间复杂度O(n^2)

好的,我来解释下这两行代码的作用:

```python
r_max = {i: max(row) for i, row in enumerate(matrix)}
```

这行利用字典推导式(dict comprehension)来构建一个字典r_max,该字典包含每个矩阵行的最大值。

具体逻辑是:

- enumerate(matrix) 枚举矩阵的每个行,返回行索引i和行内容row
- max(row) 计算该行的最大值
- 将i作为键,最大值作为值,存储到字典r_max中

举例来说,如果matrix是:

```
[[1, 2, 3],
[4, 5, 6]]
```

则r_max会是:

```
{0: 3, 1: 6}
```

同理,第二行:

```python
c_min = {j: min(col) for j, col in enumerate(zip(*matrix))} 
```

作用是获得每一列的最小值,方法是:

- zip(*matrix)将矩阵转置,获得每列
- enumerate枚举列,min获得最小值
- 存储到字典c_min中

所以它实现了高效地获得行最大值和列最小值的效果

### 字典推导式

字典推导式(Dict Comprehension)是Python中一个非常有用的语法,它可以用简洁的方式快速创建字典。

**字典推导式的基本语法**:

```python
{key: value for <循环变量> in <可迭代对象>}
```

其中:

- key: 是字典中的键
- value: 是字典中的值
- 循环变量:在可迭代对象中迭代的变量
- 可迭代对象:一个可以提供迭代项的对象,如列表、字符串等。

这个语法遵循这样的逻辑流程:

1. 从可迭代对象中依次取出元素,赋值给循环变量
2. 根据循环变量,通过一定计算,确定字典键值对中的key和value
3. 将所有计算出的键值对组合,构建为字典并返回

**示例:**

```python
dict1 = {x: x**2 for x in range(5)}
print(dict1)

# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

上例中x是循环变量,range(5)是可迭代对象。通过x**2产生对应值。

**好处:**

1. 语法简洁,符合Python的简洁风格
2. 避免重复代码的编写,提高开发效率
3. 易读易懂,成为产出字典的首选方式



## 9 分字符

好的,我来解释一下`parts = line.split(' ', 1)`这行代码:

`line.split(' ', 1)`是Python中字符串的`split()`方法的用法,它用于将字符串按照指定的分隔符进行分割,并返回一个列表。

- ```
  split()
  ```

  方法的基本用法是

  ```
  str.split(sep=None, maxsplit=-1)
  ```

  。其中:

  - `sep`是分隔符,默认是任何空白字符串(包括空格、制表符、换行符等)。
  - `maxsplit`是最大分割次数,如果为-1(默认值),则无限制分割。

- 在

  ```
  parts = line.split(' ', 1)
  ```

  中:

  - `' '`表示将空格作为分隔符。
  - `1`表示最多只分割一次,也就是说,只将字符串分成两个部分。

- 例如,如果

  ```
  line = "123 456 789"
  ```

  - `line.split(' ')`将返回`['123', '456', '789']`(按空格分割,分割次数无限制)。
  - `line.split(' ', 1)`将返回`['123', '456 789']`(按第一个空格分割一次,分成两个部分)。

所以,`parts = line.split(' ', 1)`的作用是:将输入的一行字符串`line`按照第一个空格分割成两个部分,存储在列表`parts`中。

- `parts`列表的第一个元素`parts[0]`是第一个空格之前的部分,相当于之前使用正则的`parts[0]`。
- `parts`列表的第二个元素`parts[1]`是第一个空格之后的整个部分,相当于之前使用正则的`parts[1]`。

## 10 去除空格（string）

`.strip()`是字符串的一个方法,它用于删除字符串两端的空白字符(包括空格、制表符`\t`、换行符`\n`等)。通过使用`.strip()`方法,我们可以去掉用户输入字符串两端可能存在的任何不必要的空白字符。
