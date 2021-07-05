---
title: Commit Message 规范
description: 理论上来说，Commit Message 只要能够清楚地说明本次提交的目的即可，那我们为什么还要统一 Commit Message 的规范呢？
tags: ["git"]
---

## 引子

Git 每次提交代码，都必须写提交说明。

```sh
git commit -m "Commit Message"
```

目前，社区有多种 Commit Message 的写法规范。本文采用目前使用较广的 AngularJS 的提交说明公约。

- [AngularJS](https://github.com/angular/angular.js)
- [AngularJS Git Commit Message Conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y)

## 作用

理论上来说，Commit Message 只要能够清楚地说明本次提交的目的即可，那我们为什么还要统一 Commit Message 的规范呢？

- 可以使用脚本工具生成 `CHANGELOG.md` 变动日志。
- 可以过滤一些不重要的提交记录，便于快速查找信息。

```sh
# 启动查错时
git bisect start [FROM] [TO]
# 显示日志时 仅显示本次发布新增加的功能
git log [RELEASE] HEAD --grep feature
```

- 可以在浏览历史记录时，展示更直观易读的信息。

```sh
# 仅显示指定 tag 的提交记录
git log [TAG] HEAD --pretty=format:%s
```

## 格式

```
<type>(<scope>): <subject>
<空行>
<body>
<空行>
<footer>
```

提交说明包含 `header`，`body`，`footer` 三个部分，其中只有 `header` 部分是必须的，`body` 和 `footer` 是可选的。

为了在 github 或 git 工具中更容易地阅读 commit message ，任何一行 message 都不能超过 100 个字符。

### type

- type 只允许使用下面 7 个标识。

  | Type     |                              |
  | :------- | :--------------------------- |
  | feat     | 功能（增加新的特性）         |
  | fix      | 修复（修复 Bug）             |
  | docs     | 文档                         |
  | style    | 格式（不影响代码运行的变动） |
  | refactor | 重构                         |
  | test     | 测试                         |
  | chore    | 构建（构建过程、辅助工具等） |

- 如果提交说明的 type 是 `feat` 或 `fix`，那么该提交将出现在 CHANGLOG 中。

### scope

- scope 用于指定提交更改的位置。

### subject

subject 描述要求简短，首字母小写，使用第一人称现在时的动词开头，结尾不加 `.`。

| 动词 (Verb) | CN   |
| :---------- | :--- |
| optimize    | 优化 |

### body

Body 部分是对 commit 的详细描述，通常说明代码变动的动机，以及与以前代码的对比，允许多行内容。

### footer

- 如果当前代码与上一个版本不兼容，那么 footer 部分使用 `BREAKING CHANGE:` 开头。后面是对变动的描述、以及变动理由和迁移方法。
- 如果当前 commit 针对某个 issue，那么可以在 footer 部分关闭这个 issue。允许一次关闭多个 issue。

```md
Closes #111, #222, #333
```

## Revert

如果当前 commit 用于撤销以前的 commit，那么必须以 `revert:` 开头，后面跟着被撤销 Commit 的 Header。Body 部分的格式是固定的，必须写成 `This reverts commit <hash>.`，其中的 `<hash>` 是被撤销 commit 的 SHA 标识符。

```
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

如果当前 Commit 与被撤销的 Commit 在同一个 Release 中，那么它们都不会出现在变动日志 CHANGELOG 中。

如果两者在不同的 Release 中，那么当前 Commit 会出现在 CHANGELOG 的 Reverts 小标题下。

## 参考

- [阮一峰](http://www.ruanyifeng.com/)的博客文章：[《Commit message 和 Change log 编写指南》](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
