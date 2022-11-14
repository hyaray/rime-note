[dict文件详解](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#dictyaml-詳解)
> 单字、含词，扩展字库等设计为3种输入方案
- 是 [[translators]] 的参考书，可以用`#`注释
- 通过 [[#import_tables]] 主码表(hy.dict.yaml)在「Librime」引擎中合二为一。主要依据是词频

## 文件格式要求
1. UTF-8 nobomb
2. 以`\t`为列分隔符
3. 繁、简体和源码表一致
4. 编码形式和定义一致

## 规则说明
- `简介信息`以`---`开始，以`...`结尾
### name
> 最好和文件名的前半部分一致
- [ ] 此名称和哪里相关？？
### sort
字典初始排序
- `sort: by_weight` 词频
- `sort: original` 码表
### use_preset_vocabulary
- 是否导入预设词表(八股文)
- 原因：输入方案需要词组，而码表缺少词组。
- [ ] 到底什么意思？？
### max_phrase_length
词条长度限制
### min_phrase_length

### columns
> 定义码表各列的内容，用Tab分隔
- [ ] 如何增加字符集信息，供[[rime-lua]]
#### text 字/词
#### code 可以有多个音节，多字的情况下，如果全不是多音字，可省略
#### weight 词频（非负整数或百分数）
#### stem
造词码 比如【有】打字是`e`，造词码是`de`
- [ ] 什么情况下使用？

### import_tables
> 用这个还是用 [[translator#dictionary]]

导入的词典只导入词汇，会忽略YAML定义内容
导入其他词典(字(本身)、词、英语名称、用户词、生僻字分开)，发送各格式的日期
用户词典名为去掉`.`后面内容的名称比如 `hy.ext.dict.yaml`，用户词典名为`hy`而不是`hy.ext`
```
import_tables:
  - wubi86_ci
  - wubi86_eng
```

### encode
#### rules
>[[#length]]和[[#formula]] 的条件组合,2个字怎么编码,3个字怎么编码
##### length_equal
`length_equal: 2`
##### length_in_range
`length_in_range: [4, 10]`
##### formula
- `A`=第一个字,`B`=第2个字, `Y`=倒数第2个字, `Z`=最后一个字
- `a`=第一个编码,`b`=第2个编码, `y`=倒数第2个编码, `z`=最后一个编码
- `AaBzCaYzZz` 取第一字首码，第二字尾码、第三字首码、倒数第二字尾码、最後一字尾码
- `AaAzBaBbBz` 取第一字首尾碼、第二字首次尾碼
`formula: "AaAbBaBb"`

#### exclude_patterns
> 取消某编码的造词资格
- `exclude_patterns: ['^z.*$']`

#### tail_anchor
- 造词码包含结构分割符〔仅用於仓颉〕
