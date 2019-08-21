# tabs_通过给button添加伪元素实现下划线的效果_模仿唯品会

```html
<style lang="scss" scoped>
.app-tabs {
  .active {
    color: #3399ff;

    &::after {
      content: "";
      position: absolute;
      left: 0;
      right: 0;
      height: 2px;
      bottom: -1px;
      background-color: #3399ff;
    }
  }
}
</style>

<template>
  <div class="app-tabs">
    <div class="tab-buttons" style="display: flex; height: 44px; border-bottom: 1px solid #DCDEE2;">
      <button
        v-for="tab in tabs"
        v-bind:key="tab"
        v-bind:class="['tab-button', { active: currentTab === tab }]"
        v-on:click="currentTab = tab"
        class="pure"
        style="width: 33.333333%; background: transparent; position: relative;"
      >{{ tab }}</button>
    </div>

    <div class="tab-content">
      <slot v-for="tab in tabs" :name="tab" :currentTab="currentTab"></slot>
    </div>
  </div>
</template>
```

https://m.vip.com/