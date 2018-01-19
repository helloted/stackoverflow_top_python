# @staticmethod与@classmethod的区别
[What is the difference between @staticmethod and @classmethod in Python?](https://stackoverflow.com/questions/136097/what-is-the-difference-between-staticmethod-and-classmethod-in-python)

___



> 1

注意调用的不同 `foo`, `class_foo` and `static_foo`:

```python
class A(object):
    def foo(self,x):
        print "executing foo(%s,%s)"%(self,x)

    @classmethod
    def class_foo(cls,x):
        print "executing class_foo(%s,%s)"%(cls,x)

    @staticmethod
    def static_foo(x):
        print "executing static_foo(%s)"%x    

a=A()
```

下面是一个实例对象调用方法的最普遍用法，对于a这个实例对象，作为第一个参数被隐式传送

```
a.foo(1)
# executing foo(<__main__.A object at 0xb7dbef0c>,1)
```

如果是classmethod，对象实例的class才是第一个被隐式传递的参数，而不是self

```
a.class_foo(1)
# executing class_foo(<class '__main__.A'>,1)
```

你可以用类来调用`class_foo`方法，实际上，如果如果你定义了一个类方法，你应该想要从通过类来调用而不是通过类的实例来调用，`A.foo(1)` 会导致TypeError, 但是 `A.class_foo(1)` 可以的:

```
A.class_foo(1)
# executing class_foo(<class '__main__.A'>,1)
```

如果是**staticmethods**的话，`self` (实例对象) 或者 `cls` (类) 都不会作为第一个参数被隐式传递.就是平白地执行

```
a.static_foo(1)
# executing static_foo(1)

A.static_foo('hi')
# executing static_foo(hi) 
```

静态方法用于类与类具有某种逻辑连接的函数进行分组。



`foo` 只是一个函数, 但是当你调用 `a.foo` ，你不仅仅得到了这个函数，你同样获得了实例对象 `a` 绑定为函数的第一个参数， `foo` 需要两个参数,但是 `a.foo` 只需要一个.

```
print(a.foo)
# <bound method A.foo of <__main__.A object at 0xb7d52f0c>>
```

对于 `a.class_foo`, `a` 没有绑定到 `class_foo`, 而是 `A` 绑定到了 `class_foo`.

```
print(a.class_foo)
# <bound method type.class_foo of <class '__main__.A'>>
```

对于静态函数，尽管这是一个函数, `a.static_foo` 只会返回这个函数而不会绑定其他参数. `static_foo` 需要一个参数,  `a.static_foo` 也只需要一个参数。

```
print(a.static_foo)
# <function static_foo at 0xb7d479cc>
```

 `static_foo` 被 `A` 调用也是同样的结果

```
print(A.static_foo)
# <function static_foo at 0xb7d479cc>
```