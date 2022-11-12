打字的核心拼写处理逻辑，默认只处理小写字母按键为[[功能索引#输入码]]，其他直接上屏

## alphabet
定义本方案[[功能索引#输入码]]
- `zyxwvutsrqponmlkjihgfedcba`
## use_space
是否以`空格`作为[[功能索引#输入码]]

## max_code_length
是形码的核心参数
- 如果被`recognizer`识别为url等，则会无效
- 超过则顶首项上屏
- [ ] 3码唯一时能否顶字上屏？
`max_code_length: 4`
## auto_clear
超过长度自动清除[[功能索引#输入码]]
`auto_clear: max_length`
## auto_select
[五笔 auto_select = true 时如何以 max_code_length = 4 为准 · Issue #289](https://github.com/rime/librime/issues/289)
单结果是否`自动上屏`
## auto_select_unique_candidate
- [ ] 无重码自动上屏，无效
`auto_select_unique_candidate: true`
## auto_select_pattern
`auto_select_pattern: ^ss$`
- [ ] 自动上屏规则（正则），无效

## delimiter
上屏的音节`分隔符`，五笔没用
`delimiter: "'"`

## algebra
> [[编程/正则]]
拼写运算规则，算出的拼写汇入 [[个人文件夹#hy.prism.bin]] 中

## initials
仅作为起始键
## finals
仅作为末尾键
