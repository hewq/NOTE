# Cocos2d-JS 介绍

## Cocos2d-JS 介绍

- Cocos2d-JS 是跨全平台的游戏引擎，采用原生 Javascript 语言，可发布到 web 平台、iOS、Android、Windows Phone 8、Mac、Windows 等平台。该引擎基于 MIT 开源协议，完全开源。

- Cocos2d-JS 是 Cocos2d-x 的 Javascript 版本。Cocos2d-JS 的前身为 Cocos2d-HTML5，在 3.0 版本之后，官方对 Web 引擎 Cocos2d-HTML5 和 Native 引擎 Cocos2d-x 进行整合，并为 Web 和各原生平台开发提供了一套统一的工作流，开发者只需要关注自己游戏的 Javascript 业务逻辑代码，然后使用 Cocos Console 工具管理开发以及发布等流程。

## 引擎目录结构

从 Cocos2d-x 3.7 版本之后，官方将 Cocos2d-JS 引擎整合到 Cocos2d-x 中。Cocos2d-x 引擎可在 Cocos 官网下载（[http://www.cocos.com/download/](http://www.cocos.com/download/)），也可以从 Cocos2d-x 的 GitHub 仓库拉取（[https://github.com/cocos2d/cocos2d-x](https://github.com/cocos2d/cocos2d-x)）。下载完成后，引擎包的主要内容如下：

| 目录或文件名         | 内容简介                                                     |
| -------------------- | ------------------------------------------------------------ |
| AUTHORS              | 作者目录，包含所有给 Cocos2d-x 引擎贡献代码的开发者          |
| build                | 包含测试例子、cocos2d_lib 的 Xcode 以及 Visual Studio 工程   |
| CHANGELOG            | 所有历史版本详细改动列表                                     |
| CMakeLists.txt       | cmake 配置文件                                               |
| cocos                | Cocos2d-x 引擎源代码                                         |
| CONTRIBUTING.md      | 贡献代码指南                                                 |
| docs                 | 包含 javascript 代码风格规范、当前发布说明和当前版本升级指南 |
| download-reps.py     | 下载第三方库的脚本                                           |
| extensions           | 第三方扩展                                                   |
| external             | 存放第三方库的文件夹                                         |
| licenses             | 所有许可协议                                                 |
| plugin               | 插件                                                         |
| README.cmake         | 针对 cmake 用法的说明文件                                    |
| README.md            | Cocos2d-x 引擎简介                                           |
| setup.py             | Cocos Console 的安装脚本                                     |
| templates            | Cocos Console 创建项目时使用的模板                           |
| tests                | 各分支的测试项目                                             |
| tools                | 工具文件夹                                                   |
| --bindings-generator | 脚本绑定工具                                                 |
| --cocos2d-console    | Cocos Console 工具                                           |
| --tojs               | JSB 自动绑定配置文件以及生成脚本                             |
| --tolua              | Lua 绑定配置文件以及生成脚本                                 |
| web                  | Cocos2d-JS 游戏引擎                                          |