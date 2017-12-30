---
title: 不同设备使用hexo写作的方法
date: 2017-12-30 12:31:24
tags:
- Hexo
- git设置
description: "一个使用github和git实现在不同设备上使用hexo的教程"
---

## 同步的原理

因为hexo本身上传到github上的文件是编译后的文件，所以我们要利用git的同步功能，将hexo文件夹中的文件同步到github上，然后实现在不同设备上使用hexo写作。

## 前期准备

1. 一个github账号
2. git环境
 
这两个设置都十分简单，故此处不再赘述。

## github设置

### 建立新分支

因为我们要先把hexo文件夹中的文件同步到hexo上，而yourname.github.io只有一个分支master，所以我们要新建一个分支（分支名可以随便取）

{% asset_img createdBranch.jpg 建立一个hexo分支 %}

然后进入设置，把新建立的分支设置成默认分支

{%asset_img settingBranch.jpg 设置默认分支 %}

### 导入新设备中的SSH密钥

首先算出新的密钥，使用`ssh-keygen -t rsa -C "your_email@youremail.com"`,一路回车，此过程中提示输入密码，可以选择不输入
- Windows下没有自带SSH，需要手动安装 [Windows下安装SSH](https://www.jianshu.com/p/f8ba3e51d60e)

生成之后，找到`id_rsa.pub`,打开此文件，复制文件中所有内容后去github的设置页添加，找到`Settings` -> 左栏点击 `SSH and GPG Keys` -> 点击` New SSH key` 公钥内容粘贴进“Key”文本域内。 title栏中填一个容易辨别的标题，点击 Add key。添加完毕之后可以测试一下能否正常连接。
```
alex@alex-VirtualBox:~$ ssh -T git@github.com
Hi Anthorty! You've successfully authenticated, but GitHub does not provide shell access.
```
出现此提示说明连接正常。

## 上传hexo文件夹中的文件

打开命令行，切换到hexo文件夹，使用如下git命令
详细方法见 [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
```
git remote add backup git@github.com:yourname/yourname.github.io.git
git add .
git commit -m "description"
git push backup master:hexo
```

等待完成后，在github上的hexo分支下就会出现hexo文件夹中的内容（不包括.gitignore、.npmignore中忽略的内容）

## 新设备中设置

首先搭建好hexo环境 [搭建Hexo环境](https://hexo.io/zh-cn/)
进入准备用作Hexo的文件夹，输入

```
hexo init yourblogname
cd yourblogname
git remote add <远程主机名（可以自己取）> git@github.com:yourname/yourname.github.io.git
git pull <远程主机名> <远程分支名>:<本地分支名>
```

写完之后就可以使用`hexo g -d`将文件部署到github上。

## 收尾工作

在不同环境写完之后，记得使用

```
git add .
git commit -m "description"
git push <远程主机名> <本地分支名>:<远程分支名>
```

以此保持文件一致。








