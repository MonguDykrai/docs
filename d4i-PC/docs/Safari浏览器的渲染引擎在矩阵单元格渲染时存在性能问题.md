# Safari浏览器的渲染引擎在矩阵单元格渲染时存在性能问题

解决方案：

```css
.ele {
  transform: translateZ(0),
  backface-visibility: hidden;
}
```

https://www.infoq.cn/article/d43fu-Guo5a8EJWZSHTP