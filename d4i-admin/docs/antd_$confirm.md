# $confirm

在使用 antd 作为 UI 库的项目中，用 this.$confirm 代替 window.confirm 。

```html
<template>
  <div>
    <button @click="deleteNode">删除节点</button>
    <button @click="deleteEdge">删除线</button>
  </div>
</template>

<script>
  export default {
    name: "App",
    methods: {
      showDeleteConfirm(cb, title) {
        this.$confirm({
          title, // 确认删除线吗？ ...
          content: 'Some descriptions',
          okText: 'Yes',
          okType: 'danger',
          cancelText: 'No',
          onOk() {
            cb(true)
          },
          onCancel() {
            cb(false)
          },
        });
      },
      deleteNode() {
        this.showDeleteConfirm(function (result) {
          if (!result) return

          this.$axios({
            method: "POST",
            url: `delete/node`,
            params: {
              id: "123"
            }
          })
          .then(res => {})
          .catch(error => {})
        }, "确认删除点吗？")
      },
      deleteEdge() {
        this.showDeleteConfirm(function (result) {
          if (!result) return

          this.$axios({
            method: "POST",
            url: `delete/edge`,
            params: {
              id: "321"
            }
          })
          .then(res => {})
          .catch(error => {})
        }, "确认删除线吗？")
      },
    }
  }
</script>
```

https://vue.ant.design/components/modal/#components-modal-demo-confirmation-modal-dialog