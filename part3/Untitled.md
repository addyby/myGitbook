## 维护命令

```
查看状态
sudo gitlab-ctl status
123
```

## 启停

```
# 启动Gitlab所有组件
sudo gitlab-ctl start

# 停止Gitlab所有组件
sudo gitlab-ctl stop

# 重启Gitlab所有组件
sudo gitlab-ctl restart
12345678910
```

## 备份

### 备份配置

配置文件再/etc/gitlab/ 下面，将所有的配置用tar备份即可

```
[root@localhost init.d]# cd /etc/gitlab/
[root@localhost gitlab]# ls
gitlab.rb  gitlab-secrets.json  trusted-certs
1234
```

### 备份data （以包安装的方式）

```
[root@localhost ~]# sudo gitlab-rake gitlab:backup:create
Dumping database ... 
Dumping PostgreSQL database gitlabhq_production ... [DONE]
done
Dumping repositories ...
 * root/test1 ... [DONE]
 * root/test1.wiki ...  [SKIPPED]
done
Dumping uploads ... 
done
Dumping builds ... 
done
Dumping artifacts ... 
done
Dumping pages ... 
done
Dumping lfs objects ... 
done
Dumping container registry images ... 
[DISABLED]
Creating backup archive: 1490183942_2017_03_22_gitlab_backup.tar ... done
Uploading backup archive to remote storage  ... skipped
Deleting tmp directories ... done
done
done
done
done
done
done
done
Deleting old backups ... skipping
[root@localhost ~]# ls -lrt
总用量 288
-rw-r--r--. 1 root root  279608 11月 14 2014 rlwrap-0.42.tar.gz
-rw-------. 1 root root    1886 1月  17 2016 initial-setup-ks.cfg
-rw-------. 1 root root    1608 1月  18 2016 anaconda-ks.cfg
drwxr-xr-x. 2 root root       6 1月  30 2016 桌面
drwxr-xr-x. 2 root root       6 1月  30 2016 下载
drwxr-xr-x. 2 root root       6 1月  30 2016 模板
drwxr-xr-x. 2 root root       6 1月  30 2016 音乐
drwxr-xr-x. 2 root root       6 1月  30 2016 文档
drwxr-xr-x. 2 root root       6 1月  30 2016 图片
drwxr-xr-x. 2 root root       6 1月  30 2016 视频
drwxr-xr-x. 2 root root      34 9月  23 15:21 公共
drwxr-xr-x. 8 yang users   4096 9月  23 16:12 rlwrap-0.42
[root@localhost ~]# find / -name "1490183942_2017_03_22_gitlab_backup.tar"
find: ‘/proc/23513’: 没有那个文件或目录
/var/opt/gitlab/backups/1490183942_2017_03_22_gitlab_backup.tar

1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950
```

## 恢复数据 （针对以包安装的方式）

```
[root@localhost ~]# sudo gitlab-ctl stop unicorn
[root@localhost ~]# sudo gitlab-ctl stop sidekiq
[root@localhost ~]# sudo gitlab-ctl status
[root@localhost ~]# sudo gitlab-rake gitlab:backup:restore BACKUP=1490183942_2017_03_22
```



## 修改Gitlab默认配置

修改文件为  /etc/gitlab/gitlab.rb  

在修改了之后一定要重新执行

`sudo` `gitlab-ctl reconfigure  `

配置文件才能生效

``

## 查看gitlab状态

## Gitlab的启动，停止与重启

\# Start all GitLab components

\# Stop all GitLab components

\# Restart all GitLab components

## GitLab使用gitlab-ctl日志查看的方法

**Gitlab 默认的日志文件存放在/var/log/gitlab 目录下**

\# 查看所有日志

\# 查看nginx 访问日志

\# 查看 postgresql 日志





**1) 远程仓库相关命令**

检出仓库：$ **git** clone **git**://github.com/jquery/jquery.**git**

查看远程仓库：$ **git** remote -v

添加远程仓库：$ **git** remote add [name] [url]

删除远程仓库：$ **git** remote rm [name]

修改远程仓库：$ **git** remote set-url --**push**[name][newUrl]

拉取远程仓库：$ **git** pull [remoteName] [localBranchName]

推送远程仓库：$ **git push** [remoteName] [localBranchName]

 

**2）分支(branch)操作相关命令**

查看本地分支：$ **git** branch

查看远程分支：$ **git** branch -r

创建本地分支：$ **git** branch [name] ----注意新分支创建后不会自动切换为当前分支

切换分支：$ **git** checkout [name]

创建新分支并立即切换到新分支：$ **git** checkout -b [name]

删除分支：$ **git** branch -d [name] ---- -d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项

合并分支：$ **git** merge [name] ----将名称为[name]的分支与当前分支合并

创建远程分支(本地分支**push**到远程)：$ **git push** origin [name]

删除远程分支：$ **git push** origin :heads/[name]

我从master分支创建了一个issue5560分支，做了一些修改后，使用**git push** origin master提交，但是显示的结果却是'Everything up-to-date'，发生问题的原因是**git push** origin master 在没有track远程分支的本地分支中默认提交的master分支，因为master分支默认指向了origin master 分支，这里要使用**git push** origin issue5560：master 就可以把issue5560推送到远程的master分支了。

git push

git push

git push

**3）版本(tag)操作相关命令**

查看版本：$ **git** tag

创建版本：$ **git** tag [name]

删除版本：$ **git** tag -d [name]

查看远程版本：$ **git** tag -r

创建远程版本(本地版本**push**到远程)：$ **git push** origin [name]

删除远程版本：$ **git push** origin :refs/tags/[name]

 

**4) 子模块(submodule)相关操作命令**

添加子模块：$ **git** submodule add [url] [path]

如：$ **git** submodule add **git**://github.com/soberh/ui-libs.**git** src/main/webapp/ui-libs

初始化子模块：$ **git** submodule init ----只在首次检出仓库时运行一次就行

更新子模块：$ **git** submodule update ----每次更新或切换分支后都需要运行一下

删除子模块：（分4步走哦）

1)$ **git** rm --cached [path]

2) 编辑“.gitmodules”文件，将子模块的相关配置节点删除掉

3) 编辑“.**git**/config”文件，将子模块的相关配置节点删除掉

4) 手动删除子模块残留的目录

 

**5）忽略一些文件、文件夹不提交**

在仓库根目录下创建名称为“.gitignore”的文件，写入不需要的文件夹名或文件，每个元素占一行即可，如

target

bin

*.db

 

git pull origin master



### 创建新用户。

a)      ![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145148855-1930703230.png)

 

b)      ![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145201293-70587537.png)

 

c)      因为还没有密码，所以还得重新在edit一次，设立密码。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145215246-2126383699.png)

 

d)       

e)      ![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145251714-2125733505.png)

 

### 建立新的小组。并添加小组成员。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145306261-1564342696.png)

 

### 建立新的工程。并关联小组

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145312339-1951428556.png)

 

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145318964-825788731.png)

 

### 创建master、release分支，并增添保护。

因为git是基于指针，所以必须先要创建一个最基础文件，所以需要通过先add a file 来创建一个Readme 文件，来创建 master分支。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145326293-695005190.png)

 

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145333918-1763016468.png)

 

添加保护。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145342058-64396991.png)![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145350605-1512243939.png)

 

 

![img]()

### 代码审核

​                     ![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145415261-224642646.png)

 

### 同意分支合并请求。增添标签。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145423699-961084501.png)

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145433761-510103114.png)

 

![img]()

### 分支版本回退。

根据history找到要回退版本的版本号。

![img](http://images2017.cnblogs.com/blog/1191833/201708/1191833-20170824145449043-1729805846.png)

 

取消对master的保护。（参见4）

在本地客户端，根据版本号reset。（无需写全）

git reset --hard 2131

Push 提交修改。

git push -f -u origin master

重启对master的保护。

 