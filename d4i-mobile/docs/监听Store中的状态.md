# 监听Store中的状态

'$store.state.userId'

```js
watch: {
  '$store.state.userId'() {
    this.getShareFavoriteList({userId: this.userId});
  }
}
```