
[注音字母-Unicode字符百科](https://unicode-table.com/cn/blocks/bopomofo)
> 单字符映射为任意内容
- 特殊符号的输出全在这里，key_binder 没处理的热键
- [[共享文件夹#default.yaml|default.yaml]]加载了`punctuation.yaml`

## full_shape
## half_shape
## symbols
❌❌❌[[反查#reverse_lookup_filter]]不支持，如果需要，转成[[hy.dict.yaml]]

## 基础属性
### use_space
是否空格顶字
`use_space: true`
### commit
原先会在词库里做`matching`了 只有当唯一完全匹配或者空码的时候才会上屏
放了后就直接上屏。
❌如果不会上屏，如下操作会有问题，仅测试效果：把 punctuator 放在[[recognizer]]前面，反而会造成打字时，翻页符号等全失效
### pair
`'"' : {pair: ['“','”']}`重复按键交替上屏
### 数组
`"(": ["〔", "［"]`弹出选单，数字上屏

```
  full_shape:
    __include: punctuation:/full_shape
  half_shape:
    __include: punctuation:/half_shape
```
