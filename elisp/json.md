# json
elisp系统自带json库，为*json.el*文件

## json的parse
从字符串或者buffer中读取json字符串采用以下几下函数：

### json-read
这个函数是从当前buffer的当前point中开始读取字符串，并解析成json object

### json-read-from-string
这个函数是从字符串中解析json object，语法规则如下：
```
json-read-from-string <string>
```
如下是一个例子：
```
ELISP> (json-read-from-string "{\"status\":\"success\",\"globel\":\"success\",\"status_message\":{\"demo-project\":\"deploy success\",\"machine_percent\":75}}")
((status_message
  (machine_percent . 75)
  (demo-project . "deploy success"))
 (globel . "success")
 (status . "success"))
```
从上面的例子可以看出，它其实转化成了key-value的association list(alist)
#### 解析数组
下面是一个例子
```
ELISP> (setq ab/test (json-read-from-string "[{\"a\":\"aresult\"},{\"b\":\"bresult\"}]"))
[((a . "aresult"))
 ((b . "bresult"))]
```

### json-read-file
读取文件的内容，并转换成json

## to json string
将json的object转成json string采用*json-encode*这个函数，如下：  
```
ELISP> (json-encode '((status_message
  (machine_percent . 75)
  (demo-project . "deploy success"))
 (globel . "success")
 (status . "success")))
"{\"status_message\":{\"machine_percent\":75,\"demo-project\":\"deploy success\"},\"globel\":\"success\",\"status\":\"success\"}"
```

## 参考
[http://edward.oconnor.cx/2006/03/json.el](http://edward.oconnor.cx/2006/03/json.el)
