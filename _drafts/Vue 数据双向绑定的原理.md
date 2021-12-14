---
title: Vue 数据双向绑定的原理
description:
categories: []
tags: []
lang:
color:
background:
pin:
---

## Vue 的响应式数据

数据双向绑定即MVVM，

## Object.defineProperty

Vue 2 使用 `Object.defineProperty()` 方法重新定义对象的 getter 和 setter 来劫持数据的变动，再使用发布订阅模式将数据变动发送给订阅者（Watcher）。

```javascript
const object = {}
Object.defineProperty(object, "value", {
  set: function(value) {
    this.value = value
    // ...
  },
  get: function() {
    // ...
    return this.value
  },
})
```
