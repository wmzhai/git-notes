# 基于GitFLow的分支策略及版本控制

使用[Vincent Driessen分支模型](http://nvie.com/posts/a-successful-git-branching-model/)进行团队协作的工作方法。


##1. Vincent Driessen分支模型

该模型如下图所示，描述了一种经过实践的分支策略和软件发布管理方法

![](http://nvie.com/img/git-model@2x.png)


##2. 主分支

Git里面存在两个平行的主分支

- master ： 一个始终处于`production-ready`状态的主分支
- develop ： 面向下一个`release`的最新开发状态分支，各种自动`nightly builds`在这里执行。

当`develop`分支里的内容达到一个可以稳定发布版本的时候，所有点改动都会被合并到master分支，然后形成一个特定的版本号。

![](http://nvie.com/img/main-branches@2x.png)


##3. 其他分支

团队成员使用一切其他分支来进行并发协作，这些分支生命周期有限，最终将被删除。这些分支都有明确的目的，它们从哪些分支分支出来，最终合并到哪个分支，都有明确的定义。

###3.1 Feature分支

为了开发未来功能的特性分支，当开发一个新特性时，其准备发布的版本可能是未知的。只要特性在开发，这个分支就存在，最终可能会被merge回develop，或者直接被删除。

- 从哪来：develop
- 到哪去：develop
- 命名：除了master, develop, release-*, or hotfix-* 的任何名称

另外，feature分支一般只在开发者个人`repos`里面，并不会被提交到`origin`。


#### 新建Feature分支指令

	$ git flow feature start feature-name

#### 结束Feature分支指令

	$ git flow feature finish feature-name

###3.2 Release分支

Release分支用来准备下一个产品发布分支，这个分支上可以做一些bug修正和版本号标记。而develop分支则可以用于接受下一个大的发布的Feature。从develop里分出release分支的关键时刻是develop分支几乎已经达到新发布版本预期效果的状态时。至少所有面向新发布版本的Feature需要merge回这个develop分支。 而面向再后面版本的Feature最好等release分支出来以后再合并到develop里面。在Release分支切出来以后，是禁止加入大的Feature的，这些Feature只能merge进入develop。

- 从哪来：develop
- 到哪去：develop 或 master
- 命名：release-*

当这个Release分支即将成为下一个正式发布版时，需要做如下工作

1. Release分支合并回master分支
2. 被提交到master上的提交需要添加一个方便未来引用的版本号。
3. 最后在Release分支里面进行的修改需要被合并回develop分支，这样未来的Release包括这些bug修正。


当最终完成分支以后，可以将Release分支删除，因为不再需要他们了。


###3.3 Hotfix分支


- 从哪来：master
- 到哪去：develop 或 master
- 命名：hotfix-*