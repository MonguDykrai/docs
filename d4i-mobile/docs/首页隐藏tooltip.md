# 首页隐藏tooltip

```html
<template>
  <div>
    <img class="emoji" v-show="show" src="face.svg" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true
    }
  },
  methods: {
    documentHandleClick(e) {
      if (!Array.from(e.target.classList).includes("emoji")) {
        if (this.show) {
          this.show = false;
        }
      }
    }
  },
  mounted() {
    window.addEventListener("click", this.documentHandleClick);
  },
  beforeDestroy() {
    window.removeEventListener("click", this.documentHandleClick);
  }
}
</script>
```