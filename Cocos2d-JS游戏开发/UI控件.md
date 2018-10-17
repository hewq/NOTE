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

## ccui.TextField 编辑框

编辑框（ccui.TextField）一般用来收集一些用户输入的信息，例如玩家注册一个账号时，编辑框可以获取到玩家输入的账号。另外，编辑框也可以设为密码模式，在密码模式下，玩家输入的字符将由设定字符显示（例如 * 号），而非明文。

创建一个编辑框的代码如下：

```javascript
// 加载 编辑框
loadTextField: function () {
    var node = new ccui.TextField("请输入账号：", "Arial", 30);
    this.addChild(node);
    node.setPosition(cc.winSize.width / 2, cc.winSize.height / 2);
    node.addEventListener(this.onTextFieldEvent, this); // 添加事件监听器
};

// 编辑框输入事件
onTextFieldEvent: function (textField, type) {
    switch (type) {
        case ccui.TextField.EVENT_ATTACH_WITH_IME:
            cc.log("挂载到输入法编辑器");
            break;
        case ccui.TextField.EVENT_DETACH_WITH_IME:
            cc.log("输入法编辑器失去挂载");
            break;
        case ccui.TextField.EVENT_INSERT_TEXT:
            cc.log("输入法编辑器输入");
            break;
        case ccui.TextField.EVENT_DELETE_BACKWARD:
            cc.log("输入法编辑器删除");
            break;
        default:
			break;
    }
    cc.log("编辑框中内容：", textField.getString());
}

```

在实际开发中，你可以在 case ccui.TextField.EVENT_ATTACH_WITH_IME 中写一个 Action 让 textField 运行一个向上移动到 moveTo 动作，然后在 case ccui.TextField.EVENT_DETACH_WITH_IME 里让 textField 输入框 moveTo 回来，这便解决了在手机上键盘可能挡到 textField 控件的问题。

前面说到，ccui.TextField 还有个密码模式，密码模式的开启以及密码显示的样式设定实现代码如下：

```javascript
node.setPasswordEnabled(true); // 启用密码模式
node.setPasswordStyleText("*"); // 设置密码样式
```

ccui.TextField 常用函数：

| 返回值类型 | 参数类型                       | 函数                                            | 说明                                                         |
| ---------- | ------------------------------ | ----------------------------------------------- | ------------------------------------------------------------ |
| 无         | ccui.TextField                 | onTextFieldAttachWithIME(sender)                | 挂载输入法时的回调函数                                       |
| 无         | ccui.TextField                 | onTextFieldDetachWithIME(sender)                | 取消挂载输入法时的回调函数                                   |
| 无         | ccui.TextField, String, Number | onTextFieldInsertText(sender, text, len)        | 插入文本时的回调函数。sender: 文本编辑框实例。text：将要插入的字符串。len：将要插入的字符串长度 |
| 无         | ccui.TextField, String, Number | onTextFieldDeleteBackward(sender, delText, len) | 删除文本时的回调函数。sender：文本编辑框实例。delText：将要删除的字符串。len：将要插入的字符串长度。 |
| 无         | String, Number                 | insertText(text, len)                           | 插入文本                                                     |
| 无         | 无                             | deleteBackward()                                | 回退删除                                                     |
| 无         | 无                             | openIME()                                       | 打开输入法编辑器                                             |
| 无         | 无                             | closeIME()                                      | 关闭输入法编辑器                                             |
| 无         | Boolean                        | setMaxLengthEnabled(isEnable)                   | 启用最大长度限制                                             |
| Boolean    | 无                             | isMaxLengthEnabled()                            | 获取是否启用了最大长度限制的结果                             |
| 无         | Number                         | setMaxLength(length)                            | 设置最大长度                                                 |
| Number     | 无                             | getMaxLength()                                  | 获取最大长度                                                 |
| 无         | Number                         | getCharCount()                                  | 获取总共输入的字符数                                         |
| 无         | Boolean                        | setPasswordEnabled(isEnable)                    | 启用密码输入模式                                             |
| Boolean    | 无                             | isPasswordEnabled()                             | 获取是否启用密码输入模式的结果                               |
| 无         | String                         | setPasswordStyleText(styleText)                 | 设置密码模式下的文本样式                                     |
| 无         | String                         | setPasswordText(text)                           | 设置密码                                                     |
| 无         | Boolean                        | setAttachWithIME(isAttach)                      | 设置是否挂载输入法编辑器                                     |
| 无         | Boolean                        | getAttachWithIME()                              | 获取是否挂载输入法编辑器的结果                               |
| 无         | Boolean                        | setDetachWithIME(isDetach)                      | 设置是否取消挂载输入法编辑器                                 |
| Boolean    | 无                             | getDetachWithIME()                              | 获取是否取消挂载输入法编辑器的结果                           |
| 无         | Boolean                        | setInsertText(insert)                           | 设置是否允许文本输入                                         |
| Boolean    | 无                             | getInsertText()                                 | 获取是否允许文本输入的结果                                   |
| 无         | Boolean                        | setDeleteBackward(isDeleteBakcward)             | 设置是否允许回删                                             |
| Boolean    | 无                             | getDeleteBackward()                             | 获取是否允许回删的结果                                       |

## ccui.Layout 布局

布局（ccui.Layout）是一个包含控件的容器，容器中的字节点根据布局类型进行摆放。布局类型由绝对布局、相对布局、水平布局和垂直布局 4 种，默认为绝对布局。

ccui.Layout 和 cc.Layout 类似，是一个默认看不见的节点。不过，你可以给 ccui.Layout 设置颜色和内容大小，那么整个 ccui.Layout 就很直观地显示出来，这是一个非常好的辅助功能。另外，除了设置颜色之外，ccui.Layout  还允许设置背景图像。通过如下代码可以创建出一个简单的 ccui.Layout:

```javascript
// 加载 默认布局
loadLayout: function () {
    var layout = new ccui.Layout();
    this.addChild(layout);
    layout.setContentSize(852, 480);
    // 将 layout 定位在屏幕的正中心
    layout.x = (cc.winSize.width - layout.width) / 2;
    layout.y = (cc.winSize.height = layout.height) / 2;
    // 设置 layout 背景颜色
    layout.setBackGroundColor(cc.color(128, 128, 128));
    // 设置背景颜色类型
    layout.setBackGroundColorType(ccui.Layout.BG_COLOR_SOLID);
}
```

ccui.Layout 中背景颜色相关的 API

| 参数或返回类型 | 函数                                | 说明                     |
| -------------- | ----------------------------------- | ------------------------ |
| Number         | getBackGroundColorType()            | 获取背景颜色类型         |
| Number         | setBackGroundColorType()            | 设置背景颜色类型         |
| cc.Color       | getBackGroundColor()                | 获取背景颜色             |
| cc.Color       | setBackGroundColor(color, endColor) | 设置背景颜色             |
| cc.Color       | getBackGroundStartColor()           | 获取渐变背景颜色开始的值 |
| cc.Color       | getBackGroundEndColor()             | 获取渐变背景颜色结束的值 |
| Number         | getBackGroundColorOpacity()         | 获取背景颜色不透明度     |
| Number         | setBackGroundColorOpacity(opacity)  | 设置背景颜色不透明度     |
| cc.p           | getBackGroundColorVector()          | 获取背景颜色向量         |
| cc.p           | setBackGroundColorVector(vector)    | 设置背景颜色向量         |

其中背景颜色类型可取的值如下：

ccui.Layout.BG_COLOR_NONE: 表示无颜色类型。

ccui.Layout.BG_COLOR_SOLID: 表示固定颜色类型。

ccui.Layout.BG_COLOR_GRADIENT: 表示渐变颜色类型。

ccui.Layout 与背景图片相关的 API：

| 返回值类型 | 参数类型       | 函数                                    | 说明                         |
| ---------- | -------------- | --------------------------------------- | ---------------------------- |
| 无         | String, Number | setBackGroundImage(fileName, texType)   | 设置背景图片                 |
| 无         | 无             | removeBackGroundImage()                 | 移除背景图片                 |
| cc.Color   | 无             | getBackGroundImageColor()               | 获取背景图片颜色             |
| 无         | cc.Color       | setBackGroundImageColor(color)          | 设置背景图片颜色             |
| Number     | 无             | getBackGroundImageOpacity()             | 获取背景图片不透明度         |
| 无         | Number         | setBackGroundImageOpacity(opacity)      | 设置背景图片不透明度         |
| cc.Size    | 无             | getBackGroundImageTextureSize()         | 获取背景图片纹理大小         |
| Boolean    | 无             | isBackGroundImageScale9Enabled()        | 背景图片是否启用九宫格       |
| 无         | Boolean        | setBackGroundImageScale9Enabled(enable) | 开启／关闭背景图片九宫格模式 |

其中，背景图片等纹理类型（texType）可选值如下：

ccui.Widget.LOCAL_TEXTURE: 表示单张纹理图片类型。

ccui.Widget.PLIST_TEXTURE: 表示精灵表单图集类型。

当创建好一个 ccui.Layout 之后，就可以以此布局中添加子控件，然后进行布局。ccui.LayoutParameter 是一个布局参数类，用来设置布局的排列方式，例如左对齐、右对齐或者水平居中等。ccui.LayoutParameter 有两个子类——线性布局类 ccui.LinearLayoutParameter 和相对布局类 ccui.RelativeLayoutParameter。

```javascript
// 加载 垂直布局
loadLayoutLinearVertical: function () {
    // ......
    // 设置 layout 的布局类型
    // ccui.Layout.ABSOLUTE：绝对布局类型
    // ccui.Layout.RELATIVE：相对布局类型
    // ccui.Layout.LINEAR_VERTICAL：线性垂直布局类型
    // ccui.Layout.LINEAR_HORIZONAL: 线性水平布局类型
    layout.setLayoutType(ccui.Layout.LINEAR_VERTICAL);
    var buttonTexture = "res/unit10_ui/btn_start_normal.png";
    // 按钮
    var button1 = new ccui.Button();
    layout.addChild(button1);
    button1.setTouchEnabled(true);
    button1.loadTextures(buttonTexture, buttonTexture, "");
    // 布局参数
    var lp1 = new ccui.LinearLayoutParameter();
    // 给按钮设置布局参数
    button1.setLayoutParameter(lp1);
    // 给布局参数对象设置对齐方式
    // ccui.LinearLayoutParameter.NONE: 无对齐方式
    // ccui.LinearLayoutParameter.LEFT: 左对齐
    // ccui.LinearLayoutParameter.TOP: 上对齐
    // ccui.LinearLayoutParameter.RIGHT: 右对齐
    // ccui.LinearLayoutParameter.BOTTOM: 下对齐
    // ccui.LinearLayoutParameter.CENTER_VERTICAL: 垂直居中对齐
    // ccui.LinearLayoutParameter.CENTER_HORIZONTAL: 水平居中对齐
    lp1.setGravity(ccui.LinearLayoutParameter.CENTER_HORIZONTAL);
    // 给布局对象设置外边距，外边距的 4 个参数分别表示的是 左边距 上边距 右边距 下边距
    lp1.setMargin(new ccui.Margin(0, 0, 0, 0));
}
```

ccui.Layout 的相关 API：

| 返回值类型 | 参数类型                 | 函数                                      | 说明                                     |
| ---------- | ------------------------ | ----------------------------------------- | ---------------------------------------- |
| Number     | 无                       | getLayoutType()                           | 获取布局类型                             |
| 无         | Number                   | setLayoutType(type)                       | 设置布局类型                             |
| 无         | 无                       | requestDoLayout()                         | 请求刷新布局                             |
| 无         | 无                       | forceDoLayout()                           | 强制刷新布局                             |
| Boolean    | 无                       | isClippingEnabled()                       | 获取是否开启了裁剪的结果                 |
| 无         | Boolean                  | setClippingEnabled(enable)                | 设置是否开启裁剪                         |
| Boolean    | 无                       | isLoopFocus(loop)                         | 获取是否启用循环焦点的结果               |
| 无         | Boolean                  | setLoopFocus(loop)                        | 设置是否启用循环焦点                     |
| Boolean    | 无                       | isPassFocusToChild()                      | 获取是否允许传递焦点到子节点上的结果     |
| 无         | Boolean                  | setPassFocusToChild(pass)                 | 设置是否允许传递焦点到子节点上           |
| Number     | 无                       | getClippingType()                         | 获取裁剪类型                             |
| 无         | Number                   | setClippingType(type)                     | 设置裁剪类型                             |
| 无         | ccui.Widget, ccui.Widget | findNextFocusedWidget(direction, current) | 获取指定方向中的下一个能够具有焦点的控件 |

findNextFocusedWidget(direction, current) 中的 current 表示当前焦点控件，而 direction 表示方向，其可选值如下：

ccui.Widget.LEFT: 向左。

ccui.Widget.RIGHT: 向右。

ccui.Widget.UP: 向上。

ccui.Widget.DOWN: 向下。

另外，ccui.Layout 是可以裁剪的。调用 setClippingEnabled(true) 函数之后，再结合 setContentSize(size) 即可。

```javascript
// 加载 垂直布局
loadLayoutLinearVertical: function () {
    layout.setClippingEnabled(true);
    layout.setContentSize(430, 200);
}
```

## ccui.ScrollView 滚动视图

滚动视图（ccui.ScrollView）继承自 ccui.Layout，也是一个布局类，它可以让放置在其内部的 UI 控件滚动显示。

创建一个 ccui.ScrollView 的代码如下：

```javascript
// 加载滚动视图
loadScrollView: function () {
    var scrollView = new ccui.ScrollView();
    this.addChild(scrollView);
    scrollView.setContentSize(cc.size(512, 400));
    scrollView.x = (cc.winSize.width - scrollView.width) / 2;
    scrollView.y = (cc.winSize.height - scrollView.height) / 2;
    scrollView.setTouchEnabled(true);
    // 设置滚动视图的滚动方向
    scrollView.setDirection(ccui.ScrollView.DIR_HORIZONTAL);
}
```

ccui.ScrollView 中方向相关的 API：

| 参数或返回类型 | 函数              | 说明     |
| -------------- | ----------------- | -------- |
| Number         | getDirection()    | 获取方向 |
| Number         | setDirection(dir) | 设置方向 |

方向可取值：

ccui.ScrollView.DIR_NONE: 无方向。

ccui.ScrollView.DIR_VERTICAL: 竖直方向。

ccui.ScrollView.DIR_HORIZONTAL: 水平方向。

ccui.ScrollView.DIR_BOTH: 水平和竖直方向。

滚动视图在滚动的时候，可以添加一些效果。

ccui.ScrollView 中惯性、弹力效果相关 API：

| 返回值类型 | 参数类型 | 函数                             | 说明                           |
| ---------- | -------- | -------------------------------- | ------------------------------ |
| Boolean    | 无       | isInertiaScrollEnabled()         | 获取是否开启滚动惯性效果的结果 |
| 无         | Boolean  | setInertiaScrollEnabled(enabled) | 设置是否开启滚动惯性效果       |
| Boolean    | 无       | isBounceEnabled()                | 获取是否开启弹力效果的结果     |
| 无         | Boolean  | setBounceEnabled(enabled)        | 设置是否开启弹力效果           |

```javascript
// 加载滚动视图
loadScrollView: function () {
    var scrollView = new ccui.ScrollView();
    var imageView = new ccui.ImageView("res/unit07_design/background.png");
    scrollView.addChild(imageView);
    // 设置视图内部容器的大小，
    // 这和 setContentSize(size) 是有区别的。setContentSize 设置的是滚动视图的大小，
    // 而 setInnerContainerSize 设置的是内部容器的大小。另外需要注意的是，内部容器的大小必须大于或等于滚动视图的大小。
    scrollView.setInnerContainerSize(cc.size(imageView.width, imageView.height));
    imageView.x = imageView.width / 2;
    imageView.y = imageView.height / 2;
    
}
```

ccui.ScrollView 中容器以及大小相关 API：

| 返回值类型  | 参数类型 | 函数                        | 说明                       |
| ----------- | -------- | --------------------------- | -------------------------- |
| ccui.Layout | 无       | getInnerContainer()         | 获取滚动视图的内部布局容器 |
| cc.Size     | 无       | getInnerContainerSize()     | 获取内部容器的大小         |
| 无          | cc.Size  | setInnerContainerSize(size) | 设置内部容器的大小         |

在实际开发中，很少去监听滚动视图的滚动事件，但是这些事件接口都是存在的。值得注意的是，onTouchBegan、onTouchMoved、onTouchEnded 以及 onTouchCancelled 函数为 ccui.ScrollView 内部实现用，不建议重写它们。

| 返回值类型 | 参数类型           | 函数                               | 说明                 |
| ---------- | ------------------ | ---------------------------------- | -------------------- |
| Boolean    | cc.Touch, cc.Event | onTouchBegan(touch, event)         | 触摸开始时的回调函数 |
| 无         | cc.Touch, cc.Event | onTouchMoved(touch, event)         | 触摸移动时的回调函数 |
| 无         | cc.Touch, cc.Event | onTouchEnded(touch, event)         | 触摸结束时的回调函数 |
| 无         | cc.Touch, cc.Event | onTouchCancelled(touch, event)     | 触摸取消时的回调函数 |
| 无         | Function, Object   | addEventListener(selector, target) | 添加事件监听器       |

ccui.ScrollView 中滚动相关 API：

| 返回值类型 | 参数类型                | 函数                                                    | 说明                                     |
| ---------- | ----------------------- | ------------------------------------------------------- | ---------------------------------------- |
| 无         | Number, Boolean         | scrollToBottom(time, attenuated)                        | 滚动到滚动视图的底部                     |
| 无         | Number, Boolean         | scroollToTop(time, attenuated)                          | 滚动到滚动视图的顶部                     |
| 无         | Number, Boolean         | scrollToLeft(time, attenuated)                          | 滚动到视图的左端                         |
| 无         | Number, Boolean         | scrollToRight(time, attenuated)                         | 滚动到视图的右端                         |
| 无         | Number, Boolean         | scrollToTopLeft(time, attenuated)                       | 滚动到视图的左上角                       |
| 无         | Number, Boolean         | scrollToTopRight(time, attenuated)                      | 滚动到视图的右上角                       |
| 无         | Number, Boolean         | scrollToBottomLeft(time, attenuated)                    | 滚动到视图的左下角                       |
| 无         | Number, Boolean         | scrollToBottomRight(time, attenuated)                   | 滚动到视图的右下角                       |
| 无         | Number, Number, Boolean | scrollToPercentVertical(percent, time, attenuated)      | 按百分比竖直滚动                         |
| 无         | Number，Number, Boolean | scrollToPercentHorizontal(percent, time, attenuated)    | 按百分比水平滚动                         |
| 无         | Number, Number, Boolean | scrollToPercentBothDirection(percent, time, attenuated) | 竖直方向和水平方向分别按一定的百分比滚动 |

这些接口都至少接受两个参数：time 和 attenuated。其中，time 表示持续时间，attenuated 表示滚动速度是否衰减。

ccui.ScrollView 中跳跃相关 API：

| 返回值类型 | 参数类型 | 函数                                | 说明                             |
| ---------- | -------- | ----------------------------------- | -------------------------------- |
| 无         | 无       | jumpToBottom                        | 跳到视图底端                     |
| 无         | 无       | jumpToTop()                         | 跳到视图顶端                     |
| 无         | 无       | jumpToLeft()                        | 跳到视图左端                     |
| 无         | 无       | jumpToRight()                       | 跳到视图右端                     |
| 无         | 无       | jumpToTopLeft()                     | 跳到视图左上角                   |
| 无         | 无       | jumpToTopRight()                    | 跳到视图右上角                   |
| 无         | 无       | jumpToBottomLeft()                  | 跳到视图左下角                   |
| 无         | 无       | jumpToBottomRight()                 | 跳到视图右下角                   |
| 无         | Number   | jumpToPercentVertical(percent)      | 竖直方向跳到指定百分比位置       |
| 无         | Number   | jumpToPercentHorizontal(percent)    | 水平方向跳到指定百分比位置       |
| 无         | Number   | jumpToPercentBothDirection(percent) | 竖直和水平方向跳到指定百分比位置 |

## ccui.PageView 分页视图

分页视图（ccui.PageView）也是直接继承自 ccui.Layout，与滚动视图不一样的是，分页视图将其内部的 UI 控件进行分页布局，每次只能显示一页，但是可以在多页之间进行切换。

创建一个 ccui.PageView 的代码如下：

```javascript
// 加载 PageView
loadPageView: function () {
    var pageView = new ccui.PageView();
    this.addChild(pageView);
    pageView.setTouchEnabled(true);
    pageView.setContentSize(cc.winSize);
    pageView.x = (cc.winSize.width - pageView.width) / 2;
    pageView.y = (cc.winSize.height - pageView.height) / 2;
}
```

创建一个分页后，可以通过如下 API 给分页视图添加、删除和获取页面：

| 返回值类型  | 参数类型                     | 函数                                          | 说明                           |
| ----------- | ---------------------------- | --------------------------------------------- | ------------------------------ |
| 无          | ccui.Layout                  | addPage(page)                                 | 往分页视图的最后插入一页       |
| 无          | ccui.Widget, Number, Boolean | addWidgetToPage(widget, pageIdx, forceCreate) | 把一个 UI 控件添加到分页视图中 |
| 无          | ccui.Layout, Number          | insertPage(page, index)                       | 在指定位置插入一页             |
| 无          | ccui.Layout                  | removePage(page)                              | 移除一页                       |
| 无          | Number                       | removePageAtIndex(index)                      | 移除指定位置的页               |
| 无          | 无                           | removeAllPages()                              | 移除所有页                     |
| Number      | 无                           | getCurPageIndex()                             | 获取当前显示页的索引号         |
| Array       | 无                           | getPages()                                    | 获取所有页的列表               |
| ccui.Layout | Number                       | getPage(index)                                | 获取指定页                     |
| 无          | Number                       | scrollToPage(index)                           | 滚动到一个指定的页             |

分页视图默认需要滑动到页面宽度大小一半的时候才会切换到下一页，但实际上，你可以设置这个滑动临界值，相关 API 如下：

| 返回值类型 | 参数类型 | 函数                                | 说明                               |
| ---------- | -------- | ----------------------------------- | ---------------------------------- |
| 无         | Number   | setCustomScrollThreshold(threshold) | 设置自定义滚动临界值               |
| Number     | 无       | getCustomScrollThreshold()          | 获取自定义滚动临界值               |
| 无         | Boolean  | setUsingCustomScrollThreshold(flag) | 设置是否使用自定义滚动临界值       |
| Boolean    | 无       | isUsingCustomScrollThreshold()      | 获取是否使用自定义滚动临界值的结果 |

```javascript
// 加载 PageView
loadPageView: function () {
    var pageView = new ccui.PageView();
    for (var i = 0; i < 3; ++i) {
        // 创建一个 layout 布局
        var layout = new ccui.Layout();
        // 把 ccui.Layout 对象添加到 pageView 分页视图中
        pageView.addPage(layout);
        
        var imageView = new ccui.ImageView("res/unit07_design/background.png");
        // 把 ccui.ImageView 对象添加到 ccui.Layout 中
        layout.addChild(imageView);
        imageView.x = pageView.width / 2;
        imageView.y = pageView.height / 2;
    }
    // 添加事件监听器，当分页视图有滑动事件时，则会触发 ccui.PageView.EVENT_TURNING 事件
    pageView.addEventListener(function(sender, type) {
        switch (type) {
            case ccui.PageView.EVENT_TURNING:
                var index = pageView.getCurPageIndex() + 1;
                cc.log("当前第" + index + "页");
                break;
            default:
                break;
        }
    }, this);
}
```

## ccui.ListView 列表视图

列表视图（ccui.ListView）继承自 ccui.ScrollView，所以它同样具有滚动特性。列表视图容器中的 UI 控件以项（item）为单位，项可以基于某个模型，然后通过克隆的方式高效利用。

另外需要说明的是，ccui.ListView 在创建元素的时候，如果元素个数非常多，需要考虑在移动 ListView 的过程中，动态调整项的位置来起到优化作用。比如，一个列表视图需要有 100 个项，但它一共可以显示 10 个项，此时可以多创建项，例如 12 个或者 15 个，然后在移动过程中去修改第 12 个项或者第 15 个项的位置以及其他属性。但倘若直接创建了 100 个项，那么将会非常消耗内存并且影响 ccui.ListView 的效率。

```javascript
// 加载 ListView
loadListView: function () {
    var listView = new ccui.ListView();
    this.addChild(listView);
    listView.setTouchEnabled(true);
    listView.setContentSize(cc.size(240, 120));
    listView.setDirection(ccui.ScrollView.DIR_HORIZONTAL);
    listView.setBackGroundColor(cc.color(128, 128, 128));
    listView.setBackGroundColorType(ccui.Layout.BG_COLOR_SOLID);
    listView.x = (cc.winSize.width - listView.width) / 2;
    listView.y = (cc.winSize.height - listView.height) / 2;
}
```

ccui.ListView 中项操作的相关 API 如下：

| 返回值类型 | 参数类型            | 函数                          | 说明                                                   |
| ---------- | ------------------- | ----------------------------- | ------------------------------------------------------ |
| 无         | ccui.Widget         | setItemModel(model)           | 设置项的模型                                           |
| 无         | 无                  | pushBackDefaultItem()         | 插入一个默认项（通过克隆模式创建）到列表视图的尾部     |
| 无         | Number              | insertDefaultItem(index)      | 插入一个默认项（通过克隆模式创建）到列表视图的指定位置 |
| 无         | ccui.Widget         | pushBackCustomItem(item)      | 插入一个自定义项到列表视图的尾部                       |
| 无         | ccui.Widget, Number | insertCustomItem(item, index) | 插入自定义 UI 控件到列表视图中指定索引处               |
| 无         | Number              | removeItem(index)             | 删除给定索引的项                                       |
| 无         | 无                  | removeLastItem()              | 删除最后一个项                                         |
| 无         | 无                  | removeAllItems()              | 删除所有项                                             |
| Number     | 无                  | getItem(index)                | 获取给定索引的项                                       |
| Array      | 无                  | getItem()                     | 获取所有项                                             |
| Number     | 无                  | getIndex(item)                | 获取指定项的索引                                       |
| Number     | 无                  | getCurSelectedIndex()         | 获取当前所选项的索引                                   |

设置项的模型后，将该模型作为一个蓝图，然后调用 pushBackDefaultItem 函数，将克隆出的新副本插入到列表视图中。

在 ccui.ListView 中，还可以设置每个项之间的边距、对齐方式以及方向，相关 API 如下：

| 返回值类型 | 参数类型 | 函数                   | 说明                 |
| ---------- | -------- | ---------------------- | -------------------- |
| Number     | 无       | getItemMargin()        | 获取每个项之间的边距 |
| 无         | Number   | setItemsMargin(margin) | 设置每个项之间的边距 |
| Number     | 无       | getGravity()           | 获取对齐方式         |
| 无         | Number   | setGravity(gravity)    | 设置对齐方式         |
| Number     | 无       | getDirection()         | 获取方向             |
| 无         | Number   | setDirection(dir)      | 设置方向             |

其中，方向的可取值和 ccui.ScrollView 一致。此外，ccui.ListView 还有一些刷新相关的 API：

| 返回值类型 | 参数类型 | 函数                 | 说明               |
| ---------- | -------- | -------------------- | ------------------ |
| 无         | 无       | requestRefreshView() | 请求刷新视图和布局 |
| 无         | 无       | refreshView()        | 刷新列表视图的视图 |
| 无         | 无       | forceDoLayout()      | 强制刷新控件的布局 |
| 无         | 无       | doLayout()           | 请求刷新控件的布局 |

```javascript
// 加载 ListView
loadListView: function () {
    var listView = new ccui.ListView();
    // 创建按钮
    var default_button = new ccui.Button();
    default_button.setName("TextButton");
    default_button.setTouchEnabled(true);
    default_button.loadTexture("res/unit10_ui/btn_normal.png", "res/unit10_ui/btn_pressed.png", "");
    // 创建默认模型
    var default_item = new ccui.Layout();
    default_item.addChild(default_button);
    default_item.setTouchEnabled(true);
    default_item.setContentSize(default_button.getContentSize());
    default_item.x = default_item.width / 2;
    default_item.y = default_item.height / 2;
    // 设置模型
    listView.setItemModel(default_item);
    // 添加 4 个项
    for (var i = 0; i < 4; ++i) {
        listView.pushBackDefaultItem();
    }
    // 给前 4 个项设置文本标签
    for (var i = 0; i < 4; i++) {
        var item = listView.getItem(i);
        var button = item.getChildByName("TextButton");
        var index = listView.getIndex(item);
        button.setTitleText("按钮" + i);
    }
}

// 加载 ListView
loadListView: function () {
    // 创建 listView
    var listView = new ccui.ListView();
    this.addChild(listView);
    listView.setTouchEnabled(true);
    listView.setContentSize(cc.size(240, 120));
    listView.setDirection(ccui.ScrollView.DIR_HORIZONTAL);
    listView.setBackGroundColor(cc.color(128, 128, 128));
    listView.setBackGroundColorType(ccui.Layout.BG_COLOR_SOLID);
    listView.x = (cc.winSize.width - listView.width) / 2;
    listView.y = (cc.winSzie.height - listView.height) / 2;
    listView.addEventListener(function (sender, type) {
        switch (type) {
            case ccui.ListView.EVNET_SELECTED_ITEM:
                cc.log("当前项索引：" + sender.getCurSelectedIndex());
                break;
            default:
                break;
        }
    }, this);
}
```



