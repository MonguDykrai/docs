# FullscreenApi

Edge, Chrome, Firefox 👍

keyCode 122 <=> F11

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
  <script>
    function toggleFullScreen() {
      if (!document.fullscreenElement) {
          document.documentElement.requestFullscreen();
      } else {
        if (document.exitFullscreen) {
          document.exitFullscreen(); 
        }
      }
    }

    document.addEventListener("keypress", function(e) {
      if (e.keyCode === 13) {
        toggleFullScreen();
      }
    }, false);
  </script>
</body>
</html>
```

https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API