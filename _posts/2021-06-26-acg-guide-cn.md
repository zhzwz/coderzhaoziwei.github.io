---
title: Jekyll Theme ACG 主题使用指南
description: 介绍如何从零开始配置 Jekyll Theme ACG 主题。
categories: ["Jekyll Theme ACG"]
tags: ["中文指南"]
---

## 简介

- 示例：[jekyll-theme-acg-demo](https://github.com/coderzhaoziwei/jekyll-theme-acg-demo)
- 预览：[在线预览](https://coderzhaoziwei.github.io/jekyll-theme-acg-demo)


## 使用方法

- 在 `Gemfile` 文件中添加 `jekyll-theme-acg` 插件：

```
gem "jekyll-theme-acg"
```

- 在 `_config.yml` 文件中配置主题名称：

```
theme: jekyll-theme-acg
```

- 在根目录必须存在 `index.html` 文件，其他的扩展名都不可以。

```
---
layout: home
---
```

- 在 `_posts` 文件夹中随意放一些 `.md` 格式的文章，文章的标题建议使用 `title` 属性来设置。

```
---
title: 文章的标题
---
```

- 开始本地运行。

```
bundle update && bundle exec jekyll serve -o
```

## 全局配置

配置文件 `_config.yml` 中的默认属性，如下。

```yml
# 主题名称
theme: jekyll-theme-acg
# 主题属性
acg:
  categories: Categories  # 分类显示名称
  tags: Tags              # 标签显示名称
  about: About            # 关于显示名称
  error: Page Not Found.  # 错误 404 页面的描述
  github: coderzhaoziwei  # Github ID

# 站点标题
title: Jekyll Theme ACG

# title:
#   home: Jekyll Theme ACG # 你的站点标题
#   categories: Categories
#   tags: Tags
#   about: About
# 站点作者
author: Coder Zhao
# 站点描述
description: An awesome theme for Jekyll.
# 站点语言
# 默认值：en-US
lang: en-US

# 主题颜色
# 默认值：red
# 可选值：red, blue, pink, green, yellow, purple
color: red

# 主题背景图片
background: https://cdn.jsdelivr.net/gh/coderzhaoziwei/jekyll-theme-acg/assets/images/bg.png

# 站点域名
# 默认为空，一般情况下不需要配置。
# 举例：https://coderzhaoziwei.github.io
url:

# 站点路径
# 默认为空，只有当站点路径是域名下的子路径时，才必须要设置。
# 举例：示例站点 https://coderzhaoziwei.github.io/jekyll-theme-acg-demo 的站点路径是域名下的子路径，只有设置了 `baseurl: jekyll-theme-acg-demo` 才可以正常使用。
baseurl:

# 首页展示的单页文章数量
paginate: 10
```

## 文章配置

每篇文章都必须在开头使用 YAML 格式的 Front Matter，Front Matter 会使文件被 Jekyll 识别为特殊文件，Front Matter 的内容将会被绑定为这篇文章的独有属性。

### title

文章的标题。

如果没有手动设置 title 值，那么 Jekyll 将会使用文件名生成一个 title 值。例如这篇文章的文件名是 `2021-06-01-show-rendering-cn.md`，自动生成的标题为 `Show Rendering Cn`，通常应该避免这种情况。

### description

文章的简述。

如果没有手动设置 description 的值，那么 Jekyll 将会自动提取文章的开头生成一个 description 值。

### categories

文章的分类。

如果一篇文章有多个分类，分类名称之间使用空格分割。

### tags

文章的标签。

如果一篇文章有多个标签，标签名称之间使用空格分割。

### author

文章的作者。

如果没有手动设置 author 的值，那么 Jekyll 将会读取配置文件 `_config.yml` 中的 author 值。

### color

文章的主题色。

如果没有手动设置 color 的值，那么 Jekyll 将会读取配置文件 `_config.yml` 中的 color 值。

### background

文章背景图片。

如果没有手动设置 background 的值，那么 Jekyll 将会读取配置文件 `_config.yml` 中的 background 值。

### pin

文章置顶选项。

如果没有手动设置 pin 的值，那么本篇文章就不会在首页置顶。
