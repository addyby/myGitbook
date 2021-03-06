---
typora-copy-images-to: images
---

## 1.3 角色和权限

> 一个项目如果需要团队或者多个人共同开发则需要将所有参与人员添加到该项目的成员中，并根据每个人的职责分配不同的角色权限。



首先来了解下，Gitlab系统中的五种角色：

| 角色        | 描述    |
| --------- | ----- |
| Owner     | 项目拥有者 |
| Master    | 主程序员  |
| Developer | 开发人员  |
| Reporter  | 报告者   |
| Guest     | 访客    |



![1508473546566](images/1508473546566.png)

更详细的权限说请参阅[GitLab角色权限](http://10.12.110.122/git/help/user/permissions) 。

一般来说项目的管理者设置为主程序员角色，其具有对受保护的主分支Master更新操作的权限。

其他参与的开发人员设置为开发人员角色，其无法直接对主分支Master进行更新。开发人员需要首先从主分支Master上建立一个新的开发分支，并且所有的开发均在这个新建的分支上进行。完成开发后，需要请求主程序进行合并分支操作，将开发分支的代码合并到主分支Master上。



Gitlab中首先进入你需要操作的项目页面。

![1508474202401](images/1508474202401.png)



点击左侧菜单`设置` ，并选择`成员` 功能。

![1508474327214](images/1508474327214.png)

> 填加项目成员有两种方式：
>
> 用户模式：针对每个用户账号进行角色设置。
>
> 群组模式：针对已存在的群组中所有用户进行角色设置。



### 群组模式

![1508474904897](images/1508474904897.png)

选择群组名称，而后设置`权限级别` ，这样该群组中所有用户将在该项目中具有所设置的角色权限。



![1508475032744](images/1508475032744.png)



### 用户模式

![1508475119807](images/1508475119807.png)

选择要添加的用户并设置角色权限即可。

![1508475165116](images/1508475165116.png)



这样所有添加进来的用户
