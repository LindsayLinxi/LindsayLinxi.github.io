---
title: git的使用
date: 2021-11-17 21:32:31
tags: '工具'
image: /images/theme/git.jpeg
---
### 查看配置
>git config -l
>全局：git config --global --list

### 设置用户名和密码
>git config --global user.name "lindsay"
>git config --global user.email "lindsay@xxx.com"

### 创建新仓库
>执行git init, 来创建新的 git 仓库。

### 检出仓库
创建一个本地仓库的克隆版本：
>git clone /path/to/repository

克隆远程仓库
>git clone username@host:/path/to/repository

### 工作流
你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 工作目录，它持有实际文件；第二个是 缓存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，指向你最近一次提交后的结果。
{% asset_img img_1.jpg This is an example image %}

### 添加与提交
把改动文件添加到缓存区
>git add < filename >
git add *

这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：
>git commit -m "代码提交信息"

现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。

### 推送改动
改动已经在本地仓库的 HEAD 中了。将这些改动提交到远端仓库：
>git push origin master

可以把 master 换成任何分支。
如果还没有克隆现有仓库，需要讲本地仓库连接到某个远程服务器
>git remote add origin < server >

### 分支
分支是用来将特性开发绝缘开来的。创建仓库的时候，master是“默认的”。
在其他分支上进行开发，完成后再将它们合并到主分支上。
{% asset_img img_2.jpg This is an example image %}

创建一个叫做“feature_x”的分支，并切换过去：
>git checkout -b feature_x

切换回主分支：
>git checkout master

再把新建的分支删掉：
>git branch -d feature_x

除非将分支推送到远端仓库，不然该分支就是 不为他人所见的：
>git push origin < branch >

### 更新与合并
更新本地仓库至最新改动，以在你的工作目录中 获取（fetch） 并 合并（merge） 远端的改动。
>git pull

合并其他分支到你的当前分支（例如 master）
>git merge <branch>

***两种情况下，git 都会尝试去自动合并改动。但自动合并并非次次都能成功，并可能导致 冲突（conflicts）。 这时候就需要你修改这些文件来人肉合并这些 冲突（conflicts） 了。***

改完之后，执行命令将它们标记为合并成功：
>git add < filename >
在合并改动之前，也可以使用如下命令查看：
>git diff < source_branch > < target_branch >

### 标签
软件发布时创建标签是个旧有概念，在 SVN 中也有。创建一个叫做 1.0.0 的标签：
> git tag 1.0.0 1b2e1d63ff

1b2e1d63ff 是你想要标记的提交 ID 的前 10 位字符。使用如下命令获取提交 ID：
>git log

你也可以用该提交 ID 的少一些的前几位，只要它是唯一的。


### 替换本地改动
替换掉本地改动，此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到缓存区的改动，以及新文件，都不受影响。
>git checkout -- < filename >

丢弃所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：
>git fetch origin
git reset --hard origin/master

### git提交规范
格式
>type(scope) : subject

( 1 ) type（必须） : commit 的类别，只允许使用下面几个标识：
- feat: 新功能、新特性
- fix: 修改 bug
- perf: 更改代码，以提高性能（在不影响代码内部行为的前提下，对程序性能进行优化）
- refactor: 代码重构（重构，在不影响代码内部行为、功能下的代码修改）
- docs: 文档修改
- style: 代码格式修改, 注意不是 css 修改（例如分号修改）
- test: 测试用例新增、修改
- build: 影响项目构建或依赖项修改
- revert: 恢复上一次提交
- ci: 持续集成相关文件修改
- chore: 其他修改（不在上述类型中的修改）
- release: 发布新版本
- workflow: 工作流相关文件修改

( 2 ) scope（可选） : 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

( 3 ) subject（必须） : commit 的简短描述，不超过50个字符。
- commitizen 是一个撰写合格 Commit message 的工具，遵循 Angular 的提交规范。