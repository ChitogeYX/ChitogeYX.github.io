---
title: GitHub Pages 对自定义域名支持 HTTPS
date: 2018-05-04 13:44:35
categories: GitHub
tags: GitHub
---
![](https://rin-1253361658.file.myqcloud.com/github.png)
<!-- more -->
GitHub Pages Blog 原文：[Custom domains on GitHub Pages gain support for HTTPS](https://blog.github.com/2018-05-01-github-pages-custom-domains-https/)

在 2018-05-01，GitHub Pages 官方发布了上面的一篇 Blog，告知我们 GitHub Pages 对自定义域名支持 了 HTTPS ，下面针对此新特性来做个简单的说明并提供详细的开启操作流程。

## 操作流程
关于如何在 Github Pages 上搭建一个博客，这里不再赘述，网上的教程比较多，此次仅对开启自定义域名支持 HTTPS 这一特性来进行说明。

本文以项目 ` https://github.com/ChitogeYX/ChitogeYX.github.io ` 和域名 ` yxrin.com ` 为例。

操作流程：
1. 域名解析
2. GitHub Pages 项目设置
    1. 添加 CNAME 文件
    2. 配置自定义域名

### 域名解析
开启 Github Pages 之后，会有一个默认的二级域名作为访问地址，一般是和项目同名，比如我的这个项目的默认二级域名访问地址是 ` http://chitogeyx.github.io  ` 。知道这个之后，我们对域名进行解析操作：

我们添加一条 CNAME 解析：

| 主机记录（Host）|记录类型（Type）|记录值（Values）
|-| :- | :-: 
|@|CNAME|` chitogeyx.github.io `
|www|CNAME|` chitogeyx.github.io `

上面提供了2个例子，第一个是你想使用 ` yxrin.com ` 来访问你的博客，第二个就是 ` xxx.yxrin.com ` 来访问，这里要和 GitHub Pages 项目设置 里的 CNAME 文件的内容要对应，后面会说。

解析生效后，可以尝试访问来查看是否解析成功，直接访问 ` http://yxrin.com ` ，如果是 Github Pages 的 404 界面，说明解析成功了。
### Github Pages 项目配置
大家可以参考 我的项目 ，它的根目录里有个 ` CNAME ` 文件，文件的内容是和上面的域名解析对应的。

即如果使用 `@` 值 `CNAME` 到 `chitogeyx.github.io`，则文件的内容为 `yxrin.com` ;

如果使用 `xxx` 任意值 `CNAME` 到 `chitogeyx.github.io`，则文件的内容应为 `xxx.yxrin.com` 。

添加完成后，项目根目录有了此文件，下面去项目的 settings 看一下。

在 GitHub Pages 选项卡下能看到：
```
Your site is published at http://yxrin.com/
Custom domain
Custom domains allow you to serve your site from a domain other than chitogeyx.github.io. Learn more.
yxrin.com
```
正常情况下是这样了，你勾选 `enforce HTTPS` 开启强制跳转到 HTTPS 即可，相应的Github Pages 的内容会变成：
```
Your site is published at https://yxrin.com/
```
那么如果如果之前已经开启了自定义域名，`enforce HTTPS` 无法勾选且怎么办？

按照官方提示，进行如下操作：
1. 把 Custom domain 中的值清空，并点击 `Save` 进行保存；
2. 在 Custom domain 中的填入之前清空的值，我这里是 `yxrin.com` ，填入后点击保存；
3. 尝试在浏览器里主动访问 https://yxrin.com ，地址要根据自己的情况，注意协议类型是 https，正确情况下是能正常访问的；
4. 刷新项目设置页，如果 enforce HTTPS 可勾选，勾选即可；
5. 如果 `enforce HTTPS` 不可勾选，并且提示 `Not yet available for your site because the certificate has not finished being issued”` ，说明证书尚未申请完成，等待一天即可。

注意，如果使用 Chrome 访问 https://yxrin.com 地址栏左侧仍未出现小绿锁，请检查自己的网站引用的资源文件有没有使用了 http 协议，请替换成相应的 https 资源。