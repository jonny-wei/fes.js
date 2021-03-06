# FES 文档

## 建议解决方案

* 更新日志可以接入 commit 工具，根据 commit msg 自动生成更新日志
* 国际化描述有点过时，根据 fes-ui 的国际化需求，及时更新
* 组件文档需要及时更新，为了避免后续文档割裂问题
  * 将 fes-ui 下的 example 切换成 doc 一样的格式，通过脚本一键同步文档

## fes 文档

fes 主要解决的问题在于：

* 构建：一键完成中后台系统的脚手架
* 组件库：提供一套比较完善的组件库支持
* 路由：开发者不需要关心路由的实现
* 国际化：开发者不太需要管计划怎么实现
* 权限：对路由级别的权限控制又比较好的支持
* filer: 提供多种 filer、map 做内容的映射
* api Mock: 提供 api mock 的能力
* 静态文件：提供静态文件的能力
* 登录：内置 sso 登录功能
* 内置 eslint 规范
* 数据存储
* 状态管理

### 对未来的期望

* 分析 fes 构建并进行优化
  * 不支持高版本的 node
  * 构建输出需要优化，目前只改一个文件，几乎更新了每一个文件。理论上我只更新一个业务 js，只更新一个 chunk
* 模块化
  * 目前的实现 page 下面的组件都会解析成 page，但是之前看外包代码的时候，很多外包还是会把页面级别的模块放在 page 下面。
  * page 页面也有很多需求需要进行组件拆分，建议在 page 下加个 components 目录的支持，components 下的模块不会解析成 page。
  * 比如 page/a/components 那么这些 components 只能放 a 页面的 components，这样不会全部放在 src/components 下，显的比较乱
* 路由
  * 对路由的规则能进一步梳理，避免出现死循环。（现在已有三个参数控制、需要注释才能理解代码了）。
* 页面 API
  * 对于写 fes 的用户，他们必须要了解 vue 的基本语法。又需要知道 fes 语法，会增加用户理解 fes 负担。
  * 对于 fesData | fes 生命周期等，我认为可以直接使用 vue。没必须再造一套概念。
* FesApp ｜ FesUtil | FesApi 傻傻分不清？
  * 建议可以把这些概念化整为零。像 vue | koa 等的设计、所有的 API 注入到一个地方。用户通过统一的接口调用就行。
  * 不需要关心: 这个 API 是那个暴露的
* FesFesx
  * 建议进行优化，使其表现的更为 vuex，复合大部分人的认知。
* fesHeader | fesLeft
  * 这两个组件为非必填项，应该可以自行决定是否删除
  * 可以根据是否存在 `fes-left`, `fes-header` 来决定是否显示，这样还可以减少 fes.config 的两个配置
* 提供更为丰富的模版，逐步逼近 fes 愿景
* 上单元测试，改代码不方
