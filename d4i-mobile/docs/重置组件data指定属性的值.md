# 重置组件data指定属性的值

```js
methods: {
  resetDataProperties(properties) {
    properties.forEach(property => {
      Object.keys(property).forEach(name => {
        this[name] = property[name];
      });
    });
  },
  submit() {
    this.resetDataProperties([{ password: "" }]);
  }
}
```