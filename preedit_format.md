[[编程/正则]]

修改
> 对输入的编码进行修正并显示
    - 拼音：输入`lv`，显示`lü`
    - 笔画：输入`hspnz`显示`一丨丿丶乙`

## xform
> 替换（不保留原形）
- `xform/^([nl])ue$/$1ve/`
- `nue`和`lue`不匹配，`nve`和`lve`才可获得结果

## xlit
> 批量一对一替换
- `xlit/abc/ABC/` abracadabra→ABrACAdABrA
-
## derive
>衍生（保留原形）
- `derive/^([nl])ue$/$1ve/` nue/nve/lue/lve都可获得结果
-
## erase
>删除
- `erase/^.*\d$/` dang1这种格式的全被删除

## fuzz
>畧拼（此种简拼仅组词，不出单字）

## abbrev
>简拼（出字优先级较上两组更低）

## 示例
### 地球拼音
```
- xform/([nl])v/$1ü/
- xform/([nl])ue/$1üe/
- xform/([jqxy])v/$1u/
```
### 双拼
```
translator:
dictionary: luna_pinyin # 与【朙月拼音】共用词典
prism: double_pinyin_abc # prism 要以本输入方案的名称来命名，以免把朙月拼音的拼写映射表覆盖掉
preedit_format: # 这段代码用来将输入的双拼码反转为全拼显示；待见双拼码的可以把这段拿掉
- xform/o(\w)/0$1/ # 零声母先改为0，以方便后面的转换
- xform/(\w)q/$1ei/ # 双拼第二码转换为韵母
- xform/(\w)n/$1un/ # 提前转换双拼码 n 和 g，因为转换后的拼音里就快要出现这两个字母了，那时将难以分辨出双拼码
- xform/(\w)g/$1eng/ # 当然也可以采取事先将双拼码变为大写的办法来与转换过的拼音做区分，可谁让我是高手呢
- xform/(\w)w/$1ian/
- xform/(\[dtnljqx\])r/$1iu/ # 对应多种韵母的双拼码，按搭配的声母做区分（最好别用排除式如 \[^o\]r 容易出状况）
- xform/0r/0er/ # 另一种情况，注意先不消除0，以防后面把e当作声母转换为ch
- xform/(\[nljqx\])t/$1iang/
- xform/(\w)t/$1uang/ # 上一行已经把对应到 iang 的双拼码 t 消灭，于是这里不用再列举相配的声母
- xform/(\w)y/$1ing/
- xform/(\[dtnlgkhaevrzcs\])o/$1uo/
- xform/(\w)p/$1uan/
- xform/(\[jqx\])s/$1iong/
- xform/(\w)s/$1ong/
- xform/(\[gkhaevrzcs\])d/$1ua/
- xform/(\w)d/$1ia/
- xform/(\w)f/$1en/
- xform/(\w)h/$1ang/
- xform/(\w)j/$1an/
- xform/(\w)k/$1ao/ # 默默检查：双拼码 o 已经转换过了
- xform/(\w)l/$1ai/
- xform/(\w)z/$1iao/
- xform/(\w)x/$1ie/
- xform/(\w)b/$1ou/
- xform/(\[nl\])m/$1ve/
- xform/(\[jqxy\])m/$1ue/
- xform/(\w)m/$1ui/
- "xform/(^|\[ '\])a/$1zh/" # 复原声母，音节开始处的双拼字母a改写为zh；其他位置的才真正是a
- "xform/(^|\[ '\])e/$1ch/"
- "xform/(^|\[ '\])v/$1sh/"
- xform/0(\w)/$1/ # 好了，现在可以把零声母拿掉啦
- xform/(\[nljqxy\])v/$1ü/ # 这样才是汉语拼音 :-)

- 上屏码自定义，拼音有用，把nv显示为nü
- - xform/([nl])v/$1ü/
- - xform/([nl])ue/$1üe/
- - xform/([jqxy])v/$1u/
```
