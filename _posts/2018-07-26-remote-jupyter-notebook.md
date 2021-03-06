---
layout: post
title: "访问虚拟机中的jupyter notebook"
category: 
tags: ['日常琐事']
description: 
---

# 配置ssh连接虚拟机

1. 确定虚拟机Ubuntu的IP地址

   ```
   ifconfig #例如：查看 inet addr:192.168.0.129
   ```

2. 确定windows能否与虚拟机联通

   ```
   windows下，cmd -->:ping 192.168.0.128
   ```

3. 安装ssh服务

   1. 查看ssh服务是否安装

      ```
      ssh localhost
      ```

   2. 安装ssh服务

      ```
      sudo apt-get install openssh-server
      ```

   3. 输入命令查看状态

      ```
      sudo service ssh status 
      ```

4. 配置xshell,通过ssh连接虚拟机

---

# notebook端口映射

1. 通过anaconda安装notebook

2. 自动生成配置文件

   ```
   jupyter notebook --generate-config
   ```

3. 生成密码

   ```
   from notebook.auth import passwd
   passwd()
   Out[2]: 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
   ```

4. 修改配置文件

   ```
   c.NotebookApp.ip='*'
   c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'     #注意引号前面的u
   c.NotebookApp.open_browser = False
   c.NotebookApp.port =8888 							#可自行指定一个端口, 访问时使用该端口
   ```

5. 通过xshell实现端口映射

   连接>SSH>隧道>添加TCP/IP转移规则
   源主机就填localhost，侦听端口就填宿主机中的端口，

   

   目标主机和端口就填虚拟机的ip和notebook运行的端口。