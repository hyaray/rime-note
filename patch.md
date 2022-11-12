## patch
[rime用yaml修改配置](https://github.com/rime/home/wiki/Configuration)

### __include

在當前位置包含另一 YAML 節點的內容，见[[soft/rime/自制输入方案#import_preset和__include的区别]]
`__include: local/node`
`__include: config.yaml:/external/node` 另一文件
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
- 复制原段落(第1行没缩进)到文件
- 粘贴的内容增加2缩进，如果文件没patch则前面行插入没缩进的patch:
- 修改相应的值即可

## 插入式（单句样式）
- "engine/filter/@before 3": ***
    - 数字从0开始，所以是插到到第4个之前，排在第4个
