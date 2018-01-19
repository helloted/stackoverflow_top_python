# list方法append VS. extend
[Difference between append vs. extend list methods in Python](https://stackoverflow.com/questions/252703/difference-between-append-vs-extend-list-methods-in-python)

___



> 1

```python
x = [1, 2, 3]
x.append([4, 5])
print (x)
```

得到的会是`[1, 2, 3, [4, 5]]`

```python
x = [1, 2, 3]
x.extend([4, 5])
print (x)
```

得到的是[1, 2, 3, 4, 5]