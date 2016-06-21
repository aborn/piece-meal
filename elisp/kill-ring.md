# kill ring
kill这个函数有点像删除函数，但是它保存被killed的值，以便用户能再次通过粘帖(yanking)来进行
插入。大部分有类似行为的函数是以**kill-**为前缀。相反，函数名以**delete-**开头的不保存被
删除的内容。  

kill命令一般用于交互行为。被killed的文本内容被保存在*kill ring*中。实际上它是一个保存了
最近被killed的内容的列表。之所以叫*ring*因为粘贴操作视之为有循环顺序的。这个List绑定到变量
**kill-ring**里，操作它就像操作普通的list。

## kill ring限制
kill ring就是一个字符串列表，由最新到最老，如下是一个例子：
```elisp
("some text" "a different piece of text" "even older text")
```
但这个列表不是无限大的，它受限于变量**kill-ring-max**的值。当list超过这个限制后，
添加一个新的entry会自动删除最后一个entry。譬如笔者的电脑里这个变量的值为*60*
```
ELISP> kill-ring-max
60 (#o74, #x3c, ?<)
```

## 与kill ring相关的操作函数
