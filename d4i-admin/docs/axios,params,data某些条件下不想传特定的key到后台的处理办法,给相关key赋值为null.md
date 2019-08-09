# axios,params,data某些条件下不想传特定的key到后台的处理办法,给相关key赋值为null

```js
axios({
  method: "GET",
  url: "data/delete",
  params: { version: value.length ? "v1" : null }, // value.length 小于 0
  data: { version: value.length ? "v1" : null }
})
```