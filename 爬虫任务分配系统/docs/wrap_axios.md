# wrap axios

```js
// utility.js
const utility = {
  request(options, handlers) {
    const { success, failure } = handlers;

    axios(options)
      .then(res => {
        success.call(this, res);
      })
      .catch(error => {
        failure.call(this, error);
      });
  },
};

export default utility;
```

```html
<template>

</template>

<script>
export default {
  name: "App",
  data() {
    return {
      request: this.$utils.request.bind(this),
    };
  },
  methods: {
    getUserInfo() {
      this.request(
        {
          method: "GET",
          url: `/dsg/api/v1/user_info`,
        },
        {
          success(res) {
            console.log(res);
          },
          failure(error) {
            console.log(error);
          },
        }
      );
    },
  },
  mounted() {
    this.getUserInfo();
  }
};
</script>
```