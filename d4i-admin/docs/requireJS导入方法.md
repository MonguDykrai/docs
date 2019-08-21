# requireJS导入方法

```js
// fn.js
exports = module.exports = function fn(msg) { console.log(msg) }
```

```js
// app.js
require(./fn)("hello world")
```

参考资料 express.js

```js
/**
 * Expose `createApplication()`.
 */

exports = module.exports = createApplication;
```