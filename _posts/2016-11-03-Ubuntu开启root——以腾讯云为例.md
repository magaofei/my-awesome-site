---
title: Ubuntu开启root——以腾讯云为例
layout: post
tags: 
- Ubuntu
---

Ubuntu默认没有启用root账户，这有利于安全，但在实际操作中，我们常常需要访问一些需要root权限才可以访问的目录，需要启动root账户

#### 操作步骤

1. 登陆服务器

   ```
   ssh ubuntu@yoursiteIP
   ```

2. 修改root密码

   ```
   sudo passwd root
   ```

3. 修改ssh配置

   ```
   sudo vi /etc/ssh/sshd_config
   ```

   找到  `PermitRootLogin` 这项 将其改为 `yes`

   ![]({{ site.url }}/assets/permitRootLogin.png)

4. 退出并重启ssh服务

   ```
   sudo service ssh restart
   ```

   ​