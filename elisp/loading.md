# 载入
载入一个文件意味着将内容作为Lisp Object读取到lisp运行环境中

## 程序loading

## load函数
```
load filename &optional missing-ok nomessage nosu x must-su x
```
这个函数查找到并打开filename对应的内容，并对其求值，最后再关闭这个文件.

### 如何查找？
1. 第一步找下filename.elc是否存在，若存在，则load之  
2. 如果第一步没找到再找filename.el文件  
3. 最后再找没有任何后缀的filename文件  
4. 找.gz的压缩文件
