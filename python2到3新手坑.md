#python 2到3的新手坑

##print
版本2的使用方法

```python
print 'this is version 2'
#或者
print('this is version 2')
```

版本2的使用方法，就只能加上括号，像一个函数一样来使用 print

```python
print('this is version 3')
```

##input
2里面有两个用来从命令行接受输入的函数：input 和 raw_input。

```python
value = input()
value = raw_input()
```
raw_input 接收的则是你输入的字符串，而不管你输的是什么内容。

在版本3里，为了减少混乱，这两种输入方式被合并了。只是合并的方式又坑了新手：它保留了 input 这个名字和 raw_input 的效果。3里只有input函数，它接收你输入的字符串，不管你输的是什么。

```python
text = input()
```

这种情况下，不管你是看着3的教材用2，还是看着2的教材用3，都会踩到这个坑。

那么在3里，如何像2一样得到用户输入的一个值呢？方法是 eval()：

```python
value = eval(input())
```
