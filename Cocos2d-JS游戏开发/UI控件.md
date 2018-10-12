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

