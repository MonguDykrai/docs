# async_function_reject的值捕捉不到的处理办法

使用 try ... catch

```js
methods: {
  runCypher() {
    return new Promise((resolve, reject) => {
      this.$axios({
        method: "POST",
        url: `node/rawQuery`,
        data: {
          query: "",
        },
      })
        .then(res => {
          resolve(res);
          console.log(res);
        })
        .catch(error => {
          console.log(error); // 输入参数为空
          this.$message.error(error); // 输入参数为空
          reject(666);
        });
    });
  },
  async confirm() {
    console.log(this.query);

    try {
      const runCypherRes = await this.runCypher();
    } catch (error) {
      console.log(error); // 666
    }
  },
}
```