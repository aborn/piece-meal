# elisp的异步
elisp并没有提供好的异步操作，原生的语言级别只提供了一个创建异步子进程的函数。

## 异步子进程
elisp提供了一个创建异步子进程的函数**start-process**，这个函数返回一个process对象。该函数的语法如下：   
```elisp
start-process name buffer-or-name program &rest args
```
参数解释：  
1. name 表示子进程的名字，如果该名字对应的子进程已经存在。那么它将被修改为name<1>，这样使得它名字唯一。当然，如果name<1>也存在了，名字将被修改为name<2>，以此类推；  
2. buffer-or-name 与子进程相关联的buffer名字，并且，子进程的执行结果也会显示在这个buffer上；  
3. program 为要执行的程序，如果program为nil，那么不创建子进程，只创建一个buffer；同时，其他参数（args）也被无视；  
4. args 其他参数，将作为program的参数。  

下面举一个例子：  
```elisp
(defun ab/test-start-process ()
  "test aysnc proecess"
  (interactive)
  (start-process "test-start-process" "*tsp*" "ls"
                 "-l" (file-truename "~/.spacemacs.d")))
```
然后，执行的结果将显示在\*tsp*这个buffer里  
![异步子进程的结果\*tsp\*内容](http://upload-images.jianshu.io/upload_images/297930-f0ec6e01dc33abf8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## process对象的操作
获得当前正在运行中的子进程列表，可采用**list-processes**这个函数，如下：
![运行中的子进程列表](http://upload-images.jianshu.io/upload_images/297930-074e0a9a1423ff9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
对start-process函数返回的process对象，elisp提供了以下操作函数：
* 通过子进程名获得process对象，如果进程不存在，则返回nil
```elisp
get-process name
```
* 获得子进程的状态信息
```elisp
process-status process-name
```
它的参数可为**子进程对象**，**子进程名**，**子进程对应的buffer**。这个函数返回的结果可能为：run/stop/exit/singal/open/closed/connect/failed/listen/nil。  
* 子进程是否alive
```elisp
process-live-p process
```
如果子进程仍在alive，则返回non-nil。当一个子进程的状态为run, open, listen, connect 或 stop时，它被认为是alive的。  
其他操作函数请参照手册。
* 子进程退出时的状态信息，如果子进程仍在alive，刚返回0
```elisp
process-exit-status process
```

## async包
通过以上我们发现异操作真是很繁琐。要是我想异步地执行一个lamda函数？怎么办？  
答：采用[async](https://github.com/jwiegley/emacs-async)这个异步包。该包可通过[melpa](https://melpa.org/#/async)和[popkit elpa](https://elpa.popkit.org/#/async)软件源安装。
它显然是一个更好的选择。它的使用语法如下：  
```elisp
async-start START-FUNC FINISH-FUNC
```
其中第一个参数是子进程要执行的lambda函数，第二个参数为回调函数：  
下面是其说明文档里给的一个例子：
```elisp
(async-start
 ;; 在子进程中要执行的lambda函数
 (lambda ()
   (message "This is a test")
   (sleep-for 3)  ;; 休眠3s
   222)

 ;;当子进程执行完成后要执行的回调，子进程执行的结果将作为回调函数的参数
 (lambda (result)
   (message "Async process done, result should be 222: %s" result)))
```
如果去读async的源代码，你会发现它本质上调用的还是**start-process**这个函数。不过，它通过
调用**start-process**启动了一个emacs子进程来执行lambda函数。所以，导致的一个问题是，
通过async-start创建的emacs子进程并没有继承当前emacs运行环境的上下文（context）。
下面举一个我自己写的例子（用于异步更新本地repo）：
```elisp
(defun ab/git-code-update ()
  "update code async."
  (interactive)
  (async-start
   ;; 异步执行更新code操作
   (lambda ()
     (add-to-list 'load-path "~/.spacemacs.d/parts")
     (require 'aborn-log)
     (ab/log "exec-when-emacs-boot....")
     (let ((ab--git-project-list
            '("~/.emacs.d/" "popkit" "~/.spacemacs.d/" "piece-meal" "pelpa" "eden")))
       (dolist (elt ab--git-project-list)
         (let* ((working-directory
                 (if (or (string-prefix-p "/" elt) (string-prefix-p "~" elt))
                     elt
                   (concat "~/github/" elt "/")))
                (default-directory working-directory))
           (ab/log (shell-command-to-string "echo $PWD"))
           ;; 执行操作是异步的!
           (ab/log (shell-command-to-string "git pull"))))))
   (lambda (result)
     (message "finished ab/exec-when-emacs-boot,%s" result))))
```
在这个例子中[aborn-log.el](https://github.com/aborn/.spacemacs.d/blob/master/parts/aborn-log.el)
文件虽然已经在当前启动的emacs中load了，但在新创建的异步的emacs子进程
中完全没有这个上下文（context）信息。因此，你不得不加入以下两行代码:
```elisp
(add-to-list 'load-path "~/.spacemacs.d/parts")
(require 'aborn-log)
```
这样才能调用ab/log这个函数。
