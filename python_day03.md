#Python Day03

#pickle
在使用文件存储时，通常需要对数据进行一些处理，按照一定的规范把数据整理成文本，再写入文件中。下次使用时，从文件中读出文本，再按照此规范解析这些数据。

这种将数据转成文本的过程又被称为“序列化”，即将对象状态转换为可保持或传输的格式的过程。对应的，从序列化的格式中解析对象状态的过程被称为“反序列化”。

其实 Python 提供了一个标准模块来做这件事，就是 pickle。它可以把任何 Python 对象存储在文件中，再把它原样取出来。

```python
import pickle

test_data = ['Save me!', 123.456, True]

f = file('test.data', 'w')
pickle.dump(test_data, f)
f.close()
```
这样，我们就把 test_data 这个 list 存储在了文件 test.data 中。你可以用文本编辑器打开 test.data 查看里面的内容：

```python
(lp0
S'Save me!'
p1
aF123.456
aI01
a.
```
这就是经 pickle 序列化后的数据，隐约可以看到之前对象的影子。你可能无法看出这个文件的规律，这没关系，Python 能看懂就可以了。

下面取存储的过程：

```python
import pickle

f = file('test.data')
test_data = pickle.load(f)
f.close()

print test_data
```
控制台的输出：

    ['Save me!', 123.456, True]
    
如果你想保存多个对象，一种方法是把这些对象先全部放在一个序列中，在对这个序列进行存储：

```python
a = 123
b = "hello"
c = 0.618
data = (a, b, c)

pickle.dump(data, f)
```
另一种方法就是依次保存和提取：

```python
pickle.dump(a, f)
pickle.dump(b, f)
pickle.dump(c, f)

x = pickle.load(f)
y = pickle.load(f)
z = pickle.load(f)
```

dump 方法可以增加一个可选的参数，来指定用二进制来存储：

```python
pickle.dump(data, f, True)
```
而 load 方法会自动检测数据是二进制还是文本格式，无需手动指定。

Python 还提供了另一个模块 cPickle，它的功能及用法和 pickle 模块完全相同，只不过它是用C语言编写的，因此要快得多（比pickle快1000倍）。因此你可以把上述代码中的 pickle 全部替换为 cPickle，从而提高运行速度

##lambda 表达式
lambda 表达可以被看做是一种匿名函数。它可以让你快速定义一个极度简单的单行函数。譬如这样一个实现三个数相加的函数：

```python
def sum(a, b, c):
return a + b + c

print sum(1, 2, 3)
print sum(4, 5, 6)
```
输出：

    6
    15

如果使用 lambda 表达式来实现：

```python
sum = lambda a, b, c: a + b + c

print sum(1, 2, 3)
print sum(4, 5, 6)
```
输出:
    
    6
    15
    
两种方法的结果是相同的。

lambda 表达式的语法格式： `lambda 参数列表: 表达式`

定义 lambda 表达式时，参数列表周围没有括号，返回值前没有 return 关键字，也没有函数名称。

它的写法比 def 更加简洁。但是，它的主体只能是一个表达式，不可以是代码块，甚至不能是命令（print 不能用在 lambda 表达式中）。所以 lambda 表达式能表达的逻辑很有限。

##map 函数
来看两个问题：
1. 假设有一个数列，如何把其中每一个元素都翻倍？
2. 假设有两个数列，如何求和？

第一个问题，普通程序员大概会这么写：

```python
lst_1 = [1,2,3,4,5,6]
lst_2 = []
for item in lst_1:
	lst_2.append(item * 2)
print lst_2
```
Python 程序员大概会这么写：

```python
lst_1 = [1,2,3,4,5,6]
lst_2 = [i * 2 for i in lst_1]
print lst_2
```
另一种 Python 程序员常用的写法 -- map：

```python
lst_1 = [1,2,3,4,5,6]
def double_func(x):
return x * 2
lst_2 = map(double_func, lst_1)
print lst_2
```
map 是 Python 自带的内置函数，它的作用是把一个函数应用在一个（或多个）序列上，把列表中的每一项作为函数输入进行计算，再把计算的结果以列表的形式返回。

map 的第一个参数是一个函数，之后的参数是序列，可以是 list、tuple。