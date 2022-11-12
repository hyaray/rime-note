- [ ] 介绍网址
> 全局设定
> windows相关配置在[[weasel.custom.yaml|weasel.custom.yaml]]
> 其他输入方案主要配置在[[hy.schema.yaml|hy.schema.yaml]]
## schema_list
> 修改输入方案列表
```
- schema: wubi86                # 五笔86
- schema: wubi86.unicode
- schema: terra_pinyin         # 地球拼音 dì qiú pīn yīn
- schema: luna_pinyin           # 朙月拼音
- schema: py
- schema: wubi98_chr
- schema: wubi98_ci
- schema: wubi98_dz
- schema: wubi98_single
- schema: wubi98_U
- schema: chinese_numbers       # 中文数字
- schema: luna_pinyin_simp     # 朙月拼音 简化字模式
- schema: luna_pinyin_tw       # 朙月拼音 臺灣正體模式
- schema: bopomofo             # 注音
- schema: bopomofo_tw          # 注音 臺灣正體模式
- schema: jyutping             # 粵拼
- schema: cangjie5             # 倉頡五代
- schema: cangjie5_express     # 倉頡 快打模式
- schema: quick5               # 速成
- schema: wubi_pinyin          # 五笔拼音混合輸入
- schema: double_pinyin        # 自然碼雙拼
- schema: double_pinyin_mspy   # 微軟雙拼
- schema: double_pinyin_abc    # 智能ABC雙拼
- schema: double_pinyin_flypy  # 小鶴雙拼
- schema: wugniu        # 吳語上海話（新派）
- schema: wugniu_lopha  # 吳語上海話（老派）
- schema: sampheng      # 中古漢語三拼
- schema: zyenpheng     # 中古漢語全拼
- schema: ipa_xsampa    # X-SAMPA 國際音標
- schema: emoji         # emoji表情
```

## menu
> 输入法[[候选框]]数量
### page_size
优先级比[[hy.schema.yaml#page_size]]低

### alternative_select_keys:
`alternative_select_keys: "acegi"`
- 数字键如设置为大写中文，用字母来选择个数

## Switcher
> 输入方案切换[[rime#热键]]
```yaml
caption： [方案选择]
hotkeys: ["Control+slash"]
fold_options: true
abbreviate_options: true
option_list_separator: '／'
```
### hotkeys
> 方案选择热键
内容来源：
1. [[#schema_list]]定义的输入方案列表
2. [[hy.schema.yaml#switches]]里的`status`不为空的列表
```
- Shift+space
- Control+Shift+grave
```
### save_options
> [[switches#reset]]优先级更高
- 开启后，当切换[[switches#内置开关]]状态时，状态会被保存。每当方案初始化时，会恢复保存的状态。
```
    - full_shape
    - ascii_punct
```
### fold_option
每个选项（或者是它的每个状态？）都成为一个候选
`fold_option: false`

```
【侯】局局(525312750)  14:10:22
fold_options 这样描述吧，顾名思义，折叠选项。在方案选单中，选项是折叠成一个候选的，选中就会展开。如果不折叠，应该就是直接展开的状态。

【侯】局局(525312750)  14:12:43
至于展开状态是如何布局的，反正展开状态只有一种，就不描述了。
```

### abbreviate_options
控制是否将每个选项名称略显为首字符
`abbreviate_options: true`
### option_list_separator
控制选项名之间的分隔符
`option_list_separator: '/'`
