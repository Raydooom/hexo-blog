title: 'hexo: 1.使用 Hexo 搭建博客'
author: John Doe
tags: [hexo,起步]
categories: []
date: 2019-01-07 14:24:00
---

#### 什么是 Hexo？

> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 安装

#### 基础环境

在安装 Hexo 前，必须确保已安装以下程序：

- [Node.js](https://nodejs.org/en/)
- [Git](https://git-scm.com/)

然后便可以使用 npm 来安装 Hexo 构建工具

```bash
 npm install -g hexo-cli
```

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

#### 项目结构

新建完成后，指定文件夹的目录如下：

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

##### \_config.yml

网站的配置信息。

##### scaffolds

模版文件夹。当新建文章时，Hexo 会根据 scaffold 来建立文件。

Hexo 的模板是指在新建的 markdown 文件中默认填充的内容。例如，如果您修改 scaffold/post.md 中的 Front-matter 内容，那么每次新建一篇文章时都会包含这个修改。

##### source

资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

##### themes

主题 文件夹。Hexo 会根据主题来生成静态页面。
