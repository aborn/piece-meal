# markers标记
marker是一种lisp对象，用于标记buffer中的相对于文本的位置信息。无论文本内容是否有修改或者删除，
marker将自动改变它的偏移量。因此它仍然会保持于两个符号之间。

## marker的概述
一个marker有三个属性：  
1. marker的位置
2. marker对应的buffer
3. 插入类型
marker的位置相当于所处buffer的坐标，它是一个int类型。但这个位置坐标会发生变化。插入或者删除
操作会重新定位这个markder。在marker前后做删除操作，会使得marker的位置立刻变成被删除文本之
前或者之后。插入操作也同样，在其前还是后要依赖于插入的类型。

在一个buffer中做插入或者删除操作，要重新检查所有markers并重新定位它们。当一个buffer中有大量
的markers时，这会使得处理速度变慢。当marker不被绑定到任何symbol时，它会被GC回收。

## marker操作
**1**. 创建一个marker，它不指向任何位置
```elisp
(setq m1 (make-marker))
```

**2**. 设置marker位于第99个字符与100个字符之间
```elisp
(set-marker m1 100)
```
**3**. 如果接下来插入下个字符在buffer的最前面，那么上面m1这个marker的位置将自动调整变成位于
100个字符与101个字符之间  
```elisp
(setq m2 (copy-marker m1))
```

两个marker可以指向同一个位置，are not eq, but they are equal.  

```elisp
(eq m1 m2) =>nil
(equal m1 m2) =>t
```

### marker创建
1. 函数**make-marker**它创建一个新的marker,但它不指向任何位置  
2. 函数**point-marker**它创建一个新的marker，同时指向buffer的当前位置  
3. 函数**point-min-marker**它创建一个新的marker，它指向当前buffer可读取部分的最小位置  
4. 函数**point-max-marker**它创建一个新的marker，它指向当前buffer可读取部分的最大位置
5. copy-marker语法如下：
```
copy-marker &optional marker-or-integer insertion-type
```
如果将marker做为传参，它将返回一个指向同样位置的marker。它也可以接收一个int值作为参数，它将
返回一个marker，位置为当前bufffer的marker-or-integer。

### 从marker中获取信息
从marker中获取信息有两个函数
```
marker-position marker
marker-buffer marker
```

### marker的插入类型
