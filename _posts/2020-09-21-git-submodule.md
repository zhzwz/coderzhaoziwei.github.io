---
title: Git Submodule 的简单使用
description: 使用 Git 的子模块功能，可以把大型项目拆分为多个子模块，每个子模块的版本管理都是独立的。
tags: ["git"]
---

## 添加子模块

```sh
git submodule add $MODULE_URL $MODULE_PATH
```

默认情况下，子模块会将子项目放到一个与仓库同名的目录中，本例中是 “DbConnector”。 如果你想要放到其他地方，那么可以在命令结尾添加一个不同的路径。

## 使用子模块

```sh
git submodule init
git submodule update
# 或
git submodule update --init --recursive
```

## 删除子模块

```sh
rm -rf $MODULE_PATH
rm .git/module/$MODULE_NAME
git rm --cached $MODULE_NAME
```

最后记得手动删除 `.gitmodules` 和 `.git/config` 中与子模块相关内容。
