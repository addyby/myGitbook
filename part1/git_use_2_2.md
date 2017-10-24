### 2.2.2. 跟踪新文件

------

使用命令 `git add` 开始跟踪一个文件。所以，要跟踪 README 文件，运行：

```bash
$ git add README
```

此时再运行 git status 命令，会看到 README 文件已被跟踪，并处于暂存状态：

```bash
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        new file:   README
```

只要在 Changes to be committed 这行下面的，就说明是已暂存状态。

如果此时提交，那么该文件此时此刻的版本将被留存在历史记录中。你可能会想起之前我们使用 `git init` 后就运行了 `git add (files)` 命令，开始跟踪当前目录下的文件。`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。