# move items between lists

`group="ITEMS"` 不同列表给同一个 group 名，即可实现不同列表间的拖拽。

```html
<template>
  <div class="playground" style="display: flex;">
    <div style="width: 25%;">
      <ul>
        <draggable v-model="myList" group="ITEMS">
          <li v-for="item in myList" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
    <div style="width: 25%;">
      <ul>
        <draggable v-model="myList2" group="ITEMS">
          <li v-for="item in myList2" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
    <div style="width: 25%;">
      <ul>
        <draggable v-model="myList3" group="ITEMS">
          <li v-for="item in myList3" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
    <div style="width: 25%;">
      <ul>
        <draggable v-model="myList4" group="ITEMS">
          <li v-for="item in myList4" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "Playground",
  components: {
    draggable,
  },
  data() {
    return {
      items: [
        { no: 1, name: "キャベツ", categoryNo: "1" },
        { no: 5, name: "きゅうり", categoryNo: "1" },
        { no: 9, name: "にんじん", categoryNo: "1" },
        { no: 10, name: "トマト", categoryNo: "1" },
      ],
      items2: [
        { no: 2, name: "ステーキ", categoryNo: "2" },
        { no: 6, name: "ハンバーグ", categoryNo: "2" },
        { no: 11, name: "とんかつ", categoryNo: "2" },
        { no: 12, name: "からあげ", categoryNo: "2" },
      ],
      items3: [
        { no: 3, name: "リンゴ", categoryNo: "3" },
        { no: 7, name: "バナナ", categoryNo: "3" },
        { no: 13, name: "ブドウ", categoryNo: "3" },
        { no: 14, name: "オレンジ", categoryNo: "3" },
      ],
      items4: [
        { no: 4, name: "冷蔵庫", categoryNo: "4" },
        { no: 8, name: "PS4", categoryNo: "4" },
        { no: 15, name: "電子レンジ", categoryNo: "4" },
        { no: 16, name: "Xbox", categoryNo: "4" },
      ],
      newNo: 0,
    };
  },
  computed: {
    myList: {
      get() {
        return this.items;
      },
      set(value) {
        this.items = value;
      },
    },
    myList2: {
      get() {
        return this.items2;
      },
      set(value) {
        this.items2 = value;
      },
    },
    myList3: {
      get() {
        return this.items3;
      },
      set(value) {
        this.items3 = value;
      },
    },
    myList4: {
      get() {
        return this.items4;
      },
      set(value) {
        this.items4 = value;
      },
    },
  },
};
</script>
```

`v-bind="getOptions()"` 还是利用给不同的 list 添加相同的标识来实现相互间可拖拽。

```html
<template>
  <div class="playground" style="display: flex;">
    <div style="width: 50%;">
      <ul>
        <draggable v-model="myList" v-bind="getOptions()>
          <li v-for="item in myList" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
    <div style="width: 50%;">
      <ul>
        <draggable v-model="myList2" v-bind="getOptions()>
          <li v-for="item in myList2" :key="item.no">
            <span class="badge">No.{{item.no}}</span>
            <label>{{item.name}}</label>
          </li>
        </draggable>
      </ul>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "Playground",
  components: {
    draggable,
  },
  methods: {
    getOptions() {
      return { group: "ITEMS" };
    }
  },
  data() {
    return {
      ...
    };
  },
  computed: {
    ...
  },
};
</script>
```

https://github.com/SortableJS/Vue.Draggable/blob/master/documentation/migrate.md#options-props

https://www.npmjs.com/package/vuedraggable

https://codepen.io/kabanoki/pen/PexaOm