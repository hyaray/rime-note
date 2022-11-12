[translator](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#三translator)

## 和segmentor相同的选项
> 同时也可在副 translator 中定义
![[soft/rime/segmentor]]
### echo_translator
> 没有其他候选字时，回显输入码（输入码可以`Shift+Enter`上屏）

## 通用选项

### dictionary
- 翻译器将调取此字典文件（如果有扩展，则调用扩展）
- 如果用了其他输入法的词库，则需要定义 [[#prism]] 名称以免覆盖其他输入法映射
- `dictionary: wubi86_ci.extended`

### enable_sentence
> 允许句子输入
设置了[[soft/rime/speller#max_code_length]]，此选项基本上无效

### enable_user_dict
> 是否开启用户词典（记录动态字词频、用户词）
- `"enable_user_dict": true`
### user_dict
- [[#enable_user_dict]]开启才生效？见`rime_ice.schema.yaml`
- [ ] 设定用户词典名，和主词典如何协同？
### disable_user_dict_for_patterns
> 禁止某些编码录入用户词典
```
  disable_user_dict_for_patterns:
    - "^z.*$"
    - "^a.**"
```

### db_class
- [ ] 设定用户词典类型，什么用
`db_class: tabledb #文本`
`db_class: userdb #二进制`

### initial_quality
> 此翻译器的优先级，数据越大优先级越高（影响[[soft/rime/候选框]]字序）
> 默认码表为`0`

### prism
> 设定由此主翻译器的 [[soft/rime/speller]] 生成的棱镜文件名，或此副编译器调用的棱镜名

### comment_format
> [[编程/正则]]
提示码自定义
```yaml
- "xform/$/〕/"
- "xform/^/〔/"
- "xlit|abcdefghijklmnopqrstuvwxyz |日月金木水火土竹戈十大中一弓人心手口尸廿山女田止卜片、|"
```

## 仅table_translator有效
### enable_encoder
> 是否开启自动造词
### encode_commit_history
> 是否对已上屏词自动造词
### max_phrase_length
> 最大自动成词词长
### enable_completion
> 显示尚未输入完整码的字
- [ ] `enable_completion: true` 设置后，在[[soft/rime/反查|拼音反查]]里，词组反查失效了
### sentence_over_completion
> 在无全码对应字而仅有逐键提示时也开启智能组句
### strict_spelling
> 配合[[soft/rime/speller]]中的fuzz规则，仅以畧拼码组词
### enable_charset_filter
> 是否开启字符集过滤（启用 [[soft/rime/filters#cjk_minifier]] 后可适用于 [[soft/rime/translators#script_translator]]）

## 仅script_translator有效
### spelling_hints
> 设定多少字以内候选标註完整带调拼音〔仅〕
