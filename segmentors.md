[segmentors](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#二segmentor)
> rime 可将文字、数字、符号等不同内容连续输入，此时需要将[[soft/rime/功能索引#输入码|输入码]]分成若干个[[soft/rime/功能索引.md#代码段]]（比如 `yxi` 被分成`y` `xi`），这通过数轮代码段划分操作完成。
1. 每一轮操作中，一众 [[soft/rime/segmentor]] 分别给出起始于某一处、符合特定格式的代码段，识别到的<font color=red>最长代码段</font>成为本轮划分的结果，存入 [[soft/rime/engine#context]]
2. 排在前面的 [[soft/rime/segmentor]] 也可直接 `continue` 到下一轮。
3. 而给出这一划分的一个或多个 segmentor 组件则可为该代码段打上`类型标签`；从这一新代码段的结束位置，开始下一轮划分，直到整个输入码序列划分完毕。
4. 举例来说，【朙月拼音】中，输入码 `2012nian\`，划分为三个编码段：
    1. `2012`（贴number[[soft/rime/tag]]）
    2. `nian`（贴abc标签）
    3. `\`（贴punct标签）
5. 那些标签是初步划分后判定的类型，也可能有一个编码段贴多个标签的情况。
6. 下一个阶段中，[[soft/rime/translators]] 会把特定类型的编码段翻译为文字。

## abc_segmentor
> 把字母标记为`abc`，用来查找码表

## ascii_segmentor
> 标识西文段落，如果在英文模式下直接上屏

## matcher
> 配合[[soft/rime/recognizer|recognizer]]标识符合特定规则的段落（如网址、反查等，加上特定[[soft/rime/tag]]）
- [ ] 和 [[#affix_segmentor]]区别是什么
## affix_segmentor
> 自定义tagName，`punct`和`reverse_lookup`是内置的
`affix_segmentor@tagNew`

## punct_segmentor
> 给符号分段并标记为`punct`

## fallback_segmentor
> 标识其他未标识段落，把输入码连成一段
