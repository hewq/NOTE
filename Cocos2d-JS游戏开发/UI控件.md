# UI 控件

## ccui.Widget 父类

在 Cocos2d-JS 中，UI 的命名空间为 ccui 。ccui.Widget 是所有 UI 控件的父类，而 ccui.Widget 又间接继承自 cc.Node ，这使得所有的 UI 控件都具有 cc.Node 的特性；也就是说，每个 UI 控件都可以有坐标、大小等属性，也可以运行动作等。

**使用 UI 控件，需要在 project.json 的 modules 数组中添加“ccui”字符串**，代码如下：

```javascript
"modules": ["cocos2d", "ccui"]
```

ccui.Widget 中与触摸相关的 API

| 返回值  | 参数类型           | 函数                                    | 说明                                     |
| ------- | ------------------ | --------------------------------------- | ---------------------------------------- |
| 无      | Boolean            | setTouchEnabled(isEnable)               | 设置是否启用触摸事件                     |
| Boolean | 无                 | isTouchEnabled()                        | 判断是否启用触摸事件                     |
| 无      | Function, Object   | addTouchEventListener(selector, target) | 添加触摸事件的回调函数                   |
| 无      | Boolean            | setPropagateTouchEvents(isPropagate)    | 设置触摸事件是否允许向上传播父节点       |
| Boolean | 无                 | isPropagateTouchEvents()                | 获取触摸事件是否允许向上传播父节点的结果 |
| 无      | Boolean            | setSwallowTouches(isSwallow)            | 设置控件是否吞噬触摸事件                 |
| Boolean | 无                 | isSwallowTouches()                      | 判断控件是否吞噬触摸事件                 |
| Boolean | cc.Touch, cc.Event | onTouchBegan(touch, event)              | 触摸事件开始的回调函数                   |
| 无      | cc.Touch, cc.Event | onTouchMoved(touch, event)              | 触摸事件中触点移动时的回调函数           |
| 无      | cc.Touch, cc.Event | onTouchEnded(touch, event)              | 触摸事件结束时的回调函数                 |
| 无      | cc.Point           | onTouchCancelled(touchPoint)            | 触摸事件取消时的回调函数                 |

所有的 UI 控件都支持触摸事件。触摸开关默认是关闭的，你需要通过 setTouchEnabled(isEnable) 函数启用触摸，并且需要给控件一个触摸事件监听器，代码如下：

```javascript
node.addTouchEventListener(function (sender, type) {
    switch (type) {
        case ccui.Widget.TOUCH_BEGAN: 	// 触摸事件开始时响应
            break;
        case ccui.Widget.TOUCH_MOVED:	// 触摸事件中触点移动时响应
            break;
        case ccui.Widget.TOUCH_ENDED:	// 触摸事件结束时响应
            break;
        case ccui.Widget.TOUCH_CANCELED:	// 触摸事件取消时响应
            break;
        default:
            break;
    }
}.bind(this));
```

可以发现，UI 控件的触摸并不需要像给精灵添加触摸事件那样手动判断触点是否在精灵区域内，UI 默认的有效触摸区域为自身的大小。另外，在 Cocos2d-JS 3.3 之后，引擎提供了 setSwallowTouches(isSwallow) 函数接口，这使得 UI 控件的触摸也支持事件穿透了。

ccui.Widget 还有启用或禁用状态，其 API 如下：

| 返回值类型 | 参数类型 | 函数                  | 说明                   |
| ---------- | -------- | --------------------- | ---------------------- |
| 无         | Boolean  | setEnabled(isEnabled) | 设置是否启用控件       |
| Boolean    | 无       | isEnabled()           | 获取控件是否启用的结果 |

每个 UI 控件都可以设置启用或者禁用，默认值为 true。如果设置为 false，则控件是禁用的，不会响应触摸事件。

setBright(isBright) 用来设置控件的高亮显示，其相关 API 如下：

| 返回值类型 | 参数类型 | 函数                        | 说明                           |
| ---------- | -------- | --------------------------- | ------------------------------ |
| 无         | Boolean  | setHighlighted(isHighlight) | 设置控件状态为高亮状态         |
| Boolean    | 无       | isHighlighted()             | 获取控件是否处于高亮状态的结果 |
| 无         | Boolean  | setBright(isBright)         | 设置控件是否高亮               |
| Boolean    | 无       | isBright()                  | 获取控件是否高亮的结果         |
| 无         | Number   | setBrightStyle(brightStyle) | 设置控件的高亮风格             |

ccui 里面的所有控件都有 3 种状态： normal、highlight 和 disabled 。

bright 属性控制 UI 控件是否变灰，若 bright 为 true，则还需要判断 highlight 是否为 true，如果是 true，则是 highlight 状态，否则是 normal 状态。所以，如果你想改变一个控件的外观为不可用状态，除了 setEnabled(false) 以外，还需要调用 setBright(false) 函数，否则外观不会改变。

另外，brightStyle 的可取值如下：

ccui.Widget.BRIGHT_STYLE_NORMAL: 表示控件在正常状态。

ccui.Widget.BRIGHT_STYLE_HIGH_LIGHT: 表示控件处于高亮状态。

此外，ccui.Widget 还提供了焦点操作的相关 API，如下所示。焦点就是你当前选中了哪个控件，该控件就获得了焦点。例如按下了某个按钮或者通过其他的某种方式选中了某个控件，那个此控件就获得了焦点。如果是可编辑的控件，例如编辑框，则会有一个一闪一闪的竖线在那。如果是不可编辑的控件，一般也会有些高亮的显示。

ccui.Widget 中焦点相关的 API：

| 返回值类型  | 参数类型               | 函数                               | 说明                           |
| ----------- | ---------------------- | ---------------------------------- | ------------------------------ |
| Boolean     | 无                     | isFocused()                        | 查询是否拥有焦点               |
| 无          | Boolean                | setFocused(focus)                  | 切换控件是否拥有焦点           |
| Boolean     | 无                     | isFocusEnabled()                   | 查询是否允许接受焦点           |
| 无          | Boolean                | setFocusEnabled(enable)            | 切换是否允许接受焦点           |
| 无          | 无                     | requestFocus()                     | 请求获取焦点                   |
| 无          | cc.Widget, ccui.Widget | onFocusChange(lostFocus, getFocus) | 焦点更改事件发生时会调用此方法 |
| ccui.Widget | 无                     | getCurrentFocusedWidget()          | 获取当前拥有焦点的控件         |

ccui.Widget 基于 cc.Node 之上还扩展了一些和位置有关系的快捷 API，例如获取控件左边界在父节点坐标系中的位置，ccui.Widget 中位置相关的快捷 API：

| 返回值类型 | 参数类型 | 函数                | 说明                             |
| ---------- | -------- | ------------------- | -------------------------------- |
| Number     | 无       | getLeftBoundary()   | 获取左边界在父节点坐标系中的位置 |
| Number     | 无       | getBottomBoundary() | 获取下边界在父节点坐标系中的位置 |
| Number     | 无       | getRightBoundary()  | 获取右边界在父节点坐标系中的位置 |
| Number     | 无       | getTopBoundary()    | 获取上边届在父节点坐标系中的位置 |
| cc.p       | 无       | getWorldPosition()  | 获取控件在世界坐标系中的位置     |

ccui.Widget 百分比和启用布局组件 API：

| 返回值类型 | 参数类型 | 函数                                | 说明                       |
| ---------- | -------- | ----------------------------------- | -------------------------- |
| Number     | 无       | getSizePercent()                    | 获取控件的百分比尺寸       |
| 无         | Number   | setSizePercent(percent)             | 设置控件的百分比尺寸       |
| Boolean    | 无       | isLayoutComponentEnabled()          | 获取是否启用布局组件的结果 |
| 无         | Boolean  | setLayoutComponentEnabled(isEnable) | 设置是否启用布局组件       |

## ccui.Text 文本

Text 文本用来显示玩家的名字、等级、砖石数量等，它和 cc.Label 标签类似，也分为 TTF、BMFont 和 Atlas 三种类型。

### ccui.Text 字体文本

ccui.Text 支持 TTF 字库，创建一个 ccui.Text 文本的代码如下：

```javascript
var node = new ccui.Text("我是 Text 文本", "AmericanTypewriter", 30);
```

其中，AmericanTypewriter 为系统自带的 TTF 字体，30 为字号大小。ccui.Text 的构造函数以及参数说明如下：

构造函数： `cc.Text(textContent, fontName, fontSize);`

| 参数        | 参数说明           |
| ----------- | ------------------ |
| textContent | 文本内容           |
| fontName    | 字体文件或字体名称 |
| fontSize    | 字体大小           |

ccui.Text 常用函数如下：

| 返回值类型 | 参数类型                  | 函数                                          | 说明                                  |
| ---------- | ------------------------- | --------------------------------------------- | ------------------------------------- |
| String     | 无                        | getString()                                   | 获取内容                              |
| 无         | String                    | setString(text)                               | 设置内容                              |
| cc.Size    | 无                        | getFontSize()                                 | 获取字号大小                          |
| 无         | cc.Size                   | setFontSize(size)                             | 设置字号大小                          |
| String     | 无                        | getFontName()                                 | 获取字体文件或名称                    |
| 无         | String                    | setFontSize(name)                             | 设置字体文件或名称                    |
| cc.Color   | 无                        | getTextColor()                                | 获取文本颜色                          |
| 无         | cc.Color                  | setTextColor(color)                           | 设置文本颜色                          |
| Number     | 无                        | getType()                                     | 获取类型                              |
| Number     | 无                        | getTextHorizontalAlignment()                  | 获取文本水平对齐方式                  |
| 无         | Number                    | setTextHorizontalAlignment(alignment)         | 设置文本水平对齐方式                  |
| Number     | 无                        | getTextVerticalAlignment()                    | 获取文本垂直对齐方式                  |
| 无         | Number                    | setTextVerticalAlignment()                    | 设置文本垂直对齐方式                  |
| 无         | cc.Color, cc.Size, Number | enableShadow(shadowColor, offset, blurRadius) | 启用文本阴影效果，仅 TTF 字体对象有效 |
| 无         | cc.Color, cc.Size         | enableOutline(outlineColor, outlineSize)      | 启用文本描边效果，仅 TTF字体对象有效  |
| 无         | cc.Color                  | enableGlow(glowColor)                         | 启用文本发光效果，仅 TTF 字体对象有效 |

其中，文本类型可取的值如下所示：

ccui.Text.Type.SYSTEM: 表示系统字体

ccui.Text.Type.TTF: 表示 TTF 文件字体

水平对齐方式可取的值如下：

cc.TEXT_ALIGNMENT_LEFT: 表示左对齐

cc.TEXT_ALIGNMENT_CENTER: 表示居中对齐

cc.TEXT_ALIGNMENT_RIGHT: 表示右对齐

垂直对齐方式可取的值如下：

cc.VERTICAL_TEXT_ALIGNMENT_TOP: 表示上对齐

cc.VERTICAL_TEXT_ALIGNMENT_CENTER: 表示居中对齐

cc.VERTICAL_TEXT_ALIGNMENT_BOTTOM: 表示下对齐。

### ccui.TextBMFont 位图文本

ccui.TextBMFont 与 cc.LabelBMFont 类似，它支持 FNT 类型的文件。创建一个 ccui.TextBMFont 的代码如下：

```javascript
var node = new ccui.TextBMFont("12345", "res/unit10_ui/fonts/number.fnt");
```

其中，12345 为设置的文本内容，res/unit10_ui/fonts/number.fnt 为指定的 FNT 字体文件。

ccui.TextBMFont 构造函数以及参数说明

构造函数： `ccui.TextBMFont(text, filename);`

| 参数     | 参数说明           |
| -------- | ------------------ |
| text     | 文本内容           |
| fontName | 字体文件或字体名称 |

ccui.TextBMFont 常用函数

| 返回值类型 | 参数类型 | 函数                 | 说明                          |
| ---------- | -------- | -------------------- | ----------------------------- |
| String     | 无       | getString()          | 获取文本内容                  |
| 无         | String   | setString()          | 设置文本内容                  |
| 无         | String   | setFntFile(filename) | 设置 FNT 字体文件或者字体名称 |

### ccui.TextAtlas 字符映射文本

ccui.TextAtlas 为字符映射文本，与 cc.LabelAtlas 也是类似的。创建一个 ccui.TextAtlas 对象的代码如下：

```javascript
var node = new ccui.TextAtlas("789", "res/unit10_ui/fonts/score.png", 40, 50, '0');
```

ccui.TextAtlas 构造函数以及参数说明：

构造函数： `ccui.TextAtlas(strText, charMapFile, itemWidth, itemHeight, startCharMap)`

| 参数         | 参数说明         |
| ------------ | ---------------- |
| strText      | 文本内容         |
| charMapFile  | 图片名称         |
| itemWidth    | 每个“小块”的宽度 |
| itemHeight   | 每个“小块”的高度 |
| startCharMap | 起始字符         |

ccui.TextAtlas 常用的函数：

| 返回值类型 | 参数类型 | 函数             | 说明         |
| ---------- | -------- | ---------------- | ------------ |
| String     | 无       | getString()      | 获取文本内容 |
| 无         | String   | setString(value) | 设置文本内容 |

## ccii.Button 按钮

按钮（ccui.Button）可以响应回调函数，实现一些逻辑处理。按钮的处理方式也比较简单，创建代码如下：

```javascript
// 加载 按钮
loadButton: function () {
    var node = new ccui.Button();
    this.addChild(node);
    // 设置按钮 3 个状态（常态，按下，禁用）的纹理
    // 也可以将 3 个状态放在构造函数中 new ccui.Button(res.u10_btn_start_normal_png, res.u10_btn_start_pressed_png, "");
    node.loadTextures(res.u10_btn_start_normal_png, res.u10_btn_start_pressed_png, "");
    node.setPosition(200, cc.winSize.height / 2);
    // 设置按钮触摸，每一个按钮都需要开启手动触摸
    node.setTouchEnabled(true);
    // 添加事件监听器
    node.addTouchEventListener(this.onButtonTouchEvent, this);
}

onButtonTouchEvent: function (sender, type) {
    switch (type) {
        case ccui.Widget.TOUCH_BEGAN: // 触摸（按下）
            cc.log("Touch Down");
            // sender：事件源，即按钮本身
            sender.x += 100; // 按钮坐标右移 100
            break;
        case ccui.Widget.TOUCH_MOVED: // 触摸（移动）
            cc.log("Touch Move");
            break;
        case ccui.Widget.TOUCH_ENDED: // 触摸（抬起）
            cc.log("Touch Up");
            break;
        case ccui.Widget.TOUCH_CANCELED: // 触摸（取消）
            cc.log("Touch Canceled");
            break;
        default:
            break;
    }
}
```

ccui.Button 构造函数： ccui.Button(normalImage, selectedImage, disableImage, textType)

| 参数          | 参数说明     |
| ------------- | ------------ |
| normalImage   | 常态纹理图片 |
| selectedImage | 按下纹理图片 |
| disableImage  | 禁用纹理图片 |
| textType      | 纹理图片类型 |

textType 可取值：

- ccui.Widget.LOCAL_TEXTURE: 表示本地单张图片（小图）类型。
- ccui.Widget.PLIST_TEXTURE: 表示精灵表单（大图）类型。

ccui.Button 的 3 个状态的纹理也可以通过下面 API 设置：

| 返回值类型 | 参数类型                       | 函数                                               | 说明                       |
| ---------- | ------------------------------ | -------------------------------------------------- | -------------------------- |
| 无         | String, String, String, Number | loadTextures(normal, selected, disabled, textType) | 加载按钮的纹理以及纹理类型 |
| 无         | String, Number                 | loadTextureNormal(normal, textType)                | 加载按钮正常状态的纹理     |
| 无         | String, Number                 | loadTexturePressed(selected, textType)             | 加载按钮选中状态的纹理     |
| 无         | String, Number                 | loadTextureDisabled(disabled, textType)            | 加载按钮禁用状态的纹理     |

ccui.Button 支持九宫格，可以通过以下 API 设置九宫格按钮。启用了九宫格按钮之后，可以通过 setContenSize 函数来设置按钮的大小。

| 返回值类型 | 参数类型 | 函数                     | 说明                     |
| ---------- | -------- | ------------------------ | ------------------------ |
| Boolean    | 无       | isScale9Enabled()        | 判断按钮是否为九宫格模式 |
| 无         | Boolean  | setScale9Enabled(enable) | 设置按钮为九宫格模式     |

设置按钮的文本内容：

| 返回值类型 | 参数类型 | 函数                       | 说明             |
| ---------- | -------- | -------------------------- | ---------------- |
| String     | 无       | getTitleText()             | 获取按钮文本内容 |
| 无         | String   | setTitleText(text)         | 设置按钮文本内容 |
| cc.Color   | 无       | getTitleColor()            | 获取按钮文本颜色 |
| 无         | cc.Color | setTitleColor(color)       | 设置按钮文本颜色 |
| cc.Size    | 无       | getTitleFontSize()         | 获取按钮文本字号 |
| 无         | cc.Size  | setTitleFontSize(size)     | 设置按钮文本字号 |
| String     | 无       | getTitleFontName()         | 获取按钮文本名字 |
| 无         | String   | setTitleFontName(fontName) | 设置按钮文本名字 |

ccui.Button 的缩放效果：

| 返回值类型 | 参数类型 | 函数                             | 说明                           |
| ---------- | -------- | -------------------------------- | ------------------------------ |
| Number     | 无       | getZoomScale()                   | 获取一个缩放比例               |
| 无         | Number   | setZoomScale(scale)              | 设置一个缩放比例               |
| 无         | Boolean  | setPressedActionEnabled(enabled) | 设置启用按钮被按下时的缩放操作 |

## ccui.CheckBox 复选框

复选框（ccui.CheckBox）有选中和未选中这两种状态，可以为其添加事件监听器来响应事件从而处理对应的逻辑。在游戏中，复选框一般用在一些设置中，例如是否开启特效、是否接受组队邀请、是否接受系统推送等。创建一个 ccui.CheckBox 对象的代码如下：

```javascript
// 加载 checkbox
loadCheckBox: function () {
    var node = new ccui.CheckBox();
    this.addChild(node);
    node.loadTextures("res/unit10_ui/check_box_normal.png",
                     "res/unit10_ui/check_box_normal_press.png",
                     "res/unit10_ui/check_box_active.png",
                     "res/unit10_ui/check_box_normal_disable.png",
                     "res/unit10_ui/check_box_active_disable.png");
    node.setTouchEnabled(true);
    node.setPosition(cc.winSize.width / 2, cc.winSize.height / 2);
    node.addEventListener(this.onCheckBoxSelectedEvent, this);
}

onCheckBoxSelectedEvent: function (sender, type) {
    // ccui.CheckBox 可以响应两种类型的事件，分别是未选中 ccui.CheckBox.EVENT_UNSELECTED 和 ccui.CheckBox.EVENT_SELECTED
    switch (type) {
            case: ccui.CheckBox.EVENT_UNSELECTED:
				cc.log("复选框没选中");
            	break;
            case: ccui.CheckBox.EVENT_SELECTED:
            	cc.log("复选框选中");
            	break;
        default:
            break;
    }
}
```

ccui.CheckBox 的相关纹理读取也可以放在构造函数中。

构造函数： ccui.CheckBox(backGround, backGroundSelected, cross, backGroundDisabled, frontCrossDisabled, texType);

| 参数               | 参数说明         |
| ------------------ | ---------------- |
| backGround         | 未选中常态纹理   |
| backGroundSelected | 背景选中状态纹理 |
| cross              | 勾选选中状态纹理 |
| backGroundDisabled | 背景禁用状态纹理 |
| frontCrossDisabled | 勾选禁用状态纹理 |
| texType            | 纹理类型         |

ccui.CheckBox 常用函数

| 返回值类型 | 参数类型                                       | 函数                                                         | 说明                             |
| ---------- | ---------------------------------------------- | ------------------------------------------------------------ | -------------------------------- |
| 无         | String, String, String, String, String, Number | loadTextures(backGround, backGroundSelected, cross, backGroundDisabled, frontCrossDisabled, texType) | 加载相关状态纹理以及纹理类型     |
| 无         | String, Number                                 | loadTextureBackGround(backGround, texType)                   | 加载未选中状态纹理以及纹理类型   |
| 无         | String, Number                                 | loadTextureBackGroundSelected(backGroundSelected, texType)   | 加载背景选中状态纹理以及纹理类型 |
| 无         | String, Number                                 | loadTextureFrontCross(cross, texType)                        | 加载选中状态纹理以及纹理类型     |
| 无         | String, Number                                 | loadTextureBakcGroundDisabled(backGroundDisabled, texType)   | 加载背景禁用状态以及纹理类型     |
| 无         | String, Number                                 | loadTextureBackGroundDisabled(backGroundDisabled, texType)   | 加载勾选禁用状态纹理以及纹理类型 |
| Boolean    | 无                                             | isSelected()                                                 | 获取是否选中的结果               |
| 无         | Boolean                                        | setSelected(selected)                                        | 设置是否选中                     |
| 无         | Function, Object                               | addEventListener(selector, target)                           | 添加事件监听器                   |

## ccui.Slider 滑块

滑块（ccui.Slider）一般用来控制音量或者是调整屏幕暗度等。滑块控件由滑块控制点、滑块进度条和滑块背景组成，这意味着需要提供至少 3 张图片来创建一个 Slider 滑块控件。创建 Slider 滑块控件的代码如下：

```javascript
// 加载 滑块
loadSlider: function () {
    var slider = new ccui.Slieder();
    this.addChild(slider);
    // 加载滑块背景纹理，
    slider.loadBarTexture("res/unit10_ui/slider_bar.png");
    slider.loadSlidBallTextures("res/unit10_ui/slider_ball_normal.png",
                               "res/unit10_ui/slider_ball_pressed.png",
                               "res/unit10_ui/slider_ball_disabled.png");
    // 加载滑块进度条
    slider.loadProgressBarTexture("res/unit10_ui/slider_progress.png");
    slider.setPosition(cc.winSize.width / 2, cc.winSize.height / 2);
    // 添加一个事件监听器
    slider.addEventListener(this.onSliderEvent, this);
}

onSliderEvent: function (sender, type) {
    switch (type) {
        case ccui.Slider.EVENT_PERCENt_CHANGED:
            var percent = sender.getPercent();
            cc.log("百分比：" + percent.toFixed(0)); // 取整输出
            break;
        default:
            break;
    }
}
```

## ccui.ImageView 图片视图

图片视图（ccui.ImageView）实际上就是一张单纯的图片，一般作为 UI 面板的背景图等，ccui.ImageView 的使用是所有 UI 控件中最简单的，其创建代码如下：

```javascript
// 加载 ImageView
loadImageView: function () {
    var node = new ccui.ImageView("res/node_256.png");
    this.addChild(node);
    node.setPosition(cc.winSize.width / 2, cc.winSize.height / 2);
}
```

ccui.ImageView 常用函数：

| 返回值类型 | 参数类型       | 函数                           | 说明                         |
| ---------- | -------------- | ------------------------------ | ---------------------------- |
| 无         | String, Number | loadTexture(fileName, texType) | 加载纹理图片以及纹理图片类型 |
| 无         | cc.Rect        | setTextureRect(rect)           | 设置纹理区域                 |
| 无         | Boolean        | setScale9Enabled(enable)       | 设置为九宫格                 |
| Boolean    | 无             | isScale9Enabled()              | 获取是否为九宫格的结果       |

## ccui.LoadingBar 加载条

加载条（ccui.LoadingBar）也称为进度条，一般用来显示资源加载速度、网络资源下载进度或者怪物的血条等。

创建一个 ccui.LoadingBar，仅需要一张图片即可，其代码如下：

```javascript
// 加载进度条
loadLoadingBar: function () {
    var node = new ccui.LoadingBar();
    this.addChild(node);
    node.loadTexture("res/unit10_ui/slider_progress.png");
    node.setDirection(ccui.LoadingBar.TYPE_LEFT); // 设置方向
    node.setPercent(10); // 设置百分比
    node.setPosition(cc.winSize.width / 2, cc.winSize.height / 2);
}
```

ccui.LoadingBar 的常用函数和 ccui.ImageView 的常用函数一样。