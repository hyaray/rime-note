[filters](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#四filters)
上一步已经收集到各个代码段的翻译结果，当输入法需要在界面呈现一页候选项时，就从最末一个代码段的结果集中挑选、直至取够方案中设定的页最大候选数。

每从结果集选出一条字词、会经过一组 filters 过滤。多个 filter 串行工作，最终产出的结果进入候选序列。

filter 可以：

1. 改装正在处理的候选项，修改某些属性值：简化字、火星文、菊花文有无有？过时了！有 Rime，你对文字的想象力终于得救
2. 消除当前候选项，比如有重复（由不同 translator 产生）的候选条目
3. 插入新的候选项，比如根据已有条目插入关联的结果。见[[滤镜#普通滤镜]]
4. 修改已有的候选序列
5. 码表与词典
6. 词典是 translator 的参考书。

他往往与同名输入方案配套使用，如拼音的词典以拼音码查字，仓颉的词典以仓颉码查字。但也可以由若干编码属于同一系统的输入方案共用，如各种双拼方案，都使用和拼音同样的词典，于是不仅復用了码表数据，也可共享用户以任一款此系列方案录入的自造词（仍以码表中的形式即全拼编码记录）

这批组件过滤翻译的结果，自定义滤镜皆可使用开关调控

## 自定义字符集
[自定义增广字库 · Issue #91 · rime/home](https://github.com/rime/home/issues/91)
- 如果用户可以自定义几个字符集（或其他概念），比如常用字，生僻字，内置词组，自定义词组等几类。然后用[[switches]]可以指定当前生效是哪几个字符集，这样就不需要用字典来判断了？这个不好实现吗？

## 参数

### uniquifier
过滤重复的候选字（后面的会`覆盖`前面的），有可能来自 [[#simplifier]]

### simplifier
以`simplifier`开头的都是[[opecc]]
由 [[switches#simplification]] 值控制开关，进行繁/简转化等功能。

### lua_filter
[[rime-lua.md#lua_filter]]

### single_char_filter
单字过滤器，如加载此组件，则屏敝词典中的词组（仅[[translators#table_translator]]有效）

### cjk_minifier
字符集过滤〔仅用于 [[translators#script_translator]]，使之支援extended_charset 开关

### [[反查#reverse_lookup_filter]]
