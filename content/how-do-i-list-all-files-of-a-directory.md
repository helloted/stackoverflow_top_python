# 列出一个文件夹中的所有文件
[How do I list all files of a directory?](https://stackoverflow.com/questions/3207219/how-do-i-list-all-files-of-a-directory)

___



> 1

[`os.listdir()`](https://docs.python.org/2/library/os.html#os.listdir) 可以获取一个文件夹中的所有东西

如果你想要文件，你可以用下面这种

```python
from os import listdir
from os.path import isfile, join
onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]
```

或者你可以用[`os.walk()`](https://docs.python.org/2/library/os.html#os.walk) 

```python
from os import walk

f = []
for (dirpath, dirnames, filenames) in walk(mypath):
    f.extend(filenames)
    break
```

最后，如例子所示，除了用 [`.extend()`](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) 把一个list加入到另外一个list中，你还可以用

```python
>>> q = [1, 2, 3]
>>> w = [4, 5, 6]
>>> q = q + w
>>> q
[1, 2, 3, 4, 5, 6]
```

> 2

用glob模块

```python
import glob
print(glob.glob("/home/adam/*.txt"))
```

会返回一个list:

```python
['/home/adam/file1.txt', '/home/adam/file2.txt', .... ]
```