# files 文件

## 文件操作函数

### 判断文件是否存在
判断文件是否存在，采用函数**file-exists-p**，语法如下：
```elisp
file-exists-p filename
```
如果文件不存在，或者没有访问权限则返回**nil**；否则返回**t**
文件是否可读，可执行，可写，对应以下三个函数：
```
file-readable-p filename
file-executable-p filename
file-writable-p filename
```


## 文件夹操作函数
