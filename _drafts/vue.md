# Vue 知识点梳理 <!-- omit in toc -->

- [Vue2 实例的生命周期详解](#vue2-实例的生命周期详解)
- [Vue 2 与 3 之间的版本差异](#vue-2-与-3-之间的版本差异)
  - [v-model](#v-model)
  - [v-if 与 v-for 的优先级对比](#v-if-与-v-for-的优先级对比)
  - [v-bind 合并行为](#v-bind-合并行为)

##  Vue2 实例的生命周期详解

![](https://cdn.jsdelivr.net/gh/vuejs/cn.vuejs.org/src/images/lifecycle.png)

- beforeCreate
- created
- beforeMount
- mounted
  - 挂载完成，也就是模板中的 HTML 渲染到 HTML 页面中。此时一般可以做一些 ajax 操作，mounted 只会执行一次。
- beforeUpdate
- updated
- beforeDestroy
- destroyed


## Vue 2 与 3 之间的版本差异

### v-model

### v-if 与 v-for 的优先级对比

- Vue 2 中，在一个元素上同时使用 `v-if` 和 `v-for` 时，`v-for` 会优先作用。
- Vue 3 中，`v-if` 总是优先于 `v-for` 生效。

### v-bind 合并行为
