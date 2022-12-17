> 方案名约定为<font color=red>hy</font>
> 以源文件为基础（[[#import_preset]]），[[#patch]]覆盖重新定义的选项（`custom`文件才有效）
[patch原理](https://blog.csdn.net/weixin_42148809/article/details/124827354)
[✅✅✅patch用法](https://github.com/rime/home/wiki/Configuration#補靪)
[CustomizationGuide](https://github.com/rime/home/wiki/CustomizationGuide#定製指南)

[patch @before last{n} n从10开始有问题 · Issue #592 · rime/librime](https://github.com/rime/librime/issues/592)
## import_preset和__include的区别
和上下文相关

## import_preset
> 由外部文件导入，实现模块化配置：可对各模块新建 `*.custom.yaml` 文件，每个文件里`patch:`即可实现
> 比如[[#key_binder]]设置`import_preset: default`，会从[[共享文件夹#default.yaml|default.yaml]]导入对应的配置
用到此方法的模块有 recognizer、key_binder、punctuator

## patch
### 数组操作
#### 修改
#### 插入
```yaml
最前插入
xxx/@before 0: a
xxx/@before 1: b
xxx/@before 2: c

第1项后面依次插入
xxx/@after 0: a
xxx/@after 1: a
xxx/@after 2: a

最后1项前依次插入
xxx/@before last01: a #这里是字符串排序，所以两位数兼容性比较好
xxx/@before last02: b
xxx/@before last03: c

末尾依次插入
xxx/+: #推荐
  - a
  - b
  - c

xxx/@next01: a
xxx/@next02: b
xxx/@next03: c
``` 

### 键值对
`xxx/key: value`
刪除：`xxx/`
### __include

在当前位置包含另一 YAML 节点的內容
1. 本地节点：`__include: local/node`
2. 另一文件全部：`__include: config.yaml:/`
3. 另一文件子节点：`__include: config.yaml:/external/node`
```
include_example_5:
  __include: some_map
  occupation: journalist #新增内容
  simplicity: very #覆盖原内容
```

### __patch

修改某些值
```
__patch:
  key/alpha: value A
  key/beta: value B
```

```
patch_example_1:
  sibling: old value
  append_to_list:
    - existing item
  merge_with_map:
    key: value
  replace_list:
    - item 1
    - item 2
  replace_map:
    a: value
    b: value

  __patch:
    sibling: new value
    append_to_list/+: #添加 list
      - appended item
    merge_with_map/+: #添加 map
      key: new value
      new_key: value
    replace_list/=: #修改 list
      - only item
    replace_map/=: #修改 map
      only_key: value
```

- "一级设定项/二级设定项/三级设定项": 新的设定值
- "另一个设定项": 新的设定值
- "再一个设定项": 新的设定值
- "含列表的设定项/@n": 列表第n个元素新的设定值，从0开始计数
- "含列表的设定项/@last": 列表最后一个元素新的设定值
- "含列表的设定项/@before 0": 在列表第一个元素之前插入新的设定值（不建议在补丁中使用）
- "含列表的设定项/@after last": 在列表最后一个元素之后插入新的设定值（不建议在补丁中使用）
- "含列表的设定项/@next": 在列表最后一个元素之后插入新的设定值（不建议在补丁中使用）
- `"switches/@0/reset": 1`表示switches的第1项的值改成1

## 覆盖式（列表样式）
✅✅✅
- 复制原段落(第1行没缩进)到文件
- 粘贴的内容增加2缩进，如果文件没patch则前面行插入没缩进的patch:
- 修改相应的值即可

## 插入式（单句样式）
- "engine/filter/@before 3": ***
    - 数字从0开始，所以是插到到第4个之前，排在第4个
