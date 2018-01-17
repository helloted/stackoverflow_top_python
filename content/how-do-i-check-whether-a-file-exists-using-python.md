# 判断一个文件是否存在
[How do I check whether a file exists using Python?](https://stackoverflow.com/questions/82831/how-do-i-check-whether-a-file-exists-using-python)

___



> 1

如果你需要判断存在的原因是因为你想要做一些事情，比如 `if file_exists: open_it()`, 那么加一个 `try` 会比较安全.

如果你不打算立即打开文件，那么可以使用 [`os.path.isfile`](https://docs.python.org/2/library/os.path.html#os.path.isfile)

```python
import os.path
os.path.isfile(fname) 
```

如果你需要确认是个文件

```python
from pathlib import Path

my_file = Path("/path/to/file")
if my_file.is_file():
    # file exists
```

如果你需要确认是个文件夹

```python
if my_file.is_dir():
    # directory exists
```

去检测哪个路径是否存在文件或者文件夹：

```python
if my_file.exists():
    # path exists
```

同样，你也可以使用 `resolve()` in a `try` block:

```python
try:
    my_abs_path = my_file.resolve():
except FileNotFoundError:
    # doesn't exist
else:
    # exists
```