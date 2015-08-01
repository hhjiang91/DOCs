title: 针对浮动元素，怎么居中呢？
date: 2015-07-20 17:09:00
tags:
- css
categories: 日志
---

### 什么是浮动元素
w3c：由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。

### 针对一个浮动元素，怎么居中（水平和垂直）？
这就有两种情况:
1、元素大小知道
	元素大小即已知， 我们可以通过margin和left， top进行补偿， 使得元素可以居中。
	![known](./img/floatCenter/known1.jpg)
	![known](./img/floatCenter/known2.jpg)

2、元素大小不知道
   元素大小未知， 我们通过margin auto自适应。 这里我们要补一下知识， 定位的布局取决于三个因素：元素的位置，元素的尺寸，元素的margin值。
   没有设置尺寸和 margin 的元素会自适应剩余空间，位置固定则分配尺寸，尺寸固定边会分配 margin，都是自适应的。
IE7- 的渲染方式不同，渲染规则也不一样，他不会让定位元素去自适应。
 
   ![unknown](./img/floatCenter/unknown.jpg)


### 怎么样子可以水平居中一个浮动元素？
 当然采用上述的方法肯定是可行的， 但是我们要介绍一种新方法：一个盒子浮动  加一个relative的盒子在外面  然后把盒子设为absolute  然后定位：外面盒子向右偏移50% left  里面的向左偏移50% right。
   ![unknown](./img/floatCenter/unknown0.jpg)



### 怎么居中一个图片？
1、最简单的方式， display table-cell
display:table-cell属性指让标签元素以表格单元格的形式呈现，类似于td标签。目前IE8+以及其他现代浏览器都是支持此属性的，但是IE6/7只能对你说sorry了，这一事实也是大大制约了display:table-cell属性在实际项目中的应用。我们都知道，单元格有一些比较特别的属性，例如元素的垂直居中对齐，关联伸缩等，所以display:table-cell还是有不少潜在的使用价值的，虽说IE6/7不支持此属性，但是幸运的是，IE6/7一些乱糟糟的属性与渲染，我们可以其他方法实现同样或是类似的效果。
与其他一些display属性类似，table-cell同样会被其他一些CSS属性破坏，例如float, position:absolute，所以，在使用display:table-cell与float:left或是position:absolute属性尽量不用同用。设置了display:table-cell的元素对宽度高度敏感，对margin值无反应，响应padding属性，基本上就是活脱脱的一个td标签元素了

相关应用请参考[博客](http://www.zhangxinxu.com/wordpress/2010/10/我所知道的几种displaytable-cell的应用/)

``` bash
<div class="imgDiv">
     <img src="img.jpg">
</div>

.imgDiv{
     width: 500px;
     height: 200px;
     border: 1px solid grey;
     text-align: center;
     display:table-cell; //因为table是默认居中显示的
     vertical-align: middle;
}

 ```       
 ![imgCenter](./img/floatCenter/imgCenter1.jpg)


2、理解vertical-align，添加span
但是上述会出现低版本不兼容问题， 那么为什么简单的vertical-align没有用呢？

利用vertical-align :该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐、所以这个需要把块级容易的基准线定位居中。

因此我们需要添加一个相应的基准线

``` bash
<div class="imgDiv">
     <span></span>
     <img src="ex.jpg">
</div>

.imgDiv{
     width: 500px;
     height: 200px;
     border: 1px solid grey;
     text-align: center;
}
.imgDiv img{
     vertical-align: middle;
}

.imgDiv span{
     height: 100%;
     display: inline-block;
     vertical-align: middle;
}

```
结果如图：
 ![imgCenter](./img/floatCenter/imgCenter2.jpg)


###结论
关乎定位， 还真是很有学问， 其中table-cell只是浅尝辄止， 还有很多问题没有看， 当然关于居中有很多方法， 见仁见智啦。