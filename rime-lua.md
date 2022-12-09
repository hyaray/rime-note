[wik](https://github.com/hchunhui/librime-lua/wiki/Scripting)   
[[附件/rime/小狼毫版lua脚本使用教程.pdf]]
可以用在以下4个环节
- lua_processor@p_fun
- lua_segmentor@s_fun
- lua_translator@t_fun
- lua_filter@f_fun
## api
- https://github.com/rime/weasel/issues/299
- https://github.com/rime/librime/issues/479
- https://github.com/rime/librime/blob/master/tools/rime_api_console.cc

## 输入

### input
translate 对象，为待过滤的 `Candidate` 流
`input == "date"`

### seg
[[输入码#代码段]]在输入码中的位置
`seg.start`
`seg._end` 为什么要加`_`

### key_event
`KeyEvent` 对象，为待处理的按键。

### env
#### 属性
##### [[#engine]]
##### [[#name_space]]

## 对象
### engine
[engine](https://github.com/hchunhui/librime-lua/wiki/Scripting#engine)
`env.engine`
#### 属性
##### schema
##### [[#context]]
##### active_egine
#### 方法
##### process_key
##### compose
`env.engine:compose(env.engine.context)`
##### commit_text
上屏文本
`commit_text(text)`
##### apply_schema

### name_space

### context
[context](https://github.com/hchunhui/librime-lua/wiki/Scripting#context)
`env.engine.context`
> 输入编码上下文，在不同应用输入，会单独记录此对象
> [context](https://github.com/hchunhui/librime-lua/wiki/Scripting#context)
#### 属性
| 属性名 | 类型 | 解释 |
| :-: | :-: | :-: |
| composition | Composition |  |
| input | string | 正在输入的编码字符串 |
| caret_pos | number | 脱字符位置 |
| commit_notifier | Notifier |  |
| select_notifier | Notifier |  |
| update_notifier | Notifier |  |
| delete_notifier | Notifier |  |
| option_update_notifier | OptionUpdateNotifier | 选项改变通知，使用 connect 方法接收通知 |
| property_update_notifier | PropertyUpdateNotifier |  |
| unhandled_key_notifier | KeyEventNotifier |  |
#### 方法
##### get_option
`env.engine.context:get_option(optName)`获取[[switches#options]]当前值

`refresh_non_confirm_composition()`

## 调试
[工具](https://github.com/rime/librime/tree/master/tools)
## librime-lua
- [rime-lua文档](https://github.com/hchunhui/librime-lua/wiki/Scripting#脚本开发指南)
- [shewer/librime-lua](https://github.com/shewer/librime-lua/releases)
- [✅✅✅shewer/librime-lua-script](https://github.com/shewer/librime-lua-script)

## 更新
更新[[soft/rime/共享文件夹#rime.dll|rime.dll]]

## lua_processor
[lua_processor](https://github.com/hchunhui/librime-lua/wiki/Scripting#lua_processor)
返回值为整数：
1. `0` kRejected 字符上屏
2. `1` `kAccepted` 字符不上屏
3. `2` kNoop，字符不上屏，交给下一个[[processor]]

简化形式`processor(key_event[, env])`
完整形式:
```lua
{
   init = function (env) ... end,
   func = function (key_event, env) ... end,
   fini = function (env) ... end
}
```

## lua_segmention
简化形式:`s_xxx(segmentation[, env])`
完整形式
```lua
{
   init = function (env) ... end,
   func = function (segmentation, env) ... end,
   fini = function (env) ... end
}
```

参数:
1. segmentation:
2. env
返回值为整数：
1. 0 `kRejected` 字符上屏
2. 1 `kAccepted` 字符不上屏
3. 2 `kNoop`，字符不上屏，交给下一个[[processor]]

## lua_translator
[lua_translator](https://github.com/hchunhui/librime-lua/wiki/Scripting#lua_translator)
简化形式`t_xxx(input, seg[, env])`
完整形式
```lua
init = function (env) ... end --构造时调用
func = function (input, seg, env) ... end,
fini = function (env) ... end --析构时调用
```

## lua_filter
[lua_filter](https://github.com/hchunhui/librime-lua/wiki/Scripting#lua_filter)
简化形式`f_xxx(input[, env, cands])`
完整形式
```lua
init = function (env) ... end,
func = function (input, env) ... end,
fini = function (env) ... end,
tags_match = function (segment, env) ... end  --- 可选
```
> 针对[[候选框]]
> 见[[translators#lua_translator]]
使用lua自定义过滤，例如过滤字符集、调整排序，后接`@函数名`
lua函数名即用户文件夹内`rime.lua`中函数名，参数为`(input, env)`
可以[[#get_option]]方式绑定到[[switches]]/[[key_binder]]
- `input`：`Translation` 对象，为待过滤的 `Candidate` 流。
- `env`：lua table 对象。预设 `engine` 和 `name_space` 两个成员，分别是 `Engine` 对象和前述 `name_space` 配置字符串。

完整形式是 lua table，其中 `func` 与简化形式意义相同。`init` 与 `fini` 分别在 `lua_filter` 构造与析构时调用。`tags_match` 出现时覆盖 filter 的 `TagsMatch` 方法。
## 命令
### log
- info
- warning
- error
### ReverseDb
一般用在 init
- [ ] `coredb`是什么数据类型，应该怎么用
```
local function init(env)
  -- 当此组件被载入时，打开反查库，并存入 `coredb` 中
  env.coredb = ReverseDb("build/core2020.reverse.bin")
end
```


### config
[config](https://github.com/hchunhui/librime-lua/wiki/Scripting#config)
（方案的）配置。可以通过 `env.engine.schema.config` 获得
### KeyEvent
[KeyEvent](https://github.com/hchunhui/librime-lua/wiki/Scripting#keyevent)
### Preedit
### Composition
上下文组成的“作品”。（通过此对象，可间接获得“菜单menu”、“候选词”、“片段segment”相关信息）

可通过 `env.engine.context.composition` 获得。
```lua
local composition = env.engine.context.composition

if(not composition:empty()) then
  -- 获得 Segment 对象
  local segment = composition:back()

  -- 获得选中的候选词下标
  local selected_candidate_index = segment.selected_index

  -- 获取 Menu 对象
  local menu = segment.menu

  -- 获得（已加载）候选词数量
  local loaded_candidate_count = menu:candidate_count()
end
```
### segmention
[segmention](https://github.com/hchunhui/librime-lua/wiki/Scripting#segmentation)
### Segment
[✅✅✅Setment](https://github.com/hchunhui/librime-lua/wiki/Scripting#segment)
分词片段。触发 translator 时作为第二个参数传递给注册好的 lua_translator。
或者以下方法获得: （在 filter 以外的场景使用）
```lua
local composition =  env.engine.context.composition
if(not composition:empty()) then
  local segment = composition:back()
end
--构造方法：`Segment(start_pos, end_pos)`
--1.  start_pos: 开始下标
--2.  end_pos: 结束下标
```
### 候选项

```
local composition = env.engine.context.composition

if(not composition:empty()) then
  -- 获得 Segment 对象
  local segment = composition:back()

  -- 获得选中的候选词下标
  local selected_candidate_index = segment.selected_index

  -- 获取 Menu 对象
  local menu = segment.menu

  -- 获得（已加载）候选词数量
  local loaded_candidate_count = menu:candidate_count()
end
```

#### Candidate
生成候选项
[Candidate](https://github.com/hchunhui/librime-lua/wiki/Scripting#keyevent)
`Candidate("date", seg.start, seg._end, os.date("%Y年%m月%d日"), "注释")`

#### yield
发送候选项到[[候选框]]
`yield(Candidate())`

## 应用
### 过滤字符集
1. 修改字库
