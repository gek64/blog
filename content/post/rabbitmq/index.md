---
title: RabbitMQ 学习
description: 消息队列中间件
date: 2022-08-01
slug: rabbitmq
image: 
categories:
    - technology
tags:
    - 中间件

---

## 开场
原来就听说过RabbitMQ，自己的做的项目中其实也几次碰到了这个东西，但因为是用的框架已经配置好的东西，就从来就没细致的去了解这到底是一个什么东西，和这个东西起到什么作用。

直到脑抽的同事搞坏了开发用的那一台小小的英伟达牌子的"迷你"服务器，整个项目陷入到了不断重试连接 RabbitMQ，卡组所有人的进度的情况。

不得已，我只能自己来研究一下这个大名鼎鼎的消息队列中间件了，2022年了我软件开发配的电脑价格上限是5k，这个价格我也只能用windows和linux内核的系统了，所以这篇文章主要是针对这两个系统上的 RabbitMQ 的一些情况来写的。

## 基本信息

### windows 安装参考
- https://www.rabbitmq.com/install-windows-manual.html

1. 安装 [erlang](https://erlang.org/download/otp_versions_tree.html)
2. 在系统环境变量中设置`ERLANG_HOME`,例如`C:\Program Files\Erlang OTP`
3. 解压`rabbitmq-server-windows-*.zip`
4. 运行`sbin/rabbitmq-server.bat`启动服务
5. 使用`sbin/rabbitmqctl.bat`配置


### 用户管理
```sh
# 新建用户
rabbitmqctl add_user Username Password

# 删除用户
rabbitmqctl delete_user Username

# 修改用户的密码
rabbitmqctl change_password Username Newpassword

# 查看用户列表
rabbitmqctl list_users
```

### 用户角色管理
```sh
# 设置用户角色
# UserTags...
# 1.超级管理员(administrator)
# 可登陆管理控制台(启用management plugin的情况下)，可查看所有的信息，并且可以对用户，策略(policy)进行操作
# 2.监控者(monitoring)
# 可登陆管理控制台(启用management plugin的情况下)，同时可以查看rabbitmq节点的相关信息(进程数，内存使用情况，磁盘使用情况等)
# 3.策略制定者(policymaker)
# 可登陆管理控制台(启用management plugin的情况下), 同时可以对policy进行管理。但无法查看节点的相关信息
# 4.普通管理者(management)
# 仅可登陆管理控制台(启用management plugin的情况下)，无法看到节点信息，也无法对策略进行管理。
# 5.其他角色(名称自定义)
# 无法登陆管理控制台，通常就是普通的生产者和消费者。
rabbitmqctl set_user_tags User_Name UserTags...
```

### 用户权限管理
```sh
# 查看(指定hostpath)所有用户的权限信息
rabbitmqctl list_permissions [-p VHostPath]

# 查看指定用户的权限信息
rabbitmqctl list_user_permissions User
```

### 插件管理
```sh
# 启用web网管 http://localhost:15672
rabbitmq-plugins enable rabbitmq_management
```