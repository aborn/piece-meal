## 问题
在开发[leanote-emacs](https://github.com/aborn/leanote-emacs)这个包的时候，我定义了一个spaceline的segement，代码如下：
```elisp
(defun leanote-spaceline-status ()
  "Install spaceline status, need spaceline 2.x version."
  (interactive)
  (require 'spaceline)
  (spaceline-define-segment leanote-status-seg
    "show the leanote status"
    (when leanote-mode
      (powerline-raw
       (s-trim (leanote-status)))))
  (spaceline-spacemacs-theme 'leanote-status-seg)
  (spaceline-compile))
```
其中*spaceline-define-segment*是在[spaceline](https://github.com/TheBB/spaceline)中定义的一个宏。我发现，如果我将leanote的安装放在spacemacs的启动安装包里时。当emacs启动完成后，我执行*M-x leanote-spaceline-status*打开leanote的modeline的status时会报如下错误：
```elisp
(invalid-function spaceline-define-segment)
```
我感到很困惑，为什么说是**invalid-function**无效的函数？可它明明是一个宏呀！

## 定位
不过，令我感觉奇怪的是，当我的emacs启动完成后（注：我emacs是安装了spaceline这个包的），我再手工安装leanote-emacs时不会报这个错。我将两次安装时leanote.el编译后的leanote.elc文件打开看，发现它们不一样，如下：
![报错时leanote.elc文件](http://upload-images.jianshu.io/upload_images/297930-04ff7b5fe4433dc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![正确的结果](http://upload-images.jianshu.io/upload_images/297930-76189e50e577f29c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 原因
emacs是有上下文的（如一些变量及包），当编译leanote.el这个文件的时候，上下文不一样，最后导致的编译结果会不一样。第一次将leanote放在spacemacs启动安装里时，因为这个时候spaceline这个feature还没有载入到emacs的上下文中。因此，编译leanote.el文件时，编译器并不知道*spaceline-define-segment*它是一个宏，因此，它就不会对其进行宏展开，只认为它是一个普通的函数。第二次，当我手工进行安装的时候，这个时候上下文中已经存在spaceline这个包，也就是*spaceline-define-segment*这个宏的声明已经在emacs的上下文中。所以，编译器会将这个宏进行展开，而不会将它视为一个函数对待。
