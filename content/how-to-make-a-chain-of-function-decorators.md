# 函数装饰器链
[How to make a chain of function decorators?](https://stackoverflow.com/questions/739654/how-to-make-a-chain-of-function-decorators)

___



> 1

```
def makebold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"
    return wrapped

def makeitalic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"
    return wrapped

@makebold
@makeitalic
def hello():
    return "hello world"

print hello() ## returns "<b><i>hello world</i></b>"
```