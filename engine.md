- [Rime_description#细项配置](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#細項配置)
- [SpellingAlgebra · rime/home Wiki](https://github.com/rime/home/wiki/SpellingAlgebra#拼寫運算詳解)
- [RimeWithTheDesign框架设计和示例代码](https://github.com/rime/home/wiki/RimeWithTheDesign)
- [輸入法引擎與功能組件](https://github.com/rime/home/wiki/RimeWithSchemata#輸入法引擎與功能組件)
- 流程：`输入码→（棱镜）→code→（词典）→文本`
```
【男】ss(2484799116) 22-11-16 16:16:05
https://github.com/rime/librime/blob/9086de3dd802d20f1366b3080c16e2eedede0584/src/rime/engine.cc#L96-L115
context.input 输入码更新时

https://github.com/rime/librime/blob/9086de3dd802d20f1366b3080c16e2eedede0584/src/rime/engine.cc#L144-L158
输入码打tag
https://github.com/rime/librime/blob/9086de3dd802d20f1366b3080c16e2eedede0584/src/rime/engine.cc#L155

translator+filter
https://github.com/rime/librime/blob/9086de3dd802d20f1366b3080c16e2eedede0584/src/rime/engine.cc#L156
```
## 分类

- 框架级组件：由Engine创建并调用
- 基础组件：由框架级组件实现类使用

- [[processors]]
- [[segmentors]]
- [[translators]]
- [[filters]]

##  调试
[调试说明](https://github.com/rime/home/wiki/RimeWithSchemata#關於調試)

输入引擎，作为整体来看，以`按键消息`为输入，输出包括：
1. 对按键消息的处理结果：操作系统要一个结果、这按键、输入法接是不接？
2. 暂存于输入法、尚未完成处理的内容，会展现在输入法[[候选框]]中。
3. 要「上屏」的文字，并不是每按一键都有输出。通常中文字都会伴随「确认」动作而上屏，有些按键则会直接导致符号上屏，而这些还要视具体场景而定。

## context
> 输入法上下文：输入法可能会在多个程序里运行，所以需要保存各自的信息
