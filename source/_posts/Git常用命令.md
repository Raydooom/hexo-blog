title: Git 常用命令
author: John Doe
date: 2019-01-07 14:36:14
tags: [git 命令]

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

### 查看

```bash
# vi模式查看git配置
$ vi ./git/config
# 输入:q退出
```

查看 git 项目地址

```bash
$ git config -l
# 结果
credential.helper=osxkeychain
core.excludesfile=/Users/raydom/.gitignore_global
difftool.sourcetree.cmd=opendiff "$LOCAL" "$REMOTE"
difftool.sourcetree.path=
mergetool.sourcetree.cmd=/Users/raydom/Applications/Sourcetree.app/Contents/Resources/opendiff-w.sh "$LOCAL" "$REMOTE" -ancestor "$BASE" -merge "$MERGED"
mergetool.sourcetree.trustexitcode=true
user.name= ''#全局的
user.email= ''#全局的
commit.template=/Users/raydom/.stCommitMsg
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/Raydooom/hexo-blog.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
user.email=raydom007@163.com
branch.master.remote=origin
branch.master.merge=refs/heads/master
```
