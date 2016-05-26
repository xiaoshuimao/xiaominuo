```js
// 由于 Node 原生支持模块的作用域，并不需要额外的 wrapper
// "as though the module was wrapped in a function"

var a = require('./a')  // 加载模块（同步加载）
a.doSomething()         // 等上一句执行完才会执行

exports.b = function(){ // 暴露 b 函数接口
  // do something
}
```