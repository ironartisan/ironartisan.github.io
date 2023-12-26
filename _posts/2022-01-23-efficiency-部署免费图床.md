---
layout: post
title: 如何部署免费图床，提高MarkDown写作效率？
categories: 效率
description: 如何部署免费图床，提高MarkDown写作效率？
keywords: MarkDown, PicGo,
---

## 前言

大多数朋友都喜欢用 vscode 工具写 MarkDown ，因为使用起来非常方便，而且还比较轻量化，但是如果想插入大量本地图片的话，会非常耗时，所以需要自己搭建图床，但图床大多数都是收费的，今天就分享下笔者是如何部署免费图床，进行高效写作 MarkDown 的。


## PicGo图床

PicGo 是一个用于快速上传图片并获取图片 URL 链接的工具，简单来说，就是自动把本地图片转换成链接的一款工具。

如果直接复制图片放在文档中，则是生成一个含本地文件路径名的链接，这只能在该文件中看到此图片，如果将文本复制到别的地方就只能显示此路径链接，看不到真实图片，所以需要一个图床工具，将图片放入云端，然后只需要链接就能访问图像；


PicGo 本体支持如下图床：
* 七牛图床 v1.0
* 腾讯云 COS v4\v5 版本 v1.1 & v1.5.0
* 又拍云 v1.2.0
* GitHub v1.5.0
* SM.MS V2 v2.3.0-beta.0
* 阿里云 OSS v1.6.0
* Imgur v1.6.0

可以直接在 Github 上搜索 PicGo，安装对应系统的软件版本。

笔者只介绍如何配置 Github。

首先需要新建一个 Github 仓库，并设置权限公开，用于存储图片；

* 在github首页点击 + new reporsitory
  * Repository name 仓库名：自己建一个仓库
  * Description：添加描述信息
  * Public,将仓库权限勾选为 public, 图片在任何地方都可以显示
  * README文件，是对仓库的描述信息，最好勾上，自己写也可以
  * 然后点击 Create repository
* 创建token
  * 点击 头像，进入 setting 设置界面
  * 在最下面选择 Developer setting
  * 选择Personal access tokens
  * Note 名称：说明这个 token
  * Select scopes: 勾选 repo
  * 点击生成，跳转到生成好的token令牌界面
  * **此处 token 只出现一次，自己保存好，Token的作用是提供一些仓库的权限（比如读、写等），在配 置picgo时需要填入**

配置可参考下图：

![20220123231127-2022-01-23-23-11-28](https://cdn.jsdelivr.net/gh/ironartisan/picRepo/20220123231127-2022-01-23-23-11-28.png)

具体配置手册可参见[PicGo使用文档](https://picgo.github.io/PicGo-Doc/zh/guide/)

软件使用截图如下：

![20220123230444-2022-01-23-23-04-46](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/picgo-2.0.gif)

若访问不了 Github 的朋友可以安装 Gitee 插件，配置 Gitee 仓库，配置步骤与上述内容大概相同。

## vscode中配置PicGo

用过 PicGo 软件的朋友应该都知道，每次都要打开软件上传图片，得到具体链接。有没有更简单的方法呢？

vscode 中提供了 PicGo 插件，只需要在 vscode 中安装 PicGo 插件，简单配置下就能直接在 vscode中直接使用。

在 vscode 扩展商店中搜索 PicGo 进行安装。
![20220124000912-2022-01-24-00-09-13](https://cdn.jsdelivr.net/gh/ironartisan/picRepo/20220124000912-2022-01-24-00-09-13.png)

然后在“文件->首选项->设置”中找到 PicGO 进行配置。

![20220124001311-2022-01-24-00-13-12](https://cdn.jsdelivr.net/gh/ironartisan/picRepo/20220124001311-2022-01-24-00-13-12.png)


软件快捷键

![20220124001823-2022-01-24-00-18-24](https://cdn.jsdelivr.net/gh/ironartisan/picRepo/20220124001823-2022-01-24-00-18-24.png)

对于 windows 系统来说

* 若想选择剪切板的图片。
  >快捷键: Ctrl + Alt + U
执行快捷键后自动上传剪切板内的图片到图床, 并粘贴图片访问地址到当前文本

* 若想选择本次磁盘文件
  > 快捷键: Ctrl + Alt + E
  自动调出本地文件管理器, 手动选择图片, 确定后, 自动上传图片到图床, 并粘贴图片访问地址到当前文本

是不是非常方便呢？

## 加速Github访问

如果是默认配置的话，会直接访问 Github 的链接，因为特殊原因，访问速度确实太慢了，图片经常会出现刷不出来的情况，这种情况要如何解决呢？

可以对 Github 网站进行加速，只需要修改配置中的Custom Url

```
https://cdn.jsdelivr.net/gh/用户名/仓库名
```


![20220124100145-2022-01-24-10-01-46](https://cdn.jsdelivr.net/gh/ironartisan/picRepo/20220124100145-2022-01-24-10-01-46.png)

对于加速 Github 访问的方法可参考[提高国内访问 GitHub 的速度的 10种方法](https://mp.weixin.qq.com/s/5_X3BqBsNFIDyjGhqXPQKw)



