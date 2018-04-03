# Node.js介绍

### 1. Node.js是什么

- Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). 
  - Node.js不是一门语言
  - Node.js不是库，不是框架
  - Node.js是一个JavaScript运行时环境
  - Node.js可以解析和执行JavaScript代码，以前只有浏览器可以解析执行JavaScript代码，现在的JavaScript完全可以脱离浏览器来运行 
- 浏览器中的JavaScript
   * EcmaScript
     * 基本语法
     * if
     * var
     * function
     * Object
     * Array
  * BOM
  * DOM
- Node.js中的JavaScript
  * 没有BOM,DOM
  * EcmaScript
  * 在node这个JavaScript执行环境中为JavaScript提供了一些服务器级别的操作API
    * 例如文件读写
    * 网络服务的构建
    * 网络通信
    * http服务器
    * 。。。
- 构建于chrome的v8引擎之上
  * Google Chrome的v8引擎是目前公认的解析执行JavaScript代码最快的
  * Node.js的作者把 Google Chrome中的v8引擎移植了出来，开发了一个独立的JavaScript运行环境。
- Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. 
  * Event-driven 事件驱动
  * non-blocking I/O model 非阻塞IO模型（异步）
  * lightweight and efficient 轻量和高效
- Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.
  * npm是世界上最大的开源库生态系统
  * 绝大多数的javascript相关的包都存放在npm上，可以让开发人员更方便地去下载使用。


### 2. Node.js能做什么

* Web服务器后台
* 命令行工具