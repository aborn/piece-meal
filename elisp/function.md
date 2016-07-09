# function

## 什么是函数？
函数是有传入参数的可计算的规则。计算的结果为函数返回值。大部分计算机语言里，
函数是有一个名字的。从严格意义来说，lisp函数是没有名字的。注意：函数也是一个lisp对象，把这个对象关联到一个symbol,
这个symbol就是函数名

## 函数定义
定义一个函数的语法如下：
```elisp
defun name args [doc] [declare] [interactive] body. . .
```
