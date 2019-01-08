title: Git 常用命令
author: John Doe
date: 2019-01-07 14:36:14
tags: [git命令]

---

### 配置

> 用户名和邮箱地址相当于你的身份标识，是本地 Git 客户端的一个变量，不会随着 Git 库而改变。
> 每次 commit 都会用用户名和邮箱纪录。

查看自己的用户名和邮箱地址：

```bash
$ git config user.name
$ git config user.email
```

修改自己的用户名和邮箱地址：

```bash
$ git config (--global) user.name "xxx"
$ git config (--global) user.email "xxx"
```
