# 基于GitFLow的分支策略及版本控制

使用[Vincent Driessen分支模型](http://nvie.com/posts/a-successful-git-branching-model/)进行团队协作的工作方法。


## Vincent Driessen分支模型

该模型如下图所示，描述了一种经过实践的分支策略和软件发布管理方法

![](http://nvie.com/img/git-model@2x.png)


## 主分支

Git里面存在两个平行的主分支

- master ： 一个始终处于`production-ready`状态的主分支
- develop ： 面向下一个`release`的最新开发状态分支，各种自动`nightly builds`在这里执行。

当`develop`分支里的内容达到一个可以稳定发布版本的时候，所有点改动都会被合并到master分支，然后形成一个特定的版本号。

![](http://nvie.com/img/main-branches@2x.png)


## 其他分支

团队成员使用一切其他分支来进行并发协作，这些分支生命周期有限，最终将被删除。这些分支都有明确的目的，它们从哪些分支分支出来，最终合并到哪个分支，都有明确的定义。

### Feature分支

为了开发未来功能的特性分支，当开发一个新特性时，其准备发布的版本可能是未知的。只要特性在开发，这个分支就存在，最终可能会被merge回develop，或者直接被删除。

- 可能分支自：develop
- 一定合并会：develop
- 命名规则：除了master, develop, release-*, or hotfix-* 的任何名称




### Release分支



### Hotfix分支


