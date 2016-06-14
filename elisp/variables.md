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
局部变量仅应用于某段Lisp程序内部(一般应用于一个函数内)，通过**let**或者**let***这个
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
这里要注意多个变量最外层有一对(),否则会报  
Wrong number of arguments: (lambda (arg)  
变量可以是buffer-local bindings(只跟buffer有关)

## 变量为void与nil的区别
注意在elisp语言环境里，nil是一个lisp的对象，而说一个变量为void表示为unassigned
value，对一个void变量求值为报错void-variable error，而nil不会。

## 声明全局变量
一个变量的声明表示你将用一个symbol作为全局变量。采用两种Special Form来实现：
**defvar** 或者 **defconst**  

变量的声明有三层含义:  
1. 告诉阅读代码的人该symbol是一个特殊的用途（作为变量）  
2. 告诉Lisp系统可初始化，并有文档说明  
3. 提供一个编程的工具。  

defvar与defconst的主要区别在于用途，表示这个变量的值是否会变化。Lisp不会阻止你改变
用defconst来定义的变量。defconst是无条件初始化的。

### defvar
defvar语法如下：  
```elisp
defvar symbol [value [doc-string]]
```

### defconst
它定义一个symbol作为变量，并初始化，其语法如下:  
```elisp
defconst symbol value [doc-string]
```
