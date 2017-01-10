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
    