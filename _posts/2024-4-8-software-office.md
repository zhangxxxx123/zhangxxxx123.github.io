---
layout: post
title: "Office免费安装"
date:   2023-12-4
tags: [software]
comments: true
author: Zhangxx
---

在线免费安装Office，接下来直接进入正题！

<!-- more -->

接下来是Office的安装步骤：

1. 在桌面新建一个文件夹并命名为Office；
2. 下载[Office软件部署工具](https://www.microsoft.com/en-us/download/details.aspx?id=49117)到桌面，双击》》》将部署文件安装在Office中；
3. 打开网页[office 版本自定义工具](https://config.office.com/deploymentsettings)，按照下图的提示设置自定义Office；

![1](https://zhangxxxx123.github.io/images/Office/1.png)
 
![2](https://zhangxxxx123.github.io/images/Office/2.png)

![3](https://zhangxxxx123.github.io/images/Office/3.png)

![4](https://zhangxxxx123.github.io/images/Office/4.png)

![5](https://zhangxxxx123.github.io/images/Office/5.png)

4. 将导出的config.xml文件放进Office文件夹中。
5. 打开Office文件夹。如果你的电脑是win11，直接右击终端CMD；如果你的电脑是win10，复制当前文件夹地址，打开CMD终端，输入“cd 地址”
6. 输入以下命令：
   > setup /download config.xml    #下载Office安装包
   >
   > setup /configure config.xml   #安装office安装包
7. 安装完成后，应该是激活状态了，如果没有激活，那就网上找一个激活工具吧！

