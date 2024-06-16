---
layout: post
title: "C2H5OH的振动模式与振动频率"
date:   2024-1-4
tags: [VASP]
comments: true
author: Zhangxx
---

开始乙醇（C2H5OH）振动模式与振动频率的学习啦，接下来直接进入正题！

<!-- more -->

乙醇分子的振动模式与振动频率计算分为两个部分，即结构优化和振动频率计算。

由于乙醇为单独的一个分子，因此乙醇分子的KPOINTS如下所示。

### KPOINTS
- C2H5OH
- 0
- G
- 1 1 1
- 0 0 0

## 结构优化

当获取带乙醇的POSCAR时，首先要进行结构优化，因此将INCAR、POSCAR、POTCAR和KPOINTS放在同一个文件夹中（opt），并打开INCAR进行设置。

### INCAR
- SYSTEM = C2H5OH
- PREC = Accurate \# 精度级别：Normal或Accurate，进行结构晶格弛豫计算时设置Accurate
- ISMEAR = 0
- SIGMA = 0.01
- NELM = 100
- NELMIN = 2
- NSW = 200
- IBRION = 2
- EDIFF = 1E-5
- EDIFFG = -0.01

将上述INCAR进行保存，运行vasp_std，得到结构优化的乙醇分子。

## 振动频率计算

复制opt文件并命名新的文件夹（vmf），删除POSCAR并将CONTCAR重命名POSCAR，同时对INCAR进行修改。

### INCAR

- SYSTEM = C2H5OH
- PREC = Accurate
- ISMEAR = 0
- SIGMA = 0.01
- NSW = 1
- NFREE = 2 \# 该参数决定了每个原子在xyz方向的位移次数，当NFREE = 2时，说明每个原子沿着xyz产生一个正位移和负位移，即一个原子6次位移。
- POTIM = 0.02
- IBRION = 5
- EDIFF = 1E-6

将上述INCAR进行保存，运行vasp_std，得到乙醇分子的振动模式和振动频率。通过使用grem cm-1 OUTCAR可以查看计算的频率信息。

可以通过Jmol————原子库选择器————Frequencies查看对应振动频率。

---
#### 最后，你认为有什么哪里需要修改，或者你认为有什么更好的idea，欢迎通过邮箱联系我！
