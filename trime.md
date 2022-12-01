# trime
[使用说明](https://github.com/osfans/trime/wiki/UserGuide)
[trime.yaml詳解](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3)
build文件夹，推荐由PC转过去

## 步骤
1. 手机安装release版，`3.2.9`选`配色`有bug，可以先用3.2.8，新版本肯定会修复。
2. 复制小狼毫的用户文件夹大部分文件，以下是排除列表
    - weasel.custom.yaml
    - weasel.yaml
    - installation.yaml
    - user.yaml
    - rime.dll
    - opencc 如果用`ocd`格式，需要用64位的 `opencc_dict` 编译
        - [ ] 用了txt仍无效，需要？？？
1. 同文不像小狼毫自带几个输入方案，所以还要从[[共享文件夹]]复制
    - default.yaml
    - 关联输入方案的`schema.yaml`文件
2. 部署功能因为没有日志非常难受，所以暂时就依赖PC把大部分依赖都build好迁移

## style
### auto_caps
自动句首大写（`true`:打开;`false`:关闭;`ascii`:仅英文模式句首大写）
### candidate_use_cursor
是否打开候选焦点高亮
### comment_on_top
候选项注释是否在上方（`false`:在右侧）
### horizontal
[3.2.3]水平模式。改变方向键的功能（`true`：方向键适配横排候选；`false`：方向键适配竖排候选）
### keyboards
键盘配置。除主键盘外，其它需要用到的键盘都要在这里声明。
### proximity_correction
将按键之间的空白区域分配给相邻的按键，避免空按（`true`:打开；`false`:关闭）
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

## layout
> 候选窗口设置
-   `position`: 悬浮窗位置
    -   `left`|`right`|`left_up`|`right_up` 这几种都可以让悬浮窗口动态跟随光标（需要 ≥Android5.0）
    -   `fixed`|`bottom_left`|`bottom_right`|`top_left`|`top_right` 这几种是固定在屏幕的边角上
-   `min_length`: 悬浮窗最小词长（候选词长大于等于`min_length`才会进入悬浮窗）
-   `max_length`: 连续排列的多个候选项总字数（包括候选项注释）超过`max_length`时，把超出的候选项移到下一行显示（单个候选项若超长，或者`max_length`数值过大，则由`max_width`决定是否换行）
-   `sticky_lines`: 固顶行数（不与其它候选同排，单独一行显示的候选项个数）
-   `max_entries`: 最大词条数（允许进入悬浮窗的最大词条数）
-   `all_phrases`: 显示所有长词。所有满足`min_length`的词条都显示在悬浮窗（一般只用于 table translator，有可能会改变候选项的显示顺序）
-   `border`: 边框宽度（增大边框则向内加粗，也会对悬浮窗圆角产生一点影响）
-   `max_width`: 窗口最大宽度（候选超长则自动换行）
-   `min_width`: 最小宽度（悬浮窗的初始宽度）
-   `margin_x`: 水平边距（左右留白大小）
-   `margin_y`: 竖直边距（上下留白大小）
-   `line_spacing`: 候选词的行间距（px）
-   `line_spacing_multiplier`: 候选词的行间距倍数
-   `spacing`: 悬浮窗位置上下偏移量（一般上移为正，下移为负，但当`position`设为 top_xxx 时，方向是相反的）
-   `round_corner`: 窗口圆角（同时也会使**候选栏**的高亮候选边框产生圆角）
-   `alpha`: 悬浮窗透明度*（0x00~0xff。0x00 为全透明）
-   [3.2.3]~~`background`: 悬浮窗背景*（颜色或图片二选一。比如颜色：0xFFD3FF83；图片：xxx.jpg。图片格式 jpg 与 png 皆可，相应的图片需放置在用户文件夹的 backgrounds 目录下，放在共享文件夹无效~~
-   `elevation`: 悬浮窗阴影（≥Android5.0）
-   `movable`: 是否可移动窗口，或仅移动一次 true|false|once

## window
> 候选窗口组件
### 窗口移动图标
-   `- {start: "", move: 'ㄓ ', end: ""}`  
    当`movable`设为可移动时，拖动这个图标即可调整悬浮窗的位置。`move`可改为任意符号，`start` `end`为左右修饰符号，若不需要修饰可简化为`{move: 'ㄓ '}`。
### 编码
-   `- {start: "", composition: "%s", end: "", letter_spacing: 0}`  
    `composition`若去掉则不显示编码区。`letter_spacing`为字符间距，需要 ≥Android5.0。
###  候选项
-   `- {start: "\n", label: "%s.", candidate: "%s", comment: " %s", end: "", sep: " "}`  
    `start: "\n"`表示这个组件另起一行，`label`候选项序号，`candidate`候选项，`comment`候选项注释，`sep`候选项分隔符。（除`candidate`外，其它都是可选的。比如删掉`label`则不显示候选项序号）
### 其他按键
> 另外还可以在悬浮窗内放置普通按键，比如地球拼音的声调键：
-   `- {start: "\n", click: ";", label: " ˉ ", align: center, end: " "}`  
    #`click: ";"` `label: " ˉ "`作用与键盘按键相同。`align`对齐方式，left 左对齐|right 右对齐|center 居中，默认为左对齐可省略不写（align 每行组件只需写一个，也可用于上面的编码与候选）
-   `- {click: "/", label: " ˊ ", end: " "}`  
    #`end: " "`的作用是在按键间形成间隙
-   `- {click: ",", label: " ˇ ", end: " "}`
-   `- {click: "\\", label: " ˋ "}`