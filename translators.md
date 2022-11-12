> [[soft/rime/代码段|代码段]]，需要转为[[soft/rime/候选框|候选框]]

1. 翻译的对象是[[soft/rime/代码段|代码段]]
2. 代码段可由几种 [[soft/rime/translator|translator]] 分别翻译（单个往往只翻译特定标签的代码段）、
3. 翻译的结果可能有多条，每条结果成为一个展现给用户的候选项。默认显示每条结果的首个选项，按一定规则合并成[[soft/rime/候选框]]
4. 候选项所对应的编码未必是整个代码段(比如用拼音输句子时，词组后面继续列出单字候选)

每个方案有一个主 `translator`（以 `translator:` 定义）

## 示例
举例来说，【朙月拼音】中，输入码 `2012nian\`，划分为三个编码段：

| input |  tag   | translations                         |
|:-----:|:------:|:------------------------------------ |
| 2012  | number | [ "2012" ], [ "二〇一二" ]           |
| nian  |  abc   | [ "年", "念", "唸",... ], [ "nian" ] |
|   \   | punct  | [ "、", "\\" ]                       |

## history_translator
`history_translator@l_historyZ`

## translator
[[soft/rime/translator]]

## punct_translator
转换标点符号，可能是数字后面自动转英文符号

## reverse_lookup_translator
❌已淘汰：被[[soft/rime/filters#reverse_lookup_filter]]替代
反查翻译器，用另一种编码方案输入+反查：比如用拼音打字，并显示五笔编码
## reverse_lookup_filter
[reverse_lookup_filter](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#四reverse_lookup_filter)
反查滤镜，以更灵活的方式反查，Rime1.0后<font color=red>替代</font>[[soft/rime/translators.md#reverse_lookup_translator]]
> 此属性虽定义在[[soft/rime/translators]]，本质上属于[[soft/rime/filters]]
可加载多个实例，后接`@+filterName`
- `reverse_lookup_filter@reverse_lookup`
- `reverse_lookup_filter@pinyin_lookup`
- `reverse_lookup_filter@jyutping_lookup`

- [ ] 如何实现

## lua_translator
[hchunhui/librime-lua](https://github.com/hchunhui/librime-lua/issues)
[加入 Lua 脚本扩展支持 · Issue #248 · rime/librime](https://github.com/rime/librime/issues/248)
格式：`lua_translator@函数名`
> 针对[[soft/rime/功能索引#输入码]]
```
- lua_translator@date_translator  #自定义日期输出
- lua_translator@week_translator  #自定义星期输出
- lua_translator@number_translator  #自定义数字转大写以/引导
```

## 翻译器
> 二选一
### table_translator
五笔用，码表翻译器，从码表里查找[[soft/rime/segmentors#abc_segmentor|abc_segmentor]] 标记的内容
- 码表为 [[#dictionary]] 选项对应的文件，比如[[soft/rime/hy.dict.yaml]]

### script_translator
❌脚本翻译器，用于拼音等基于音节表的输入方案

