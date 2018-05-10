# npm & package.json

## npm

> node package manager

### npm 网站

- [npmjs.com](https://www.npmjs.com/)

### npm命令行工具

查看版本：

```shell
npm --version
```

升级 npm:

```shell
npm istall --global npm
```

### 常用命令

- npm init
  - npm init -y 可以跳过向导，快速生成
- npm install
  - 一次性把dependencies选项中的依赖项全部加载
  - npm i
- npm install 包名
  - 只下载
  - npm i 包名
- npm install--save 包名
  - 下载并保存依赖项(package.json文件中的dependencies选项)
  - npm i -S 包名
- npm uninstall 包名
  - 只删除，如果有依赖项依然会保存
  - npm un 包名
- npm uninstall --save 包名
  - 同时删除依赖项
  - npm un -S 包名
- npm help 
  - 查看帮助
- npm 命令 --help
  - 查看指定命令的使用帮助

### 解决npm被墙问题

> http://npm.taobao.org 淘宝的开发团队把npm在国内做了一个备份

- 安装淘宝的cnpm

  - ```shell
    # 在任意目录执行都可以
    # --global表示安装到全局
    # --global不能省略，否则不管用
    npm install --global cnpm
    ```

- 装包时把npm换成cnpm

- 或者，不想安装cnpm又想使用淘宝的服务器来下载

  - ```shell
    npm install xxx --registry=https://registry.npm.taobao.org
    ```

  - 进一步可以将 --registry选项加入配置文件中

    - ```shell
      npm config set registry https://registry.npm.taobao.org
      ```

## package.json

- 每个项目都要有一个package.json文件（包描述文件），这个文件可以通过npm init的方式自动初始化出来