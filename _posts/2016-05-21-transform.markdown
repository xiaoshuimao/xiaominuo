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

---



<s id="rotate"></s>
### 如何使用 transform 功能 ###
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
{% highlight ruby %}
.rotate-div-1 {
	width: 300px;
	margin: 150px auto;
	background-color: #22baa0;
	text-align: center;
	transform: rotate(45deg);
}
{% endhighlight %}
这里使用了 **transform: rotate(45deg)** 顺时针旋转了45度。deg是css3中 “ Value and Utils” 模块中定义的**角度单位** 



### transform功能的分类 ###
在css3中，可以使用transform的实现4种文字或者图像的处理，分别是[旋转](#rotate)、[缩放](#scale)、[倾斜](#skew)、[移动](#translate)

旋转的功能已经在上面介绍过了，使用rotate的方法，参数中传入一个角度值，后面紧跟着一个“deg”，表示角度单位文字，旋转方向顺时针，如果要逆时针，只要在角度值前加 **负号 “ - ”**即可。
{% highlight ruby %}
transform: rotate(-45deg);
{% endhighlight %}

<s id="scale"></s>
#### 1. 缩放
使用**sacle**关键字来实现文字或者图片的缩放，在scale中传入参数指定缩放的倍数。例如[scale(0.5)表示缩小一半](#scale-div-1)，[scale(2)表示放大一倍](#scale-div-2)。
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
{% highlight ruby %}
.scale-div-1 {
	width: 300px;
	margin: 50px auto;
	background-color: #22baa0;
	text-align: center;
	transform: scale(0.5);
} 
{% endhighlight %}

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
{% highlight ruby %}
.scale-div-2 {
	width: 300px;
	margin: 50px auto;
	background-color: #22baa0;
	text-align: center;
	transform: scale(2);
} 
{% endhighlight %}

To be continued...

