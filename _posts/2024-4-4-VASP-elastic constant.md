---
layout: post
title: "材料的弹性性能计算"
date:   2024-2-14
tags: [VASP]
comments: true
author: Zhangxx
---

开始弹性常数（Elastic constant）的学习啦，接下来直接进入正题！

<!-- more -->


**弹性常数计算可以用来预测材料合理的晶体模型**

在弹性常数计算中，布里渊区选择Monkhorst-Pack方案，例如体心立方晶体结构（BCC），采用的KPOINTS如下：

### KPOINTS

- NAME
- 0
- M
- 4 4 4
- 0 0 0


弹性性能的INCAR设置如下：

### INCAR

- \# Global Parameters 
- ISTART = 1
- LREAL = Auto
- LWAVE = F
- LCHARG = F
- ADDGRID = T
- PREC = Low

- \# elastic constant calculation
- IBRION = 6
- NFREFF = 2
- POTIM = 0.015
- ISIF = 3
- NSW = 1   \# 一般情况下，适当增加NSW值可以使体系更加趋近于平衡。

将上述的INCAR、POSCAR、POTCAR和KPOINTS放置在同一个文件夹中（ecc），运行vasp_std。

在ecc文件夹中找到OUTCAR，搜索关键词SYMMETRIZED ELASTIC MODULI获得弹性常数矩阵，再通过各类弹性常数计算公式，计算出C11，C12，C44，C11-C12，C11+2C12，G/GPa，B，E/GPa，B/G，G/B，V，C12-C44，Az，AVR等。

---
#### 最后，你认为有什么哪里需要修改，或者你认为有什么更好的idea，欢迎通过邮箱联系我！
