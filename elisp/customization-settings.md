# Customization Settings
本节note讲讲定制化设置，并不是一定要通过代码来改变emacs的设置。也可以通过定制化界面
(Customize interface)来达到相同的效果

## 分类
定制化项分为以下三类  
1. 定制化变量，采用defcustom这个宏来定义  
2. 定制化界面(customizable faces),采用defface来定义  
3. 定制化组(customization groups),采用defgroup来定义  

## 通用关键字(Common Item Keywords)
1. :group group 将定制化的化归为组  
2. :link link-data 包括一个额外链接,一般用于按钮  
3. :load file 在显示定制化项目前载入一个文件  
4. :require feature 当保存定制化值是执行(require 'feature)  
5. :version version 版本  
6. :package-version ’(package . version)  

## defcustom
定义可定制化的变量，这称之为用户选项，语法如下：
```
defcustom option standard doc [keyword value]. . .
```
option为变量名，standard为变量的默认值，doc为其文档，后面就为keyword value这样的pair了.
其中keyword可为以下几种：
1. :type type 数据类型，可取舍为sexp,integer, number, float, string, regexp,
character, file, directory, hook, symbol, function, variable, face, boolean,
key-sequence, coding-system, color. 注意：如果你不想设置类型，或者类型是不确定的，
那可以将其值设置为sexp。

## defgroup
语法如下：  
```elisp
defgroup group members doc [keyword value]. . .
```
定义一个可定制的group,并声明其成员,注意，大部分时间members是nil。一般是通过
:group来指定成员
