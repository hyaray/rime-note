相当于脚本里的 Label，定义一组功能

## option_name
和 [[soft/rime/switches#name]] 一致
## opencc_config
- [ ] 全匹配才替换
`opencc_config: s2t.json`
`opencc_config: s2tw.json`
## tags
设定此 filter 的作用范围
`tags: [ pinyin_lookup ]` 挂在这个[[soft/rime/tag]]所对应的[[soft/rime/translator]]上

## overwrite
是否覆盖其他提示
## tips
## show_in_comment
设定是否仅将转换结果显示在备注中，否则和候选框对调位置
`show_in_comment: true`
## excluded_types
取消特定范围〔一般为❌`reverse_lookup_translator`〕转化用字
## comment_format
![[soft/rime/translator.md#comment_format]]
