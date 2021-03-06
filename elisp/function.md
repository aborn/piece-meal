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

## 检查一个函数是否定义
检查一个函数是否定义
```elisp
(fboundp 'info)                         ; t
(fboundp 'setq)                         ; t
(fboundp 'xyz)                          ; nil
```

## 函数参数
有些参数是可选的，当用户没有传是，设置一个默认值，下面是一个例子：
```elisp
(defun piece-meal/fun-option-parameter (a &optional b)
  (when (null b)
    (message "paramete b is not provided")
    (setq b "ddd"))    ;; set to default value
  (message "a=%s, b=%s" a b))
```

## 函数调用
函数的调用有两种方式，**funcall**和**apply**
