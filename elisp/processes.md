# 进程process
从操作系统的角度来说，一个进程就是一个程序的可执行空间。
emacs可以创建两种类型的子进程：同步、异步。当你创建的是一个同步的子进程，
lisp程序等待子进程执行结束后继续执行。异步的子进程不需要等待，它们是并行执行。
异步子进程在emacs中是用对象表示，我们把这个对象称
之为process。可以给这个process对象发送信号，获得子进程状态，或者收到其输出结果。
判断对象是否为process，调用如下函数：  
```elisp
(processp object)
```

## 常用与Process有关的函数
```elisp
(get-process "process-name")   ;; 通过process名字取到process对象
```

## 创建子进程的函数
有三个函数可以创建子进程，即**start-process**(异步，返回一个process对象)、
**call-process**、**call-process-region**，后两个是同步的，不返回process对象。

## 创建异步子进程
关于elisp的异步，请参考我写的这篇博客
