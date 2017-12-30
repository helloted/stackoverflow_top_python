# Python中的metaclass
[What is a metaclass in Python?](https://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python)

___



> 1

一个metaclass是一个类的'类'，如同一个类是定义了一个实例对象的行为，一个metaclass定义了一个类的行为。类是metaclass的实例。

![img](/images/02.png)

While in Python you can use arbitrary callables for metaclasses (like [Jerub](https://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python/100037#100037) shows), the more useful approach is actually to make it an actual class itself. `type` is the usual metaclass in Python. In case you're wondering, yes, `type` is itself a class, and it is its own type. You won't be able to recreate something like `type` purely in Python, but Python cheats a little. To create your own metaclass in Python you really just want to subclass `type`.

在python中，你可以使用任何可调用