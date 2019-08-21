# vue2-scrollbar

```bash
yarn add vue2-scrollbar
```

```html
<template>
  <div class="sidebar" style="padding: 0;" ref="sidebar">
    <vue-scrollbar style="height: 100%;">
    <app-tabs
        :tabs="['图谱', '关系', '属性']"
        defaultValue="图谱"
        :style="{ width: '204px' }"
        style="position: absolute;"
        :scrollTop="scrollTop"
      >
    </app-tabs>
  </div>
</template>

<script>
import VueScrollbar from "vue2-scrollbar";
import "vue2-scrollbar/dist/style/vue2-scrollbar.css";

export default {
  components: {
    VueScrollbar,
  }
}
</script>
```

https://bosnaufal.github.io/vue2-scrollbar/

https://github.com/BosNaufal/vue2-scrollbar