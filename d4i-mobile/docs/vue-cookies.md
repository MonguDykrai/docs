# vue-cookies

## 设置顶级域名Cookie

```js
const splitedLocationOrigin = location.origin.split(".");

const lengthOfSplitedLocationOrigin = splitedLocationOrigin.length;

const lastButOne = splitedLocationOrigin[lengthOfSplitedLocationOrigin - 2]; // 倒数第二 zylliondata
const lastOne = splitedLocationOrigin[lengthOfSplitedLocationOrigin - 1]; // 倒数第一 local

const topLevelDomain = ["", lastButOne, lastOne].join("."); // https://www.data4industry.com -> .data4industry.com

const time = 60 * 60 * 24 * 1;

// const time = 30; // s

const token = "123456";

this.$VueCookies.set("token", token, time, null, topLevelDomain);

console.log(this.$VueCookies.get("token"));

console.log(this.$VueCookies.remove("token", "/", ".data4industry.com"));
```

## 设置 cookie

```js
// cookie 默认有效时间 1 天
this.$VueCookies.set("token", token, time, null, topLevelDomain);

// session 级别的 cookie
this.$VueCookies.set("token", "123", 0); // 过期时间设置为 0 即可
```

## 获取 cookie

```js
console.log(this.$VueCookies.get("token"));
```

## 移除 cookie

```js
console.log(this.$VueCookies.remove("token", "/", ".data4industry.com"));
```

https://www.npmjs.com/package/vue-cookies

## decodeURIComponent

```js
decodeURIComponent('https%3A%2F%2Fm.data4industry.com%2F%23%2Findex%2Fhome') // "https://m.data4industry.com/#/index/home"
```