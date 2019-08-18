---
title: "如何用hugo搭建个人博客"
date: 2019-08-17T22:21:10+08:00
draft: false
---
# 如何用Hugo搭建个人网站
## 下载和安装Hugo
Hugo是用Go语言写的，可以直接下载，不需要额外的依赖。

win64x对应的是hugo_x.xx.x_Windows-64bit.zip，下载后创建安装目录，例如D:\Hugo，之下建两个子目录bin和Sites，然后解压，例如解压到D:\Hugo\bin，把解压的hugo_x.xx.x_windows_amd64.exe文件重命名为hugo.exe，然后加到环境变量Path里，方便在命令行里使用。

添加成功后打开cmd或者PowerShell，运行命令hugo version，如果安装成功，会输出Hugo Static Site Generator vx.xx.x 

## 搭建个人网站
首先要确定自己要搭建什么网站，我要建的是托管到Github的用户网站，按照Github Pages规则，网站名应该是<username.github.io>，所以我第一步创建网站用以下命令：
```
cd D:\Hugo\Sites
hugo new site brent-li.github.io
```
之后在Site目录下多了一个brent-li.github.io文件夹，进入文件夹可以看到目录结构如下：

```
|-- archetypes
|-- config.toml
|-- content
|-- data
|-- layouts
|-- static
```
archetypes目录里可以放一些原型，用于hugo新建内容的配置属性。config.toml是网站的配置属性文件。content文件夹里放你网站的内容，例如你发布的博客文章。data目录是Hugo使用的配置文件存放的地方。layout目录存放布局内容。static目录存放静态资源如图片、css等。

接下来我们先在content里放点东西。命令如下：
```
cd xxx.github.io
hugo new post/开博大吉.md
```
Hugo会在content目录下创建post目录，在post目录下创建开博大吉.md文件。之后打开md文件，里面已经有些内容
```
---
title: "开博大吉"
date: 2019-08-13T14:49:45+08:00
draft: true
---
```
---包起来的内容是TOML配置信息，叫作扉页(front matter)，默认这3项，可以再添加一些，其中draft是true时Hugo不会真正发布它，要发布时改成false。修改后的扉页如下：
```
---
date = "2017-02-08T22:07:46+08:00"
title = "Scala学习笔记之模式匹配"
draft = false
tags = ["scala","pattern matching","模式匹配"]
share = true
---
```
然后再把我的博客内容复制进md文件，一篇博客完成了。
## 本地测试
Hugo自带服务器，可以用命令行启动：
```
hugo server -D 
```
服务器启动后访问http://localhost:1313访问网站，发现问题可以及时修改。
## 发布到github
本地测试网站没有问题后，就可以准备发布了。执行以下命令

hugo -t casper
Hugo将编译所有文件并输出到public目录，你需要在github上创建repository，名字就是<你的用户名>.github.io，创建完后，返回你本地命令行，进入public目录，执行以下命令：
```
git init
git add .
git commit -v
<!-- 这条在github上创建新文件时直接复制 -->
git remote add origin git@github.com:xxx.github.io.git
git push -u origin master
```
稍等片刻后，打开<你的用户名>.github.io网址，就可以看到你的个人网站了。

