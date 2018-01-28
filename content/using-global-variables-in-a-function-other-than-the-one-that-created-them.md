# 全局变量的使用
[Using global variables in a function other than the one that created them](https://stackoverflow.com/questions/423379/using-global-variables-in-a-function-other-than-the-one-that-created-them)

___



> 1

您可以在其他函数中使用全局变量，方法是要赋值给它的每个函数中将其声明为全局变量：

```python
globvar = 0

def set_globvar_to_one():
    global globvar    # 需要声明为全局变量如果需要赋值
    globvar = 1

def print_globvar():
    print(globvar)     # 如果只是取值不需要声明为全局变量

set_globvar_to_one()
print_globvar()       # Prints 1
```

因为全局变量非常危险，所以Python希望通过明确地声明`global`关键字来确保你确实知道你在做什么。