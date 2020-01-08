---
title: Hexo配置Algolia搜索
date: 2018-05-09 14:29:45
categories: Hexo
tags: [Hexo,Algolia]
---
今天给博客添加站内搜索，最后选择使用第三方服务-Algolia,途中也遇到了一些错误。
<!-- more -->
- 在[Algolia官网](https://www.algolia.com/)注册一个账户，完成账户注册后，创建一个Index，如下图：
![](https://rin-1253361658.file.myqcloud.com/algolia_index.png)

- 安装Hexo Algolia扩展， 这个扩展的功能是搜集站点的内容并通过 API 发送给 Algolia。前往站点根目录，执行命令安装：
```
npm install --save hexo-algolia
```

- 在 Algolia 服务站点上找到需要使用的一些配置的值，包括 ApplicationID、Search-Only API Key、 Admin API Key。注意，Admin API Key 需要保密保存。
![](https://rin-1253361658.file.myqcloud.com/algolia_key.png)

- 点击ALL API KEYS 找到对应的key，编辑权限，在弹出框中找到ACL选择勾选Add records, Delete records, List indices, Delete index权限，点击update更新：
![](https://rin-1253361658.file.myqcloud.com/algolia_set.png)

- 编辑站点配置文件，新增以下配置：这些值除了chunkSize不用修改，其他都可从Algolia网站上API Keys获得：
```
algolia:
  applicationID: '你的APPID'
  apiKey: '你的API Key'
  indexName: '你的Index名字'
  chunkSize: 5000
```

- **接着，是最关键，坑最多的一步了。**  <br />
在git bash里面输入以下命令：切记切记要用git bash，因为Windows下无论powershell还是cmd都无法执行export命令。
```
export HEXO_ALGOLIA_INDEXING_KEY=你的API Key
```

- 配置好Key后，在Hexo根目录执行 `hexo algolia` 来更新Index，若出现如下图所示，则表示更新成功：

![](https://rin-1253361658.file.myqcloud.com/hexo_algolia.png)

经过上述的操作后，部署Hexo，便可在博客中添加搜索功能，其效果图如下：
![](https://rin-1253361658.file.myqcloud.com/hexo_sousuo.png)
