1、在Python中调用外部命令

```python
from subprocess import call
call(["ls", "-l"])
```

或者

```python
import os
os.system("your command")
```

2、for循环获取index

```python
for idx, val in enumerate(list):
    print(idx, val)
```

3、list里值的index

```python
>>> ["foo", "bar", "baz"].index("bar")
1
```

