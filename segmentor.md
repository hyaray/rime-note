[Rime_description#segmentor](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#二segmentors)

## tag
设定[[tag]]，后续传递给[[translator]]处理（不填则仅针对 `abc`）

## prefix
> 须配合 [[recognizer#patterns]]
设定此[[输入码]]的`前缀`标识，排除无效字符，才能让[[translator]]给出结果
## suffix
`后缀`标识，如果像拼音这样可以输长句子可能会用到
- [ ] 如果可以用来当常用字的临时开关（比如翻译）用会非常爽，但是目前一按候选框就清空了。

## tips
- 按了 [[#prefix]]，还未输入时的提示内容
`tips: "【临时拼音】"`

## closing_tips
- 设定其结束输入提示符，可不填
- 当按下[[#suffix]]时，会在[[输入码]]后面添加此提示文字（见 `cangjie6_express.schema.yaml` 里，反查后，按`;`时会有效果）

## extra_tags
为此[[segmentor]]所标记的[[输入码#代码段]]加上额外[[tag]]，这样下一步就会匹配额外的[[translator]]来生成候选项
比如临时拼音时，又想输入生僻字。目的都是解决不会五笔的情况，所以合并是合理的
`extra_tags: [unicode]`