---
title: Homebrew 安装过程记录
description: Homebrew 实在是 macOS 安装软件的一大利器，用过了就再也丢不掉。
tags: ["homebrew"]
---

## 前言

在备份了重要资料之后，我抹盘安装了苹果的新一代操作系统 `macOS Big Sur 11.1`，于是才有了这篇记录重新安装 `Homebrew 2.7.3` 的过程。

目前我对于 `Big Sur` 的体验还算良好，只遇到了一些小问题。比如在某些情况下，无法切换至搜狗输入法进行中文输入。建议追求系统环境稳定、不愿意折腾的朋友，对于系统的更新可以再等一等。

*CoderZhao 2021-01-16*

- [Homebrew Homepage](https://brew.sh)
- [Homebrew 官网（简体中文）](https://brew.sh/index_zh-cn)

> 补充：无法切换至搜狗输入法进行中文输入的情况，重启之后就正常了。除了不再能运行 32 位的程序，后续使用没有再遇到其他问题。

## 简介

Homebrew 官网的自我介绍是：macOS（或 Linux）缺失的软件包的管理器，我认为这句话名副其实。使用 Homebrew 在 macOS 中可以快速安装各种软件包或应用程序，而且操作非常简单。

例如，运行命令 `brew install node` 可以安装 `node.js`，运行命令 `brew install wechat` 可以安装微信，运行命令 `brew uninstall wechat` 可以卸载微信。软件包的运行依赖 Homebrew 也会自动安装，所有文件将安装到指定目录（默认 `/usr/local/Homebrew`）。


## 安装

### 安装失败

根据官网介绍，安装 Homebrew 只需要将以下命令粘贴至终端运行即可。

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

由于网络问题，国内用户通常会安装失败。

```md
curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused
```

连接被拒绝，无法连接到 `raw.githubusercontent.com` 的 443 端口。

### 添加 DNS 解析

我直接在浏览器地址栏粘贴 `https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh`，发现仍然无法连接，可能是国内网络环境存在 DNS 污染，可以尝试手动添加解析。

想要手动添加解析，就需要知道真实的 IP 地址。访问 https://www.ipaddress.com 可以查询到 `raw.githubusercontent.com` 的 IP 地址，我的查询结果如下。

| Domain              | githubusercontent.com |
| :------------------ | :-------------------- |
| IP Address          | 199.232.96.133        |
| Web Server Location | United States         |

这里我查询到的 IP 地址是 `199.232.96.133`，不同地区不同时间查询到的结果可能不一致，请以实际查询结果为准。

下面这条命令会在 `hosts` 文件末尾加上一行 `199.232.96.133 raw.githubusercontent.com`，由于修改的是系统只读文件，需要输入用户密码。

```zsh
sudo /bin/zsh -c "echo '199.232.96.133 raw.githubusercontent.com' >> /etc/hosts"
```

`hosts` 文件修改之后，我的浏览器就可以直接访问 `raw.githubusercontent.com` 了，直接执行官网的指令也不会直接提示连接失败了，但是安装速度仍然极慢，还时不时中断导致失败。

### 使用国内镜像

为了加速安装，我使用了中科大（USTC）的镜像资源，详细说明可以查阅[中国科学技术大学镜像资源帮助文档](http://mirrors.ustc.edu.cn/help)。

- Homebrew 源代码仓库替换为 USTC 镜像：

```zsh
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```

- Homebrew 预编译二进制软件包替换为 USTC 镜像：（`.zshrc` 是 zsh 的配置文件，bash 请自行查看文档）

```zsh
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

- Homebrew 核心软件仓库替换为 USTC 镜像：

```zsh
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-core
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

- Homebrew cask 软件仓库替换为 USTC 镜像：

```zsh
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```

> Homebrew 主目录 `$(brew --repo)` 的具体路径在我这里是 `/usr/local/Homebrew`，如果遇到子目录不存在导致 `cd` 命令失败的情况，可以先手动创建 `/usr/local/Homebrew/Library/Taps/homebrew` 再创建两个子目录 `homebrew-core` 和 `homebrew-cask`。


## 常用指令

| 指令                     | 说明     |
| :----------------------- | :------- |
| brew search {AppName}    | 搜索软件 |
| brew info {AppName}      | 查看软件 |
| brew install {AppName}   | 安装软件 |
| brew upgrade {AppName}   | 更新软件 |
| brew uninstall {AppName} | 卸载软件 |
| brew update              | 更新全部 |
| brew list                | 显示全部 |
| brew help                | 帮助信息 |


## 常用软件

保存为文件 `install.sh`，需要运行命令 `zsh install.sh`。

```sh
brew install node               # node.js
brew install yarn
brew install ffmpeg
brew install you-get            # 下载工具（需要 ffmpeg 前置）

brew install visual-studio-code # 编辑器
brew install clashx             # 网络代理
brew install github             # github-desktop
brew install tinypng4mac        # 图片压缩
brew install qq                 # 腾讯
brew install wechat             # 微信
brew install the-unarchiver     # 压缩解压
brew install caffeine           # 屏幕常亮
brew install motrix             # 下载器 Motrix

brew install microsoft-edge     # edge
# 安装 edge 之后，脚本会自动安装 microsoft-auto-update，需要用户手动输入密码。

brew install sogouinput         # 搜狗输入法
# 脚本下载搜狗输入法程序的安装包之后，需要用户手动安装，文件路径是 `/usr/local/Caskroom/sogouinput`。
```


## 结语

类似这种由于网络问题而导致变得复杂的操作流程，最简单的解决办法其实是使用网络代理。但是网络代理的使用不适合所有的用户，于是就要使用到相应的国内镜像资源。

我记得几年前第一次安装 Homebrew 的时候，官方的安装命令是使用的 `Ruby`，现在（2021）已经改为了 `Bash`。如果现在还是参考一些过时的文章，很可能看了反而一头雾水，所以遇到问题一定要查询最新的信息。
