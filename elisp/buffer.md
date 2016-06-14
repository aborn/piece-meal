# buffer
本节讲解buffer

## 常用函数
(current-buffer)  ;获取当前buffer  
(buffer-name &optional buffer)     ;获取buffer名  
(rename-buffer newname &optional unique) ;重命名当前buffer  
(buffer-file-name &optional buffer)      ;返回buffer对应的file名  

;切换<buffer-or-name>为当前buffer  
;这函数不显示buffer在任何window，用户对这个buffer不一定可见  
(set-buffer <buffer-or-name>)

## 临时操作另一个buffer方法
有时候想对另一个buffer进行操作，操作完了以后返回到当前buffer,有以下两种方式实现：  
1. 将set-buffer放在save-current-buffer的form里
```elisp
(defun append-to-buffer (buffer start end)
  "Append the text of the region to BUFFER."
  (interactive "BAppend to buffer: \nr")
  (let ((oldbuf (current-buffer)))
    (save-current-buffer
      (set-buffer (get-buffer-create buffer))
      (insert-buffer-substring oldbuf start end))))
```
2. 另一种方式是采用with-current-buffer这个宏
```elisp
(defun append-to-buffer (buffer start end)
  "Append the text of the region to BUFFER."
  (interactive "BAppend to buffer: \nr")
  (let ((oldbuf (current-buffer)))
    (with-current-buffer (get-buffer-create buffer)
      (insert-buffer-substring oldbuf start end))))
```

## 宏with-temp-buffer
with-temp-buffer body...  
它在一个临时的buffer里执行body里的表达式,并将这个temp buffer作为当前buffer.当body里的
表达式执行完成后kill掉temp buffer，返回原来的buffer
