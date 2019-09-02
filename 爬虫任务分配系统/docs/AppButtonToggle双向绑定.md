# AppButtonToggle双向绑定

`@change="$emit('input', $event)"`

```html
<!-- MtTaskStatistics.vue -->
<template>
  <v-sheet>
    <app-button-toggle v-model="toggle_exclusive"></app-button-toggle>
  </v-sheet>
</template>

<script>
export default {
  name: "MtTaskStatistics",
  data() {
    return {
      toggle_exclusive: undefined,
    };
  },
};
</script>
```

```html
<!-- AppButtonToggle.vue -->
<template>
  <v-btn-toggle
    :value="value"
    @change="$emit('input', $event)"
    mandatory
    style="position: absolute; right: 0;"
  >
    <v-btn style="height: 32px;">周统计图</v-btn>
    <v-btn style="height: 32px;">月统计图</v-btn>
  </v-btn-toggle>
</template>

<script>
export default {
  name: "AppButtonToggle",
  props: ["value"],
};
</script>
```