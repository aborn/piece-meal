# 变量
变量是程序中的一个代表值的名字，在elisp中，变量通过lisp的symbol表示。变量名即为symbol的名，
变量的值存储在symbol对应的值空间。

## 全局变量
全局变量是应用于Lisp系统的所有地方。一次只能赋一个值，通过**setq**这个Special Form
来设置全局变量的值（这个过程也称之为绑定），如下：
```elisp
(setq x '(a b))
```
是设置全局变量x的值为(a b),注意：**setq**是一个Special Form,它不计算第一个参数（变量名），
它计算第二个参数，将结果作为新的值。

## set与setq
**set**是一个内置函数，而setq是一个Special Form,他们的区别看如下例子(他们的作用是等价的)：
```elisp
(setq a "aaa")
(set 'a "aaa")
```

## 检测变量是否被定义
检测变量是否被定义，采用**boundp**
```elisp
(boundp 'load-path)                     ; t
(boundp 'nil)                           ; t
(boundp 'xyz)                           ; nil
```

## 常量
有一种变量是自解析的，称之为常量。我们最常见的是**nil**和**t**这两个，还有一种是以':'开头
的，这些称之为原子(celled keywords),用keywordp函数可以判断是否为celled keywords:
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
变量可以是buffer-local bindings(只跟buffer有关),局部变量也可多次绑定，采用**setq**来进行
再次绑定。

## 变量为void与nil的区别
注意在elisp语言环境里，nil是一个lisp的对象。说一个变量为void，表示这个变量的值空间还没
被初始化(unassigned value)。对一个void变量求值为报错void-variable error，而nil不会。
采用**makunbound symbol**取消绑定，将一个变量变成void，这个函数返回该变量的symbol。
采用**boundp variable**来判断变量是否为void，当不为void时，返回*t*。

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
举例如下：
```elisp
(defconst float-pi 3.141592653589793 "The value of Pi.")
```

## 定义可定制化的变量(Defining Customization Variables)
可定制化的变量也称为用户选项(User Options),它是全局的Lisp变量,它的值可通过定制接口
来重新设置,采用**defcustom**这个宏来定义：
```elisp
defcustom option standard doc [keyword value]. . .
```
standard表示默认值（如果用户没设置时）。  
defcustom这个宏接收以下keyword
1. :type type 数据类型  
2. :options value-list 合法的取值列表  
3. :set setfunction 指定setfunction作为改变的方式  
4. :get getfunction 指定获得方式  
5. :initialize function 初始化函数  
..  
指定:require这个keyword非常有用，表明打开一种特性。
下面是一个例子
```elisp
(defcustom save-place nil
  "Non-nil means automatically save place in each file..."
  :type ’boolean
  :require ’saveplace
  :group ’save-place)
```

## 其他
