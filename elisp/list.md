# 列表操作

## 对列表元素的操作

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
