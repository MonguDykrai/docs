# UTC转本地

```js
function utcToLocalTime(time) {
  return this.$moment
    .utc(time)
    .local()
    .format("YYYY/MM/DD");
}
```

```js
function utcToLocalTime(time) {
  return this.$moment
    .utc(time)
    .local()
    .format("YYYY年MM月DD日 HH:mm:ss");
}
```

https://momentjs.com/