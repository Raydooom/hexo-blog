---
title: 'Hexo: 4.主题和常用插件'
date: 2019-01-07 16:17:11
tags:
---

### 主题

创建 Hexo 主题非常容易，您只要在 themes 文件夹内，新增一个任意名称的文件夹，并修改 \_config.yml 内的 theme 设定，即可切换主题。一个主题可能会有以下的结构：

```bash
.
├── _config.yml
├── languages
├── layout
├── scripts
└── source
```

#### \_config.yml

主题的配置文件。修改时会自动更新，无需重启服务器。

#### 下载主题

官方主题地址：[hexo 主题](https://hexo.io/themes/)  
推荐两款主题：

- [Next](https://github.com/theme-next/hexo-theme-next) 精简黑白主题 [具体使用](https://blog.csdn.net/qq_32454537/article/details/79482896)
- [Vexo](https://github.com/theme-next/hexo-theme-next) vue 官网风格主题

```bash
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改站点配置文件\_config.yml

```bash
theme: next
```

### 插件

#### 评论插件

很多主题已经自带有评论插件了，如果想更换或者没有带的可以自己添加上去，目前`gitment`用的比较多，因为可以直接使用 GitHub 账号授权登录， 本站使用的是`valine`，主要  因为`valine`响应速度比较快，也更简洁。这里只介绍一下`valine`的使用  方法：

- [valine 官网](https://valine.js.org)
  > 官网介绍：Valine 诞生于 2017 年 8 月 7 日，是一款基于 Leancloud 的快速、简洁且高效的无后端评论系统。理论上支持但不限于静态博客，目前已有 Hexo、Jekyll、Typecho、Hugo 等博客程序在使用 Valine。
- [Leancloud](https://leancloud.cn)
  > 在这里使用 Leancloud 主要是为了存储数据，因为 hexo 发布以后是纯静态的 html 页面，必须要有存储数据的地方才能保证评论内容不会丢失。

1. 注册 Leancloud 账号，不再赘述。
2. 创建一个新应用，使用开发版即可
   ![创建应用](/images/hexo01.png)
3. 应用创建好以后，进入刚刚创建的应用，选择左下角的设置>应用 Key，然后就能看到你的 APP ID 和 APP Key 了：
   ![获取APP ID 和APP Key](/images/hexo02.png)
   若要在自己的域名下调用，必须把域名加入web安全域名中
   ![设置安全域名](/images/hexo04.jpg)
4. 添加`valine`代码
    ```html
    <head>
    ...
    <script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
    <script src="//unpkg.com/valine/dist/Valine.min.js"></script>
    ...
    </head>
    <body>
    ...
    <div id="vcomments"></div>
    <script>
        new Valine({
        el: "#vcomments",
        appId: "<API_ID>",
        appKey: "<API_Key>"
        });
    </script>
    </body>
    ```
5. 在 hexo 中配置`valine`，在项目根目录或主题目录的`_config.yml`文件中设置
    ```bash
    comment: valine #
    valine:
    appid:  appid
    appkey: appkey
    notify: false # mail notifier , https://github.com/xCss/Valine/wiki
    verify: false # Verification code
    placeholder: ヾﾉ≧∀≦)o来啊，快活啊! # 输入框占位符
    meta: nick,mail,link # 评论者相关属性。
    pageSize: 10 # 评论列表分页，每页条数。
    visitor: true # 文章阅读量统计
    ```

6. Valine 从 `v1.2.0`开始支持文章阅读量统计。
    ```js
    new Valine({
        el:'#vcomments',
        ...
        visitor: true // 阅读量统计
    })
    ```

    > 如果开启了阅读量统计，Valine 会自动检测 leancloud 应用中是否存在 Counter 类，如果不存在会自动创建，无需手动创建~

    Valine 会自动查找页面中 `class` 值为 `leancloud-visitors` 的元素，获取其 `id` 为查询条件（可以使用 js 动态获取当前页面路径来作为 id 属性来确保唯一性）。并将得到的值填充到其 `class` 的值为 `leancloud-visitors-count` 的子元素里：

    ```html
    <!-- id 将作为查询条件 -->
    <span
    id="<Your/Path/Name>"
    class="leancloud-visitors"
    data-flag-title="Your Article Title"
    >
    <em class="post-meta-item-text">阅读量 </em>
    <i class="leancloud-visitors-count">1000000</i>
    </span>
    <script>
    $(function() {
        $(".leancloud-visitors").attr("id", location.pathname); 
        /* valine 浏览量统计设置id*/
    });
    </script>
    ```
7. 数据查看
    ![查看数据](/images/hexo03.jpg)