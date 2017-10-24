## GitLab Flow的十一个规则

使用 Git 版本控制，是对使用它之前的所有版本控制方式的一种改进。然而，很多组织最终以太过混乱或过于复杂的流程来结束。这个问题对于刚从其他版本控制系统转过来的组织来说特别突出。

在本文中我们会列出 GitLab 工作流 的11条规则，以帮助简化、整理工作流程。这些规则最主要的益处是(或我们希望是) 它能够简化流程并且产生一个更高效和更清楚的成果。

我们认为总会有可改善的空间，并且每一次改善都是草案。一如既往，每个人都可以做出贡献!反馈和提意见是非常受欢迎的。

**1. 使用功能分支，不直接提交到master**

如果你从 SVN过来，例如，你将习惯于基于trunk的工作流。当使用Git的时候，你应该为你做的任何事情创建一个分支，以便你以merge前的代码评审作为结束。

**2. 测试所有的提交，不仅仅是master上的提交**

一些人设置他们的CI仅仅测试那些被合并到master的提交。这太迟了;对于master总是绿色的测试人们应感到有信心。对人们来说在他们开始开发新功能前不得不测试master是没有意义的，例如，CI不是很昂贵，所以按这种方式做才有意义。

**3. 在所有的提交上运行所有的测试(如果运行测试多于5分钟，并行运行它们)**

如果你工作在一个特性分支并添加新提交,然后在那个分支运行测试。如果测试花费较长时间，试着并行的运行它们。在服务端的合并请求运行所有的测试套件。如果你有一个服务于开发的测试套件，另一个仅仅是对新版本的，那么值得设置并行测试，分别运行它们。

**4. 在合并到master前执行代码评审，而非事后**

不要在一周结束的时候测试所有的东西。 当场做,因为你会更容易抓住可能导致问题的事情，其他人也会努力想出解决方案。

**5. 部署是自动的，基于分支或基线**

如果你不想每次部署master，可以创建一个生产分支。但是这里没有理由为什么你可能使用一个脚本或登录到某个地方手动部署。让一切自动化，或者一个特定的分支触发一次生产部署。

**6. 基线是人为创建，而不是CI创建**

用户创建一个基线，基于那个基线，CI将执行一个操作。你不应该让CI更改代码仓库。如果你需要非常详细的指标，您应该有一个服务器报告列出了新版本。

**7. 依赖tags版本进行发布**

如果你为你的项目生成tag，这表示你发布了一个新版本。

**8.绝不以重置方式提交变更**

如果你将一个项目的变更提交到一个公共的分支上，你不应该使用重置方式(即不应用 git rebase),否则将造成难以追踪你对该项目的改善和相应的测试结果，这样做实际上破坏了他人选择最有利于的版本的依据。

我们有时也违反这条准则，当我们要求一个贡献者使用(git merage --spansh)提交他的修改，以便提供真实的修改历史，忽略他本地不规范的修改历史时。这样做以后查阅修改历史时，容易根据修改历史做版本恢复。但是总而言之 推荐做法为：代码应该纯净，修改历史应该真实。

**9. 每个人都应该从主支开始，并一直以主支为基础**

这意味着你不从任何分支开始。你检出主支内容,然后创建你的特性，提交你的合并请求，下次修改还是以主支为基础。在你合并内容到主枝上时，你应该完成审查，不应该包含其他中间阶段的内容。

**10. 先修改主支中的错误，之后发布分支**

如果你发现一个bug，最差的事是你修改了刚发布的版本，而未修改主支。

避免这种情况发生，你应该总是先修改主枝，之后再发布另外一个版本用来修复已发布版本中的错误。

**11. 提交的信息中反应你修改部分的意图**

你应该不止说明你做了什么，还应该说明你为什么这么做。如果你解释为什么这么做而没有使用其他方式，这将会更有用。





现在讲下针对Gitflow的一些实践：

**master分支**

- 主分支
- 保持稳定
- 不允许直接往这个分支提交代码，只允许往这个分支发起merge request
- 只允许release分支和hotfix分支进行合流

**develop分支**

- 开发分支
- 相对稳定的分支
- 用于日常开发，包括代码优化、功能性开发

**feature分支**

- 特性分支
- 从develop分支拉取，用于下个迭代版本的功能特性开发
- 功能开发完毕合并到develop分支

**release分支**

- 发布分支
- 从develop分支拉取
- 用于回归测试，bug修复
- 发布完成后打tag并合入master和develop

**hotfix分支**

- 热更新分支
- 从develop分支拉取
- 用于紧急修复上线版本的问题
- 修复后打tag并合入master和develop

大家可能会发现我们这个跟标准的Gitflow工作流有些差别，其实也没有什么标准不标准的，前面说到要结合团队的实际情况，我们团队对于目前所采用的工作方式都是达成共识的，所以有一些差异并没有关系。

说了这么久，还没有一句git命令，那就让大家感受一下吧（感谢Bugly小色熊整理）：

1). 首先将远程代码拉取到本地

```bash
    git clone xxx
    git checkout -b develop origin/develop
```

2).新建feature分支

```bash
    git checkout -b feature 1
```

3).多人在feature上开发，如果中途需要将develop的变更合入feature，所有人需要将本地的代码变更提交到远程

```bash
    git fetch origin 
    git rebase origin/feature
    git push origin feature123
```

然后由feature负责人rebase develop分支，删除原来feature分支，重新新建feature分支；

```bash
    git fetch origin
    git rebase origin/feature
    git rebase develop
    git push origin :feature
    git push origin feature
```

这样可以保证feature保持线性变更；

4).feature开发完成后，所有人需要将本地的代码变更提交到远程

```bash
    git fetch origin 
    git rebase origin/feature
    git push origin feature
```

然后由feature负责人rebase develop分支，然后将feature分支合入develop，删除feature；

```bash
    git fetch origin
    git rebase origin/feature
    git rebase develop
    git checkout develop
    git merge feature
    git push origin :feature123456
```

这样可以保证develop保持线性变更，各feature的变更完整可追溯； 
5).合入feature后拉出对应的release/feature分支，后续bug修复在release/feature上

```bash
    git checkout develop
    git checkout -b release/feature
```

release/feature分支的同步合并与feature分支相同 
6).release/feature分支bug修复完成后，拉取对应的tag推送远程进行发布

```bash
    git tag -a v1.0 -m 'feature发布'
    git push origin v1.012
```

之后将release/feature合入develop分支，然后删除

```bash
    git rebase develop
    git checkout develop
    git merge release/feature
    git push origin :release/feature1234
```

7).发布完成后将release合入master分支，保证master为最新稳定版本（实际操作为发起merge request）