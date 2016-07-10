# 字符串处理
本节node学习字符串处理，在elisp环境中，字符串是字符的数组.但elips的字符串一但创建，无法修改。
对于非ASCII编码的字符串，在elisp中有两种表示方式：**unibyte**和**multibyte**

## 字符串表示
字符串的的非ASCII(大于127)字符的表示有两种方式：
### 多字节(multibyte)
multibyte保存的是人可读的文本，每个字符对应的数值范围为0~4194303
### 统一字节(unibyte)
unibyte保存的是原始byte，每个字符对应一个byte，即它的值为0~255
### 注意点
But beware: If a string constant contains hexadecimal
or octal escape sequences, and these escape sequences
all specify unibyte characters (i.e., less than 256)

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
### format
下面是一个例子
```elisp
(format "The value of fill-column is %d. %s" fill-column "a")
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
### join操作
与split对应的是对string list的join操作，对应函数为**string-join**
```elisp
ELISP> (string-join '("a" "b") " ")
"a b"
ELISP> (string-join '("a" "b") ";")
"a;b"
```

### 字符串比较
判断字符串相等采用:
```
string= string1 string2
```
注意函数string-equal与string=相同

### suffix & prefix
java程序中我们经常有这们的操作startWith及endWith，相应的elisp中有两个对应的函数
*string-prefix-p* 与 *string-suffix-p*
它们的语法类似  
```elisp
string-suffix-p suffx string &optional ignore-case
```

### 数字与字符串的转换
number-to-string number  
string-to-number string &optional base  
```
(number-to-string -23.5); =>  "-23.5"
(string-to-number "-4.5"); => -4.5
```
