---
title: 随笔-1
published: 2026-06-14
updated: 2026-06-16
tags: [Essay,Tools,EdgeOne,CI/CD]
category: Essay
draft: false 
description: EdgeOne 的尝试,顺便整理下Edge的书签
version: 1.0.4
---

# EdgeOne CI/CD
1. 注册EdgeOne的Makers
2. 从Github引用项目
3. 构建与自动部署
4. 配置SSL
>[!tip] 目前有个怪问题,Edge访问会提示不安全,其他浏览器一切正常(次日已正常,疑似dns缓存?)


# EdgeOne 边缘加速-1
1. Claude Code 修改agens ai 生图技能
2. 利用生图和编程技能创建主站
3. 创建[test](https://test.19930618.xyz/)极简网站测试边缘加速(双SSL证书,加速侧强制https,服务器端let's Entry 自动续签同强制https)
4. 测试成功,上传并启动[主站](https://www.19930618.xyz/)加速

>[!tip] 1.0.4的时候遇到了奇奇怪怪的bug,将1panel反代后的网站加入EdgeOne后,出现了上传无权限但是能删除能新增

# EdgeOne 边缘加速-2
>[!IMPORTANT] 删除所有1panel相关操作,并关闭服务器黑白名单(测试时高频访问导致黑名单)
1. 创建1panel静态站
2. 1panel静态站开启https并测试是否联通
3. 1panel静态站开启反代
4. 1panel静态站测试是否已指向代理地址
5. EdgeOne添加加速
6. EdgeOne配置https
7. 测试加速后网站是否可以正常访问
8. 开启WAF修改拦截规则拉黑30分钟
    1. 10秒50次url
    2. 60秒10次拦截
    3. 10秒15次404


# 书签整理
1. 娱乐
2. 学习
3. 工作
4. 其他

>[!tip] 后面再看要不要保存到博客吧目前还是用的Edge同步
