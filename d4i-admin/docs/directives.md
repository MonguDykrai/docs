

```js
   //全局directive的写法
   // 提交以后禁用按钮一段时间，防止重复提交
   import Vue from 'vue';
   Vue.directive('noMoreClick', {
     inserted(el, binding) {
       el.addEventListener('click', e => {
         el.classList.add('is-disabled');
         el.disabled = true;
         setTimeout(() => {
           el.disabled = false;
           el.classList.remove('is-disabled');
         }, 3000)
       })
     }
   });
```

```js
//局部directive的写法
directives:{
      noMoreClick: {
        inserted(el, binding) {
          el.addEventListener('click', () => {
            el.classList.add('is-disabled');
            el.disabled = true;
            setTimeout(() => {
              el.disabled = false;
              el.classList.remove('is-disabled');
            }, 2000)
          })
        }
      }
    }

```

地址：

- [directivesAPI](https://www.cnblogs.com/lalalagq/p/9960383.html)
