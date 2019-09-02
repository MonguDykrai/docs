# provide inject

```html
<!-- App.vue -->
<template>
  <div id="app">
    <RouterView v-if="isRouterAlive" />
  </div>
</template>

<script>
export default {
  name: 'App',
  provide() {
    return {
      reload: this.reload,
    };
  },
  data() {
    return {
      isRouterAlive: true,
    }
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

```html
<!-- Profile.vue -->
<template>
  <div class="profile">
    昵称：<input type="text" v-model="username" />
    <button @click="update">保存修改</button>
  </div>
</template>

<script>
export default {
  name: 'Profile',
  inject: ["reload"],
  data() {
    return {
      username: "jack",
    };
  },
  methods: {
    update() {
      this.request({
        method: 'PUT',
        url: `/profile`,
        params: {
          username,
        },
      }, {
        success(res) {
          this.$Message.success("用户名更新成功！");

          this.reload();
        },
        failure(error) {
          this.$Message.error(error);
        }
      })
    }
  }
}
</script>
```