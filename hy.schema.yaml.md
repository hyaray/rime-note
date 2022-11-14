## schema
### schema_id
唯一方案名称，在代码中引用此方案时以此名为正，通常由英文、数字、下划线组成

### name
### version
发布新版前确保升级版本号
- [ ] 具体用途？
### author
### description
### dependencies
> 填写其他方案的[[#schema_id]]列表
> 定义后，[[用户文件夹#build|build]]会生成`xxx.reverse.bin`文件
#### 场景
1. 反查
2. 多种方案混用

#### 相关
[[#dependencies]]和[[default.custom.yaml#schema_list]]区别
1. 前者是输入方案内部使用，

## menu
### page_size
优先级比 [[default.custom.yaml#page_size]]高
候选项个数（不超过10，会无法选字）`page_size: 10`
### alternative_select_keys
> 指定选字上屏的热键(代替`12345`)
> 当数字键有其他用时，比如？
`alternative_select_keys: aeiou`

## switches
[[switches]]
## engine
[[engine]]
