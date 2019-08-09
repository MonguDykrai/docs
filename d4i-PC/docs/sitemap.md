# Sitemap

## Sitemaps XML format

The Sitemap protocol format consists of XML tags. All data values in a Sitemap must be entity-escaped. The file itself must be UTF-8 encoded.

The Sitemap must:
- Begin with an opening <urlset> tag and end with a closing </urlset> tag.
- Specify the namespace (protocol standard) within the <urlset> tag.
- Include a <url> entry for each URL, as a parent XML tag.
- Include a <loc> child entry for each <url> parent tag.

Sample XML Sitemap

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

  <url>

    <loc>http://www.example.com/</loc>

    <lastmod>2005-01-01</lastmod>

    <changefreq>monthly</changefreq>

    <priority>0.8</priority>

  </url>

</urlset> 
```

[sitemaps.org - Protocol](https://www.sitemaps.org/protocol.html)

## 在项目根目录下动态生成 sitemap.xml

### 1. 安装依赖

```bash
# install dependency
$ npm i @nuxtjs/sitemap # Or yarn add @nuxtjs/sitemap
```

### 2. 修改 nuxt.config.js 文件

```js
const axios = require("axios"); // cannot use import

module.exports = {
  modules: [ "@nuxtjs/axios", "@nuxtjs/sitemap" ], // always declare the sitemap module at end of array
  sitemap: {
    gzip: true,
    exclude: [
      "/login",
      "/search-result",
      "/search-result/**",
      "/reset-password/**",
      "/user-center/**",
    ],
    defaults: {
      priority: .5,
      lastmod: "2019-06-12",
      changefreq: "monthly"
    },
    async routes () {
      const getUsersRes = await getUsers();

      if (!getUsersRes) return;

      return [
        {
          url: "/",
          priority: 1,
          lastmod: "2019-06-12",
          changefreq: "monthly",
        },
        ...getUsersRes
      ];

      function getUsers() {
        return new Promise((resolve, reject) => {
          axios({
            method: "GET",
            url: "https://jsonplaceholder.typicode.com/users"
          })
          .then(res => {
            resolve(res.data.map(user => '/users/' + user.username));
          }).catch(err => {
            reject();
          });
        });
      }
    }
  }
}
```

#### 2.1 Configuration

- routes
  - 值类型可以为 Array 或 Function
  - Array / routes: [ { url: "/", priority: 1, lastmod: "2019-06-12", changefreq: "monthly" } ]
  - Function / routes() { return axios({ method: "GET", url: ".../users" }).then(res => res.data.map(user => "/users/" + user.username)) }
- defaults
  - The defaults parameter set the default options for all routes.
- exclude
  - The exclude parameter is an array of glob patterns to exclude static routes from the generated sitemap.

[@nuxtjs/sitemap - npm](https://www.npmjs.com/package/@nuxtjs/sitemap)

### 3. 修改 robots.txt 文件

显示添加 `Sitemap: https://www.data4industry.com/sitemap.xml` 到 robots.txt 文件中

```
User-agent: *
Request-rate: 1/1
Crawl-delay: 60

Disallow: /user-center
Disallow: /user-terms-of-use
Disallow: /user-privacy-protocol
Disallow: /search-result

Sitemap: https://www.data4industry.com/sitemap.xml
```

[Build and submit a sitemap](https://support.google.com/webmasters/answer/183668?hl=en)

### 4. 样例

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

  <url>

    <loc>http://192.168.1.242:3000/</loc>

    <lastmod>2019-06-12</lastmod>

    <changefreq>monthly</changefreq>

    <priority>1.0</priority>

  </url>

  <url>

    <loc>http://192.168.1.242:3000/users/Bret</loc>

    <lastmod>2019-06-12</lastmod>

    <changefreq>monthly</changefreq>

    <priority>0.5</priority>

  </url>
  
  <url>

    <loc>http://192.168.1.242:3000/about</loc>

    <lastmod>2019-06-12</lastmod>

    <changefreq>monthly</changefreq>

    <priority>0.5</priority>

  </url>
  
</urlset>
```