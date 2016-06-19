# face
face是用于显示文本图形属性的集合，如字体、前景色、背景色、可选的下划线。face控制
文本在emacs的buffer中怎么显示

## face的属性
1. :family 字体集
2. :foundry
3. :width 相对字符宽度，可取以下值：ultra-condensed,
extra-condensed, condensed, semi-condensed, normal, semi-expanded,
expanded, extra-expanded, or ultra-expanded.
4. :height 字体的高度,为Int类型
5. :weight 字体weight,可取以下值：ultra-bold, extra-bold, bold,
semi-bold, normal, semi-light, light, extra-light, or ultra-light
6. :foreground 前景颜色，值可为颜色名或者十六进制的表示法
7. :distant-foreground 另一种前景颜色
8. :background 背景色
9. :underline 下划线，可取值为nil, t, color
10. :overline 上划线
11. :strike-through 删除线
12. :box 是否用box框起来，可取值为nil, t, color
13. :font 字体

## face的定义
采用defface这个宏来定义face
```elisp
defface face spec doc [keyword value]. . .
```


