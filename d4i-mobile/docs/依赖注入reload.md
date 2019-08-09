# 依赖注入 reload

App.vue

```vue
<template>
  <div id="app">
    <router-view v-if="isRouterAlive" />
  </div>
</template>

<script>
export default {
  provide() {
    return {
      reload: this.reload
    };
  },
  data() {
    return {
      isRouterAlive: true
    };
  },
  methods: {
    reload() {
      this.isRouterAlive = false;
      this.$nextTick(() => {
        this.isRouterAlive = true;
      });
    }
  }
};
</script>
```

Component.vue

```js
export default {
  inject: ["reload"],
  methods: {
    handleClick() {
      this.reload();
    }
  }
}
```