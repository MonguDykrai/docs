# binding an object of attributes

以 Object 的形式动态绑定多个属性传递给子组件。

```html
<template>
  <div>
    <Child v-bind="{ cols: 12, sm6 }" v-bind:name="'jack'" />
  </div>
</template>
```

https://vuejs.org/v2/api/#v-bind