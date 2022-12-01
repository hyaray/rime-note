[segmentors](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#二segmentor)
> rime 可将文字、数字、符号等不同内容连续输入，此时需要将[[输入码]]分成若干个[[输入码#代码段]]（比如 `yxi` 被分成`y` `xi`，`ni3hao`→`nǐhao`），这通过数轮代码段划分操作完成。
1. 每一轮操作中，一众 [[segmentor]] 分别给出起始于某一处、符合特定格式的代码段，识别到的<font color=red>最长代码段</font>成为本轮划分的结果，存入 [[engine#context]]
2. 排在前面的 [[segmentor]] 也可直接 `continue` 到下一轮。
3. 而给出这一划分的一个或多个 segmentor 组件则可为该代码段打上`类型标签`；从这一新代码段的结束位置，开始下一轮划分，直到整个输入码序列划分完毕。
4. 举例来说，【朙月拼音】中，输入码 `2012nian\`，划分为三个编码段：

| input |  tag   | translations                         |
|:-----:|:------:|:------------------------------------ |
| 2012  | number | [ "2012" ], [ "二〇一二" ]           |
| nian  |  abc   | [ "年", "念", "唸",... ], [ "nian" ] |
|   \   | punct  | [ "、", "\\" ]                       |
5. 那些标签是初步划分后判定的类型，也可能有一个编码段贴多个标签的情况。
6. 下一个阶段中，[[translators]] 会把特定类型的编码段翻译为文字。

## abc_segmentor
把常规输入码标记为`abc`，用来查找码表
仅可设置[[segmentor#extra_tags]]属性
## ascii_segmentor
> 标识西文段落，如果在英文模式下直接上屏

## matcher
配合[[recognizer#patterns]]，如果匹配则标识[[tag]]为定义前面的名称
✅✅✅一般还需要[[#affix_segmentor]]加工
## affix_segmentor
✅✅✅对[[#matcher]]识别的[[tag]]进一步处理，标识[[segmentor#prefix]]，[[translator]]才能正确翻译。
主要工作有：
1. 删除[[segmentor#prefix]]和 suffix
2. 标记[[segmentor#extra_tags]]
`affix_segmentor@as_xxx`

## punct_segmentor
> 给符号分段并标记为`punct`

## fallback_segmentor
> 标识其他未标识段落，把[[输入码]]连成一段
