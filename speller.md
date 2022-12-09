[speller](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#一speller)
## 逻辑
> 主要考虑已有候选项后的[[#alphabet]]按键处理逻辑，可用`lun`测试
> [[#auto_select]]开启
> 约定：之前候选项数量 `n`
1. 已设置[[#max_code_length]]
    1. 之前码长`=max`：则必然`n>1`，会上屏之前首项，并设置当前按键为输入码
    2. 之前码长`<max`，判断 `n`
        1. `n == 1`
            1. 如果和候选项的后续编码一致，则补充
            2. 不一致：是上屏还是无脑补充到输入码？
        2. `n > 1`补充当前按键
2. 未设置[[#max_code_length]]
    1. `n > 1`补充当前按键，更新后若`n == 1`，则直接上屏
## algebra
✅✅✅打字的核心拼写处理逻辑，修改输入码。默认只处理小写字母按键为[[输入码]]，其他直接上屏
指定生成[[用户文件夹#hy.prism.bin]]文件的拼写运算规则，也可将一组并击编码转换为拼音音节
可以实现五笔中`z`当万能键的功能，不过可能会变卡
语法见[[preedit_format]]
[[编程/正则]]
[algebra](https://github.com/rime/home/issues/1153)
见`terra_pinyin.custom.yaml`
- 比如输入`yoa`能转成`yao`以匹配`要`


## alphabet
定义本方案[[输入码]]字母表，包含用于并击的按键。
击键虽有先后，形成并击时，一律以字母表顺序排列
- `alphabet: zyxwvutsrqponmlkjihgfedcba`
## use_space
是否以`空格`作为[[输入码]]

## max_code_length
✅五笔则需要设置此项，，这样在此范围内输入码没有找到结果时，不会乱上屏减较码长的内容，比如`luns`
- 如果被`recognizer`识别为url等，则会无效
- 优先级比[[translator#enable_sentence]]高
`max_code_length: 4`
## auto_clear
超过长度自动清除[[输入码]]
- 如果错误率低，不需要

`auto_clear: max_length`

## auto_select
[五笔 auto_select = true 时如何以 max_code_length = 4 为准 · Issue #289](https://github.com/rime/librime/issues/289)
✅✅✅单结果可`自动上屏`，且能实现当输入码超过[[#max_code_length]]时，会自动首字上屏。
如果未设置[[#max_code_length]]，在任意码长，只要无码都会自动顶之前有码的首字上屏，剩余输入码变成当前输入码
在[[recognizer#patterns]]匹配时==无效==
上面的功能，不一定好用，会导致如下问题：
1. 如`lua`时，已经无候选项，则会上屏`lu`的首字`较`上屏，再输入码设置为`a`
2. 唯一时自动上屏，但我们不一定记得住，仍然敲`空格`想要上屏，导致输出了无效的`空格`

## auto_select_unique_candidate
~~❌淘汰了~~
## auto_select_pattern
`auto_select_pattern: ^ss$`
- ❌无效，没什么用。自动上屏规则（正则）

## delimiter
上屏的音节`分隔符`，五笔没用
`delimiter: "'"`

## initials
仅作为起始键
## finals
仅作为末尾键
