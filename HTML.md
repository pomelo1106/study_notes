# 1、HTML5 有哪些新特性？ 

- （1）HTML4 规定了三种声明方式，分别是：**严格模式**、**过渡模式** 和 **框架集模式**；而HTML5因为不是 SGML的子集，只需要就可以了： 
- （2）语义化更好的内容标签。header/footer/article等 
- （3）音频、视频 API(audio,video) 
- （4）表单控件：HTML5 拥有多个新的表单输入类型。这些新特性提供了更好的输入控制和验证。 color date datetime datetime-local email month number range search tel time url week 
- （5）5个API-本地存储，长期存储数据的 localStorage，比较常用，临时存储的 sessionStorage，浏览 器关闭后自动删除，实际工作中使用的场景不多。 
- （6）画布/Canvas，canvas，figure,figcaption. 地理/Geolocation.地理位置 API 允许用户向 Web 应用程序提供他们的位置。出于隐私考虑，报 告地理位置前会先请求用户许可。
- （7）拖拽释放.HTML拖拽释放 (Drag and drop) 接口使应用程序能够在浏览器中使用拖放功能。例如， 通过这些功能，用户可以使用鼠标选择可拖动元素，将元素拖动到可放置元素，并通过释放鼠标按 钮来放置这些元素。可拖动元素的一个半透明表示在拖动操作期间跟随鼠标指针。 
- （8）Web Workers.webworker, websocket, Geolocation,当在 HTML 页面中执行脚本时，页面的状态 是不可响应的，直到脚本已完成。web worker 是运行在后台的 JavaScript，独立于其他脚本，不 会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

# 2、Doctype作⽤?

**严格模式与混杂模式如何区分？它们有何意义?** 

`<!DOCTYPE >`声明位于⽂档中的最前⾯，处于标签之前。告知浏览器的解析器， ⽤什么⽂档类型 规范来解析这个⽂档 严格模式的排版和 JS 运作模式是 以该浏览器⽀持的最⾼标准运⾏ 在混杂模式中，⻚⾯以宽松的向后兼容的⽅式显示。模拟⽼式浏览器的⾏为以防⽌站点⽆法⼯作。 DOCTYPE 不存在或格式不正确会导致⽂档以混杂模式呈现 

# **3、如何实现浏览器内多个标签页之间的通信？**

​			**调用 localstorge、cookies 等本地存储方式；**

- 调用 localstorge、cookies 等本地存储方式； 在 B 页面中可以使用 window.opener 获得 A 页面的 window 句柄，使用该句柄即可调用 A 页面 中的对象，函数等。 
- 例如 A 页面定义 js 函数 onClosePageB，在 B 页面可以用 window.opener.onClosePageB 来进行 回调。
- 使用 window.showModalDialog(sURL [, vArguments] [,sFeatures])打开新窗口。 其中 vArguments 参数可以用来向对话框传递参数。传递的参数类型不限，包括数组、函数等。对话框 通过window.dialogArguments来取得传递进来的参数。
- 如果是支持 HTML5 的话，建议用本地存储 (local storage)，它支持一个事件方法 window.onstorage，只要其中一个窗口修改了本地存储，其他同源窗口会触发这个事件。 

​          **总结：** 

- WebSocket、SharedWorker；
- 也可以调用 localstorge、cookies 等本地存储方式；
- localstorge 另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件， 我们通过监听事件，控制它的值来进行页面信息通信； 
- 注意 quirks：Safari 在无痕模式下设置 localstorge 值时会抛出 QuotaExceededError 的异常；

​           **3.1、方法一：调用 localstorge**

- 标签1：

  ```html
  <input id="name">
  <input type="button" id="btn" value="提交">
  <script type="text/javascript">
  $(function(){
  $("#btn").click(function(){
  var name=$("#name").val();
  localStorage.setItem("name", name); //存储需要的信息
  });
  });
  </script>
  ```

- 标签2：

  ```javascript
  $(function(){ window.addEventListener("storage", function(event){ console.log(event.key + "=" + event.newValue); }); //使用storage事件监听添加、修改、删除的动作 });
  ```

​           **3.2、方法二：使用 cookie+setInterval **

​					将要传递的信息存储在 cookie 中，每隔一定时间读取 cookie 信息，即可随时获取要传递的信息。

- 标签1:

```javascript
 $(function(){ 
     window.addEventListener("storage", function(event){ 
         console.log(event.key + "=" + event.newValue); //使用storage事件监听添加、修改、删除的动作
     }); 
 }); 
```

# 4、⾏内元素有哪些？块级元素有哪些？ 

- 空(void)元素有那些？⾏内元 素和块级元素 有什么区别？ 
- ⾏内元素有： a b span img input select strong 
- 块级元素有： div ul ol li dl dt dd h1 h2 h3 h4… p 
- 空元素： br,hr img input link meta 
- ⾏内元素不可以设置宽⾼，不独占⼀⾏ 块级元素可以设置宽⾼，独占⼀⾏ 

# 5、简述⼀下src与href的区别？ 

- src ⽤于替换当前元素，href⽤于在当前⽂档和引⽤资源之间确⽴联系。
- src 是 source 的缩写，指向外部资源的位置，指向的内容将会嵌⼊到⽂档中当前标签所在位置；在 请求 src 资源时会将其指向的资源下载并应⽤到⽂档内，例如 js 脚本，img 图⽚和 frame 等元素 。
- 当浏览器解析到该元素时，会暂停其他资源的下载和处理， 直到将该资源加载、编译、执⾏完毕，图⽚和框架等元素也如此，类似于将所指向资源嵌⼊当前标签内。这也是为什么将js脚本放在底 部⽽不是头部
- href 是 Hypertext Reference 的缩写，指向⽹络资源所在位置，建⽴和当前元素（锚点）或当前⽂ 档（链接）之间的链接，如果我们在⽂档中添加 
- `<link href="common.css" rel="stylesheet"/>`那么浏览器会识别该⽂档为 css ⽂件，就会 并⾏下载资源并且不会停⽌对当前⽂档的处理。这也是为什么建议使⽤ link ⽅式来加载 css ，⽽不 是使⽤ @import ⽅式 

# 6、 cookies,sessionStorage,localStorage 的区别？

- cookie 是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加 密）。
- cookie 数据始终在同源的 http 请求中携带（即使不需要），记会在浏览器和服务器间来回传递。 
- sessionStorage 和 localStorage 不会自动把数据发给服务器，仅在本地保存。

​		**存储大小** 

- cookie 数据大小不能超过 4k。 
- sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得多，可以达到 5M 或 更大。 

​       **有期时间**

- localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
- sessionStorage 数据在当前浏览器窗口关闭后自动删除。 
- cookie 设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭

# 7、HTML5 的离线储存的使用和原理？

​		**相似存储**

- localStorage 长期存储数据，浏览器关闭后数据不丢失； sessionStorage 数据在浏览器关闭后自动删 除。

​		**离线存储**    两种方式 

- HTML5 的离线存储.appcache文件【废弃】
- service-worker 的标准

​		**HTML5的离线存储 .appcache文件[弃用]**

- 在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓 存文件。 
- 原理：HTML5 的离线存储是基于一个新建的。appcache 文件的缓存机制（不是存储技术），通过这个 文件上的解析清单离线存储资源，这些资源就会像 cookie 一样被存储了下来。
- 之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示

​		**如何使用**

- 页面头部像下面一样加入一个 manifest 的属性 
- 在 cache.manifest 文件的编写离线存储的资源
- 在离线状态时，操作 window.applicationCache 进行需求实现。 `service-worker`

# 8、怎样处理 移动端 1px 被 渲染成 2px 问题？

- meta 标签中的 viewport 属性 ，initial-scale 设置为 1
- rem 按照设计稿标准走，外加利用 transfrome 的 scale(0.5) 缩小一倍即可； 2 全局处理 
- meta 标签中的 viewport 属性 ，initial-scale 设置为 0.5 
- rem 按照设计稿标准走即可

​      **解释**

- UI 设计师设计的时候，画的 1px（真实像素）实际上是 0.5px(css) 的线或者边框。但是他不这么认为， 他认为他画的就是 1px 的线，因为他画的稿的尺寸本身就是屏幕尺寸的 2 倍。假设手机视网膜屏的宽度 是 320x480 宽，但实际尺寸是 640x960 宽，设计师设计图的时候一定是按照 640x960 设计的。但是前 端工程师写代码的时候，所有 css 都是按照 320x480 写的，写 1px(css)，浏览器自动变成 2px（真实像素）。
- 那么前端工程师为什么不能直接写 0.5px(css) 呢？因为在老版本的系统里写 0.5px(css) 的话，会被浏览 器解读为 0px(css)，就没有边框了。所以只能写成 1px(css)，实际在屏幕上显示出来就是设计师画的 1px（真实像素）的 2 倍那么宽，所以设计师会觉得这个线太粗了，和他的设计稿不一样。在新版的系 统里，已经开始逐渐支持 0.5px(css) 这种写法。所以如果设计师在大图上设计了一个 1px（真实像素） 的线的话，前端工程师直接除以 2，写 0.5px(css) 就好了。

​       **另外一种解释** 

- 事实就是它并没有变粗，就是 css 单位中的 1px，对于 dpr 为 2 的设备，它实际能显示的最小值是 0.5px。 设计师口中说的 1px 是针对设备物理像素的，换算成 css 像素就是 0.5px。 
- 一句话总结，background:1px solid black 在任何屏幕上都是一样粗的，但是 retina 屏可以显示比这更 细的边框，然后设计师就不乐意了，让你改。

# 9、浏览器是如何渲染页面的？

1. 浏览器会将`HTML`文件自上而下的解析成DOM树；
2. 将CSS文件进行样式规划；
3. 根据DOM树和CSS样式规划表构建`Render Tree`;
4. 进行布局（重排）；
5. 绘制；

# 10、 iframe 的优缺点？

-  iframe 会阻塞主页面的 Onload 事件； 
-  iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。 
-  使用 iframe 之前需要考虑这两个缺点。
-  如果需要使用 iframe，最好是通过 javascript 动态给 iframe 添加 src 属性值，这样可以可以绕开以上两个问题。

# 11、 Canvas 和 SVG 图形的区别是什么？

​		 Canvas 和 SVG 都可以在浏览器上绘制图形。

​		 SVG Canvas 绘制后记忆，换句话说任何使用 SVG 绘制的形状都能被记忆和操作，浏览器可以再次显示 Canvas 则是绘制后忘记，一旦绘制完成你就不能访问像素和操作它 SVG 对于创建图形例如 CAD 软件是 良好的，一旦东西绘制，用户就想去操作它 Canvas 则用于绘制和遗忘类似动漫和游戏的场画。 

​		为了之后的操作，SVG 需要记录坐标，所以比较缓慢。

​		 因为没有记住以后事情的任务，所以 Canvas 更快。

​		 我们可以用绘制对象的相关事件处理我们不能使用绘制对象的相关事件处理，因为我们没有他们的参考 分辨率独立分辨率依赖 

- SVG 并不属于 html5 专有内容，在 html5 之前就有 SVG。 
- SVG 文件的扩展名是”.svg”。
- SVG 绘制的图像在图片质量不下降的情况下被放大。
- SVG 图像经常在网页中制作小图标和一些动态效果图。

# 12、meta 标签？ 

​		**核心 **  提供给页面的一些元信息（名称 / 值对），有助于 SEO。 

​		**属性值**   

- name 

  名称 / 值对中的名称。author、description、keywords、generator、revised、others。 把 content 属性关联到一个名称。

- http-equiv 

  没有 name 时，会采用这个属性的值。content-type、expires、refresh、set-cookie。把 content 属性关联到 http 头部 

- content 

  名称 / 值对中的值， 可以是任何有效的字符串。 始终要和 name 属性或 http-equiv 属性一起使用

- scheme 

  用于指定要用来翻译属性值的方案。



# 13、img的title和alt有什么区别

- `alt`是图片加载失败时，显示在网页上的替代文字；
- `title`是鼠标放上面时显示的文字。
- `alt`是`img`必要的属性，而`title`不是。

# 14、从浏览器地址栏输入URl到显示页面的步骤

1. 浏览器根据请求的Url交给DNS域名进行解析，找到真实的IP，向服务器发送网络请求
2. 服务器交给后台处理完成后，返回数据，浏览接收文件
3. 浏览器对加载到的资源（html,css,js）等进行语法解析，解析相应的内部数据结构。
4. 载入解析到的资源文件，渲染页面，完成

# 15、介绍一下你对浏览器内核的理解

浏览器内核主要包括两部分： 渲染引擎和`ＪＳ`引擎。

​		－渲染引擎：负责去的网页的内容，整理讯息（ｃｓｓ），以及计算网页的显示方式，最后输出到显示器或者打印机。

​		－ＪＳ引擎：负责解析和执行`javascript`来实现网页的动态效果；

# 16、 在 input 里，ID，name

id是一个标签的标识，name是一个标签的名称；