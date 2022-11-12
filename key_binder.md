# key_binder
## 不在配置内
- [[soft/rime/default.custom.yaml#hotkeys|hotkeys]]不在此配置
- 上屏提示内容`Control+Shift+return`

## 可配置项
- `;'`选第`2/3`项
- `,.`候选翻页键
- 详见 `key_bindings.yaml`
指定按键设置为其他功能，比如逗号作为翻页键，在第一页的情况下（不需要上翻页），直接上屏当前字且输出逗号

## bindingg
### 参数说明
#### when
> 条件
- always
- has_menu 有多个选项
- paging 按过下一页
- composing 操作输入码
#### 做什么
- send: 发送按键, `escape`则为清空内容
- toggle: 切换开关
- select: `.next`
#### accept
> [[rime/按键]]

### 选中第2/3项
```yaml
{when: has_menu, send: 2, accept: semicolon} #分号次选
{when: has_menu, send: 3, accept: apostrophe} #撇号3选
```
### 翻页
```
{accept: minus, send: Page_Up, when: paging} #-
{accept: equal, send: Page_Down, when: paging} #=

{accept: comma, send: Page_Up, when: paging} #,
{accept: period, send: Page_Down, when: paging} #.
```
