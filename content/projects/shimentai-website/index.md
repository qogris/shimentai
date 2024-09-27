---
title: Shimentai - Powered by Hugo
date: 2024-09-20T09:42:44Z
lastmod: 2024-09-27T09:42:44Z
draft: false
description: learn to use static website generator and themes configration
summary: Building a simple and elegant personal website with Hugo and Congo.
tags:
  - static-website
  - blog-engine
  - go
  - html
  - css
  - Hugo
  - Congo
  - theme
  - hugo-theme
  - emoji
  - shortcode
categories:
  - Expression
  - Project
  - Challenge
authors:
  - haifeng
  - qogris
slug: shimentai-powered-by-hugo
---

| Date | Update | Tags | Status |
|----|----|-----|-----|
| {{ < current-time > }} | 网站内容结构规划 | 规划 | 进行中 |

## 前言

建立网站的初衷在[[我的人生四面体]](/content/posts/about-shimentai)中有过介绍，这里就不再赘述。一时兴起立了flag，就不能再沉浸于漫无边际的思想游戏，而是要真的去学习实践，变身工程师来把它具体落地。从网站框架及开发语言的选取，到控制外观布局及响应方式的样式设置，甚至到一个很小的Icon图标的视觉美化，这里面所涉及的内容之多可想而知，对一个有点追求完美主义的INFP来说，需要投入的精力之大也不难想象:sweat_smile:。不过就像在另一篇[[近期日常]](/content/posts/2024-09-26-近期日常/)文章中提到的，这个过程我本人还是非常乐在其中的。所以在走完这一整套工程实践，基本实现的当初目标之后，我也很愿意将之详细记录下来，因为，输出分享（Outputs）也即是我建立Shimetai这个网站的主要目的:medal_military:

## 准备（可选）

在开始建立网站之前可能会有几项前期工作要首先完成（如选择托管平台，该步骤可能不完全需要），例如网站服务器、网站平台、域名申请等。

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

### 1.网站服务器

考虑是否要托管到自己的VPS还是选择比如WordPress，Github Pages，Cloudflare等这些个人网站托管平台 ...

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

### 2.域名购买

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

### 3.域名解析

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

### 4.证书申请

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

## 建站

### 1.Nginx搭建与配置

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

### 2.Hugo安装与建站

经过调研后，我发现静态网站（static-site）近年来越来越流行，其在性能、安全性、扩展性、维护成本以及开发者体验上有着自身的优势。另外，随着像 Hugo、Jekyll、Gatsby 等静态网站生成器的出现，使得构建静态网站也变得非常方便。静态网站适用于多种应用场景，尤其非常适合**个人博客**、**个人简介**和**作品集**网站等。用户可以通过静态网站生成器快速发布和更新内容，而不需要担心服务器的复杂性。由于博客内容多是固定的，静态网站能提供极快的加载速度，并且易于管理和扩展。

{{< icon "coffee">}}<a class="text-xs">待補充...</a>

使用 **Hugo** 和 **Congo Theme** 来建立个人网站，以下是详细的步骤：

#### （1）安装 Hugo

首先需要安装 **Hugo**：

- 对于 macOS

```bash
brew install hugo
```

- 对于 Windows

你可以使用 **Chocolatey**：

```bash
choco install hugo -confirm
```

或直接从 [Hugo Releases](https://github.com/gohugoio/hugo/releases) 下载并安装。

- 对于 Linux

```bash
sudo apt-get install hugo
```

#### （2）创建新站点

在想要放置网站项目的文件夹下，运行以下命令创建一个 Hugo 网站：

```bash
hugo new site website
```

这会在 `website` 文件夹内生成 Hugo 的基本项目结构。

#### （3）下载并安装 Congo 主题

进入网站目录，并使用 `git` 克隆 Congo 主题：

```bash
cd my-blog
git init
git submodule add https://github.com/jpanther/congo.git themes/congo
```

然后，在站点的 `config.toml` 文件中设置主题：

```toml
theme = "congo"
```

#### （4）配置网站

修改 `config.toml` 文件来配置网站。可以设置标题、描述等基本信息。这里是一个示例：

```toml
baseURL = "https://yourdomain.com"
languageCode = "en-us"
title = "Haifeng's Blog"
theme = "congo"

[params]
  subtitle = "Exploring Innovation, Expression, Reflection, and Challenge"
  dateFormat = "2006-01-02"
```

#### （5）创建内容

使用 Hugo 命令生成新页面或文章。例如，创建一篇新博客文章：

```bash
hugo new posts/my-first-post.md
```

然后编辑生成的 Markdown 文件 `content/posts/my-first-post.md`，撰写你的内容。

#### （6）本地预览

可以使用 Hugo 的本地服务器功能预览网站。在项目根目录下运行以下命令：

```bash
hugo server
```

然后在浏览器中访问 `http://localhost:1313` 预览网站。

#### （7）部署网站

#### （8）定制 Congo 主题

Congo 提供了高度可定制的布局和样式。你可以通过修改 `themes/congo/layouts` 中的模板文件，或者在 `static/` 目录下添加自定义 CSS 来实现个性化定制。

## 运维

### 1.Git

### 2.Visual Studio Code

### 3.Frontmatter

## 工具

在整个网站开发建设过程中，我也学习掌握了很多的建站工具，这里推荐几个我个人非常喜欢的

- [1] Visual Studio Code
- [2] [Canva](https://www.canva.com/)
- [3] Online SVG Editor: [Boxy SVG Editor (boxy-svg.com)](https://boxy-svg.com/)

## 资源

- [1] [Illustrations | unDraw](https://undraw.co/illustrations)
- [2] [SVG Repo - Free SVG Vectors and Icons](https://www.svgrepo.com/)
