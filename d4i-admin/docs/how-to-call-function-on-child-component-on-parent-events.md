# how-to-call-function-on-child-component-on-parent-events

```html
<div id="app">
  <child-component ref="childComponent"></child-component>
  <button @click="click">Click</button>  
</div>
```

```js
var ChildComponent = {
  template: '<div>{{value}}</div>',
  data: function () {
    return {
      value: 0
    };
  },
  methods: {
    setValue: function(value) {
        this.value = value;
    }
  }
}

new Vue({
  el: '#app',
  components: {
    'child-component': ChildComponent
  },
  methods: {
    click: function() {
        this.$refs.childComponent.setValue(2.0);
    }
  }
})
```

https://stackoverflow.com/questions/42632711/how-to-call-function-on-child-component-on-parent-events