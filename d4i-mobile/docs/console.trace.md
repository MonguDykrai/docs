# console.trace

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <script>
      function a() {
        b();
      }
      function b() {
        c();
      }
      function c() {
        console.trace(`trace c`);
        // b();
      }
      function d() {
        a();
      }

      d();
    </script>
  </body>
</html>
```

https://developer.mozilla.org/en-US/docs/Web/API/console/trace