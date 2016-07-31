# 列表操作

## 对列表元素的操作

### 获取列表元素
* (car list) 获取列表第一个元素
* (nth n list) 获取列表第n个元素
* (car (last list)) 获取列表最后一个元素

### 获取子列表
* (cdr list) 第二个到最后一个元素构成的列表
* (nthcdr n list) 第n个到最后一个元素构成的列表
* (butlast list n) 除去最后n个元素剩余的列表

### 插入元素到列表头
* (cons x list) 返回一个新的列表newList,其中x为(car newList),list为(cdr list)

### 添加元素到列表
添加元素到列表有以下几种方式：
* 用**add-to-list**函数
```elisp
add-to-list symbol element &optional append compare-fn
```
功能为当element不在symbol对应的list中时，添加element元素到symbol对应的list。
下面为一个例子：
```elisp
ELISP> (setq ab/debug '(("a" . "b") ("b" . "b")))
(("a" . "b")
 ("b" . "b"))

ELISP> (add-to-list 'ab/debug '("c" . "c"))
(("c" . "c")
 ("a" . "b")
 ("b" . "b"))
```
默认情况是添加到列表头，要想添加到列表尾，那么append参数为t，下面是一个例子:
```elisp
ELISP> (setq ab/debug '(("a" . "b") ("b" . "b")))
(("a" . "b")
 ("b" . "b"))

ELISP> (add-to-list 'ab/debug '("c" . "c") t)
(("a" . "b")
 ("b" . "b")
 ("c" . "c"))
```

* 采用*cl-lib*库，这个库中有一个对应的函数叫*cl-pushnew*：
```elisp
(cl-pushnew X PLACE [KEYWORD VALUE]...)
```
插入元素X到PLACE,举个例子：
```elisp
ELISP> (setq ab/debug '(("a" . "b") ("b" . "b")))
(("a" . "b")
 ("b" . "b"))
ELISP> (cl-pushnew '("c" . "c") ab/debug)
(("c" . "c")
 ("a" . "b")
 ("b" . "b"))
```
注意：cl-pushnew这个函数返回的对象就是*PLACE*。

* 另一个函数*push*也一样
```
ELISP> (push '("c" . "c") ab/debug)
(("c" . "c")
 ("a" . "b")
 ("b" . "b"))
```
