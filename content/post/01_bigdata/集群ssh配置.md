---
title: "企业级大数据实战之路(3)---集群SSH配置"
date: 2018-04-04T16:16:12+08:00
draft: false
share: false
tags: ["ssh","linux"]
image: "/images/集群SSH配置/0.jpg"
---

```
本文档旨在为集群间的root用户建立ssh互信,其他用户均可通用本方法.
```

##### 配置hadoop01免密登录hadoop02:
1. 先要删除hadoop01节点root用户目录下的.ssh文件
```bash
[root@hadoop01 ~]# rm -rf  ~/.ssh/
```

2. 生成hadoop01的公钥与私钥
```bash
[root@hadoop01 ~]# ssh-keygen -t rsa
```
遇到确认,点击回车均可,最后结果如下:
![1](/images/集群SSH配置/1.png)

3. 将公钥发送至hadoop02
```bash
[root@hadoop01 ~]# ssh-copy-id -i ~/.ssh/id_rsa.pub hadoop02
```
输入hadoop02的密码,点击回车.此时,hadoop01可以免密登录hadoop02,结果如下:
![2](/images/集群SSH配置/2.png)
 
4. 验证是否成功
```bash
[root@hadoop01 ~]# ssh hadoop02
```
成功:
![3](/images/集群SSH配置/3.png)

至此,hadoop01免密登录hadoop02成功.

##### 配置Hadoop01免密登录其他节点:
hadoop01免密登录其他主机方法,重复执行上述操作即可,最后可实现hadoop01免密登录所有节点;

##### 配置所有节点双向免密登录:
Hadoop02-hadoop14免密登录其他主机方法也同上;




