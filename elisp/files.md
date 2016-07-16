# files文件

## 文件操作函数

### 判断文件是否存在
判断文件是否存在，采用函数**file-exists-p**，语法如下：
```elisp
file-exists-p filename
```
如果文件不存在，或者没有访问权限则返回**nil**；否则返回**t**
文件是否可读，可执行，可写，对应以下三个函数：
```elisp
file-readable-p filename
file-executable-p filename
file-writable-p filename
```

## 文件夹操作函数
* 创建文件夹**make-directory**,当文件夹不存在时:
```elisp
make-directory dirname &optional parents
```
最后一个参数*parent*如果non-nil，刚循环创建其parent directory.

## 文件路径操作
**expand-file-name**，这个函数是将文件名转换成一个绝对文件名，语法如下：
```elisp
expand-file-name filename &optional directory
```
下面是一些例子：
```
(expand-file-name "foo")
;; "/xcssun/users/rms/lewis/foo"
(expand-file-name "../foo")
;; "/xcssun/users/rms/foo"
(expand-file-name "foo" "/usr/spool/")
;;"/usr/spool/foo"
```
注意：当参数**directory**没有提供的时候，directory值会采用
**default-directory**的值。
