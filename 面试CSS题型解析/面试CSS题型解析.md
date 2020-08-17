# CSS部分解析

### 1、移动端适配



### 2、盒模型

> 
>
> ​	==实际盒子的总宽高===内容（context）的宽度+border + padding + margin
>
> ​	
>
> ​	`标准盒子模型（W3C标准）`
>
> ​	标准盒模型设置的宽度=内容（context）的宽度
>
> ​	标准盒模型设置的高度=内容（context）的高度
>
> ​	
>
> ​	`IE盒子模型（怪异盒模型）`
>
> ​	怪异盒模型设置的宽度=内容（context）的宽度 + border（左右）+ padding（左右）
>
> ​	怪异盒模型设置的高度=内容（context）的高度 + border（上下）+ padding（上下）
>
> ​	
>
> ​	相较标准盒模型来说，怪异盒模型设置的宽高包含了元素的边框和padding，在适配上优于标准盒模型，
>
> ​	设置方法：
>
> ​	box-sizing: content-box;    //`标准盒模型`
>
> ​	box-sizing: border-box; 	//`怪异盒模型`
>
> 



### 3、元素居中方法

#### 水平/垂直居中

> ​	1、水平元素居中 （有宽度的块状元素）｛ margin：0 auto ｝
>
> ​	2、在块级元素中设置，使文字，内联元素水平居中 ｛ text-align : center ｝
>
> ​	3、文字垂直居中 ｛ line-height: 元素高度 ｝

#### 绝对居中

> ​	div水平垂直居中：
>
> ​	1、设置为absolute绝对定位，top，left设置5%，margin-left-top 偏移宽高的一半
>
>   **position: absolute;**
>
> ​      **left: 50%;**
>
> ​      **top: 50%;**
>
> ​      **margin-left: -150px;**
>
> ​      **margin-top: -150px;**  
>
> ​	`优点：浏览器兼容性强`，==缺点：必须知道具体宽高==
>
> 
>
> ​	2、 设置absolute绝对定位，top，left设置50%，用CSS3的transform:translate方法上左各偏移-50%
>
> ​		**position: absolute;**
>
> ​      **left: 50%;**
>
> ​      **top: 50%;**
>
> ​      **transform: translate(-50%, -50%);**
>
> ​	`优点：不需要知道元素宽高`，==缺点:css3方法，部分低版本浏览器不支持==
>
> 
>
> ​	3、 设置absolute绝对定位，上下左右设置为0px，margin设置auto
>
> ​	  **position: absolute;**
>
> ​      **top: 0px;**
>
> ​      **bottom: 0px;**
>
> ​      **left: 0px;**
>
> ​      **right: 0px;**
>
> ​      **margin: auto;**
>
> ​	`优点：浏览器兼容性较好`，==缺点:不支持IE7以下浏览器==
>
> 
>
> ​	4、在父元素中设置display：flex ，设置水平垂直方向居中
>
> ​		**display: flex;**
>
> ​      **justify-content: center;**
>
> ​      **align-items: center;**
>
> ​		`适合移动端布局`
>
> 
>
> ​	5、✨ 将父元素display:设置为table-cell，此时就可以使用vertical-align: middle对内部的子元素进行垂直居中。之后在子元素样式中使用margin: 0 auto;实现水平居中
>
> ​	**father {**
>
> ​      **display: table-cell;**
>
> ​      **vertical-align: middle;**
>
> ​    **}**
>
> ​    **son {**
>
> ​      **margin: 0 auto;**
>
> ​    **}**
>
> ​	（不使用，了解即可）



### 4、CSS3动画





### 5、CSS选择器权重

> ​	权重计算优先级别（引用方式）
>
> ​	内联样式表（写在元素标签内部style属性中）>嵌入样式表（写在head头部style中）>外部样式表（外部导入css文件）
>
> - 内嵌样式： 优点： 方便书写，权重高；缺点： 没有做到结构和样式分离；
> - 内联样式： 优点：结构样式相分离； 缺点：没有彻底分离；
> - 外联样式： 优点： 完全实现了结构和样式相分离； 缺点： 需要引入才能使用；
>
> 
>
> **CSS选择器列表：**
>
> ```
> 1、ID　　#id
> 2、class　　.class
> 3、标签　　p
> 4、通用　　*
> 5、属性　　[type="text"]
> 6、伪类　　：hover
> 7、伪元素　　::first-line
> 8、子选择器、相邻选择器
> ```
>
> 
>
> **CSS选择器权重比：**
>
> ```
> 1、第一等：内联样式，如: style=””，权值为1000。
> 2、第二等：ID选择器，如：#content，权值为0100。
> 3、第三等：类，伪类和属性选择器，如.content，权值为0010。
> 4、第四等：标签选择器和伪元素选择器，如div p，权值为0001。
> 5、通配符、子选择器、相邻选择器等的。如*、>、+,权值为0000。
> 6、继承的样式没有权值。
> ```
>
> ​	
>
> ​	在同等优先级别下，遵循css选择器权重，`!important`具有最高的优先级别
>
> 



### 6、Position属性

> ​	
>
> `Position属性值列表：`
>
> ​	relative:（相对定位）定位原点是元素本身所在的位置
>
> ​	absolute: （绝对定位）定位原点是距离自身最近的一个relative定位父元素的左上角
>
> ​	static:（默认）默认正常流，设置top，left，right，bottom，z-index属性无效
>
> ​	flex:（固定定位）定位原点是浏览器窗口
>
> ​	inherit:（继承父元素定位）继承父级元素的定位属性
>
> 

### 7、Flex属性

> ​	**Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。**
>
> ​	`⭐:`设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。
>
> ![](bg2015071004.png)
>
> ​	flax布局有主轴和交叉轴，项目默认沿着主轴排列。
>
> ​	**容器属性：**
>
> - flex-direction
> - flex-wrap
> - flex-flow
> - justify-content
> - align-items
> - align-content

#### 容器属性

>   **flex-direction**:	 属性决定主轴的方向，即项目排列方向。
>
> ​	（row、row-reverse、column、column-resverse）[水平向右，水平向左，垂直向下，垂直向上]
>
> ​	**flex-wrap:	**属性绝定在主轴上超出可视区是否换行。
>
> ​	（nowrap、wrap、wrap-resverse）[默认不换行，向下换行，向上换行]
>
> ​	**flex-flow:** 	是flex-direction和flex-wrap的结合简写形式
>
> ​		[ flex-flow: <flex-direction> || <flex-wrap>; ]
>
> ​	**justify-content:**	属性定义了项目在主轴上的对齐方式。
>
> ​	（flex-start 、flex-end 、 center 、 space-between 、 space-around、space-evenly）
>
> ​		[默认左对齐，右对齐，居中，两端对齐，项目两侧间距相同，所有间距相同]
>
> ​	**align-items:**	定义交叉轴上项目的对齐方式
>
> ​	（flex-start 、 flex-end 、 center、 baseline 、 stretch;）
>
> ​		[交叉轴起点对齐，交叉轴终点对齐，中心对齐，项目第一行文字基准线对齐，占满容器高度]
>
> ​	**align-content** 定义多跟交叉轴线的对齐方式，必须结合flex-wrap使用
>
> ​	（flex-start 、 flex-end 、 center、space-between、space-around、stretch）
>
> ​		[交叉轴起点对齐，终点对齐，中心对齐，两端对齐，项目两端间隔对齐，默认占满高度]

#### 容器内项目属性

> ​	**order:**	定义项目排列顺序，数值越小，排列越靠前，默认为0
>
> ​	**flex-grow:**	定义项目空间占比，默认为0不进行放大。
>
> ![](bg2015071014.png)
>
> ​		如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
>
> ​	
>
> ​	**flex-shrink:**	属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
>
> ![](bg2015071015.jpg)
>
> ​		如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。
>
> 
>
> ​	**flex-basis：**	属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。
>
> 
>
> ​	**align-self:**	属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。
>
> ![](bg2015071016.png)









### 8、浏览器兼容性问题



### 9、H5和CSS3新增方法



### 10、Link和@import区别



### 11、清除浮动方法



### 12、触发BFC条件



### 13、Z-index作用和失效条件



### 14、Canvas用法



### 15、Float常用属性和影响



### 16、常用单位（px，em，rem……）



### 17、回流重绘原理和避免方法

> ​	`浏览器渲染机制：`
>
> 1、浏览器采用流式布局 （Flow Based Layout）
> 2、浏览器首先会把Html解析成DOM，形成DOM树，把CSS解析成CSSOM，DOM树和CSSOM合并形成渲染树
> 3、浏览器根据渲染树就能根据每个DOM节点在页面中的位置和样式把DOM渲染到页面中。
>
> ​	`重绘：`
>
> ​	DOM节点仅发生样式变化，或几何属性的变化不影响布局，称为重绘。（浏览器必须验证DOM树上的其他节点是否发生变化，消耗性能）
>
> ​	`回流:`
>
> ​	回流是网页布局或几何属性发生了变化称为回流，回流及其消耗网页性能，因为涉及部分页面甚至整个网页的布局发生了变化或更新，一个DOM节点发生回流，可能会影响其所有子元素也发生回流……
>
> `⭐重绘不一定会引发回流，回流一定会发生重绘`
>
> 
>
> ​	避免减少重绘回流的方法：
>
> ​			**CSS方法**
>
> 1. ​	使用transform来代替top，left等属性。
>
> 2. 使用visibility：hidden 来替代display：none
>
> 3. 避免使用table来布局
>
> 4. 尽可能在DOM树的最末端来改变class样式
>
> 5. 避免嵌套多层内联样式	css选择器不可过多 确保减少无意义的选择器
>
> 6. 将动画效果作用到position：flex或position：absolute上，避免影响其他DOM元素产生回流。
>
> 7. 避免使用CSS表达式
>
> 8. 使用CSS3硬件加速，使用transform、opacity、filters这些动画效果不会引起回流和重绘。
>
>    **JS方法**
>
>    1. 避免频繁操作样式
>    2. 避免频繁操作DOM，
>    3. 不要频繁读取 获得位置信息等属性（==offsetTop==等等）
>    4. 对具有复杂动画的元素使用绝对定位让其脱离文档流。



### 18、优雅降级和渐进增强

> ​	**渐进增强（Progressive Enhancement）**：一开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。
>
> ​	**优雅降级（Graceful Degradation）**：一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。



### 19、轮播图原理（手写）



### 20、Less和Stylus的区别



### 21、Doctype的作用

> ​	**DOCTYPE 是 html5 标准网页声明，必须放在HTML文档的第一行，用来告知浏览器该HTML文档是用什么规格编写的，让浏览器用正确的解析器对HTML文档内容进行解析**  `区分XML和HTML`



### 22、边框1px的解决方案



### 23、Html语义化的理解

> ​	**1、使HTML结构清晰明了，呈现良好的代码组织架构**
>
> ​	**2、在丢失css样式的情况下，能一目了然的知道网页的布局**
>
> ​	**3、有利于seo，便于搜索引擎爬虫抓取更多信息**
>
> ​	**4、遵循W3C标准，减少团队之间代码差异，语义化更具有可读性**



### 24、栅格布局和两栏布局原理



### 25、CSS性能优化







