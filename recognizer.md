- 通过[[#patterns]]对不同情况的[[输入码]]定义`pinyin`、`url`、`mail`等名称
- 后续见[[segmentors#matcher|matcher]]
- 非内置`tagName`，其它字段不调用输入法引擎，`输入即输出`〔如`url`等字段〕

## patterns
> 注意`数字`，否则可能无法选择项目
> 命令的唯一目的，就是在[tag]里可以指定
配合[[segmentor#prefix]]和`suffix`完成段落劃分、[[功能索引#tag]]分配

### punct
配合 [[processors#punctuator]]
`punct: '^z[a-zA-Z\\''"\(\)\[\];]+$'` 用`\D`会影响`-=`等功能按键的翻 

### reverse_lookup
❌已淘汰，和[[translators#reverse_lookup_translator]]搭配
