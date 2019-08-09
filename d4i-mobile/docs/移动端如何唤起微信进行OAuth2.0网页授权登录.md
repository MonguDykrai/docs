# 移动端如何唤起微信进行OAuth2.0网页授权登录 ( 走不通 / 放弃 )

结论：微信已不支持移动 Web应用 OAuth 授权？ —— 先不做了

```js
// 丽华
window.open('https://open.weixin.qq.com/connect/oauth2/authorize?appid='+appid+'&redirect_uri='+path+'&response_type=code&scope=snsapi_base&state=STATE#wechat_redirect')

// 掘金
window.open('https://open.weixin.qq.com/connect/oauth2/authorize?appid=XX&redirect_uri=XX%3D&response_type=code&scope=snsapi_login&state=&connect_redirect=1#wechat_redirect')

// 京东
window.open('https://open.weixin.qq.com/sns/explorer_broker?appid=wx2f5d8f9715c59d10&redirect_uri=https%3A%2F%2Fplogin.m.jd.com%2Fcgi-bin%2Fml%2Fwxcallback%3Flsid%3Dnp1tapxzcvm8wgq4c2w8wgi7h03tf212&response_type=code&scope=snsapi_userinfo&state=ws2m050q&connect_redirect=1#wechat_redirect')

// redirect_uri: https://plogin.m.jd.com/cgi-bin/ml/wxcallback?lsid=np1tapxzcvm8wgq4c2w8wgi7h03tf212
```

## PC

```js
const APPID = "wxe3432cd574d1552a";
const SCOPE = "snsapi_login";
const REDIRECT_URI = "https%3A%2F%2Fwww.data4industry.com%2Flogin";
const STATE = "wechat";
const url = `https://open.weixin.qq.com/connect/qrconnect?appid=${APPID}&redirect_uri=${REDIRECT_URI}&response_type=code&scope=${SCOPE}&state=${STATE}#wechat_redirect`;

// https://open.weixin.qq.com/connect/qrconnect?appid=wxe3432cd574d1552a&redirect_uri=https%3A%2F%2Fwww.data4industry.com%2Flogin&response_type=code&scope=snsapi_login&state=wechat#wechat_redirect

// https://www.data4industry.com/login
```

- https://juejin.im/post/5bf8f7095188257c5237b477
- https://my.oschina.net/u/2617082/blog/1592521
- https://www.jianshu.com/p/0a5dc38daa95