---
title: Scss 与 CSS 语法冲突的解决办法
tags: ["css", "scss"]
---

- CSS 中的 [min()](https://developer.mozilla.org/docs/Web/CSS/min()) 方法允许从逗号分隔符表达式中选择一个最小值作为 CSS 的属性值。

```css
body {
  width: min(100%, 1024px);
}
```

- 然而，上面的这种写法在 Scss 中会报错：`Internal Error: Incompatible units: 'px' and '%'.`，这是因为 Scss 调用了自身的 `min()` 方法对其中的值进行比较。

- 由于CSS 的语法方面对大小写不敏感，而 Scss 则对大小写敏感，所以遇到这种情况可以使用大写的 `MIN()` 来规避 Scss 调用方法。

```css
body {
  width: MIN(100%, 1024px);
}
```

- 参考资料：https://stackoverflow.com/questions/66764596/scss-min-with-both-px-and-percentage-units
