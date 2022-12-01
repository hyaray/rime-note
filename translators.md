[Rime_collections/Rime_description.md at master · LEOYoon-Tsaw/Rime_collections](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#三translators)
> [[代码段|代码段]]，需要转为[[候选框|候选框]]

1. 翻译的对象是[[代码段|代码段]]
2. 代码段可由几种 [[translator]] 分别翻译（单个往往只翻译特定标签的代码段）、
3. 翻译的结果可能有多条，每条结果成为一个展现给用户的候选项。默认显示每条结果的首个选项，按一定规则合并成[[候选框]]
4. 候选项所对应的编码未必是整个代码段(比如用拼音输句子时，词组后面继续列出单字候选)

每个方案有一个主 `translator`（以 `translator:` 定义）

## history_translator
`history_translator@l_historyZ`

## translator
[[translator]]

## punct_translator
转换标点符号，可能是数字后面自动转英文符号

## reverse_lookup_translator
❌已淘汰：被[[filters#reverse_lookup_filter]]替代
反查翻译器，用另一种编码方案输入+反查：比如用拼音打字，并显示五笔编码
`reverse_lookup_translator #等同于 reverse_lookup_translator@reverse_lookup`
## lua_translator
[hchunhui/librime-lua](https://github.com/hchunhui/librime-lua/issues)
[加入 Lua 脚本扩展支持 · Issue #248 · rime/librime](https://github.com/rime/librime/issues/248)
格式：`lua_translator@函数名`
> 针对[[输入码]]
```
- lua_translator@date_translator  #自定义日期输出
- lua_translator@week_translator  #自定义星期输出
- lua_translator@number_translator  #自定义数字转大写以/引导
```

## 翻译器
> 二选一
### table_translator
码表翻译器，从码表里查找[[segmentors#abc_segmentor|abc_segmentor]] 标记的内容，比如在五笔里使用
- 码表为 [[translator#dictionary]] 选项对应的文件，比如[[hy.dict.yaml]]
```yaml
table_translator #效果等同于 table_translator@translator
table_translator@lt_xxx
```

### script_translator
用于拼音等基于音节表的输入方案

