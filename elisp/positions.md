# positions位置
位置是在一个buffer中文本字符的坐标。更精确一点，位置是指两个字符之间。不过，我们经常说某个字符
在某个位置，意思这个字符在这个位置之后。位置常常用int值代表（从1开始），也可以用markers表示。

## 操作函数
1. **point**这个函数返回当前buffer当前位置的值。
2. **point-min**这个函数返回当前buffer最小可获取区域的值
3. **point-max**这个函数返回当前buffer最大可获取区域的值


## 移动
 **goto-char**,语法格式为:  
 ```elisp
 goto-char position
 ```
 将当前位置值设置为新的position值。

**forward-char**向前移动当前位置count字符:  
```elisp
forward-char &optional count
```
有一个相对应的**backward-char**函数
