---
title: "Shimentai - Powered by Hugo&Congo"
date: 2024-09-20T09:42:44Z
draft: false
description: "learn to use static website generator and themes configration"
summary: "Building a simple and elegant personal website with Hugo and Congo."
tags: ["static-site","blog-engine","go","html","css","Hugo","Congo","theme","hugo-theme","emoji"]
categories: ["Expression"]
---


{{<lead>}}
未完待续 ... 
{{</lead>}}



要使用 **Hugo** 和 **Congo Theme** 来建立个人网站，以下是详细的步骤：

### 1. 安装 Hugo

首先需要安装 **Hugo**：

#### 对于 macOS：
```bash
brew install hugo
```

#### 对于 Windows：
你可以使用 **Chocolatey**：
```bash
choco install hugo -confirm
```
或直接从 [Hugo Releases](https://github.com/gohugoio/hugo/releases) 下载并安装。

#### 对于 Linux：
```bash
sudo apt-get install hugo
```

### 2. 创建新站点

在想要放置网站项目的文件夹下，运行以下命令创建一个 Hugo 网站：
```bash
hugo new site website
```
这会在 `website` 文件夹内生成 Hugo 的基本项目结构。

### 3. 下载并安装 Congo 主题

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

### 4. 配置网站

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

### 5. 创建内容

使用 Hugo 命令生成新页面或文章。例如，创建一篇新博客文章：
```bash
hugo new posts/my-first-post.md
```

然后编辑生成的 Markdown 文件 `content/posts/my-first-post.md`，撰写你的内容。

### 6. 本地预览

可以使用 Hugo 的本地服务器功能预览网站。在项目根目录下运行以下命令：
```bash
hugo server
```
然后在浏览器中访问 `http://localhost:1313` 预览网站。

### 7. 部署网站


### 8. 定制 Congo 主题

Congo 提供了高度可定制的布局和样式。你可以通过修改 `themes/congo/layouts` 中的模板文件，或者在 `static/` 目录下添加自定义 CSS 来实现个性化定制。

你可以将你的 logo、博客主题思想（如“创新、表达、反思、挑战”）通过设计和排版展现出来，增强个人风格。

如果你希望在 `Congo` 主题中进一步整合哲学、物理思考的表达方式，可以通过创建自定义内容模板来引导读者从多个维度理解你的想法。

---

这样，你就可以利用 Hugo 和 Congo 主题快速创建并发布个人网站了！如果需要任何细节或定制化帮助，随时可以深入探讨。
