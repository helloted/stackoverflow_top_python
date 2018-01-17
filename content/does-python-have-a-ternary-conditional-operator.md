# Python的三元运算
[Does Python have a ternary conditional operator?](https://stackoverflow.com/questions/394809/does-python-have-a-ternary-conditional-operator)

___



> 1

格式是

```python
a if condition else b
```

首先 `condition` 是判断条件, 然后 `a` or `b` 返回值，基于 `condition` [Boolean](https://en.wikipedia.org/wiki/Boolean_data_type) 

如果 `condition` 鉴定是 *True* `a` 返回, 否则 `b` 返回.

举例

```Python
>>> 'true' if True else 'false'
'true'
>>> 'true' if False else 'false'
'false'
```