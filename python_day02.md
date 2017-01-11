#Python Day02

##break
跳出循环，直接上代码：

```python
while True:
   a = raw_input()
   if a == 'EOF':
       break
       
for i in range(10):
   a = raw_input()
   if a == 'EOF':
       break
```

##continue
break是彻底地跳出循环，而continue只是略过本次循环的余下内容，直接进入下一次循环。

```python
for score in data[1:]:
   point = int(score)
   if point < 60:
       continue
   sum += point
```

##异常处理
语法

    try:
        可能会出现异常的代码
    except:
        出现异常后执行的代码

代码

```python
try:
   f = file('non-exist.txt')
   print 'File opened!'
   f.close()
except:
   print 'File not exists.'
print 'Done'

```

##字典（dictionary）
在字典中，名字叫做“键”，对应的内容信息叫做“值”。字典就是一个键/值对的集合。它的基本格式是（key是键，value是值）：

```python
#键/值对用冒号分割，每个对之间用逗号分割，整个字典包括在花括号中。
d = {key1 : value1, key2 : value2 }
```

关于字典的键要注意的是：

1. 键必须是唯一的；
2. 键只能是简单对象，比如字符串、整数、浮点数、bool值。

list就不能作为键，但是可以作为值。

举个简单的字典例子：

```python
score = {
   '萧峰': 95,
   '段誉': 97,
   '虚竹': 89
}
```

python字典中的键/值对没有顺序，我们无法用索引访问字典中的某一项，而是要用键来访问。

```python
print score['段誉']
```

注意，如果你的键是字符串，通过键访问的时候就需要加引号，如果是数字作为键则不用。

字典也可以通过for...in遍历：

```python
#注意，遍历的变量中存储的是字典的键
for name in score:
   print score[name]
   
#如果要改变某一项的值，就直接给这一项赋值
score['虚竹'] = 91

#增加一项字典项的方法是，给一个新键赋值
score['慕容复'] = 88

#删除一项字典项的方法是del,注意，这个键必须已存在于字典中
del score['萧峰']

#如果你想新建一个空的字典，只需要
d = {}
```

##模块
通俗点讲就是函数库，如何引用呢
    
    import random
    
import语句告诉python，我们要用random模块中的内容。然后便可以使用random中的方法，比如：

    random.randint(1, 10)
    random.choice([1, 3, 5])
    
注意，函数前面需要加上“random.”，这样python才知道你是要调用random中的方法。

想知道random有哪些函数和变量，可以用dir()方法：

    dir(random)
    
如果你只是用到random中的某一个函数或变量，也可以通过from...import...指明：

    from math import pi
    print pi
    
为了便于理解和避免冲突，你还可以给引入的方法换个名字：
    
    from math import pi as math_pi
    print math_pi
    
##函数的默认参数
定义一个函数

```python
def hello(name):
   print 'hello ' + name
```
然后我们去调用这个函数

```python
hello('world')
```
程序就会输出

    hello world
    

如果很多时候，我们都是用world来调用这个函数，少数情况才会去改参数。那么，我们就可以给这个函数一个默认参数：

```python
def hello(name = 'world'):
   print 'hello ' + name
```

注意，当函数有多个参数时，如果你想给部分参数提供默认参数，那么这些参数必须在参数的末尾。比如：

```python
def func(a, b=5)#是正确的
def func(a=5, b)#就会出错
```

##函数的参数传递
定义：

```python
def func(arg1, arg2):
	print arg1, arg2
```
调用

```python
func(3, 7)
```
我们把函数定义时的参数名（arg1、arg2）称为形参，调用时提供的参数（3、7）称为实参。

这种方式是根据调用时提供参数的位置进行匹配，要求实参与行参的数量相等，默认按位置匹配参数。调用时，少参数或者多参数都会引起错误。这是最常用的一种函数定义方式。

在调用时，也可以根据形参的名称指定实参。如：

```python
func(arg2=3, arg1=7)
```
但同样，必须提供所有的参数。

Python 语言还提供了其他一些更灵活的参数传递方式，如：

```python
func2(a=1, b=2, c=3)
func3(*args)
func4(**kargs)
```
> func2这种方式：func2(a=1, b=2, c=3)

这种方式可以理解为，在一般函数定义的基础上，增加了参数的默认值。这样定义的函数可以和原来一样使用，而当你没有提供足够的参数时，会用默认值作为参数的值。

例如：

```python
def func(arg1=1, arg2=2, arg3=3):
	print arg1, arg2, arg3
	
#调用
func(2, 3, 4)
func(5, 6)
func(7)
```
输出：

    2 3 4
    5 6 3
    7 2 3
    
提供的参数会按顺序先匹配前面位置的参数，后面未匹配到的参数使用默认值。

也可以指定其中的部分参数，如：

```python
func(arg2=8)
func(arg3=9, arg1=10)
```

输出为

    1 8 3
    10 2 9
    
或者混合起来用：

```python
func(11, arg3=12)
```
输出为

    11 2 12
    
但要注意，没有指定参数名的参数必须在所有指定参数名的参数前面，且参数不能重复。以下的调用都是错误的：

```python
func(arg1=13, 14)
func(15, arg1=16)
```

> func3这种方式：func3(*args)

这种方式的厉害之处在于，它可以接受任意数量的参数。来看具体例子：

```python
def calcSum(*args):
	sum = 0
	for i in args:
		sum += i
	print sum

```
调用：

```python
calcSum(1,2,3)
calcSum(123,456)
calcSum()
```
输出：

    6
    579
    0

在变量前加上星号前缀（*），调用时的参数会存储在一个 tuple（元组）对象中，赋值给形参。在函数内部，需要对参数进行处理时，只要对这个 tuple 类型的形参（这里是 args）进行操作就可以了。因此，函数在定义时并不需要指明参数个数，就可以处理任意参数个数的情况。

不过有一点需要注意，tuple 是有序的，所以 args 中元素的顺序受到赋值时的影响。

> func4这种方式：func4(**kargs)

上次说的 func(\*args) 方式是把参数作为 tuple 传入函数内部。而 func(\*\*kargs) 则是把参数以键值对字典的形式传入。

示例：

```python
def printAll(**kargs):
	for k in kargs:
		print k, ':', kargs[k]

printAll(a=1, b=2, c=3)
printAll(x=4, y=5)
```

输出

```python
a : 1
c : 3
b : 2
y : 5
x : 4
```
字典是无序的，所以在输出的时候，并不一定按照提供参数的顺序。同样在调用时，参数的顺序无所谓，只要对应合适的形参名就可以了。于是，采用这种参数传递的方法，可以不受参数数量、位置的限制。

当然，这还不够。Python 的函数调用方式非常灵活，前面所说的几种参数调用方式，可以混合在一起使用。看下面这个例子：

```python
def func(x, y=5, *a, **b):
print x, y, a, b

func(1)
func(1,2)
func(1,2,3)
func(1,2,3,4)
func(x=1)
func(x=1,y=1)
func(x=1,y=1,a=1)
func(x=1,y=1,a=1,b=1)
func(1,y=1)
func(1,2,3,4,a=1)
func(1,2,3,4,k=1,t=2,o=3)
```
输出

```python
1 5 () {}
1 2 () {}
1 2 (3,) {}
1 2 (3, 4) {}
1 5 () {}
1 1 () {}
1 1 () {'a': 1}
1 1 () {'a': 1, 'b': 1}
1 1 () {}
1 2 (3, 4) {'a': 1}
1 2 (3, 4) {'k': 1, 't': 2, 'o': 3}
```
在混合使用时，首先要注意函数的写法，必须遵守：
带有默认值的形参(arg=)须在无默认值的形参(arg)之后；
元组参数(\*args)须在带有默认值的形参(arg=)之后；
字典参数(\*\*kargs)须在元组参数(*args)之后。

可以省略某种类型的参数，但仍需保证此顺序规则。

调用时也需要遵守：
指定参数名称的参数要在无指定参数名称的参数之后；
不可以重复传递，即按顺序提供某参数之后，又指定名称传递。

而在函数被调用时，参数的传递过程为：
1.按顺序把无指定参数的实参赋值给形参；
2.把指定参数名称(arg=v)的实参赋值给对应的形参；
3.将多余的无指定参数的实参打包成一个 tuple 传递给元组参数(\*args)；
4.将多余的指定参数名的实参打包成一个 dict 传递给字典参数(\*\*kargs)。


##对象和类
关键字class加上类名用来创建一个类。之后缩进的代码块是这个类的内部。在这里，我们用pass语句，表示一个空的代码块。

```python
class MyClass:
    pass

mc = MyClass()
print mc
```

输出结果：

    <__main__.MyClass instance at 0x7fd1c8d01200>
    
这个意思就是说，mc是__main__模块中MyClass来的一个实例（instance），后面的一串十六进制的数字是这个对象的内存地址。

给这个类加上一些域：

```python
class MyClass:
    name = 'Sam'

    def sayHi(self):
        print 'Hello %s' % self.name

mc = MyClass()
print mc.name
mc.name = 'Lily'
mc.sayHi()
```

MyClass类增加了一个类变量name，并把它的值设为'Sam'。然后又增加了一个类方法sayHi。调用类变量的方法是“对象.变量名”。你可以得到它的值，也可以改变它的值。

注意到，类方法和我们之前定义的函数区别在于，第一个参数必须为self。而在调用类方法的时候，通过“对象.方法名()”格式进行调用，而不需要额外提供self这个参数的值。self在类方法中的值，就是你调用的这个对象本身。

输出结果：

    Sam
    Hello Lily

之后，在你需要用到MyClass这种类型对象的地方，就可以创建并使用它。

##类继承
Vehicle类被称为基本类或超类，Car类和Bike类被成为导出类或子类。

```python
#父类
class Vehicle:
	#构造函数
    def __init__(self, speed):
        self.speed = speed

    def drive(self, distance):
        print 'need %f hour(s)' % (distance / self.speed)

#子类Bike继承自Vehicle
class Bike(Vehicle):
    pass

#子类Car继承自Vehicle
class Car(Vehicle):
    def __init__(self, speed, fuel):
        Vehicle.__init__(self, speed)
        self.fuel = fuel

    def drive(self, distance):
        Vehicle.drive(self, distance)
        print 'need %f fuels' % (distance * self.fuel)

b = Bike(15.0)
c = Car(80.0, 0.012)
b.drive(100.0)
c.drive(100.0)

```

##and or
看下代码就明白了，有学过c/c++/java的同学应该会发现，三元运算符（bool?a:b）

```python
a = "heaven"
b = "hell"
c = True and a or b
print c
d = False and a or b
print d
```
输出
    
    heaven
    hell

##元组
元组（tuple）也是一种序列，和我们用了很多次的list类似，只是元组中的元素在创建之后就不能被修改，比如：

```python
postion = (1, 2)
geeks = ('Sheldon', 'Leonard', 'Rajesh', 'Howard')
```
都是元组的实例。它有和list同样的索引、切片、遍历等操作

```python
print postion[0]
for g in geeks:
    print g
print geeks[1:3]
```
其实我们之前一直在用元组，就是在print语句中：

```python
print '%s is %d years old' % ('Mike', 23)
```
('Mike', 23)就是一个元组, 这是元组最常见的用处

```python
def get_pos(n):
    return (n/2, n*2)
```
得到这个函数的返回值有两种形式，一种是根据返回值元组中元素的个数提供变量：

```python
x, y = get_pos(50)
print x
print y
```
还有一种方法是用一个变量记录返回的元组：

```python
pos = get_pos(50)
print pos[0]
print pos[1]
```
