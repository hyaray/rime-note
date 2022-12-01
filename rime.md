- 万分感谢`局外人`（QQ`525312750`）的大量帮助，让我终于能清晰地了解rime的处理逻辑细节。
- 感谢`风之漫舞`（QQ`847243643`）提供的
# Rime
- [wiki](https://github.com/rime/home/wiki)
- [也致第一次安装RIME的你](https://blog.csdn.net/xianghongai/article/details/79540525)
- [在线笔记](https://www.yuque.com/shenshanhongye/uo23kv/nuvz43)
- [fxliang/weasel at PR](https://github.com/fxliang/weasel/tree/PR)
- [弓辰](https://github.com/lotem)
- [深蓝词库转换工具](https://github.com/studyzy/imewlconverter/releases)

## 特色
- 候选项增加提示信息：效果如图，提示信息也能输出
![[附件/rime/rime效果.png]]
- [ ] 当设置为唯一输入法时，有时候会一直禁用，导致无法打字
- [ ] AutoHotkey无法获取当前中文/英文状态，且无法获取

- [[hy.schema.yaml]]
- [[soft/rime/rime-lua]]
- [[功能索引]]
- [[engine]]
- [[用户文件夹]]
- [[共享文件夹]]

## 其他资料
[✅双拼练习](https://github.com/BlueSky-07/Shuang)
[双拼练习](https://github.com/Yidadaa/shuangpin)

## 使用说明
### 文件说明
1. 输入方案配置：`wubi86.schema.yaml`
2. 主词库：`wubi86.dict.yaml`里面定义了常用单字和要加载的分词库（见`import_tables`配置内容）
3. 分词库：在`dict`文件夹下，各功能如下
    1. `eng_`开头的是最常用英语，和五笔混打。
    2. `wubi86_user.dict.yaml`定义自定义的词组，第3项数字是当前词组的优先级，影响候选项排序
    3. `wubi86_z.dict.yaml`定义`z`开头的快捷短语，和下面的符号区别是这里支持==提示==，定义的语法不同
4. `z`开头的符号定义，见`symbols.yaml`，==不支持提示功能==，示例有：
    1. 箭头：`zjt`
    2. 标点：`zbd`
    3. 符号：`zfh`
    4. 数字：`zsz`
5. 提示内容：`hytips.dict.yaml`
### 快捷键
1. 切换输入方案和功能开关:`shift-space`
2. 开关拆字和拼音提示：`ctrl-/`
3. 全角/半角切换：`ctrl-,`
4. 中/英标点：`ctrl-.`

```tasks
path includes soft/rime
not done
hide recurrence rule
hide task count
sort by start
sort by priority
```