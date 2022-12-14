rime 输入法的笔记，是用[obsidian](https://obsidian.md/)记录的，里面配置项大部分都进行了双链(以`[[xxx]]`)包裹的内容

配置以`hy`为例命名，见
- `hy.dict.yaml.md`
- `hy.schema.yaml.md`

## 特色
- 跨平台（windows，MAC，linux，安卓，IOS），各平台统一配置
- 安全：手机上不需要特殊权限
- 功能强：全配置，可扩展：支持`lua`扩展功能
- 候选项增加提示信息：效果如图，提示信息也能输出
- 开源
- 内置特性：按数字后自动修改`.`键输出为小数点，而不是句号
<img src="https://github.com/hyaray/rime-note/blob/main/windows效果.png">
<img src="https://github.com/hyaray/rime-note/blob/main/安卓效果.png">

## 缺点
- 不支持云功能
- 手机是否支持语音录入待验证
- 能否读取通讯录

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
