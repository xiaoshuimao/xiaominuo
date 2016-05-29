---
layout: post
title: transform的基础知识(一)
subtitle: "rotate, scale, skew, translate"
date: 2015-05-25
author: w567675
---
> This document is not completed and will be updated anytime.

## 前言

w567675的博客开始写第一篇文章。主要记录每天学习的知识。

这篇文章是阅读了一本《HTML5 于 CSS3 权威指南》下册记录下的.

---



<s id="rotate"></s>
### 如何使用 transform 功能

> 这里主要展示下基本的transform的rotate用法

<style type="text/css"> 
	.rotate-div-1 {
		width: 300px;
		margin: 150px auto;
		background-color: #22baa0;
		text-align: center;
		transform: rotate(45deg);
	} 
</style>
<div class="rotate-div-1">rotate(45deg)</div>

```css
.rotate-div-1 {
	width: 300px;
	margin: 150px auto;
	background-color: #22baa0;
	text-align: center;
	transform: rotate(45deg);
}
```
这里使用了 `transform: rotate(45deg)` 顺时针旋转了45度。`deg`是css3中 “ Value and Utils” 模块中定义的`角度单位` 



### 1. transform功能的分类 ###
在css3中，可以使用transform的实现4种文字或者图像的处理，分别是[旋转](#rotate)、[缩放](#scale)、[倾斜](#skew)、[移动](#translate)

旋转的功能已经在上面介绍过了，使用`rotate`的方法，参数中传入一个**角度值**，后面紧跟着一个“`deg`”，表示角度单位文字，旋转方向顺时针，如果要逆时针，只要在**角度值**前加 `负号 “ - ”`即可。

```css
transform: rotate(-45deg);
```
	
<s id="scale"></s>

#### 1.1 缩放（scale）
使用`sacle`关键字来实现文字或者图片的缩放，在scale中传入参数指定缩放的倍数。例如[scale(0.5)表示缩小一半](#scale-div-1)，[scale(2)表示放大一倍](#scale-div-2)。
<style type="text/css"> 
	.scale-div-1 {
		width: 300px;
		margin: 50px auto;
		background-color: #22baa0;
		text-align: center;
		transform: scale(0.5);
	} 
</style>
<div class="scale-div-1" id="scale-div-1">scale(0.5)</div>
<p class="pic-tips">图（一）</p>

```css
.scale-div-1 {
	width: 300px;
	margin: 50px auto;
	background-color: #22baa0;
	text-align: center;
	transform: scale(0.5);
} 
```

<style type="text/css"> 
	.scale-div-2 {
		width: 300px;
		margin: 50px auto;
		background-color: #22baa0;
		text-align: center;
		transform: scale(2);
	} 
</style>
<div class="scale-div-2" id="scale-div-2">scale(2)</div>
<p class="pic-tips">图（二）</p>

```css
.scale-div-2 {
	width: 300px;
	margin: 50px auto;
	background-color: #22baa0;
	text-align: center;
	transform: scale(2);
} 
```

`scale(x, y)`可以分别指定2个参数，`x`表示 水平方向的放大倍数，`y`表示垂直方向的放大倍数。如果只是输入一个参数表示**水平**和**垂直**的放大倍数**一致**。


<s id="skew"></s>

#### 1.2 倾斜（skew）
使用`skew`关键字来实现文字或者图片的倾斜处理。使用`skew`的方法，参数中传入一个**角度值**，
后面紧跟着一个“`deg`”。例如[skew(30deg)](#skew-div-1):

<style type="text/css"> 
	.skew-div-1 {
		width: 300px;
		margin: 50px auto;
		background-color: #22baa0;
		text-align: center;
		transform: skew(30deg);
	} 
</style>
<div class="skew-div-1" id="skew-div-1">skew(30deg)</div>


`skew(x, y)`也可以分别指定2个参数，`x`表示 水平方向的倾斜角度，`y`表示垂直方向的倾斜角度。
 看到这里可能不知道`skew`具体是怎么倾斜的？ 下面就仔细分析下（果断借用大拿的示例图）。

![](/img/in-post/transform-base-1/skew-x30-deg.jpg) 

> `skew(30deg, 0deg)`， `x`轴角度向逆时针倾斜了`30deg`

![](/img/in-post/transform-base-1/skew-y10-deg.jpg) 

> `skew(0deg, 10deg)`， `y`轴角度向顺时针倾斜了`10deg`

![](/img/in-post/transform-base-1/skew-x30y10-deg.jpg) 

> `skew(30deg, 10deg)`， `x`轴角度向逆时针倾斜了`30deg`, `y`轴角度向顺时针倾斜了`10deg`

**注意：**`skew`方法，y轴顺时针转为正，X轴逆时针转为正, 到这里你应该能清楚知道skew倾斜的方法了。纳尼，不知道？`what are you 弄啥咧？`

<s id="移动（translate）"></s>

#### 1.3 移动（translate）
使用translate来实现文字或图片的移动，在参数中分别指定水平方向上移动距离和垂直反向上的移动距离。例如[translate(50px, 0)](#translate-div-1) 和 [translate(0, 50px)](#translate-div-2)：

<style type="text/css"> 
	div.transform-container {
		width: 200px;
		height: 200px;
		margin: 50px auto;
		border: 1px solid #ccc;
	}
	.translate-div-1 {
		width: 100px;
		background-color: #22baa0;
		text-align: center;
		transform: translate(50px, 0);
	} 
</style>
<div class="transform-container">
	<div class="translate-div-1" id="translate-div-1">translate(50px, 0)</div>
</div>
```css
.translate-div-1 {
	width: 100px;
	background-color: #22baa0;
	text-align: center;
	transform: translate(50px, 0);
} 
```

<style type="text/css"> 
	.translate-div-2 {
		width: 100px;
		background-color: #22baa0;
		text-align: center;
		transform: translate(0, 50px);
	} 
</style>
<div class="transform-container">
	<div class="translate-div-2" id="translate-div-2">translate(0, 50px)</div>
</div>
```css
.translate-div-2 {
	width: 100px;
	background-color: #22baa0;
	text-align: center;
	transform: translate(0, 50px);
} 
```

**注意：** ``translate``方法中的2个参数可以修改成1个参数。如果只是1个参数，省略另外1个参数，这种情况被视为只是在水平距离上的移动，垂直距离上不移动。
	

### 2. 对一个元素使用多种变形

#### 2.1 对一个元素使用多种变形的方法

上面我们已经看到了transform中的 `rotate`、`scale`、`skew`、`translate`种变形方法。
现在我们对一个元素操作试试看有什么不同的区别。

首先我们对一个元素按照`translate`、`rotate`、`scale`的执行顺序来写我们的css代码。结果如：
<style type="text/css">
	.translate-rotate-scale-div-1 {
		width: 100px;
		background-color: #22baa0;
		transform: translate(50px, 100px) rotate(45deg) scale(1.5);
	}
</style>
<div class="transform-container">
	<div class="translate-rotate-scale-div-1" id="translate-rotate-scale-div-1">translate-rotate-scale-div-1</div>
</div>
```css
.translate-rotate-scale-div-1 {
	width: 100px;
	background-color: #22baa0;
	transform: translate(50px, 100px) rotate(45deg) scale(1.5);
}
```

看到这里，结果的确如我们所预期的那样：

1.  首先`translate(50px, 100px)`, 水平方向`向右移动50px`，垂直方向`向下移动100px`。
2.  然后`rotate(45deg)`, 旋转45度。
3.  最后`scale(1.5)`, 放大了1.5倍。


这里我们改变下变形的执行顺序，元素按照`rotate`、`translate`、`scale`的执行顺序来写我们的css代码。看看是什么效果：

<style type="text/css">
	.translate-rotate-scale-div-2 {
		width: 100px;
		background-color: #22baa0;
		transform: rotate(45deg) translate(50px, 100px)  scale(1.5);
	}
</style>
<div class="transform-container">
	<div class="translate-rotate-scale-div-2" id="translate-rotate-scale-div-2">translate-rotate-scale-div-2</div>
</div>
```css
.translate-rotate-scale-div-2 {
	width: 100px;
	background-color: #22baa0;
	transform: rotate(45deg) translate(50px, 100px)  scale(1.5);
}
```
``what!? `` 结果好像和第一次执行的结果``不一样么``？why? why?。

真想只有一个！

请看下集（css3-transform 连环变形坐标“杀人”事件）

### to be continue...