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

2、