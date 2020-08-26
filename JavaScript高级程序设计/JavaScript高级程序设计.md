# JavaScript 高级程序设计

- <a href="#brief">JavaScript 简介</a>
- <a href="#useInHtml">在 HTML 中使用 JavaScript</a>
- <a href="#basic">基本概念</a>
- <a href="#var">变量、作用域和内存问题</a>
- <a href="#type">引用类型</a>
- <a href="#object">面向对象的程序设计</a>
- <a href="#function">函数表达式</a>
- <a href="#bom">BOM</a>
- <a href="#dom">DOM</a>
- <a href="#json">JSON</a>
- <a href="#perfomance">性能</a>



## <a name="brief">JavaScript 简介</a>

JavaScript 是一种专为与网页交互而设计的脚本语言，由下列三个不同的部分组成：

- ECMAScript，由 ECMA-262定义，提供核心语言功能；
- 文档对象模型（DOM），提供访问和操作网页内容的方法和接口；
- 浏览器对象模型（BOM），提供与浏览器交互的方法和接口。

JavaScript 的这三个组成部分，在当前五个主要浏览器（IE、Firefox、Chrome、Safari和Opera）中都得到了不同程度的支持。其中，所有浏览器对 ECMAScript 第 3 版的支持大体上都还不错，而对 ECMAScript 5 的支持程度越来越高，但对 DOM 的支持则彼此相差比较多。对已经正式纳入 HTML5 标准的 BOM 来说，尽管各浏览器都实现了某些众所周知的共同特性，但其他特性还是会因浏览器而异。



## <a name="useInHtml">在 HTML 中使用 JavaScript</a>

把 JavaScript 插入到 HTML 页面中要使用 `<script>` 元素。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。而我们需要注意的地方有：

- 在包含外部的 JavaScrpt 文件式，必须将 src 属性设置为指向相应文件的 URL。而这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件。
- 所有 `<script>` 元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用 defer 和 async 属性的情况下，只有在解析完前面 `<script>` 元素中代码之后，才会开始解析后面 `<script>` 元素中的代码。
- 由于浏览器会先解析不使用 defer 属性的 `<script>` 元素中的代码，然后再解析后面的内容，所以一般应该把 `<script>` 元素放在页面最后，即主要内容后面，`</body>`标签前面。
- 使用 defer 属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行。
- 使用 async 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。

另外，使用 `<noscript>` 元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用脚本的情况下，浏览器不会显示 `<noscript>` 元素中的任何内容。	



## <a name="basic">基本概念</a>

JavaScript 的核心语言特性在 ECMA-262 中是以名为 ECMAScript 的伪语言的形式来定义的。ECMAScript 中包含了所有基本的语法、操作符、数据类型以及完成基本的计算任务所必需的对象，但没有对取得输入和产生输出的机制作规定。理解 ECMAScript 及其纷繁复杂的各种细节，是理解其在 Web 浏览器中的实现——JavaScript 的关键。目前大多数实现所遵循的都是 ECMA-262 第 3 版，但很多也已经着手开始实现第 5 版了。以下简要总结了 ECMAScript 中基本的要素。

- ECMAScript 中的基本数据类型包括 Undefined、Null、Boolean、Number 和 String。
- 与其他语言不同，ECMAScript 没有为整数和浮点数值分别定义不同的数据类型，Number 类型可用于表示所有数值。
- ECMAScript 中也有一种复杂的数据类型，即 Object 类型，该类型是这门语言中所有对象的基础类型。
- 严格模式为这门语言中容易出错的地方加了限制。
- ECMAScript 提供了很多与 C 及其他类 C 语言中相同的基本操作符，包括算术操作符、布尔操作符、关系操作符、相等操作符及赋值操作符等。
- ECMAScript 从其他语言中借鉴了很多流控制语句，例如 if 语句、for 语句和 switch 语句等。

ECMAScript 中的函数与其他语言中的函数有诸多不同之处。

- 无须指定函数的返回值，因为任何时候 ECMAScript 函数都可以在任何时候返回任何值。
- 实际上，未指定返回值的函数返回的是一个特殊的 **undefined** 值。
- ECMAScript 中没有函数签名的概念，因为其函数参数是以一个包含零或多个值的数组的形式传递的。
- 可以向 ECMAScript 函数传递任意数量的参数，并且可以通过 arguments 对象来访问这些参数。
- 由于不存在函数签名的特性，ECMAScript 函数不能重载。



## <a name="var">变量、作用域和内存问题</a>

JavaScript 变量可以用来保存两种类型的值：基本类型和引用类型值。基本类型的值源自以下 5 种基本数据类型：Undefined、Null、Boolean、Number 和 String。基本类型值和引用类型值具有以下特点：

- 基本类型值在内存中占据固定大小的空间，因此被保存在栈内存中；
- 从一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本；
- 引用类型的值是对象，保存在堆内存中；
- 包含引用类型值的变量实际上包含的并不是对象本身，而是一个指向该对象的指针；
- 从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象；
- 确定一个值是哪种基本类型可以使用 typeof 操作符，而确定一个值是哪种引用类型可以使用 instanceof 操作符。

所有变量（包括基本类型和引用类型）都存在一个执行环境（也称为作用域）当中，这个执行环境决定了变量的生命周期，以及哪一部分代码可以访问其中的变量。以下是关于执行环境的几点总结：

- 执行环境有全局执行环境（也称为全局环境）和函数执行环境之分；
- 每次进入一个新执行环境，都会创建一个用于搜索变量和函数的作用域链；
- 函数的局部环境不仅有权访问函数作用域的变量，而且有权访问其包含（父）环境，乃至全局环境；
- 全局环境只能访问在全局环境中定义的变量和函数，而不能直接访问局部环境中的任何数据
- 变量的执行环境有助于确定应该何时释放内存。

JavaScript 是一门具有自动垃圾收集机制的编程语言，开发人员不必关心内存分配和回收问题。可以对 JavaScript 的垃圾收集例程坐如下总结。

- 离开作用域的值将被自动标记为可以回收，因此将在垃圾收集期间被删除。
- "标记清除"是目前主流的垃圾收集算法，这种算法的思想是给当前不使用的值加上标记，然后再回收其内存。
- 另一种垃圾收集算法是"引用计数"，这种算法的思想是跟踪记录所有值被引用的次数。JavaScript 引擎目前都不再使用这种算法；但在 IE 中访问非原生 JavaScript 对象（如 DOM 元素）时，这种算法仍然可能会导致问题。
- 当代码中存在循环引用现象时，"引用计数"算法就会导致问题。
- 解除变量的引用不仅有助于消除循环引用现象，而且对垃圾收集也有好处。为了确保有效地回收内存，应该及时解除不再使用的全局对象、全局对象属性以及循环引用变量的引用。



## <a name="type">引用类型</a>

- 使用 Array 构造函数时可以省略 new 操作符

```javascript
var colors = Array(3) // 创建一个包含 3 项的数组
var names = Array('Thomas') // 创建一个包含 1 项，即字符串"Greg"的数组
```

- 数组的 length 属性很有特点——它不是只读的。因此，通过设置这个属性，可以从数组的末尾移除项或向数组中添加新项。

  ```javascript
  var colors = ['red', 'blue', 'green'] // 创建一个包含 3 个字符串的数组
  colors.length = 2
  alert(colors[2]) // undefined
  ```

- 数组最多可以包含 4294967295 个项，这几乎已经能够满足任何编程需求了。如果想添加的项数超过这个上限值，就会发生异常。而创建一个初始大小与这个上限接近的数组，则可能会导致运行时间超长的脚本错误。

- `alert()` 接收字符串参数

- 如果不给 `join()` 方法传入任何值，或者给它传入 undefined，则使用逗号作为分隔符。IE7 及更早版本会错误地使用字符串"undefined"作为分隔符。

- 如果数组中的某一项的值是 null 或者 undefined，那么该值在 `join()` 、`toString()` 和 `valueOf()` 方法返回的结果中以空字符串表示。

- `push()` 方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改数组的长度。而 `pop()` 方法则从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

  ```javascript
  var colors = new Array()
  var count = colors.push('red', 'green')
  alert(count) // 2
  
  count = colors.push('black')
  alert(count) // 3
  
  var item = colors.pop()
  alert(item) // "black"
  alert(colors.length) // 2
  
  ```

- 在默认情况下，`sort()` 方法按升序排列数组项——即最小的值位于最前面，最大的值排在最后面。为了实现排序，`sort()` 方法会调用每个数组项的 `toString()`转型方法，然后比较得到的字符串，以确定如何排序。即使数组的每一项都是数值，`sort()` 方法比较多也是字符串，如下所示。

  ```js
  var values = [0, 1, 5, 10, 15]
  values.sort()
  alert(values) // 0, 1, 10, 15, 5
  ```

  `sort()` 接收一个比较函数作为参数，比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回0，如果第一个参数应该位于第二个参数之后则返回一个正数。

  ```js
  function compare(value1, value2) {
    if (value1 < value2) {
      return -1
    } else if (value1 > value2) {
      return 1
    } else {
      return 0
    }
  }
  ```

  当然，也可以通过比较函数产生降序排序的结果，只要交换比较函数返回的值即可。

  ```js
  function compare(value1, value2) {
    if (value1 < value2) {
      return 1
    } else if (value1 > value2) {
      return -1
    } else {
      return 0
    }
  }
  ```

- `reverse()` 和 `sort()` 方法的返回值是经过排序之后的数组。

- 对于数值类型或者 `valueOf()` 方法会返回数值类型的对象类型，可以使用一个更简单的比较函数。这个函数只要用第二个值减第一个值即可。

  ```js
  function compare(value1, value2) {
    return value2 - value1
  }
  ```

- `concat()` 方法可以基于当前数组中的所有项创建一个新数组。具体来说，这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本到末尾，最后返回新构建的数组。在没有给 `concat()` 方法传递参数的情况下，她只是复制当前数组并返回副本。如果传递给 `concat()` 方法的是一个或多个数组，则该方法会将这些数组中的每一项都添加都结果数组中。如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾。

  ```js
  var colors = ['red', 'green', 'blue']
  var colors2 = colors.concat('yellow', ['black', 'brown'])
  
  alert(colors) // red, green, blue
  alert(colors2) // red, green, blue, yellow, black, brown
  ```

- `slice()` 方法不会影响原始数组

- `splice()` 方法的主要用途是向数组的中部插入项，但使用这种方法的方式则有如下 3 种。

  - 删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。例如，splice(0, 2) 会删除数组中的前两项。
  - 插入： 可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、0（要删除的项数）和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项。例如，splice(2, 0, "red", "green") 会从当前数组的位置 2 开始插入字符串"red"和"green"。
  - 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项和要插入的任意数量的项。插入的项数不必与删除的项数相等。例如，splice(2, 1, "red", "green") 会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串 "red" 和 "green"。

- `splice()` 方法始终返回一个数组，该数组中包含从原始数组中删除的项（如果没有任何项，则返回一个空数组）

  ```js
  var colors = ['r', 'g', 'b']
  var removed = colors.splice(0, 1)
  alert(colors) // g,b
  alert(removed) // r
  
  removed = colors.splice(1, 0, 'y', 'o')
  alert(colors) // g,y,o,b
  alert(removed) // 返回一个空数组
  
  removed = colors.splice(1, 1, 'r', 'p')
  alert(colors) // g,r,p,o,b
  alert(removed) // y
  ```

- `indexOf()` 方法从数组的开头（位置 0）开始向后查找，`lastIndexOf()` 方法则从数组的末尾开始向前查找。**这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引**。在比较第一参数与数组中的每一项是，会使用**全等操作符**。

  ```js
  var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1]
  
  alert(numbers.indexOf(4)) // 3
  alert(numbers.lastIndexOf(4)) // 5
  
  alert(numbers.indexOf(4, 4)) // 5
  alert(numbers.lastIndexOf(4, 4)) // 3
  
  var person = { name: "Thomas"}
  var people = [{ name: "Thomas" }]
  
  var morePeople = [person]
  
  alert(people.indexOf(person))  // -1
  alert(morePeople.indexOf(person)) // 0
  
  ```

- `every()` ：对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true。

- `filter()`：对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组。

- `forEach()`：对数组中的每一项运行给定函数。这个方法没有返回值。

- `map()`：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。

- `some()`：对数组中的每一项运行给定函数，如果该函数对任何一项返回true，则返回true。

  以上方法都不会修改数组中的包含的值。

  ```js
  var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1]
  var everyResult = numbers.every(function (item, index, array) {
    return (item > 2)
  })
  
  alert(everyResult) // false
  
  var someResult = numbers.some(function (item, index, array) {
    return (item > 2)
  })
  alert(someResult) // true
  
  ```

  ```js
  var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1]
  var filterResult = numbers.filter(function (item, index, array) {
    return (item > 2)
  })
  
  alert(filterResult) // [3, 4, 5, 4, 3]
  ```

  ```js
  var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1]
  var mapResult = numbers.map(function (item, index, array) {
    return item * 2
  })
  
  alert(mapResult) // [2, 4, 6, 8, 10, 8, 6, 4, 2]
  ```

- `reduce()` 和 `reduceRight()` 这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中，`reduce()` 方法从数组的第一项开始，逐个遍历到最后。而`reduceRight()`则从数组的最后一项开始，向前遍历到第一项。

  ```js
  var values = [1, 2, 3, 4, 5]
  var sum = values.reduce(function (prev, cur, index, array) {
    return prev + cur
  }) 
  alert(sum) // 15
  ```

- 正则表达式的 `valueOf()` 方法返回正则表达式本身。

- **函数的名字仅仅是一个包含指针的变量而已。因此，即使是在不同的环境中执行，全局的sayColor()函数与o.sayColor()指向的仍然是同一个函数。**

- prototype属性是不可枚举的，因此使用 for-in 无法发现。

- 我们使用 false 值创建了一个 Boolean 对象。然后，将这个对象与基本类型值 true 构成了逻辑与表达式。在布尔运算中，false && true 等于 false。可是，示例中的这行代码是对 falseObject 而不是对它的值（false）进行求值。布尔表达式中的所有对象都会被转换为 true，因此 falseObject 对象在布尔表达式中代表的是 true。

  ```js
  var falseObject = new Boolean(false)
  var result = falseObject && true
  alert(result) // true
  
  var falseValue = false
  result = falseValue && true
  alert(result)
  ```

- 可以为 `toString()` 方法传递一个表示基数的参数，告诉它返回几进制的字符串形式

  ```js
  var num = 10
  alert(num.toString()) // "10"
  alert(num.toString(2)) // "1010"
  alert(num.toString(8)) // "12"
  alert(num.toString(10)) // "10"
  alert(num.toString(16)) // "a"
  ```

- `concat()` 、`slice()` 、`substr()` 和 `substring()` 不会修改字符串本身的值。

- `slice()` 方法会将传入的负值与字符串长度相加，`substr()` 方法将负的第一个参数加上字符串的长度，而将负的第二个参数转换为 0。`substring()` 方法会把所有负值的参数都转换为 0 。

  ```js
  var stringValue = 'hello world'
  alert(stringValue.slice(-3)) // "rld"
  alert(stringValue.substring(-3)) // "hello world"
  alert(stringValue.substr(-3)) // "rld"
  alert(stringValue.slice(3, -4)) // "lo w"
  alert(stringValue.substring(3, -4)) // "hel"
  alert(stringValue.substr(3, -4)) // "" (空字符串)
  ```



## <a name="object">面向对象的程序设计</a>

- Object.defineProperty() 把 configurable 属性定义设置为不可配置（false）之后，就不能再把它变回可配置了。

  ```js
  var person = {}
  Object.defineProperty(person, "name", {
    configurable: false,
    value: "Thomas"
  })
  
  // 抛出错误
  Object.defineProperty(person, "name", {
    configurable: true,
    value: "Thomas"
  })
  ```

- 在调用 Object.defineProperty() 方法时，如果不指定，configurable、enumerable 和 writable 特性的默认值都是 false。

- `new` 操作符会经历以下 4 个步骤：

  - 创建一个新对象
  - 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）
  - 执行构造函数中的代码（为这个新对象添加属性）
  - 返回新对象

- 构造函数的缺点是针对每个实例都会创建同样一组新方法。

## <a name="function">函数表达式</a>

- 初始化未经声明的变量，总是会创建一个全局变量。在严格模式下给未经声明的变量赋值会导致错误。

## <a name="bom">BOM</a>

- 全局变量不能通过 delete 操作符删除，而直接在 window 对象上的定义的属性可以。
- window.location 和 document.location 引用的是同一个对象

## <a name="dom">DOM</a>

- document.URL 取得完整的 URL
- document.domain 取得域名
- document.referrer 取得来源页面的 URL
- 取得特性的方法：`getAttribute()` 、`setAttribute()` 、 `removeAttribute()`
- 创建新元素：`document.createElement()`
- 创建文本节点：`document.createTextNode()`
- 创建文档片段：`document.createDocumentFragment()`

## <a name="json">JSON</a>

- 在序列化 JavaScript 对象时，所有函数及原型成员都会被有意忽略，不体现在结果中。此外，值为 undefined 的任何属性也都会被跳过。结果中最终都是值为有效 JSON 数据类型的实例属性。

## <a name="performance">性能</a>

- 避免全局查找，使用全局变量和函数肯定要比局部的开销更大，因为要涉及作用域链上的查找。
- 避免 with 语句，with 语句会创建自己的作用域，因此会增加其中执行的代码的作用域链的长度。由于额外的作用域链查找，在 with 语句中执行的代码肯定会比外面执行的代码要慢。
- 避免不必要的属性查找，使用变量和数组要比访问对象上的属性更有效率。
- 优化循环
  - 减值迭代
  - 简化终止条件
  - 简化循环体
  - 使用后测试循环
- 展开循环
- 避免双重解释
- 原生方法较快
- switch 语句较快
- 位运算符较快
- 多个变量声明
- 插入迭代值
- 使用数组和对象字面量
- 最小化现场更新
- 使用 innerHTML
- 使用事件代理
- 注意 HTMLCollection，任何时候要访问 HTMLCollection，不管它是一个属性还是一个方法，都是在文档上进行一个查询，这个查询开销很昂贵。最小化访问 HTMLCollection 的次数可以极大地改进脚本的性能。以下情况会返回 HTMLCollection 对象：
  - 进行了对 getElementsByTagName() 的调用
  - 获取了元素的 childNodes 属性
  - 获取了元素的 attributes 属性
  - 访问了特殊的集合，如 document.forms、document.images 等。