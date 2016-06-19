---
layout: post
title: 尾调用、尾递归
subtitle: ""
date: 2016-06-19
author: w567675
tags:
    - 随手笔记
---









### 尾调用

尾调用（Tail Call）是函数式编程的一个重要概念。简单来说就是一个函数的执行的最后一步是调用另外一个函数。例如：

```js
function b(x) {
  return a(x); // 这个是尾调用
}
```
上面的函数 `b` 在 执行的最后一步调用了函数 `a` ，这是尾调用。

出现下面几种情况都不算尾调用：

1：在调用函数 `a` 之后还有赋值操作。

```js
function b(x) {
  var result =  a(x); // 这里进行了赋值操作
  return result;
}
```

2：这个和第1种情况一样，在调用函数 `a` 之后还有赋值操作。

```js
function b(x) {
  return a(x) + 1; // 这里进行了赋值操作
  return result;
}
```

3：没有return 调用的函数 `a`，函数 `b` 会默认**return undefined 操作**。这样调用的函数 `a` 就不是最后一步操作。

```js
function b(x) {
  a(x); //没有return返回

  /* return undefined */ 
  //  ^--------- 没有返回值得情况下，函数的最后一步操作，返回undefined
}
```

总而言之，**尾调用就是只要是最后一步操作即可，并不一定是在函数尾部**。

```js
function b(x) {
  if(x) {
    return a(x); //尾调用
  }
  return c(x); //尾调用
}
```



### 尾调用优化

函数的调用会在内存中形成 “调用记录” ，叫做 **“调用帧”(call frame)**，用来保存位置和内部变量等信息。

假如一个``函数A``被调用了， 就会形成``调用帧A``。 在``函数A``内部调用了``函数B``，那就会在``调用帧A``顶部插入一个``调用帧B``，等``函数B``执行完毕并将结果返回到``函数A``的时候，``调用帧B``就会销毁。当``函数A``自身运行结束的时候，``调用帧A``也销毁了。

当然如果``函数B``有调用了``函数C``，``函数C``又调用了``函数D``.....以此类推，就会形成一个**调用栈（call stack）**。

尾调用相对来说比较特殊。**因为尾调用是函数的最后一步操作， 就不用在保留外层函数的调用帧（因为已经不需要该调用帧保存的数据）。直接用内部调用帧取代外部的调用帧即可**。

例如：

```js
function b() {
  let x = 1;
  let y = 2;
  return a(y - x);
}
b();

//等同于

function b() {
  return a(1);
}
b();


//等同于

a(1);
```

上面的代码为什么说是可以等同呢？ 如果说函数a 不是尾调用， 那么势必``函数b``要保存内部变量 ``x`` 、``y`` 、 ``函数a``的调用位置等相关数据。但是``函数a``调用之后，``函数b``就执行完毕了。所以**执行到最后一步，可以删除调用帧b，保留调用帧a**。

这就是**“尾调用优化”（Tail Call Optimization）**， 在保留内部函数的调用帧。如果所有函数**都是尾函数调用**，那么**每次执行时调用帧基本只有一项，大大节省了内存**。“尾优化”的意义的存在就是这个。


注意点：

不是所有都能进行“尾调用优化”，例如：

```js
function b(x) {
  let y = 1;

  function a(z) {
    return y - z;
//         ^------ 调用了外部的变量 y    
  }
  return a(x);
}
```

上面的``函数a`` 用到了 ``函数b`` 定义的变量 ``y``。


### 尾递归

通常的函数调用自身称为递归。那么尾递归就是**尾调用自身**。

递归比较耗费内存，遇到调用次数过多时，会保存成百上千的``调用帧``，就很容易发生“栈溢出”（stack overflow）。上面提到过，尾调用只会存在一个``调用帧``， 意味着 尾递归永远不会发生“栈溢出”。

下面我们来看一个计算阶乘的函数[（n! = 1 x 2 x 3 x ... x n）](http://baike.baidu.com/link?url=FqZP9J3CHfTrzEXfpRd74SsYkFaaY6_Srk6_B9GYKDPT_IiDIwocJmoaPLQPCLkpc-gMyk6DYq1WEnWgM8DzJq){:target="_blank"}:

```js
function factorial(n) {
  if(n === 1) return 1;
  return n * factorial(n - 1); //递归
}
```

上述代码是我们通常会实现的情况，在计算``n!``的时候会保存 ``n个调用帧``。时间复杂度为O(n)。

现在我们改写成尾递归：

```js
function factorial(n, total) {
  if(n === 1) return total;
  return factorial(n - 1, n * total); //尾递归
}
```

上述代码时间复杂度为O(1)。由此可见，“尾调用的优化”对递归非常重要。


### 如何改写成尾递归？

尾递归的实现需要改写递归函数， 确保最后一步一定是调用自己的操作（为什么？请回上面看看...）。如何做到这点，就是**把所有内部用到的参数全部改成函数的参数**。

例如上面的计算阶乘的函数，其中需要``total``来记录每次变化的数值。那就把这个参数改写到函数的参数中去。但是这里可能有一个比较变扭的地方，就是计算一个阶乘为什么要传2个参数...

我们可以在用几种方式来优化下。

第一种自己再封装一次：

```js
function tailFactorial(n, total) {
  if(n === 1) return total;
  return factorial(n - 1, n * total); //尾递归
}

function factorial(n) {
  return tailFactorial(n, 1);
}

factorial(3); // 这里就是统一的对外api接口了。
```
上面简单的封装，另外也可以通过[柯里化（currying）](http://baike.baidu.com/link?url=m7BZK_4ca_NP5lGvSMTwVRwUL38c38rRNIh5d3b7EghlEaTE-hQ28bXKbEaebfu3an5rBAQk5LXEHzvZI5r3QK){:target="_blank"}的方式修改，这里就不展开了。



第二种ES6的默认参数：

```js
function tailFactorial(n, total = 1) {
//                              ^------ ES6 默认参数（自行google）                       
  if(n === 1) return total;
  return factorial(n - 1, n * total); //尾递归
}
```

<img src="https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1466344582&di=00572166f3968b7a37a90d09728597d8&src=http://img5.duitang.com/uploads/blog/201407/24/20140724091456_VVQJz.jpeg" alt="">
