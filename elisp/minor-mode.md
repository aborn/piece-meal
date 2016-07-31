# minor mode
minor mode提供了一种可选的功能

## 写minor mode的一些规范
1. 定义一个以-mode结尾的变量，也称这种变量为**mode变量**。当这个变量的值为nil是该minor mode就关闭态，否则就打开。
2. 定义一个mode command，名字与**mode变量**一样。它的作用是用来设置这个mode command,并且可以外加一些其他操作。
这个mode command函数接收一个可选参数。当处于交互模式时，并且没有前缀参数时，对这个minor进行切换
（即，原来这个minor mode是关闭态就打开它，反之则关闭它）。当有正的前缀参数时，刚打开它，反之则关闭它。
3. 为每个minor-mode，添加一个相应元素到**minor-mode-alist**这个alist

## 定义一个minor mode
采用宏**define-minor-mode**去定义一个minor-mode
