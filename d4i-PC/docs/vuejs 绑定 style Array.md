# vuejs 绑定 style Array

```html
<template>
  <div :style="[styles, { background: 'red' }]">
  </div>
</template>

<script>
export default {
  data() {
    return {
      styles: "color: red;"
    }
  }
}
</script>
```

https://vuejs.org/v2/guide/class-and-style.html#Array-Syntax-1