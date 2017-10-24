## 2.3 版本回退

### 版本回退尽量用git bash命令

> 平时当中gitlab的master分支是protected的 ![输入图片说明](https://static.oschina.net/uploads/img/201709/09145217_bza9.png) 平时这个分支的合并和push并没有问题， 但是，当你回滚到某个版本再push的时候就会报错

```powershell
remote: GitLab: You are  allowed  to  deleted protected branches from this project. 
To http://gitlab.test.com/root/test.git !
 [remote rejected] master (pre-receive hook declined) error: failed to push some refs to 'http://gitlab.test.com/xxxx/xxxx.git'
```

> 这个时候要先把这个分支unproected回滚后再proetected回来

- 新建backup分支 作为备份，以防万一

```shell
git branch backup 
```

- 本地仓库彻底回退到xxxxx版本，xxxxx版本之后的commit信息将丢失

```
git reset --hard xxxxx 

```

- 加入-f参数，强制提交，远程端将强制跟新到reset版本

```
git push -f origin master 

```

## 有jenkins自动同步的服务器的（与gitlab不在同一台服务器的），如果有回滚，则需要

```shell
报错
Your branch is ahead of 'origin/master' by 3 commits.
```

```
 git reset --hard origin/master

```

或者直接在构建的脚那里

```
git pull &&  git reset --hard origin/master

```

\####回滚之后的远程同步（也是触发gitlab来同步）

##### 如果远程是master分支

```shell
cd /home/www/test && git checkout -f master && git pull && git reset --hard origin/master
这样可以
如果
cd /home/www/test && git checkout -f master && git pull origin master && git reset --hard origin/master 
这样则不行
```

##### 如果远程是其他分支（test），则一定要这样

```shell
 cd /home/www/test && git checkout -f test && git pull origin test && git reset --hard origin/test
```

### 所以gitlab与代码运行不在同一台服务器的，包括jenkins触发的代码同步和回滚同步要实行以下两个规则

```shell
master的则一定要这样：
 cd /home/www/test && git checkout -f master && git pull && git reset --hard origin/master
其他分支的比如test分支，则一定要这样：
cd /home/www/test && git checkout -f test && git pull origin test && git reset --hard origin/test
```