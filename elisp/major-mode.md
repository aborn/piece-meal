# major mode
major mode也称为主模式，它是互斥的。每个buffer只可能同时存在一种major模式

## 主模型规范
每个主模式都遵循以下几种编码规范，包括对local keymap,语法表的初始化，函数，变量名
及hooks。如果采用define-derived-mode这个宏来定义主模式，它将自动采用这些规范中
的大部分。

. 定义主模式的命令，一般以-mode结尾；如果没有任何参数，调用这个command里它将当前
buffer切换到这个主模式，同时设置其keymap, syntax, 和局部变量；
. 要有docment string来描述主模式；
. major mode的命令应该设置变量*major-mode*为主模式的命令symbol
. major mode的命令应该设置变量*mode-name*为相应的模式名，类型为string
. 要有自己的命名空间
. major mode应该有自己的keymap，它用作本模式的局部keymap，主模式命令应该调用
*use-local-map*来安装这个local map,keymap名为modename-mode-map
. keymap以C-c开头
. 要有正常的hook函数，命名为modename-mode-hook
. 
