---
title: Hexo -d报错
date: 2018-04-19 13:48:45
categories: Hexo
tags: Hexo
---
修改配置文件：根目录下的_config.yml，修改deploy节点。

## 原来的配置为：

``` bash
deploy:
type: git
repo: https://github.com/{yourname}/{yourname}.github.io.git
branch: master
```

## 修改为如下：

``` bash
deploy:
type: git
repo: https://{yourname}:{yourpassword}@github.com/{yourname}/{yourname}.github.io.git
branch: master
```
<!-- more -->

亲测可行。
如果在使用hexo d命令的前提下直接修改.git下面的config文件是无法成功的。原因是：使用该命令之后，会根据_config.yml下面的deploy节点进行cofig文件的覆盖。也就是说，_config.yml如果不做修改，无论如何修改.git下面的配置文件都是无效的，都会被覆盖。