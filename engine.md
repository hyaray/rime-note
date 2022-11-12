- [Rime_description.md#细项配置](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#細項配置)
- [RimeWithTheDesign框架设计和示例代码](https://github.com/rime/home/wiki/RimeWithTheDesign)
##  调试
[调试说明](https://github.com/rime/home/wiki/RimeWithSchemata#關於調試)

输入引擎，作为整体来看，以`按键消息`为输入，输出包括：
1. 对按键消息的处理结果：操作系统要一个结果、这按键、输入法接是不接？
2. 暂存于输入法、尚未完成处理的内容，会展现在输入法[[soft/rime/候选框]]中。
3. 要「上屏」的文字，并不是每按一键都有输出。通常中文字都会伴随「确认」动作而上屏，有些按键则会直接导致符号上屏，而这些还要视具体场景而定。

## context
> 输入法上下文：输入法可能会在多个程序里运行，所以需要保存各自的信息

## 分类

- 框架级组件：由Engine创建并调用
- 基础组件：由框架级组件实现类使用

## processors
[[soft/rime/processors]]
## segmentors
[[soft/rime/segmentors]]
## translators
[[soft/rime/translators]]
## filters
[[soft/rime/filters]]
