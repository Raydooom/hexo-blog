title: 'Hexo: 2.基本命令'
date: 2019-01-07 15:10:58
tags: [hexo,命令]
---

### 基本命令

#### init

```bash
$ hexo init [folder]
```

新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

#### new

```bash
$ hexo new [layout] <title>
```

新建一篇文章。如果没有设置 layout 的话，默认使用 `\_config.yml` 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

#### generate

```bash
$ hexo generate
$ hexo g # 缩写
```

生成静态文件。

| 选项 | 描述                            |
| ---- | ------------------------------- |
| -d,  | --deploy 文件生成后立即部署网站 |
| -w,  | --watch 监视文件变动            |

#### publish

```bash
$ hexo publish [layout] <filename>
```

发布

#### server

```bash
$ hexo server
```

启动服务器。默认情况下，访问网址为： http://localhost:4000/

| 选项 | 描述                                 |
| ---- | ------------------------------------ |
| -p,  | --port 重设端口                      |
| -s,  | --static 只使用静态文件              |
| -l,  | --log 启动日记记录，使用覆盖记录格式 |

#### deploy

```bash
$ hexo deploy
```

部署网站。

| 参数 | 描述                                |
| ---- | ----------------------------------- |
| -g,  | --generate 部署之前预先生成静态文件 |

#### clean

```bash
$ hexo clean
```

清除缓存文件 (db.json) 和已生成的静态文件 (public)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。
