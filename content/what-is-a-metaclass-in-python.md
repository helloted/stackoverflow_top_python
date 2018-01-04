# Python中的metaclass
[What is a metaclass in Python?](https://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python)

___



> 1

一个metaclass，称为元类，是一个类的'类'，如同一个类是定义了一个实例对象的行为，一个metaclass定义了一个类的行为。类是metaclass的实例。

![img](/images/02.png)

在python中，你可以使用任何可调用的元类，更有用的方法则是使其成为一个实际的类本身。 `type` 在python中是一个有用的元类，你无法重新创建一个类似于type那样纯粹的东西，但是Python有小小的作弊。要创建你自己的元类，你只需要一个子类。

一个元类在作为类工厂方法是最为常用，就如同你通过调用一个类来创建这个类的实例，Python通过调用元类方法来创建一个新的类。与寻常的 `__init__` 和 `__new__` 方法相比，元类允许你在创建类时做其他事，比如注册新类，甚至于完整地替换这个类。

当类语句被执行时，Python首先像执行一个普通的代码块一样地执行类语句的主体， 由此产生的命名空间（一个字典）保存类的属性。元类的确定，是通过查看类（元类是继承的）的基类，__metaclass__全局变量的__metaclass__属性。 元类然后调用类的名称，基类和属性来实例化它。

然而，元类实际上定义了一个类的类型，而不仅仅是一个工厂方法，所以你可以做更多的事情。 例如，您可以在元类上定义常规方法。 这些元类方法就像类方法，因为它们可以在没有实例的情况下在类上调用，但是它们也和类方法有不同，因为它们不能在类的实例上调用。 `type.__subclasses__()`是元类方法的一个例子。 您还可以定义常规的“魔术”方法，如`__add__`, `__iter__` and `__getattr__`,以实现或更改类的行为方式。

下面是汇总示例：

```python
def make_hook(f):
    """Decorator to turn 'foo' method into '__foo__'"""
    f.is_hook = 1
    return f

class MyType(type):
    def __new__(cls, name, bases, attrs):

        if name.startswith('None'):
            return None

        # 查看属性看看是否需要被重命名
        newattrs = {}
        for attrname, attrvalue in attrs.iteritems():
            if getattr(attrvalue, 'is_hook', 0):
                newattrs['__%s__' % attrname] = attrvalue
            else:
                newattrs[attrname] = attrvalue

        return super(MyType, cls).__new__(cls, name, bases, newattrs)

    def __init__(self, name, bases, attrs):
        super(MyType, self).__init__(name, bases, attrs)

        # classregistry.register(self, self.interfaces)
        print "Would register class %s now." % self

    def __add__(self, other):
        class AutoClass(self, other):
            pass
        return AutoClass
        # Alternatively, to autogenerate the classname as well as the class:
        # return type(self.__name__ + other.__name__, (self, other), {})

    def unregister(self):
        # classregistry.unregister(self)
        print "Would unregister class %s now." % self

class MyObject:
    __metaclass__ = MyType


class NoneSample(MyObject):
    pass

# Will print "NoneType None"
print type(NoneSample), repr(NoneSample)

class Example(MyObject):
    def __init__(self, value):
        self.value = value
    @make_hook
    def add(self, other):
        return self.__class__(self.value + other.value)

# Will unregister the class
Example.unregister()

inst = Example(10)
# Will fail with an AttributeError
#inst.unregister()

print inst + inst
class Sibling(MyObject):
    pass

ExampleSibling = Example + Sibling
# ExampleSibling is now a subclass of both Example and Sibling (with no
# content of its own) although it will believe it's called 'AutoClass'
print ExampleSibling
print ExampleSibling.__mro__
```

