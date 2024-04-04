---
layout: post
title: "材料平衡晶格常数计算"
date:   2023-12-4
tags: [VASP]
comments: true
author: Zhangxx
---

开始学习通过计算获得最佳的晶格常数啦，接下来直接进入正题！

<!-- more -->


计算平衡的晶格常数其实就是寻找材料晶胞能量最低时的晶格常数。

基本思路：通过构建不同晶格常数的POSCAR进行计算，获取能量最低晶胞的晶格常数。

### INCAR
