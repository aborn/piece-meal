# 变量
本节note主要学习elips的变量

## 全局变量
全局变量是应用于Lisp系统的所有地方，一次只能是一个值，通过**setq**这个Special Form
来表示，如下：
```elisp
(setq x '(a b))
```
是设置全局变量x的值为(a b)

## 常量
有一种变量是自解析的，称之为常量。我们最常见的是**nil**和**t**这两个，还有一种是以':'开头
的，这些称之为celled keywords,用keywordp函数可以判断是否为celled keywords:
```elisp
(keywordp obj)
```

## 局部变量
局部变量仅应用于某段Lisp程序内部(一般应用于一个函数内)，通过**let**或者**let\***这个
Special Form来定义局部变量：下面是两个例子，
```
(setq y 2)

(let ((y 1)
     (z y))
     (list y z));   结果是 (1 2),因为y采用的是全局的那个值

(let* ((y 1)
     (z y))
    (list y z));    结果是 (1 1),因为y采用的是局部的那个值，这就是let*与let的区别
```
