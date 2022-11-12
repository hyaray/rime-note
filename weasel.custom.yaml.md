- 和操作系统相关，配置不太多
## app_options
- [ ] cmd.exe设置无效，如果小狼毫能全局默认英文，此bug则可无视
```
explorer.exe: {ascii_mode: true}
cmd.exe: {ascii_mode: true}
```
preset_color_schemes
## style
- `color_scheme`=当前使用的style
![[附件/小狼毫配色.png]]
[Rime-See-Me/](https://bennyyip.github.io/Rime-See-Me/)
- 注意，颜色是BGR
```
- font_face：DejaVu Sans Mono for Powerline
- font_point：13 #字号
- horizontal：false #是否横向
- fullscreen
- inline_preedit
- preeedit_type
- display_tray_icon：true 显示托盘图标
- label_format
    - "%s."
- layout
    > 候选框样式
    - min_width
    - min_height
    - border_width
    - margin_x
    - margin_y
    - spacing
    - candidate_spacing
    - hilite_spacing
    - hilite_padding
    - round_corner：圆角
- color_scheme
    - name: 青天／Azure #当前使用样式
    - author:
    - text_color: 0xffe8ca
    - candidate_text_color: 0xfff8ee
    - back_color: 0x8b4e01
    - border_color: 0x8b4e01
    - hilited_text_color: 0xfff8ee
        - 当前项文字颜色
    - hilited_back_color: 0x8b4e01
        - 当前项背景颜色
    - hilited_candidate_text_color: 0x7ffeff
        - 当前项文字颜色
    - hilited_candidate_back_color: 0xa95e01
    - comment_text_color: 0xc69664
```
