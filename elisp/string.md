# 字符串处理
本节node学习字符串处理，在elisp环境中，字符串是字符的数组.但elips的字符串一但创建，无法修改。
对于非ASCII编码的字符串，在elisp中有两种表示方式：**unibyte**和**multibyte**

## 字符串长度
计算字符串的长度函数是string-width,
```
string-width string
```

## 字符串操作

### substring
substring可通过函数：  
```
substring string start &optional end
```

来获得,这个函数返回一个新的子串，如下例子：  
```elisp
(substring "abcdefg" 0 3);  => "abc"
(substring "abcdefg" -3 -1); => "ef"
(substring "abcdefg" -3 nil); => "efg"
```

### concat
语法如下：  
```
concat &rest sequences
```
如下例子：
```
(concat "abc" nil "-def") ; "abc-def" 注意nil是空字符串
```

### split操作
语法如下：
```
split-string string &optional separators omit-nulls trim
```
该函数对字符串进行分割，按照separators的RE表达式来分
如果omit-nulls是nil则会返回的list中可能含有nil字符串
如果separators是nil则分割符是split-string-default- separators
```elisp
(split-string "Soup is good food" "o") ;=>("S""upisg""""df""""d")
(split-string "Soup is good food" "o" t) ;=> ("S" "up is g" "d f" "d")
```

### 字符串比较
判断字符串相等采用:
```
string= string1 string2
```
注意函数string-equal与string=相同

### 数字与字符串的转换
number-to-string number  
string-to-number string &optional base  
```
(number-to-string -23.5); =>  "-23.5"
(string-to-number "-4.5"); => -4.5
```
