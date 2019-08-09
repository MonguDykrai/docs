# Invalid Host Header

## 问题描述

通过 `http://admin-page.edge.zylliondata.local/#/login` 访问基于 `dev` 分支构建完的项目，报错 `Invalid Host Header` 。

## 解决办法

修改🔨 `vue.config.js` 文件

在 `devServer` 配置项中增加 `disableHostCheck: true`

```js
module.exports = {
  devServer: {
    host: "0.0.0.0",
    port: 8888,
    disableHostCheck: true,
  }
};
```

更安全的做法，指定许可的 `hosts` 列表

```js
module.exports = {
devServer: {
 allowedHosts: [
  'host.com',
  'subdomain.host.com',
  'subdomain2.host.com',
  'host2.com'
   ]
  }
};
```

参考资料：
- [I am getting an invalid host header message when running my react app in a Webpack dev Server](https://stackoverflow.com/questions/43619644/i-am-getting-an-invalid-host-header-message-when-running-my-react-app-in-a-we)
- [How do I disable running an app on the local network when using vue-cli?](https://stackoverflow.com/questions/52829363/how-do-i-disable-running-an-app-on-the-local-network-when-using-vue-cli)