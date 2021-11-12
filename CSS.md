# 1、CSS 的权重和优先级

## 						1-1、权重

- 从0开始，
- 一个行内样式+1000
- 一个id选择器+100
- 一个属性选择器、class或者伪类+10
- 一个 元素选择器，或者伪元素+1
- 通配符+0

##                1-2、优先级

- 权重相同，写在后面的覆盖前面的 
- 使用 !important 达到最大优先级，都使用 !important 时，权重大的优先级高
- ==!important > id > class > tag;   !important  比 内联优先级高==

# 2、 Flex 布局

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性；

## 2-1、注意:

设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效

## 2-2、兼容`Webkit`(必须)

`Webkit` 内核的浏览器，必须加上`-webkit`前缀

```css
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
```

## 2-3、开启flex的几大属性

#### 2-3-1、flex-direction（父盒子）

作用：决定主轴的排列方式，（就是竖着还是横着）

```css
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823110652881.png" alt="image-20210823110652881" style="zoom:80%;" />

#### 2-3-2、flex-wrap（父盒子）

作用：决定在主轴方向上，元素如果排不下，是否换行？

```css
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

- `nowrap`（默认）：不换行

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823111004372.png" alt="image-20210823111004372" style="zoom: 67%;" />

- `wrap`：换行，第一行在上方

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823111044083.png" alt="image-20210823111044083" style="zoom: 67%;" />

- `wrap-reverse`：换行，第一行在下方

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823111101371.png" alt="image-20210823111101371" style="zoom:67%;" />

#### 2-3-3、justify-content（父盒子）

作用：决定在主轴方向上的元素对齐方式

```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

下面以`flex-direction:row`，主轴方向是**横向**为准

- flex-start（左对齐）----- 默认

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112352084.png" alt="image-20210823112352084" style="zoom:67%;" />

- flex-end：（右对齐）

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112417509.png" alt="image-20210823112417509" style="zoom:67%;" />

- center：居中对齐

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112320296.png" alt="image-20210823112320296" style="zoom:67%;" />

- space- between：两端对齐

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112512097.png" alt="image-20210823112512097" style="zoom:67%;" />

- space-around：沿轴线均匀分布

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112545564.png" alt="image-20210823112545564" style="zoom:67%;" />

#### 2-3-4、align-items（父盒子）

作用：属性定义项目在交叉轴上如何对齐

```css
.box {
  align-items: flex-start | flex-end | center  | stretch | baseline;
}
```

理解：如果主轴方向为`row`横向的，那么align-items属性设置的就是：“垂直方向上的排列方式”

例如：下面以`flex-direction:row`，主轴方向是**横向**为准

- flex-start：顶端对齐----默认

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823113026129.png" alt="image-20210823113026129" style="zoom:67%;" />

　　　　flex-end：底部对齐

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823113053793.png" alt="image-20210823113053793" style="zoom:67%;" />

- center：竖直方向上居中对齐

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823112957641.png" alt="image-20210823112957641" style="zoom: 67%;" />

- stretch：当item未设置高度时，item将和容器等高对齐

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823113429353.png" alt="image-20210823113429353" style="zoom:67%;" />

#### 2-3-4、order（子元素）

在开启弹性布局，给子元素设定order的值是整数，默认为0，整数越小，item排列越靠前

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210823114149627.png" alt="image-20210823114149627" style="zoom:67%;" />

#### 2-3-5、flex-grow（子元素）

作用：在主轴的方向上，将**剩余的空间**瓜分（放大），默认值为0:

```css
<div class="wrap">
    <div class="div" style="flex-grow:1"><h2>item 1</h2></div>
    <div class="div" style="flex-grow:2"><h2>item 2</h2></div>
    <div class="div" style="flex-grow:3"><h2>item 3</h2></div>
</div>
```

#### 2-3-6、flex-shrink（子元素）

作用：在主轴的方向上，**当容器空间不足时**，决定了子元素是否（缩小），默认值为1；

#### ...... (其他的不常用)

# 3、 `CSS`实现自适应正方形、等宽高比矩形

- 双重嵌套，外层 relative，内层 absolute 

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
    <style>
        .outer {   
            width: 50%;
            height: 0;
            background: #ccc;
            padding-top: 50%;
            position: relative;
        }
        .inner {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: blue;
        }
    </style>
</head>
<body>
    <div class="outer">
   		 <div class="inner">hello</div>
    </div>
</body>
</html>
```

- padding 撑高 

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
<style>
        .outer {
            width: 400px;
            height: 600px;
            background: blue;
        }
        .inner {
            width: 100%;
            height: 0;
            padding-bottom: 100%;
            background: red;
        }
    </style>
</head>
<body>
    <div class="outer">
     	<div class="inner"></div>
    </div>
</body>
</html>
```

-  伪元素设置 margin-top: 100% 撑高

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
<style>
        .outer {
            width: 400px;
            overflow:hidden;
            background: blue;
        }
        .inner {
            content:"";
            margin-top:100%;
            display:block;
        }
    </style>
</head>
<body>
    <div class="outer">
   		 <div class="inner"></div>
    </div>
</body>
</html>
```

# 4、CSS 动画有哪些？

​      animation、transition、transform、translate 这几个属性要搞清楚： 

- **animation**：用于设置动画属性，他是一个简写的属性，包含6个属性 
- **transition**：用于设置元素的样式过度，和animation有着类似的效果，但细节上有很大的不同 
- **transform**：用于元素进行旋转、缩放、移动或倾斜，和设置样式的动画并没有什么关系 
- **translate**：只是transform的一个属性值，即移动，除此之外还有 scale 等

# 5、Css2 垂直居中 和 水平居中

​	5-1、已知宽高，设置水平垂直居中

```html
<style>
    .outer {
        position: relative;
        width: 400px;
        height: 600px;
        background: blue;
     }
     .inner {
        position: absolute;
        width: 200px;
        height: 300px;
        background: red;
        left: 50%;
        top: 50%;
        margin: -150px 0 0 -100px;
    }
</style>
<body>
<div class="outer">
	<div class="inner"></div>
</div>
</body>

```

  5-2、宽高未知，比如内联元素 ，设置垂直水平居中

```html
<style>
    .outer {
        width: 400px;
        height: 600px;
        /* background: blue; */
        border: 1px solid red;
        background-color: transparent;
        position: relative;
    }
    .inner {
        position: absolute;
        background: red;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }
</style>
<body>
    <div class="outer">
    	<span class="inner">我想居中显示</span>
    </div>
</body>
```

  **5-3、绝对定位的 div 水平垂直居中**

```html
<style>
    .outer {
        width: 400px;
        height: 600px;
        /* background: blue; */
        border: 1px solid red;
        background-color: transparent;
        position: relative;
    }
    .inner {
        position: absolute;
        background: red;
        left: 0;
        right: 0;
        bottom: 0;
        top: 0;
        width: 200px;
        height: 300px;
        margin: auto;
        border: 1px solid blue;
    }
</style>
<body>
    <div class="outer">
    	<div class="inner">我想居中显示</div>
    </div>
</body>
```

  **5-4、图片和其他元素使用 display: table-cell; 进行垂直居中**

```html
	<style>
	.outer {
        width: 400px;
        height: 600px;
        /* background: blue; */
        border: 1px solid red;
        background-color: transparent;
        display: table-cell;
        vertical-align: middle;
    }  
    .inner {
        background: red;
        width: 200px;
        height: 300px;
        border: 1px solid blue;
        margin: 0 auto;
    }
</style>
<body>
    <div class="outer">
   		 <div class="inner">我想居中显示</div>
    </div>
</body>

```

# 6、Css3垂直居中 和 水平居中

​	6-1、弹性布局

```html
<style>
    .outer {
        width: 400px;
        height: 600px;
        display: flex;
        /* 垂直居中 */
        align-items: center;
        /* 水平居中 */
        justify-content: center;
        border: 1px solid red;
        background-color: transparent;
    }
    .inner {
        background: red;
        width: 200px;
        height: 300px;
        border: 1px solid blue;
    }
</style>
<body>
    <div class="outer">
    	<div class="inner">我想居中显示</div>
    </div>
</body>
```

# 7、visibility 和 display 的差别（还有opacity)

- visibility：

  设置 hidden 会隐藏元素，但是其位置还存在与页面文档流中，不会被删除，所以会触 发浏览器渲染引擎的重绘 

- display：

  设置了 none 属性会隐藏元素，且其位置也不会被保留下来，所以会触发浏览器渲染引擎 的回流和重绘。 

- opacity：

  会将元素设置为透明，但是其位置也在页面文档流中，不会被删除，所以会触发浏览器 渲染引擎的重绘

  可以设置过渡效果
  
  <img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210726145921940.png" alt="image-20210726145921940" style="zoom:67%;" />



# **8、 什么是 `BFC`**

​			`BFC`（Block Formatting Context）格式化上下文，是 Web 页面中盒模型布局的 `CSS` 渲染模式，指一个独立的渲染区域或者说是一个隔离的独立容器。

## 8-1、作用/用处

- **高度塌陷问题**：通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合。这时就可以用`BFC`来清除浮动了
- **div浮动兄弟遮盖问题**：由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。可以给蓝色块加 overflow: hidden，触发`BFC`来解决遮挡问题
- **margin塌陷问题**：在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。可以用`overflow：hidden`产生`BFC`来解决

## 	8-2、BFC 的特性

- 内部的 Box 会在垂直方向上一个接一个的放置。 
- 垂直方向上的距离由 margin 决定 
- BFC 的区域不会与 float 的元素区域重叠。
- 计算 bfc 的高度时，浮动元素也参与计算
- bfc 就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。

## 	8-3、如何开启 BFC (五种)

- 浮动元素，float 除 none 以外的值 
- 定位元素 ：position（absolute，fixed） 
- display 为以下其中之一的值 inline-block，table-cell，table-caption 
- overflow 除了 visible 以外的值（hidden，auto，scroll） 
- HTML 就是一个 BFC

## 8-4、BFC 与 IFC 区别 

- BFC 是块级格式上下文
- IFC 是行内格式上下文： 
- 内部的 Box 会水平放置 水平的间距由 margin，padding，border

##  8-5、BFC 会与 float元素 相互覆盖吗？为什么？举例说明 

1. 不会，
2. 因为 BFC 是页面中一个独立的隔离容器，其内部的元素不会与外部的元素相互影响，
3. 比如两个 div，上面的 div 设置了 float，那么如果下面的元素不是 BFC，也没有设置 float，会形成对上面的元素 进行包裹内容的情况，如果设置了下面元素为 overflow：hidden；属性那么就能够实现经典的两列布 局，左边内容固定宽度，右边因为是 BFC 所以会进行自适应。

# 9、position属性，都有啥特点？

- static：无特殊定位，对象遵循正常文档流。top，right，bottom，left等属性不会被应用。 
- relative：对象遵循正常文档流，但将依据top，right，bottom，left等属性在正常文档流中偏移位置。 而其层叠通过z-index属性定义。
- absolute：==对象脱离正常文档流==，使用top，right，bottom，left等属性进行绝对定位。而其层叠通过z-index属性定义。 
- fixed：==对象脱离正常文档流==，使用top，right，bottom，left等属性以窗口为参考点进行定位，当出现 滚动条时，对象不会随着滚动。而其层叠通过z-index属性定义。
- sticky：具体是类似 relative 和 fixed，在 viewport 视口滚动到阈值之前应用 relative，滚动到阈值之后 应用 fixed 布局，由 top 决定。

# 10、清除浮动

为什么要清除浮动：

​		当父元素没有设定指定的高度，或者设定的高度小于 子元素高度的总和时，会出现高度塌陷

- clear清除浮动（添加空div法）在浮动元素下方添加空div,并给该元素写css样式： 	{clear:both;height:0;overflow:hidden;} 

- 给浮动元素父级设置高度

- 父级同时浮动（需要给父级同级元素添加浮动） 

- 父级设置成inline-block，其margin: 0 auto居中方式失效 给父级添加overflow:hidden 清除浮动方法 

- 万能清除法 after伪类 清浮动（现在主流方法，推荐使用）

  --- >>> **只要给 需要清除浮动的 父元素 添加 .clearfix 类样式名即可**

```html
<style>  
    .clearfix::after{
		content: "";
		display: block;
		height: 0;
		clear: both;
		visibility: hidden;
	}
	.clearfix {
		/* IE专用 */
		*zoom:  1;
	}
</style>

```

# 11、透明度 opacity



​		opacity: 给该元素 添加透明度属性 可选值是:  0~1  之间的数值 
​									0：完全透明
​									1：饱和度最大

​		但是IE8及以下 不兼容
​								需要用：  filter: alpha(opacity=透明度);
​								透明度： 0~100

```html
opacity: 0.5;
filter: alpha(opacity=50); 兼容ie浏览器
```

# 	12、Overflow

**属性指定在元素的内容太大而无法放入指定区域时是剪裁内容还是添加滚动条**

​			overflow 属性可设置以下值：

1. visible - 默认。溢出没有被剪裁。内容在元素框外渲染
2. hidden - 溢出被剪裁，其余内容将不可见
3. scroll - 溢出被剪裁，同时添加滚动条以查看其余内容
4. auto - 与 scroll 类似，但仅在必要时添加滚动条

`overflow` 属性**仅适用于具有指定高度**的块元素



# 13、Less基础

​			为了解决 css 文件编写样式时，出现的代码冗余问题，在css 的基础上开发了Less语言

## 			13-1、安装node环境

​						[Node.js 中文网 (nodejs.cn)](http://nodejs.cn/)

## 			13-2、查看是否安装成功

![image-20210727150010363](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210727150010363.png)

## 			13-3、安装less

​							`npm i -g -less`

## 			13-4、查看less是否安装成功

![image-20210727150157005](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210727150157005.png)

## 			13-5、VsCode 下载插件编译less

（下载成功之后记得重启vscode）

![image-20210727150706103](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210727150706103.png)

## 			13-6、使用

当你保存less文件时，会自动生成对应名称的css文件，只需要将编译成功后的css文件引入就可以使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <link rel="stylesheet" href="./My_less/index.css">
    <title>Document</title>
</head>
<body>
    <div class="box">
        <p>2512</p>
    </div>
</body>
</html>
```

## 			13-7、样式嵌套使用

```less
.box{
    width:100%;
    height:200px;
    background-color:pink;
    
    p{
        font-size:20px;
        // 伪类元素的写法
        &:hover{
            color:red;
        }
    }
}
```

# 14、Rem适配

## 	14-1、设计稿：

​			目前主流 以  IPhone6/7/8  750px 屏幕宽度为基准；

设计稿 是指：将屏幕宽度为分几等分，例如15等分，那么 设计稿设计html的字体大小就可以为：750/15 = 50px;

```css
html{  font-size: 50px }
```

# 15、`position`有哪些值？有什么作用

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211011210124524.png" alt="image-20211011210124524" style="zoom:80%;" />



# 16、垂直居中

![image-20211011210405923](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211011210405923.png)

# 17、水平居中

![image-20211011210424934](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211011210424934.png)

# 18、盒模型

## 18-1、W3C 标准盒模型

​		属性width,height只包含内容content，不包含border和padding

​		width/height = content

## 18-2. IE 盒模型(怪异盒模型)

​		属性width,height包含border和padding，指的是content+padding+border。

​		width/height = content + border + padding

# 19、`CSS` 加载方式有几种？

```html
1、行内样式
<p style="color:red;">123</p>
2、内联样式
<style></style>
3、链如外部样式表
<link></link>
4、导入样式
（直接在
	<style>
        @import '../asd.css';
	</style>
 ）
```

# 20、页面导入时，使用 link 和 @import 有什么区别？

1. 引入的位置；
2. 一个标签，一个`css`独有的；
3. 加载顺序，link 先加载；@import会等页面出来才开始加载；
4. 兼容性，Link没有兼容性的问题，@import有ES5之前不支持；
5. ⻚⾯被加载的时， link 会同时被加载，⽽ @imort ⻚⾯被加载的时， link 会同时被加 载，⽽ @import 引⽤的 CSS 会等到⻚⾯被加载完再加载 import 只在 IE5 以上才能识 别，⽽ link 是 XHTML 标签，⽆兼容问题 link ⽅式的样式的权重 ⾼于 @import 的权 重

# 21、伪类选择器\元素

# 22、什么是 `CSS` 继承？哪些属性能继承，哪些不能？

### 22-1、能继承的属性

**1. 字体系列属性:**font、font-family、font-weight、font-size、font-style;
**2. 文本系列属性:**
（1）内联元素：color、line-height、word-spacing、letter-spacing、text-transform;
（2）块级元素：text-indent、text-align;
**3. 元素可见性：**visibility
**4. 表格布局属性：**caption-side、border-collapse、border-spacing、empty-cells、table-layout;
**5. 列表布局属性：**list-style
**6. 生成内容属性：**quotes
**7. 光标属性：**cursor
**8. 页面样式属性：**page、page-break-inside、windows、orphans;
**9. 声音样式属性：**speak、speech-rate、volume、voice-family、pitch、stress、elevation;

### 22-2、不能继承的属性

**1. display：**规定元素应该生成的框的类型；
**2. 文本属性：**vertical-align、text-decoration;
**3. 盒子模型的属性：**width、height、margin 、border、padding;
**4. 背景属性：**background、background-color、background-image;
**5. 定位属性：**float、clear、position、top、right、bottom、left、min-width、min-height、max-width、max-height、overflow、clip;
**6. 生成内容属性：**content、counter-reset、counter-increment;
**7. 轮廓样式属性：**outline-style、outline-width、outline-color、outline;
**8. 页面样式属性：**size、page-break-before、page-break-after;
**9. 声音样式属性：**pause、cue、play-during;

# 23、 px，em，rem，vw 有什么区别？

# 24、box-sizing

默认值：

1. content-box（默认） ->  此时元素的宽度 = width + padding + border （高度同理）
2. border-box  ->  此时元素的宽度 = width （高度同理）
3. inherit  ->  此时元素的宽度 = 继承父容器设置过`box-sizing = border-box`的宽度