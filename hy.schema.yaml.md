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
如果本方案依赖于其它方案〔通常来说会依頼其它方案`反查`，抑或是`多种方案混用`时〕，填写其他方案的[[#schema_id]]列表
- [ ] 这里定义后，是编译时会把词库关联起来吗？

## menu
### page_size
优先级比 [[soft/rime/default.custom.yaml#page_size]]高
候选项个数（不超过10，会无法选字）`page_size: 10`

## switches
[[soft/rime/switches]]
## engine
[[soft/rime/engine|engine]]
