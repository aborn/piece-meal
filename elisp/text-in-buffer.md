# buffer中的文本操作


## 获焦点附近文本

### char-after
该函数的语法为：
```elisp
char-after &optional position
```
该函数返回当前buffer在焦点position后（当前字符）的字符。类似的，获得焦点前的字符，采用
**char-before**函数。

### following-char
语法为，没有参数，与**(char-after (point))**等价。
```elisp
following-char
```
类似的**precding-char**为前一个。


## 获得buffer的内容
