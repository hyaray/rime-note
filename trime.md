[使用说明](https://github.com/osfans/trime/wiki/UserGuide)
[trime.yaml詳解](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3)
[Trime中为什么没有`共享文件夹`？](https://github.com/osfans/trime/issues/104)
[在设置界面设置候选词数量 by tumuyan · Pull Request #768 · osfans/trime](https://github.com/osfans/trime/pull/768)
[Improvement for logging by WhiredPlanck · Pull Request #866 · osfans/trime](https://github.com/osfans/trime/pull/866)
build文件夹，推荐由PC转过去
> 重启算法服务：


## 路径
`/sdcard/Android/data/com.osfans.trime/rime`
`/sdcard/rime`

## 安装步骤
1. 手机安装release版，`3.2.9`选`配色`有bug，可以先用3.2.8，新版本肯定会修复。

## 设置
1. 键盘设置：拦截相关热键

## switches
- `_hide_candidate` 隐藏候选栏`Candidate_switch`
- `_hide_comment` 隐藏候选项注释`Comment_switch`
- `_hide_key_hint` 隐藏按键下方的助记符号`Hint_switch`
- [3.2.6]`_hide_key_symbol` 隐藏按键上方的符号

## 键盘要求
1. 没有直接的数字按键
2. 没有 CapsLock 功能
3. 按键`z`和`a`两行按键同列，和实际键盘有出入
4. 修改常用的符号到按键上
2. 复制小狼毫的用户文件夹大部分文件，以下是排除列表
    - weasel.custom.yaml
    - weasel.yaml
    - installation.yaml
    - user.yaml
    - rime.dll
    - opencc 如果用`ocd`格式，需要用64位的 `opencc_dict` 编译
        - [ ] opencc用了txt格式仍无效，需要做什么？？？
1. 同文不像小狼毫自带几个输入方案，所以还要从[[共享文件夹]]复制
    - default.yaml
    - 关联输入方案的`schema.yaml`文件
2. 部署功能因为没有日志非常难受，所以暂时就依赖PC把大部分依赖都build好迁移



## 键盘整体逻辑
### 基础定义
1. 颜色定义：颜色是`RGB`和[[soft/rime/weasel.custom.yaml]]相反
    1. [[#colors]]定义最基础的颜色
    2. [[#fallback_colors]]颜色补充
    3. 主题：[[#preset_color_schemes]]如果只用单风格键盘，只设计一套即可
2. 按键功能定义：[[#android_keys]]和[[#preset_keys]]
### 键盘
1. 根据[[#preset_keys]]制作单个键盘：
    - [定制键盘](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#示例给键盘添加删词功能)
    - 整体样式[[#style]]
    - ![a](https://camo.githubusercontent.com/2328e18764bde46bd20fc0eb30c392123a11b4479190ca683f503960f639f10e/687474703a2f2f696d677372632e62616964752e636f6d2f666f72756d2f7069632f6974656d2f386131393865353166336465623438663562323638393637663731663361323932636635373831622e6a7067)
    - ![[附件/小狼毫配色.png]]
    - 按键上面按键组合成[[#preset_keyboards]]
1. 多个键盘：[[#keyboards]]主键盘绑定各子键盘

## style
界面样式及特色功能，具体见 [[#preset_color_schemes]]

### 尺寸
#### horizontal_gap
按键水平间距
#### vertical_gap
按键行间距
#### candidate_padding
候选项内边距，如`5`
#### candidate_spacing
候选间距，如`0.5`


### auto_caps
是否开启自动句首大写（其中`ascii`:仅英文模式句首大写）
### background_dim_amount
❌暂时没用，`tongwenfeng`里定义了`0.5`
### max_height
❌暂时没用
### min_height
❌暂时没用
### candidate_use_cursor
是否打开候选焦点高亮
### comment_on_top
候选项注释是否在上方（`false`:在右侧）
### horizontal
[3.2.3]水平模式。改变方向键的功能（`true`：方向键适配横排候选；`false`：方向键适配竖排候选）
### keyboards
✅✅✅键盘配置。除主键盘外，其它需要用到的键盘都要在这里声明。
### proximity_correction
✅将按键之间的空白区域分配给相邻的按键，避免空按
一般`proximity_correction: true`
### background_folder
[3.2.3]背景图路径，即保存在 background 的哪个子目录。 使用此参数可以方便管理多个主题的图片（当然也可以指定多个主题共用一套图片）。
### reset_ascii_mode
不同进程中显示键盘时是否重置中英文状态
### latin_locale
在英文状态（ascii_mode）下，朗读按键时所用的语言。
### locale
在中文状态下，朗读上屏文本和按键时所用的语言。  
    ※ 需要先在同文设置界面开启朗读功能。朗读功能还需要手机的 TTS 引擎支持。可使用系统默认引擎，也可安装讯飞语记等第三方引擎。`latin_local`和`local`可以设置的语言也取决于 TTS 引擎。常见的语言：`zh_TW`, `zh_CN`, `zh_HK`, `en_US`, `ja_JP`, `ko_KR`,……
### speech_opencc_config
语音输入简繁转换（默认值`s2t.json`: 将语音识别的结果转换成繁体再上屏）  
    需要配合 OpenCC 组件来使用。转换的选项有：
### layout
> 候选窗口设置
- `position`: 悬浮窗位置
    -   `left`|`right`|`left_up`|`right_up` 这几种都可以让悬浮窗口动态跟随光标（需要 ≥Android5.0）
    -   `fixed`|`bottom_left`|`bottom_right`|`top_left`|`top_right` 这几种是固定在屏幕的边角上
- `min_length`: 悬浮窗最小词长（候选词长大于等于`min_length`才会进入悬浮窗）
- `max_length`: 连续排列的多个候选项总字数（包括候选项注释）超过`max_length`时，把超出的候选项移到下一行显示（单个候选项若超长，或者`max_length`数值过大，则由`max_width`决定是否换行）
- `sticky_lines`: 固顶行数（不与其它候选同排，单独一行显示的候选项个数）
- `max_entries`: 最大词条数（允许进入悬浮窗的最大词条数）
- `all_phrases`: 显示所有长词。所有满足`min_length`的词条都显示在悬浮窗（一般只用于 table translator，有可能会改变候选项的显示顺序）
- `border`: 边框宽度（增大边框则向内加粗，也会对悬浮窗圆角产生一点影响）
- `max_width`: 窗口最大宽度（候选超长则自动换行）
- `min_width`: 最小宽度（悬浮窗的初始宽度）
- `margin_x`: 水平边距（左右留白大小）
- `margin_y`: 竖直边距（上下留白大小）
- `line_spacing`: 候选词的行间距（px）
- `line_spacing_multiplier`: 候选词的行间距倍数
- `spacing`: 悬浮窗位置上下偏移量（一般上移为正，下移为负，但当`position`设为 top_xxx 时，方向是相反的）
- `round_corner`: 窗口圆角（同时也会使**候选栏**的高亮候选边框产生圆角）
- `alpha`: 悬浮窗透明度*（`0x00~0xff`。0x00 为全透明）
- `background`
    - [3.2.3]❌~~悬浮窗背景*（颜色或图片二选一。比如颜色：0xFFD3FF83；图片：xxx.jpg。图片格式 jpg 与 png 皆可，相应的图片需放置在用户文件夹的 backgrounds 目录下，放在共享文件夹无效~~
- `elevation`: 悬浮窗阴影
- `movable`: 是否可移动窗口，或仅移动一次 true|false|once

### window
> 编码、候选项等组件 [window](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#4悬浮窗口)
#### 窗口移动图标
- `- {start: "", move: 'ㄓ ', end: ""}`  
    当`movable`设为可移动时，拖动这个图标即可调整悬浮窗的位置。`move`可改为任意符号，`start` `end`为左右修饰符号，若不需要修饰可简化为`{move: 'ㄓ '}`。
#### 编码
- `- {start: "", composition: "%s", end: "", letter_spacing: 0}`  
    `composition`若去掉则不显示编码区。`letter_spacing`为字符间距
#### 候选项
- `- {start: "\n", label: "%s.", candidate: "%s", comment: " %s", end: "", sep: " "}`  
    `start: "\n"`表示这个组件另起一行，`label`候选项序号，`candidate`候选项，`comment`候选项注释，`sep`候选项分隔符。（除`candidate`外，其它都是可选的。比如删掉`label`则不显示候选项序号）
#### 其他按键
> 另外还可以在悬浮窗内放置普通按键，比如地球拼音的声调键：
- `- {start: "\n", click: ";", label: " ˉ ", align: center, end: " "}`  
    #`click: ";"` `label: " ˉ "`作用与键盘按键相同。`align`对齐方式，left 左对齐|right 右对齐|center 居中，默认为左对齐可省略不写（align 每行组件只需写一个，也可用于上面的编码与候选）
- `- {click: "/", label: " ˊ ", end: " "}`  
    #`end: " "`的作用是在按键间形成间隙
- `- {click: ",", label: " ˇ ", end: " "}`
- `- {click: "\\", label: " ˋ "}`


## fallback_colors
[fallback_colors](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#二fallback_colors)
[[#style]]未定义的颜色，在这里补充
因为这个机制，最少只需要`back_color`和`text_color`就可以做出一个配色方案

## preset_color_schemes
[preset_color_schemes](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#三preset_color_schemes)
配色方案
### dark_scheme
表示当前是明亮模式，如果系统切换为深色模式，则自动切换到值对应的方案
`dark_scheme: dark`
### 颜色格式
- `red`、`green`、`blue`……
- `0xaarrggbb`
- `0xrrggbb` （省略了 aa，表示完全不透明）
- `"#aarrggbb"` （引号不能省略，否则会与注释冲突）
- `"#rrggbb"` （同上）
- `0xaa`
### [[soft/rime/trime-color]]

## android_keys
❌内置按键以及各种可用的条件、功能查阅，一般没什么用了。见[[#preset_keys]]
[android_keys](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#四android_keys)

### when
- `click`: ✅单击
- `long_click`: ✅长按，按键字符同`hint`
- `composing`: ✅输入状态标签（处于输入过程中）
- `swipe_left`: ✅左滑
- `swipe_right`: ✅右滑
- `swipe_up`: ✅上滑
- `swipe_down`: ✅下滑
- `ascii`: 西文标签（处于英文状态时）
- `paging`: 翻页标签（翻页时）
- `has_menu`: 菜单标签（出现候选项时——非空码时）
- #`always`: 始终
- #`hover`: 滑过
- `combo`: 并击
- #`double_click`: 双击

### property
#### label
✅中文状态的按键标签
#### hint
✅按键助记（用于显示双拼的韵母等，显示在按键下方，修改颜色见[[soft/rime/trime-color#key_symbol_color]]）
#### preview
✅按键气泡提示，默认读取`label`，空格键默认读取输入方案名
#### send_bindings
用来控制`composing`、`has_menu`、`paging`时是否发送按键给后台（默认`true`：发送；`false`：不发送，仅改变按键标签，按键的实际功能仍是`click`）
#### states
状态标签（用于切换开关的状态）
#### width
#### height
#### shift_lock
Shift、Ctrl、Alt、Meta 等修饰键的锁定方式（click：单击锁定，可用于「选择」键；long：长按锁定（`默认`）；ascii_long：仅英文状态长按锁定）
#### repeatable
长按重复
#### gap
间隔
- [3.2.6]`label_symbol`: 按键的符号标签（通常显示在按键字符上方，当缺少此参数时，显示 long_click 指定的预设按键的的 label）
- `enter_labels`：回车键的文本会动态变化[由App指定Enter键的文字 · Issue #669 · osfans/trime](https://github.com/osfans/trime/issues/669)
#### functional
✅是否跟随功能键的颜色风格
### action
- `command`: 执行命令。目前内建支持的值包含：`liquid_keyboard paste_by_char broadcast clipboard date commit run share_text`,其他值会作为 Intent 处理
- `send`: ✅发送按键
- `option`: 命令参数
- `select`: 选择（键盘布局）
- `toggle`: 切换状态
- `commit`: 直接上屏 （用于输出各种网址邮箱等）
- `VOICE_ASSIST`语音输入
#### text
✅组合键，比如`(){left}`，不能直接用在键盘布局中，要定义到按键后，需要用`click`等绑定才生效
```yaml
- "{Escape}{/fh}"：清空前面的输入码并输入`/fh` （配合 symbols.yaml 可以输入符号）
- "「」{Left}{Keyboard_default}"：输出成对符号`「」`并把光标移到符号中间再返回主键盘
- "{Control+Left}"：逐词移动。（单个组合键也可以直接用`send: Control+Left`，`text`可以看作是组合键的组合）
```

```yaml
  Date: {label: 日期, send: function, command: date, option: " yyyy-MM-dd "}
  Time: {label: 時間, send: function, command: date, option: "HH:mm:ss"} #時間： date 格式
  TrimeApp: {label: 同文, send: function, command: run, option: "com.osfans.trime"} #運行程序: run 包名
  TrimeCmp: {label: 同文組件, send: function, command: run, option: "com.osfans.trime/.Pref"} #運行程序指定組件: run 包名/組件名
  Homepage: {label: 同文主頁, send: function, command: run, option: "https://github.com/osfans/trime"} #查看網頁: run 網址
  Wiki: {label: 維基, send: function, command: run, option: "https://zh.wikipedia.org/wiki/%s"} #搜索網頁: %s或者%1$s爲當前字符
  Google: {label: 谷歌, send: function, command: run, option: "https://www.google.com/search?q=%s"} #搜索網頁: %s或者%1$s爲當前字符
  MoeDict: {label: 萌典, send: function, command: run, option: "https://www.moedict.tw/%3$s"} #搜索網頁: %3$s爲光標前字符
  Baidu: {label: 百度搜索, send: function, command: run, option: "https://www.baidu.com/s?wd=%4$s"} #搜索網頁: %4s爲光標前所有字符
  Zdic: {label: 漢典, send: function, command: run, option: "http://www.zdic.net/sousuo/?q=%1$s"} #搜索網頁: %s或者%1$s爲當前字符
  Zdic2: {label: 漢典, send: function, command: run, option: "http://www.zdic.net/sousuo/?q=%2$s"} #搜索網頁: %2$s爲當前輸入的編碼
  WebSearch: {label: 搜索網頁, send: function, command: web_search, option: "%4$s"} #搜索，其他view、dial、edit、search等intent，參考安卓的intent文檔：https://developer.android.com/reference/android/content/Intent.html
```

## preset_keys
✅✅✅自定义按键，对[[#android_keys]]的补充
这里定义的键，默认[[#functional]]为true
> 如果指定的`name`在`android_keys`和`preset_keys`中都找不到，那就以文本形式直接输出（比如`{click: 你好}`，单击该键时，就直接输出「你好」）。在制作特殊符号键盘时，可能需要这种效果。
[preset_keys](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#五preset_keys)
[按键功能组合示例](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#按键功能组合示例)
```yaml
copy: {label: 复制, send: Control+c}
copy_all: {label: 全誊, text: "{Control+a}{Control+c}"} #全选并复制
`{click: v, composing: "'", long_click: ~, swipe_left: Date, swipe_right: Time}` #打字过程中输出 ', 平时单击输出 v，长按输出 ~ ，左滑输出日期，右滑输出时间
Keyboard_xxx: {label: 符号, send: Eisu_toggle, select: xxx}
```
### 切换键盘
`xxx_keyboard_switch: { label: 显示文字, send: function, command: liquid_keyboard, option: "符号表" }`

## preset_keyboards
[preset_keyboards](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#六preset_keyboards)
预置的键盘布局（一个主题里可以有多个键盘布局）
### keys
按键排列顺序  
✅✅✅键盘中每对`{}`代表一个按键，按`从左到右、从上到下`的顺序排列。每行的宽度排满`100`或虽然不足`100`但无法再容纳一个按键又或者每行按键数量达到`columns`的设定值时，转到下一行继续排列。
### name
布局名称
### author
作者信息
### ascii_mode
键盘的默认状态（`0`：中文；`1`：英文）
### ascii_keyboard
非标准键盘（比如注音、仓颉、双键等），在切换到英文模式时，自动跳转到这里设定的英文键盘（试验功能，有待完善）
### reset_ascii_mode
切换键盘、重新弹出键盘时，是否重置到当前 keyboard 指定的 ascii_mode 描述的状态（默认 false）。与`style/reset_ascii_mode`(指定弹出键盘时是否重置 ASCII 状态）配合使用。
### label_transform
中文模式下按键字母标签自动大写（`uppercase`：自动大写，仅对单个字母生效，长标签请直接更改 label；`none`：无，可省略不写）
### lock
在不同程序中切换时锁住当前键盘，不返回默认的主键盘。用于单手键盘等。（`true`：锁住；`false`：不锁，可省略不写）
### columns
键盘最大列数，超过则自动换行，默认 30 列。
### width
按键默认宽度（也可以在按键里面单独定义某个按键的宽度）
### height
每行的高度（要想改变单独一行的高度，可以直接在那一行行首的按键里设`height`）
### [3.2.6]`auto_height_index`
当使用`style/keyboard_height`参数锁定键盘高度时，由于像素只能取整数，如果缩放产生了余数，哪一行吸收缩放后的余数。第一行即 0，第二行为 1，以此类推；特别的，当值为负数时，为倒序序号（-1 即倒数第一个）;当值大于按键行数时，为最后一行。
### [3.2.6]`keyboard_height`
键盘锁定的高度。当 style 中锁定键盘高度时，如 preset_keyboard 再次指定键盘高度，则当前键盘以此为准
### [3.2.6]`keyboard_height_land`
横屏下键盘锁定的高度，同上
### key_hint_offset_x
助记符号 x 方向偏移量（向右为正，下同）
### key_hint_offset_y
助记符号 y 方向偏移量（向下为正，下同）
### key_symbol_offset_x
长按符号 x 方向偏移量
### key_symbol_offset_y
长按符号 y 方向偏移量
### key_text_offset_x
按键文本 x 方向偏移量
### key_text_offset_y
按键文本 y 方向偏移量
### key_press_offset_x：按键按下时所有文本 x 方向偏移量
### key_press_offset_y：按键按下时所有文本 y 方向偏移量  
    ※以上这几个 offset 也可以直接写在按键中，仅对该按键生效。
- `keys`
按键排列顺序  
    键盘中每对{}括号代表一个按键，按从左到右、从上到下的顺序排列。每行的宽度排满`100`或虽然不足`100`但无法再容纳一个按键又或者每行按键数量达到`columns`的设定值时，转到下一行继续排列。

### 布局调用

`trime.yaml`已经内置了很多种键盘布局，一般常用的输入方案都可以自动匹配到合适的预置键盘。  
※️`style/keyboards`中的`.default`，就是用来自动匹配键盘布局的。

自动匹配的过程：

- 如果输入方案的`schema_id`可以找到对应的键盘布局`ID`，则直接使用这个布局  
    比如仓颉五代的`schema_id`是`cangjie5`，在`trime.yaml`中刚好有`ID`为`cangjie5`的键盘布局，那就直接使用它。
- 如果匹配不了`ID`，那根据输入方案的`speller/alphabet`所用的字符，匹配最合适的布局方案  
    比如朙月拼音的`speller/alphabet`是`zyxwvutsrqponmlkjihgfedcba`，恰好使用了 26 个英文字母。那就自动套用`预设26键`键盘。
- 如果`ID`和`speller/alphabet`都匹配不到，就用默认的`预设26键`键盘。

如果自动匹配的布局不理想，还可以手动设置。如下面的示例。

#### [](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3#示例指定朙月拼音使用-36-键键盘布局)示例：指定朙月拼音使用 36 键键盘布局

（36 键键盘比 26 键的多了一排数字键，可以快捷输入数字）

# trime.custom.yaml
```
patch:
  "preset_keyboards/luna_pinyin/import_preset": qwerty0 #预设36键布局的ID是qwerty0
```

如是即可。

再看看，重新部署后，补丁融入`trime.yaml`之中，就被展开成这种格式：

luna_pinyin:
  import_preset: qwerty0

可以理解成：新建了一个`ID`是`luna_pinyin`的布局，这个布局导入了`qwerty0`的全部设置。

⚠ 如果这里指定的键盘出错了，就会自动调用`default`键盘。
