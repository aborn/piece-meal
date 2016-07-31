# 列表操作
对于列表(List)，有很多相关的操作，如获取列表长度(length list)。下面介绍其相关操作

## mapcar和mapc
* **mapcar**的语法如下：
```elisp
(mapcar function sequence) 
```
它的作用是将function函数应用到sequence中的每个元素，然后返回一个结果列表。
```elisp
(mapcar '1+ (list 1 2 3 4)) ; (2 3 4 5)
(mapcar 'car '((1 2) (3 4) (5 6))) ; (1 3 5)
```
mapc和mapcar操作一样，只不过，它返回的是nil

## while操作
```elisp
(let ((myList '(a b c)))
  (while myList
    (message "%s" (pop myList))
    (sleep-for 1)))
```

## 对列表元素的操作

### 获取列表元素
* (car list) 获取列表第一个元素
* (nth n list) 获取列表第n个元素
* (car (last list)) 获取列表最后一个元素

### 获取子列表
* (cdr list) 第二个到最后一个元素构成的列表
* (nthcdr n list) 第n个到最后一个元素构成的列表
* (butlast list n) 除去最后n个元素剩余的列表
以上操作只会生成一个新的列表，不会对老列表进行改变。

### 插入元素到列表头
* (cons x list) 返回一个新的列表newList,其中x为(car newList),list为(cdr list)
注意不会改变原列表。

### 改变列表元素
* (push x list) 添加元素到列表头，会改变原list，返回新的列表。注意返回的列表与原列表相等。
与之相反的有一个pop操作
```elisp
ELISP> (setq ab/debug '("a" "b" "c"))
("a" "b" "c")

ELISP> (setq ab/debug2 (push 'a ab/debug))
(a "a" "b" "c")

ELISP> (eq ab/debug ab/debug2)
t
ELISP> (pop ab/debug)
a
ELISP> ab/debug
("a" "b" "c")

ELISP> ab/debug2
(a "a" "b" "c")
```
* (setcar list x) 用x元素替换list的第一个元素，返回x，与之类似的有(setcdr list x)。

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
