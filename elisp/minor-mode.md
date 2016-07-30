# minor mode
minor mode提供了一种可选的功能

## 写minor mode的一些规范
1. 定义一个以-mode结尾的变量，也称这种变量为mode变量。当这个变量的值为nil是该minor mode
就关闭，否则就打开
2. 定义一个mode command，名字与mode变量一样。它的作用是用来设置这个mode command,
外加其他一些操作。这个mode command函数接收一个可选参数
3.

## 定义一个minor mode
