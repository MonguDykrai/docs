# DraggableListItem双向绑定v-model

```html
<!-- DraggableListItem.vue -->
<template>
  <draggable :value="value" @input="$emit('input', $event)">
    <ul>
      <li v-for="item in value" :key="item.no">
        {{ item.name }}
      </li>
    </ul>
  </draggable>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "DraggableListItem",
  components: {
    draggable,
  },
  props: {
    value: {
      type: Array,
      required: true,
    }
  }
}
</script>
```

```html
<!-- DraggableLists.vue -->
<template>
  <div class="draggable-lists">
    <draggable-list-item :value="items5" @input="items5 = $event">和 v-model 等价</draggable-list-item>
    <draggable-list-item v-model="items4"></draggable-list-item>
  </div>
</template>

<script>
import DraggableListItem from "./DraggableListItem";

export default {
  name: "DraggableLists",
  components: {
    DraggableListItem,
  },
  data() {
    return {
      items5: [{ no: 0, name: "display" }],
      items4: [{ no: 1, name: "display" }],
    }
  }
}
</script>
```