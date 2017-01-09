#Python Day01

##开发环境
* win系统官网下载安装包，安装一路next完成后，配置环境变量(win7系统是右键单击“计算机”，点击“属性”->“高级系统设置”->“环境变量”；win10系统需要在Path里新建一条记录，把路径加进去，无需分号）

* mac自带Python，无需下载安装 

##Hello World及print
编写代码有以下两种方式：

1. 打开命令行输入python回车，进入python命令行
2. 命令行中输入`IDLE `回车打开python自带工具

python命令行或IDLE中输入以下代码回车：

```python
print “Hello World”
```
 基本格式是：
`print 你要打印的东西`
或者
`print(你要打印的东西)`

示例：

```python
print "hello"
hello

print('world')
world

print 1
1

print(3.14)
3.14

print 3e30
3e+30

print 1 + 2 * 3
7

print(2 > 5)
False
```

注意：python3记得在后面必须加上()


##input
python有一个接收命令行下输入的方法：

```python
input()
```
注意，和print不同的是，这次我们必须得加上()了，而且得是英文字符的括号。

python还有一个输入的方法：

```python
raw_input()
```
它把所有的输入都直接当作一串字符，于是就可以不用加引号

##变量
python中没有像java那样必须在变量前声明类型，直接声明变量名即可,变量名声明规范：

* 第一个字符必须是字母或者下划线“_”
* 剩下的部分可以是字母、下划线“_”或数字（0-9）
* 变量名称是对大小写敏感的，myname和myName不是同一个变量。

```python
name = 'CharryLi'  #字符串
myVar = 666 #整数
price = 6.66 #浮点数
visible = True #布尔
```

##逻辑运算符
常用的逻辑运算符包括：

\>：大于

<：小于

\>=：大于等于

<=：小于等于

==：等于。比较两个值是否相等。之所以用两个等号，是为了和变量赋值区分开来。

!=：不等与

not：逻辑“非”。如果x为True，则not x为False

and：逻辑“与”。如果x为True，且y为True，则x and y为True

or：逻辑“或”。如果x、y中至少有一个为True，则x or y为True

##if else
代码：

```python
if a == 1:
   print 'right'
else:
   print 'wrong'
   
#if elif else
if a == 1:
   print 'one'
elif a == 2:
   print 'two'
elif a == 3:
   print 'three'
else:
   print 'too many'
```

##while
语法为：

	while 条件:
	    循环执行的语句

同if一样，注意冒号，注意缩进。

代码：

```python
a = 1  #先a设为1
while a != 0:  #a不等于0就一直做
    print "please input"
    a = input()
print "over"
```

##for
语法：for ... in ...

代码：

```python
for i in range(1, 101):
   print i
```

##字符串格式化
字符串拼接：

```python
str1 = 'hello'
str2 = 'world'
print str1 + str2
#或者
pint str1 + 'world'

#格式化

#输出的时候，%d会被%后面的值替换。输出My age is 18
num = 18
print 'My age is %d' % num

#输出Price is 4.990000
print ‘Price is %f’ % 4.99

#如果你想保留两位小数，需要在f前面加上条件：%.2f，输出Price is 4.99
print ‘Price is %.2f’ % 4.99

#另外，可以用%s来替换一段字符串，输出Charry is a good teacher.
name = 'Charry'
print '%s is a good teacher.' % name
#或者
print 'Today is %s.' % 'Friday' 

#多个参数格式化
print "%s's score is %d" % ('Charry', 66)
#或者
name = ‘Charry’
score = 95
print "%s's score is %d" % (name, score)
#('Charry', 66)这种用()表示的一组数据在python中被称为元组（tuple）

```
字符串分割（split）

```python
sentence = 'I am an Englist sentence'
sentence.split()
#得到一个list ['I', 'am', 'an', 'Englist', 'sentence']

section = 'Hi. I am the one. Bye.'
section.split('.')
#得到['Hi', ' I am the one', ' Bye', '']
```
除了空格外，split()同时也会按照换行符\n，制表符\t进行分割。所以应该说，split默认是按照空白字符进行分割。


##类型转换
python提供了一些方法对数值进行类型转换：

```python
int(x) #把x转换成整数
float(x) #把x转换成浮点数
str(x) #把x转换成字符串
bool(x) #把x转换成bool值
```

##bool类型转换
为什么要单独说一下bool类型转换呢？因为在python中，以下数值会被认为是False：

> 为0的数字，包括0，0.0

> 空字符串，包括''，""

> 表示空值的None

> 空集合，包括()，[]，{}

其他的值都认为是True。

在if、while等条件判断语句里，判断条件会自动进行一次bool的转换。比如

```python
a = '123'
if a:
	print 'this is not a blank string'

#这在编程中是很常见的一种写法。效果等同于
if bool(a)
#或者
if a != ''
```

##函数
python里的关键字叫def（define的缩写），格式如下：

```python
def sayHello():
   print 'hello world!'
```
然后我们去调用这个函数：

```python
sayHello()
```

带参数的函数

```python
def sayHello(someone):
   print someone + ' says Hello!'
```
或者

```python
def plus(num1, num2):
   print num1+num2
```

##list

list格式就是用中括号包围、逗号隔开的一组数值：

```python
ary = [1, 1, 2, 3, 5, 8, 13]
```
可以用print输出这个列表：

```pyton
print ary
```
同样也可以用for...in遍历这个列表，依次输出了列表中的每一项：

```python
for i in ary:
   print i,
```
列表中的元素也可以是别的类型，比如：

```python
ary = ['meat', 'egg', 'fish', 'milk']
ary = [365, 'everyday', 0.618, True]
```

##list操作
代码：

```python
#访问list中某个元素
print ary[1]

#修改list中的元素
ary[0] = 123

#向list中添加元素
ary.append(1024)

#删除list中的元素
del ary[0]
```
list索引操作

* ary[-1]表示l中的最后一个元素。
* ary[-3]表示倒数第3个元素。
* ary[:3]如果不指定第一个数，切片就从列表第一个元素开始。
* ary[1:]如果不指定第二个数，就一直到最后一个元素结束。
* ary[:]都不指定，则返回整个列表的一个拷贝。

list拼接

```python
s = ';'
li = ['apple', 'pear', 'orange']
fruit = s.join(li)
print fruit
#得到结果'apple;pear;orange'
```

##文件操作
打开一个文件的命令很简单,这里的文件名可以用文件的完整路径，也可以是相对路径。因为我们把要读取的文件和代码放在了同一个文件夹下，所以只需要写它的文件名就够了:

```python
file('文件名')
#打开一个文件赋值给变量f
f = file('data.txt')
#读取文件内容
data = f.read()
#输入文件内容
print data
#做完文件操作，记得一定要调用close()关闭文件
f.close()

#读取文件内容的方法还有
readline() #读取一行内容
readlines() #把内容按行读取至一个list中

```

如果想要写入内容，在打开文件的时候需要指定打开模式为写入：

```python
f = file('output.txt', 'w')
f.write('a string you want to write')
#write的参数可以是一个字符串，或者一个字符串变量。

data = 'I will be in a file.\nSo cool!'
out = open('output.txt', 'w')
out.write(data)
out.close()
```
'w'就是writing，以这种模式打开文件，原来文件中的内容会被你新写入的内容覆盖掉，如果文件不存在，会自动创建文件。
不加参数时，file为你默认为'r'，reading，只读模式，文件必须存在，否则引发异常。
另外还有一种模式是'a'，appending。它也是一种写入模式，但你写入的内容不会覆盖之前的内容，而是添加到文件中。

打开文件还有一种方法，就是open()，用法和file()是一致的。











 