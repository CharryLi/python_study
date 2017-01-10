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
