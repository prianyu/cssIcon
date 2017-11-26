 图标作为网页设计中的一部分，其在凸显网页重要元素特性，视觉交互、引导以及网页装饰等充当的角色作用举足轻重。由于图标普遍具有尺寸小的特点，在项目实践时不宜将每个图标作为单个图片元素进行加载，这会大大增加Http请求，影响网页的性能。因此，在实际中，我们可能见到以下一些常见的解决方案：

 + 将多个图标按照一定排列顺序合并在一个图片里（即`sprite图`），再通过CSS设置元素的`background-position`来为元素设置背景从而展示图标
 + 将单个图标元素转成`base64`格式，并在CSS声明背景
 + 使用`SVG`或者图标字体库来绘制图标
 + 使用CSS来绘制图标
 + ...
 
以上方式都可以很好的实现功能，各有各的优缺点。在移动端，我个人比较偏好使用CSS来实现一些图标，原因有以下几点：

+ 适应性和定制性强，如可以随意改变颜色，大小
+ 占用空间小
+ 在移动端兼容性高
+ 可以不断使自己熟悉CSS3的各个属性并得以应用


而由于CSS3的普及和在各大浏览器的不断增强支持，使CSS具有更大的可能性和能力去绘制更多样化，更复杂的图标。当然，也有不少人反对网站图标使用CSS绘制的，在这里不加以讨论。

本文将单独讲解如何用CSS绘制一些图标。而由于用CSS实现图标绘制，偶尔意味着你需要用更复杂的html结构去支持图标的绘制，所以本文讲解的将是`单标签CSS图标`。这样可以实现类似仅用`img`标签或者单个标签应用字体库实现图标绘制的效果。讲解如何绘制之前，先给大家看看前阵子得闲绘制的若干个单标签CSS图标。

![](./images/demo.png)

### 你需要掌握的CSS属性

绘制图标，单从绘制来讲，无非就是画点、线、面。然后将多个点线面组合得到图标。因此，你至少应该掌握以下CSS属性的应用

+ 盒子模型
+ border属性的应用（很重要，可以参考）
+ position的各个属性值的应用
+ transform变形
+ `outline`,`box-shadow`（常见于多边框绘制）
+ CSS渐变(常用于图标中透明过渡)
+ 伪类和伪元素的应用
+ `transition`，`animation`（如果要绘制动态图标，本文仅讲解静态图标）

需要掌握的主要为以上内容，有些特殊的处理可能还需要其他一些CSS属性的应用。

### 几个说明

+ 由于大部分情况下图标的大小按照所处环境上下文的字体大小来决定，所以本文所有例子的大小单位大部分使用`em`，按照当前字号来设定大小
+ 有些`border`属性没有指明`border-color`,如`border-top: .4em solid`,是因为`border-color`默认继承了字体颜色
+ 所有图标仅作为例子展示，实现方法多样，不代表最佳实践

### 基本元素的绘制

### 用`border`属性绘制元素

border除了作为简单的绘制边框以外，还可以绘制三角形，梯形，星形等任意的多边形，以下为绘制的两个三角形和梯形，更多的应用可以参考
[border属性的多方位应用和实现自适应三角形](https://juejin.im/post/5a162d3ff265da43062a6e27)这篇文章，里面全面的介绍了用border绘制各种多边形。
```html
<div class="triangle1"></div>
<div class="triangle2"></div>
<div class="trapezoid"></div>
```

```css
.triangle1 {/*锐角三角形*/
	width: 0;
	height: 0;
	border-top:50px solid transparent;
	border-bottom:100px solid #249ff1;
	border-left: 30px solid transparent;
	border-right: 100px solid transparent;
}
.triangle2 {/*直角三角形*/
	width: 0;
	height: 0;
	border-top: 80px solid transparent;
	border-bottom: 80px solid #ff5b01;
	border-left: 50px solid #ff5b01;
	border-right:50px solid transparent;
	}
.trapezoid {/*梯形*/
	width:0;
	height:0;
	border-top:none;
	border-right:80px solid transparent;
	border-bottom:60px solid #13dbed;
	border-left: 80px solid #13dbed;
}

```
![](./images/border.png)


#### 用`border-radius`绘制元素

`border-radius`主要用于绘制圆点、圆形、椭圆、圆角矩形等形状，以下为简单绘制的两个图形。

```html

<div class="circle"></div>
<div class="ellipse"><div>

```

```css
.circle,.ellipse {
	width: 100px;
	height: 100px;
	background: #249ff1;
	border-radius: 50%;
}
.ellipse {
	width: 150px;
	background: #ff9e01;
}
```
![](./images/circle.png)

但`border-radius`属性实际上可以设置最多8个值，通过改变8个值可以得到许多意想不到的图像，如图（该图来源于[这里](http://www.zhangxinxu.com/wordpress/2015/11/css3-border-radius-tips/)）

![](./images/borderradius.gif) 
![](./images/borderradius2.gif)

更多关于`border-radius`属性的特点和应用请参考张鑫旭写的[《秋月何时了，CSS3 border-radius知多少？》](http://www.zhangxinxu.com/wordpress/2015/11/css3-border-radius-tips/)