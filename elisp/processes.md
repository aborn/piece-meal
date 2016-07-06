# 进程process
emacs可以创建两种类型的子进程，即同步或异步。如果创建的是一个同步的子进程，lisp程序等待子进程
执行结束后继续执行。异步的子进程不需要等待，它们是同步执行。异步子进程是一个elisp的object,称
之为process。可以给这个process对象发送信号，获得子进程状态，或者收到其输出结果。  
```elisp
(processp object)
```

## 创建子进程的函数
有三个函数可以创建子进程，即**start-process**(异步，返回一个process对象),**call-process**
,**call-process-region**，后两个是同步的，不返回process对象。

## 创建异步子进程
