# URLSearchParams

```js
const params = { fruits: ["apple", "orange"], prices: [20, 4]};
const searchParams = new URLSearchParams();

Object.keys(params).forEach(key => {
  params[key].forEach(value => {
    searchParams.append(key, value);
  });
});

console.log(searchParams.toString()); // fruits=apple&fruits=orange&prices=20&prices=4
```

https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams