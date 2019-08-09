# 设置顶级域名Cookie

```js
const splitedLocationOrigin = location.origin.split(".");

const lengthOfSplitedLocationOrigin =
  splitedLocationOrigin.length;

const lastButOne =
  splitedLocationOrigin[lengthOfSplitedLocationOrigin - 2]; // 倒数第二 zylliondata
const lastOne =
  splitedLocationOrigin[lengthOfSplitedLocationOrigin - 1]; // 倒数第一 local

const topLevelDomain = ["", lastButOne, lastOne].join("."); // https://www.data4industry.com -> .data4industry.com

const oneDay = 60 * 60 * 24 * 1;

this.$VueCookies.set("token", token, oneDay, null, topLevelDomain);
```