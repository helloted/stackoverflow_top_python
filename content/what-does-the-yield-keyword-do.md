# yield关键字作用？
[What does the “yield” keyword do?](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do)

___



> 1

要理解 `yield` , 你首先要理解什么是生成器(*generators*). 在讨论生成器(*generators*)之前我们先看看迭代器( *iterables*).

#### 迭代器( *iterables*)

当你创建了一个list，你可以一个接一个地读取里面的元素，这种就叫做迭代(iteration)

```python
>>> mylist = [1, 2, 3]
>>> for i in mylist:
...    print(i)
1
2
3
```

`mylist` 是一个迭代器. 当你使用一个list时, 你创建一个list的同时，创建了一个迭代器

```
>>> mylist = [x*x for x in range(3)]
>>> for i in mylist:
...    print(i)
0
1
4
```

你可以使用"`for... in...`"在任何迭代器上，`lists`, `strings`, 文件等等...

这种迭代器很方便，因为您可以随意地读取它们，但是你将所有值存储在内存中，当有很多值时，您并不总是得到想要的值。

#### 生成器(*generators*)

生成器属于迭代器，是一种只能迭代一次的迭代器，生成器不会将所有的值存储到内存中，生成器会在需要的时候立即生成值。

```python
>>> mygenerator = (x*x for x in range(3))
>>> for i in mygenerator:
...    print(i)
0
1
4
```

除了用 `()` 替换 `[]`，其他都一样，但是，你不能再次运行 `for i in mygenerator` ，因为生成器只能用一次：算出 0, 然后忘掉再计算出 1, 然后再计算出 4, 一个接一个

`yield` 是一个类似于 `return`的关键字，除了它的功能是返回一个生成器。

```python
>>> def createGenerator():
...    mylist = range(3)
...    for i in mylist:
...        yield i*i
...
>>> mygenerator = createGenerator() # create a generator
>>> print(mygenerator) # mygenerator is an object!
<generator object createGenerator at 0xb7555c34>
>>> for i in mygenerator:
...     print(i)
0
1
4
```

要理解 `yield`, 你必须明白：当你调用这个函数，这个函数里的代码并没有运行，这个函数只是返回了一个生成器对象 。

下面难的部分：

for循环第一次调用这个生成器对象时，它会从创建这个生成器的函数的开始运行直到yield，然后返回循环的第一个值，然后每一次调用生成器，都会运行创建函数里的循环一次，然后返回下一个值。一直到没有值返回