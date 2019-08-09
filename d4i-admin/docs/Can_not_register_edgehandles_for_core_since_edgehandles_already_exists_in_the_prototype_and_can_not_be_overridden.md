# Can not register `edgehandles` for `core` since `edgehandles` already exists in the prototype and can not be overridden

```js
preConfig() {
  //register panzoom extension
  if (typeof cytoscape('core', 'panzoom') !== 'function') {
    panzoom(cytoscape, $);
  }
  // register edgehandles extension
  if (typeof cytoscape('core', 'edgehandles') !== 'function') {
    edgehandles(cytoscape, $);
  }
  // register navigator extension
  if (typeof cytoscape('core', 'navigator') !== 'function') {
    navigator(cytoscape, $);
  }
}
```

https://github.com/cytoscape/cytoscape.js-panzoom/issues/19