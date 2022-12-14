> ✅✅✅逻辑入口，根据[[#处理器]]定义的<font color=red>顺序</font>依次判断按键，比如[[#ascii_composer]]不匹配则交给[[#recognizer]]，参考脚本语言的`if`
- [ ] 如果匹配后，是跳过下面处理器还是继续处理？

> 通过组合可以承担[[engine]]的全部任务，但为了将逻辑继续细分、又设置了[[segmentors]], [[translators]]和[[filters]]功能组件
> 最常见的处理，便是将按键所产生的字符记入上下文中的「[[输入码]]」序列，由下一组件[[segmentors]]开始一轮新的作业

1. 对按键的处理结果，返回给操作系统
    - 拒：操作系统自己处理
    - 收
        - 直接处理
        - 交给其他`processor`
1. 暂存于输入法，尚未完成处理的内容，会展现在[[候选框]]中
2. 要上屏的文字，并不是每按一键都有输出，要视情况而定

## 按键分类
> `大写字母`如果未在以下列表匹配，则会自动顶字上屏
- `自定义热键`由 [[#key_binder]] 定义，优先级最高
- `shift` 和 `ctrl` 控制【中英文状态】由 [[ascii_composer]] 处理
- `数字`上屏候选项，`上下键`切换候选项，【换页】由 [[#selector]] 处理
- `空格`，`回车`上屏，`BackSpace`删除[[输入码]]由 [[#express_editor]] 处理

- `标点符号`由 [[#punctuation]] 处理
- `字母`由 [[speller]] 处理
- `正则判断`由 [[recognizer]] 处理

## 处理器
> 基本上都是内置的
- [[ascii_composer]]
- [[recognizer]]
- [[key_binder]]
- [[speller]]
- [[editor]]

### [[punctuator]]
### express_editor
编辑器，处理回车上屏、回退键等
和 [[#fluid_editor]] 互斥

### fluid_editor
[ascii_punct 開關在 fluid_editor 下行為似乎不正確 · Issue #203 · rime/librime](https://github.com/rime/librime/issues/203)
[请教，语句流 fluid_editor 的一个疑问，谢谢。【rime吧】_百度贴吧](https://tieba.baidu.com/p/1794305386)

> 和 [[#express_editor]] 互斥
> 句式编辑器，以空格断词、回车上屏的【注音】、【语句流】等输入方案
> 也可以写作 `fluency_editor`

### selector
[[候选框]]处理器（数字键、上下、换页）

### navigator
[[输入码]] 内的光标移动（左右，Home，End）

### chord_composer
示例`combo_pinyin.schema.yaml`
❌和弦作曲家等多键并击的输入方案
并击把键盘分两半，相当于两块键盘。两边同时击键，系统默认在其中一半上按的键先于另一半，由此得出上屏码

#### [[speller#alphabet]]
#### [[speller#algebra]]

#### output_format
并击完成后套用的式样，追加隔音符号

#### prompt_format
并击过程中套用的式样，加方括号

