## 2.5 系统维护命令

```
查看状态
sudo gitlab-ctl status

```

## 启停

```
# 启动Gitlab所有组件
sudo gitlab-ctl start

# 停止Gitlab所有组件
sudo gitlab-ctl stop

# 重启Gitlab所有组件
sudo gitlab-ctl restart

```

## 备份

### 备份配置

配置文件再/etc/gitlab/ 下面，将所有的配置用tar备份即可

```
[root@localhost init.d]# cd /etc/gitlab/
[root@localhost gitlab]# ls
gitlab.rb  gitlab-secrets.json  trusted-certs

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

/var/opt/gitlab/backups/1490183942_2017_03_22_gitlab_backup.tar

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
