# login.vue

```vue
<template>
  <div style="position: fixed; top: 0; left: 0; right: 0; bottom: 0; font-weight: 700;">
    <div
      style="width: 100%; height: 100px; line-height: 100px; color: #000; text-align: center;"
    >正在登陆...</div>
  </div>
</template>

<script>
import request from "@/assets/js/request/index.js";
const { LOGIN, STATUS_CODE } = request;

export default {
  name: "Login",
  layout: "WechatDefaults",
  mounted() {
    // console.log(this.$VueCookies.get("redirect_uri"));

    const CODE = this.$nuxt.$route.query.code;

    const params = {
      code: CODE,
      state: "wechat"
    };

    LOGIN.WECHAT_LOGIN(params, this.$axios)
      .then(res => {
        if (res.status == STATUS_CODE.SUCCESS) {
          // console.log(res);

          if (this.$VueCookies.get("redirect_uri")) {
            this.$VueCookies.set(
              "token",
              res.data,
              120,
              null,
              ".data4industry.com"
            );

            location.href = decodeURIComponent(
              this.$VueCookies.get("redirect_uri")
            );
          } else {
            window.opener.callbackFn({ thirdPartyLoginRes: res.data });
            window.close();
          }
        }
      })
      .catch(error => {
        if (this.$util.isBadRequest.call(this, error)) return;

        this.$Message.error(this.$util.matchErrorResponseStatus(error));
      });
  }
};
</script>

<style lang="scss">
</style>

```