[Rime_description#translator](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#三translator)

## 通用选项

### ![[preedit_format]]
### comment_format
默认显示编码提示，格式见 [[preedit_format]]
### echo_translator
> 没有其他候选字时，回显[[输入码]]（`Shift+Enter`上屏）

### dictionary
- 翻译器将调取此字典文件（如果有扩展，则调用扩展）
- 如果用了其他输入法的词库，则需要定义 [[#prism]] 名称以免覆盖其他输入法映射
- 如果是 `reverse` 相关，则填主[[translator]]里定义的词典
- `dictionary: wubi86_ci_extended`
```
- 【侯】局局(525312750)  23:46:28
涉及 dictionary 选项时，就只与 dictionary 有关。luna_pinyin_simp 方案本身的 dictionary 就是 luna_pinyin 的，所以只能用 luna_pinyin 的，反查也是
```
### enable_sentence
✅✅✅允许句子输入，可以多个音节组合，是拼音输入法的核心选项
设置了[[speller#max_code_length]]，此选项基本上无效
默认为`true`

### enable_user_dict
> 是否开启用户词典（记录动态字词频、用户词）
- `enable_user_dict: true`
### user_dict
- [[#enable_user_dict]]开启才生效，见`rime_ice.schema.yaml`
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

## initial_quality
> 此翻译器的优先级，数据越大优先级越高（影响[[候选框]]字序）
> 默认码表为`0`

## prism
设定由此主翻译器的 [[speller]] 生成的[[用户文件夹#hy.prism.bin]]棱镜文件名，或此副编译器调用的棱镜名
默认指向和[[#dictionary]]同名`prism`文件

## 仅table_translator有效
### enable_encoder
> 是否开启自动造词
### encode_commit_history
> 对已上屏的内容整合成词条儿，看需求
### max_phrase_length
- 自动造词的最长字数
### enable_completion
> 显示尚未输入完整码的字
- `enable_completion: true` 设置后，在[[反查|拼音反查]]里，词组反查会失效
### sentence_over_completion
> 在无全码对应字而仅有逐键提示时也开启智能组句
### strict_spelling
> 配合[[speller]]中的fuzz规则，仅以畧拼码组词
### enable_charset_filter
> 是否开启字符集过滤（启用 [[filters#cjk_minifier]] 后可适用于 [[translators#script_translator]]）

## 仅script_translator有效
### spelling_hints
> 设定多少字以内候选标注完整带调拼音〔仅〕
