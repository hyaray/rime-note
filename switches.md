> 定义开关，设置热键在 [[key_binder]]
> 折叠和展开见[[default.custom.yaml#fold_options]]
> 是否可以定义字符集开关，这样就能实现字符集的自由组合了
[开关](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#開關)

## name
> 和[[filter#option_name]]一致

### 内置开关
#### ascii_mode
0英文，1中文
#### full_space
0半角，1全角
#### ascii_punct
0中文，1英文标点
#### extended_charset
❌不好用，但是自己用码表管理更好
0为CJK字符集，1为全字符集（仅[[translators#table_translator|table_translator]]可用）
#### simplification
> 汉字简繁体转换开关，常规是不用的

`0不开启，1开启`

### 自定义

## options
`options: [normal, extended]` 和[[#name]]二选一即可
## states
若不写，则[[default.custom.yaml#hotkeys]]不会显示此项

## reset
如果想要记住状态，则
重置状态，以下情况会生效：
1. 切换输入方案
2. 切换输入法
3. rime重新部署

```
20221109
【侯】局局(525312750)  10:41:51
状态默认值可以被记忆值（保存值）覆盖，而 reset 会反过来覆盖记忆值。
你无法将一个选项的状态默认值设置为 1，而又允许它的状态在切换时被记忆并在再次初始化时自动恢复。

【侯】局局(525312750)  10:43:52
设定默认值不应当影响记忆和恢复功能，而设定重设值则会使记忆恢复功能失效。

【侯】局局(525312750)  10:49:16
比如一个方案是给多个人使用的，一个开关项可以统一设定一个默认值，同时启用状态记忆功能，这样就可以在不改动方案的情况下适应不同用户的习惯。当我们不能设定非 0 的默认值，就只能设定 reset 为这个值，那么就会有用户无法习惯，而必须改动方案。

【侯】局局(525312750)  10:51:04
同一个用户在不同时间也可能持续使用不同的状态，而 reset 总会重置为同一个状态，所以也不能满足他。
```
