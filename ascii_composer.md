
> 中英文状态切换键，【可选】输出已上屏按键或候选项，详见[[#值]]
## good_old_caps_lock
`good_old_caps_lock: true` CapsLock是否输出大写字母

## switch_key

### 键
> 长按键`shift`不生效，是否优化过？
- `Shift_L/R`
- `Control_L/R`
- `Caps_Lock`
### 值
- `noop` 无视
- `inline_ascii` 切换为英文，但不上屏(`默认`)
- `commit_code` 切换为英文并上屏之前的字母
- `commit_text` 切换为英文并上屏汉字
- `clear` 切换为英文并清除之前的内容
```
Shift_L: inline_ascii
Shift_R: commit_text
Control_L: noop
Control_R: noop
Caps_Lock: clear
```

