- 与 [[soft/rime/segmentors#matcher|matcher]] 搭配，通过[[#patterns]]识别特定内容(`「拼音反查」`、`url`、`mail`等)
- 配合[[soft/rime/translator#prefix|prefix]]和[[soft/rime/translators#suffix|suffix]]完成段落划分、[[soft/rime/tag]]分配
- 前字段可以为以 [[soft/rime/segmentors#affix_segmentor]] 定义的 [[soft/rime/tag]]名，或者 [[#punct]]、[[#reverse_lookup]]两个内设的字段。
- 非内置`tagName`，其它字段不调用输入法引擎，`输入即输出`〔如`url`等字段〕

## patterns

配合[[soft/rime/segmentor#prefix]]和`suffix`完成段落劃分、[[soft/rime/功能索引#tag]]分配
### reverse_lookup
`reverse_lookup: "^'[a-z]*$"` 这里的`'`符必须和[[#reverse_lookup]]
### punct
配合 [[soft/rime/processors#punctuator]]
`punct: '^z[a-zA-Z\\''"\(\)\[\];]+$'` 用`\D`会影响`-=`等功能按键的翻页

### 示例
```yaml
- email: "^[A-Za-z][-_.0-9A-Za-z]*@.*$"
- uppercase: "[A-Z][-_+.'0-9A-Za-z]*$"
- url: "^(www[.]|https?:|ftp[.:]|
- mailto:|file:).*$|^[a-z]+[.].+$"
```
