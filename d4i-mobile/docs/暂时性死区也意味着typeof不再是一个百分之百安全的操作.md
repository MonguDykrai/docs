# 暂时性死区也意味着typeof不再是一个百分之百安全的操作

```js
typeof x // ReferenceError
let x
```

http://es6.ruanyifeng.com/#docs/let