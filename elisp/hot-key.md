# key
一些常用的按键表示

## hot-key
一些特殊的按键表示：
```elisp
(global-set-key (kbd "M-<return>") 'command)   ;; M-enter键
(global-set-key (kbd "M-<left>") 'command')    ;; M-左方向键，同理<right> <down> <up>
(global-set-key (kbd "C-s-<left>") 'command')  ;; mac系统，C-alt-left
(global-set-key (kbd "<C-tab>") 'command)      ;; C-tab键
(global-set-key (kbd "C-SPC") 'command)        ;; space key
```
