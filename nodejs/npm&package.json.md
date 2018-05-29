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

## package.json和package-lock.json

### package.json

- 每个项目都要有一个package.json文件（包描述文件），这个文件可以通过npm init的方式自动初始化出来。

### package-lock.json

- npm 5以前是不会有package-lock.json这个文件的，npm 5以后才加入这个文件。
- 当安装包的时候，npm都会生成或者更新package-lock.json这个文件。
- npm 5以后的版本安装包的时候不需要--save,它会自动保存依赖信息。
- package-lock.json这个文件会保存node_mohules中所有包的信息（版本、下载地址），这样的话重新`npm isntall`的时候速度就可以提升。
- 从文件来看，有一个`lock`锁
  - 这个`lock`是用来锁定版本的
  - 如果项目依赖了`1.1.1`版本，重新install其实会下载最新版本，而不是`1.1.1`
  - 所以这个pageage-lock.json文件的另一个作用就是锁定版本号，防止自动升级新版。