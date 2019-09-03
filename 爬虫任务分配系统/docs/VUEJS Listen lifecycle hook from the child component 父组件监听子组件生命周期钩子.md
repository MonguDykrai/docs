# 监听子组件生命周期

`childMounted` 函数将在子组件 mounted 钩子函数触发时被触发。

```html
<!-- Parent.vue  -->
<template>
  <div>
    <Child @hook:mounted="childMounted" />
  </div>
</template>

<script>
  export default {
    name: "Parent",
    methods: {
      childMounted() {
        console.log(`childMounted`)
      }
    }
  }
</script>
```

https://dev.to/f3ltron/vuejs-listen-lifecycle-hook-from-the-child-component-2hp9