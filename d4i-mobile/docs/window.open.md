# window.open

window.open(URL,name,specs,replace)

URL: 	可选。打开指定的页面的URL。如果没有指定URL，打开一个新的空白窗口

name: _self - URL替换当前页面

```js
// parent
window.open(url, "_self")

window.callbackFn = function (message) {
  console.log(message)
}.bind(this)
```

```js
// child
window.opener.callbackFn("hello, there")
```

https://www.runoob.com/jsref/met-win-open.html