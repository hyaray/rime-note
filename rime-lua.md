[Rime_collections/Rime_description.md at master · LEOYoon-Tsaw/Rime_collections](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#七lua)
[[附件/rime/小狼毫版lua脚本使用教程.pdf]]
## api
- https://github.com/rime/weasel/issues/299
- https://github.com/rime/librime/issues/479
- https://github.com/rime/librime/blob/master/tools/rime_api_console.cc


## librime-lua
- [rime-lua文档](https://github.com/hchunhui/librime-lua/wiki/Scripting#脚本开发指南)
- [shewer/librime-lua](https://github.com/shewer/librime-lua/releases)
- [✅✅✅shewer/librime-lua-script](https://github.com/shewer/librime-lua-script)

## 更新
更新[[soft/rime/共享文件夹#rime.dll|rime.dll]]

## lua_processor
返回值为整数：
1. 0 kRejected 字符上屏
2. 1 `kAccepted` 字符不上屏
3. 2 kNoop，字符不上屏，交给下一个[[processor]]
参数:
1. key_event
2. env

## lua_segmention
返回值为整数：
1. 0 `kRejected` 字符上屏
2. 1 `kAccepted` 字符不上屏
3. 2 `kNoop`，字符不上屏，交给下一个[[processor]]
参数:
1. key_event
2. env

## lua_filter
> 针对[[候选框]]
> 见[[translators#lua_translator]]
使用lua自定义过滤，例如过滤字符集、调整排序，后接`@函数名`
lua函数名即用户文件夹内`rime.lua`中函数名，参数为`(input, env)`
可以`env.engine.context:get_option("option_name")`方式绑定到[[switches]]/[[key_binder]]
### input
translate 对象，为待过滤的 `Candidate` 流
### env
lua `table`对象，预设 `engine` 和 `name_space` 两个成员，分别是 `Engine` 对象和前述 `name_space` 配置字符串。

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
### engine
`env.engine`
#### 属性
1. schema
2. context
3. active_egine
#### 方法
1. process_key
2. compose
3. commit_text(text) 上屏文本
4. apply_schema
### context
> 输入编码上下文
> [context](https://github.com/hchunhui/librime-lua/wiki/Scripting#context)
`env.engine.context`
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
候选词
[Candidate](https://github.com/hchunhui/librime-lua/wiki/Scripting#keyevent)

`Candidate("date", seg.start, seg._end, os.date("%Y年%m月%d日"), "")`
#### yield
发送候选项到[[候选框]]
`yield(Candidate())`

### 获取
`env.engine.context:get_option("option_name")`获取[[switches#options]]当前值
`env.engine:compose(env.engine.context)`
`refresh_non_confirm_composition()`

## 应用
### 过滤字符集
1. 修改字库
