- [✅✅✅必知必会-创作输入方案](https://github.com/rime/home/wiki/RimeWithSchemata)
- [✅Schema.yaml](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md)

- [输入方案下载](https://github.com/rime/plum#packages)
- [fkxxyz/rime-cloverpinyin](https://github.com/fkxxyz/rime-cloverpinyin/issues) 
- [oniondelta/Onio n_Rime_Files: 電腦 Rime 洋蔥方案（注音、雙拼、拼音、形碼、行列30）](https://github.com/oniondelta/Onion_Rime_Files)
- [雾凇拼音，我的 Rime 配置及新手指引](https://dvel.me/posts/my-rime)
- [我的 Rime 配置 2022 - Dvel](https://dvel.me/posts/my-rime-setting-2022)
- [特色功能-开源好用的98五笔输入法-基于Rime的高效五笔输入法](http://www.98wubi.com/tese.html)
## schema
### schema_id
唯一方案名称，在代码中引用此方案时以此名为正，通常由英文、数字、下划线组成

### name
### version
发布新版前确保升级版本号
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
### page_down_cycle
❌`page_down_cycle: true`
## switches
[[switches]]
## engine
[[engine]]
