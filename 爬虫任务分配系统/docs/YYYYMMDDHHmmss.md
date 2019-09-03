# YYYYMMDDHHmmss

```js
function getReleaseTime(param) {
  const insertPrefixZero = function(value) {
    if (value < 10) {
      return `0${value}`;
    } else {
      return `${value}`;
    }
  };

  var d = new Date(param);
  var YYYY = `${d.getFullYear()}`;
  var MM = insertPrefixZero(d.getMonth() + 1);
  var DD = insertPrefixZero(d.getDate());
  var HH = insertPrefixZero(d.getHours());
  var mm = insertPrefixZero(d.getMinutes());
  var ss = insertPrefixZero(d.getSeconds());

  return `${YYYY}${MM}${DD}${HH}${mm}${ss}`;
}

getReleaseTime(new Date());
```