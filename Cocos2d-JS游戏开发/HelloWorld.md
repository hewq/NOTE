# HelloWorld

## Cocos Console

	`Cocos Console` 是 Cocos2d-x 引擎下的一个命令行工具，它用来管理 Cocos 工程，其中包含**创建、运行、编译、调试以及打包项目等**。

 	Cocos Console 位于引擎包 cocos2d-x/tools/cocos2d-console 目录下，通过运行引擎包目录下的 setup.py 脚本即可安装。在安装的过程中，Cocos Console 需要开发者提供 Android NDK、Android SDK 和 Apache ANT 的文件路径。

	另外，Cocos Console 是一个采用 Python 语言编写的跨平台脚本工具，所以在安装 Cocos Console 之前，需要先安装好 Python。

### 安装 Python

#### Mac OS X

- 下载

  在 Mac OS X 中，操作系统本身自带了 Python。若你的 Mac OS X 系统中没有 Python，可在 [https://www.python.org/downloads/index.html](https://www.python.org/downloads/index.html) 下载安装。

- 安装

  在 Mac OS X 上，Python 的安装较为简单，双击打开 .pkg 文件，然后一直点击“继续”按钮，即可完成安装。

- 验证

  在 Mac OS X 上，可以打开终端，输入 `python --version` 验证是否安装成功。

#### Windows

- 下载

  在 Windows 操作系统中，Python 则需要我们自行下载并安装，下载地址为：[https://www.python.org/downloads/index.html](https://www.python.org/downloads/index.html) 

- 安装

  - Python 安装：双击下载的 .msi 文件，将 Python 安装在指定的磁盘路径下（这里将 Python 安装到 C:\Python27）。
  - 环境变量配置
    - 右击“我的电脑”，进入“属性”菜单，在“属性”菜单中选择“高级系统设置”，打开“环境变量”对话框；
    - 编辑“系统变量”中的“path”，在变量值的最后输入 Python 的安装路径，并在路径前面加上一个分号，例如 `;C:\Python27`；
    - 点击“确定”按钮关闭窗口。至此，Windows 上的 Python 安装成功。

- 验证

  打开命令行工具，输入 `ptyhon --version` 验证。

###  Android 环境配置

	当安装好 Python 之后，便可以开始准备 Android 相关的软件包了。如果不需要支持 Android，除了 Apache Ant 之外，其余步骤可以跳过，不必配置。Android 所需的相关软件包如下所示。

- Apache Ant: 将软件编译、测试、部署等步骤联系在一起加以自动化的一个工具，大多用于 Java 环境中的软件开发。下载地址：[http://ant.apache.org/bindownload.cgi](http://ant.apache.org/bindownload.cgi)。

- Android SDK: 即 Software Development Kit 的简称，中文译为软件开发工具包。在 Android 中，它为开发者提供了库文件以及其他开发所用到的工具。下载地址：[http://developer.android.com/tools/sdk/ndk/index.html](http://developer.android.com/tools/sdk/ndk/index.html)

- Android NDK: 即 Native Development Kit 的简称，它是一系列工具的集合，可以帮助开发者快速开发 c/c++ 的动态库。另外，它还能自动将 .so 文件和 Java 应用一起打包成 .apk 。下载地址： [https:// developer.android.com/sdk/index.html?hl=sk](https://developer.android.com/sdk/index.html?hl=sk)

- JDK: Java 的开发工具包，包括 Java 运行环境、Java 工具和 Java 基础类库。下载地址： [https://www.oracle.com/downloads/index.html](https://www.oracle.com/downloads/index.html)

  当下载好以上所需要的依赖后，便可以正式安装 Cocos Console 了。此时打开终端进入 Cocos2d-x 引擎目录下，然后运行 setup.py 脚本根据提示操作即可。

## 创建、编译和运行工程

当 Cocos Console 安装完毕后，便可通过 Cocos Console 创建 Cocos2d-JS 工程，具体有如下几种方式：

- 创建一个名为 projecName，并同时包含 Cocos2d-HTML5 和 Cocos2d-x JSB 的项目

  ```shell
  cocos new projectName -l js
  ```

- 创建一个名为 projectName，且仅包含 Cocos2d-HTML5 的项目， --no-native 表示不需要支持 Native 平台（iOS、Android、Mac、Windows 等），仅支持浏览器即可。

  ```shell
  cocos new projectName -l js --no-native
  # --no-native 用于 cocos studio, cocos studio 已被取消，所以该参数已被删除
  ```

- 在桌面上创建一个名为 projectName 的项目

  ```shell
  cocos new projectName -l js -d ./Desktop
  ```

- 在桌面上创建一个名为  projectName 的项目，并设置为竖屏

  ```shell
  cocos new projectName -l js -d ./Desktop --portrait
  ```

当项目创建完毕后，可以通过命令 `cocos run -p web` 将项目运行在浏览器中.

除创建命令外， Cocos Console 还为工程提供了运行、编译等命令，具体如下：

```shell
# 运行在指定的平台上
cocos run -p web|ios|android|mac|win32
# 将项目工程打包到指定的平台上
cocos compile -p web|ios|android|mac|win32 -m release
```

## 项目的目录结构

| 目录或文件名               | 内容简介                                                     |
| -------------------------- | ------------------------------------------------------------ |
| CMakeLists.txt             | Cocos Console 编译时所依赖的文件                             |
| frameworks                 | 包含 Web 引擎和 Native 引擎                                  |
| frameworks > cocos2d-html5 | Cocos2d-HTML5 游戏引擎                                       |
| frameworks > cocos2d-x     | Cocos2d-x 游戏引擎                                           |
| frameworks > runtime-src   | 各平台的项目工程文件，包含 iOS、Mac OS X、Android 以及 Windows 等 |
| index.html                 | Web 工程等主页面，其主要内容和职责如下：1. 包含用于显示游戏场景的 canvas 元素；2. 引入用于引擎初始化和加载的引擎脚本：CCBoot.js；3. 引入游戏启动的入口脚本： main.js；4. 包含一些适配移动端浏览器页面的 meta 元素 |
| main.js                    | 游戏入口文件，其中包含游戏初始化代码以及启动代码             |
| manifest.webapp            | 热更新配置文件                                               |
| project.json               | 工程配置文件                                                 |
| publish                    | 该目录初始状态下不存在，当工程以发布模式打包后，会创建该文件夹并保存对应平台的发布包 |
| Runtime                    | 该目录初始状态下不存在，用来存储调试模式打包的工程执行文件   |
| res                        | 项目资源文件夹，用来存储所有图片、音频、字体以及动画等资源   |
| res > HelloWorld.png       | 默认资源图片                                                 |
| res > loading.js           | 浏览器上页面启动的 loading 效果                              |
| src                        | 项目脚本文件夹，用来存储游戏的所有 javascript 代码           |
| src > app.js               | 项目代码                                                     |
| src > resource.js          | 资源的全局变量定义                                           |

其中，project.json 为项目配置文件，其内容如下所示：

```json
{
    "project_type": "javascript",

    "debugMode" : 1,
    "showFPS" : true,
    "frameRate" : 60,
    "noCache" : false,
    "id" : "gameCanvas",
    "renderMode" : 0,
    "engineDir":"frameworks/cocos2d-html5",

    "modules" : ["cocos2d"],

    "jsList" : [
        "src/resource.js",
        "src/app.js"
    ]
}

```

各属性的意义如下：

- project_type：项目类型
- debugMode：表示程序的调试级别，默认值是 1，可选值为 0 到 6
  - 0 ：不显示任何调试信息；
  - 1 ：cc.error、cc.assert、cc.warn、cc.log 在调试终端中打印信息，这是默认值。
  - 2 ：cc.error、cc.assert、cc.warn 在调试终端中打印信息；
  - 3 ：cc.error、cc.assert 在调试终端中打印信息；
  - 4 ：cc.error、cc.assert、cc.warn、cc.log 在 canvas 上显示消息，这是 Cocos2d-HTML5 引擎独有的功能。这在**微信开发**上是一个非常有用的功能；
  - 5 ：cc.error、cc.assert、cc.warn 在 canvas 上显示消息，这是 Cocos2d-HTML5 引擎独有的功能；
  - 6 ：cc.error、cc.assert 在 canvas 上显示消息，这是 Cocos2d-HTML5 引擎独有的功能。
- showFPS：若其值为 true，则游戏窗口坐下角会显示绘制函数调用次数、渲染时间以及帧率。默认取值为 true，项目打包上线时，应将其设置为 false。
- frameRate：设置期望帧率。游戏中的实际帧率会取决于游戏每帧消耗时间和运行平台等条件，期望帧率会保证游戏运行帧率不会超过期望帧率，并尽力运行在期望帧率上。
- noCache：设置是否让浏览器缓存 html 页面
- id：web 引擎页面中 canvas 元素的 id，仅服务于 Cocos2d-HTML5 引擎
- renderMode：引擎绘制模式，仅服务于 Cocos2d-HTML5 引擎，在 Native 上无效，其值的可取范围为 0 ～ 2，表示意义如下：
  - 0 ：由引擎自动选择绘制模式，遵循“择优选择”的理念，即若支持 WebGL，则优先考虑使用 WebGL 绘制，否则采用 canvas 绘制；
  - 1 ：强制使用 canvas 绘制模式；
  - 2 ：强制使用 WebGL 绘制模式，但是实际上 WebGL 仍然可能会在一些移动浏览器上被忽略而自动使用 canvas 绘制模式。
- engineDir：Cocos2d-HTML5 引擎路径，仅在 debug 模式下有效，保持默认值即可。如果采用 Cocos2s-JS Lite 版开发游戏，则此字段可以忽略。
- modules：模块配置。可将游戏中需要引入的模块添加到此数组中，例如游戏中需要 Chipmunk 物理引擎支持，则应该在此数组中添加 chipmunk 字符串。此配置仅服务于 Cocos2d-HTML5 引擎，当 Cocos Console 在发布模式下编译生成时，会根据 modules 中所包含的模块进行打包。所以，modules 应当保持精简，按需取值，避免打出的包中引入了没有用到的模块，增大了游戏脚本的大小。关于存在哪些模块以及每个模块的定义，可以参考 `frameworks/cocos2d-html5/modulesConfig.json` 文件
- jsList：开发者的 JS 脚本游戏逻辑代码列表，游戏中所依赖的脚本都应该放入这个列表中。此外，应当注意这些 JS 文件的相互依赖关系以及加入先后顺序。

## 项目在 Web 和 Native 上的启动流程

Cocos2d-JS 是一个跨浏览器和原生平台的游戏引擎，在对应平台上的启动流程自然也有所不同。

### web

在 web 上，index.html 生成 canvas，并加载 CCBoot.js 文件，然后 CCBoot.js 读取 project.json 文件，从而预加载 resource.js 以及 jsList 中所有的 .js 文件。到此，游戏中所有的代码被加载完毕。随后，index.html 又引入 main.js 文件，最终 main.js 启动了游戏。整个过程的代码如下：

```html
<body style="padding: 0; marign: 0; background: #000;">
	<script src="res/loading.js"></script>
    <canvas id="gameCanvas" width="800" height="450"></canvas>
    <script src="frameworks/cocos2d-html5/CCBoot.js"></script>
    <script cocos src="main.js"></script>
</body>
```

### Native

在 Native 中，Cocos2d-JS 工程的启动流程相对简单一些。打开 `frameworks/runtime-src/Classes/AppDelegate.cpp` 文件，可以在 AppDelegate 类的 applicationDidFinishLaunching 函数中看到如下代码：

```c++
bool AppDelegate::applicationDidFinishLaunching () {
    // 导演初始化
    auto director = Director::getInstance();
    auto glview = director->getOpenGLView();
    if(!glview) {
        ...
    }
    director->setAnimationInterval(1.0 / 60); // 帧率设置
    // 获取脚本引擎（SpiderMonkey）单例对象
    ScriptingCore* sc = ScriptingCore::getInstance();
    sc->addRegisterCallback(register_all_cocos2dx);
    sc->addRegisterCallback(register_cocos2dx_js_core);
    sc->addRegisterCallback(jsb_register_system);
    // ...
    sc->start();
    sc->runScript("script/jsb_boot.js"); // 运行 jsb_boot.js 脚本
    // ...
    ScriptEngineProtocol *engine = ScriptingCore::getInstance();
    ScriptEngineManager::getInstance()->setScriptEngine(engine);
    ScriptingCore::getInstance()->runScript("main.js");
    return true;
}
```

在代码中 `sc->runScript("script/jsb_boot.js")` 运行了 jsb_boot.js 脚本，此脚本中同样读取 project.json 配置文件，然后 `ScriptingCore::getInstance()->runScript("main.js")` 运行 main.js 文件，从而进入游戏。

> 说明：Native 即为原生操作系统平台，例如 iOS、Android、Mac OS X 等。总之，在 Cocos2d-JS 中，除了浏览器外，都可以称为 Native。