# elisp编码规范
为了让你写的elisp代码更加广泛地接受，下面的一些编码规范可供参考

## 规范
1. 加载一个包不应该改变emacs的编辑行为。这个规范是必须要遵守的。
2. 由于所有的elisp变量和函数共享同样的命名空间。对于独立的包，应该采用一个统一的前缀
作为自己的命名空间。在这个包中，所有的变量和函数名以这个为开头，并加上一个连字符。如
你的命名空间为markdown,那么所有的函数或变量应满足这种形式markdown-*。对于包中的不
"私有"函数（不想被其他包调用的函数），请采用两个连字符(--)。
3. 为每个独立包(文件)，在文件最后提供一个调用provide。
4. 当包依赖于其他包时，将require语句放在文件的最前面。
5. 如果一个文件*foo*要使用定义在*bar*文件中的*宏*，但不想使用任何在bar文件中的变量
或者函数，那么在*foo*文件中添加如下语句:  
```elisp
(eval-when-compile (require 'bar))
```
6. 避免在运行里加载额外的库，除非你真的需要。
7. 如果想用Comman Lisp的扩展，请使用**cl-lib**。不要用老的**cl**库,因为老的库没有
命名空间，如果加载老的*cl*库，会引起命令冲突。产生各种诡异问题。
8. 如果定义major mode，请遵循major mode的一系列规范。
9. 如果定义minor mode，请遵循minor mode的一系列规范。
10. 如果某个函数的功能是判断某个条件是真还是假，那么函数的命名应以p结尾。如果函数名只
有一个单词，那么p紧跟其后，如果有多个单词，那么以-p结尾。
11. 如果一个变量的目的是保存单个函数，那这个变量应以-function结尾。如果变量目的是保存
一个函数列表，也就是hook，请遵循[hook的命名规范](https://www.gnu.org/software/emacs/manual/html_node/elisp/Hooks.html#Hooks)。
12. 如果载入一个文件添加函数到hook
13. 对emacs的原始类型进行重作别名操作，是一个不好的编辑习惯。通常情况下，你就应该采用
标准命名，除非是做向后兼容的工作。
14. 在包中尽量避免使用eval-after-load
15. 在某些语言中变量名以\*开头和结尾，在emacs中不这样用。
16. emacs默认的编码系统为UTF-8。
17. 对文件格式化，请采用默认的格式化参数。
18. Don’t make a habit of putting close-parentheses on lines by themselves; Lisp programmers find this disconcerting.
19. 添加copyright信息在文件头，[参考](https://www.gnu.org/software/emacs/manual/html_node/elisp/Library-Headers.html#Library-Headers)


## 参考
[Emacs Lisp Coding Conventions](https://www.gnu.org/software/emacs/manual/html_node/elisp/Coding-Conventions.html)
