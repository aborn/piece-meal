# 异步
elisp并没有提供好的异步操作，原生的语言级别只提供了一个创建异步的子进程的函数。

## 异步子进程
elisp提供了一个创建异步子进程的函数**start-process**，这个函数返回一个process
对象。该函数的语法如下：   
```elisp
start-process name buffer-or-name program &rest args
```
参数解释：
1. name 表示子进程的名字，如果该名字对应的子进程已经存在。那么它将名字变为name<1>,
这样使得它唯一。当然，如下name<1>也存在了，名字被修改为name<2>，以此类推；  
2. buffer-or-name 这个执行的子进程绑定的buffer名字，自然，子进程的执行结果也会
显示在这个buffer上；  
3. program 要执行的程序，如果program为nil，那么不创建子进程，只创建一个buffer,
同时，其他参数（args）也被无视；  
4. 
