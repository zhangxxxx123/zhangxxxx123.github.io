---
layout: post
title: "Band和Dos的计算过程（持续更新中）"
date:   2024-4-4
tags: [VASP]
comments: true
author: Zhangxx
---

开始能带和态密度的学习啦，接下来直接进入正题！

<!-- more -->

想要准确的计算能带和态密度，大致上要经历以下三个过程。
## 结构优化
**获得最稳定的结构，该过程包括了电子和离子的弛豫**

关于VASP计算，其中最重要的就是INCAR设置啦，以下是我的结构优化设置。

### INCAR
- #Global  parameter
- SYSTEM = BST
- ISTART = 0
- ISPIN  = 1 
- ICHARG = 2
- LWAVE = T 
- LCHARG = T 
- LVTOT = F 
- LELF = F 
- ENCUT = 600 
- LORBIT = 11
- #Electronic Relaxation
- ISMEAR = 0
- SIGMA = 0.05
- NELM = 300
- NELMIN = 6
- EDIFF = 1E-06
- #Ionic Relaxation
- NSW = 200
- IBRION = 2
- ISIF = 3
- EDIFFG = -1E-03
- #HSE06
- #LHFCALC   = .TRUE.
- #HFSCREEN  = 0.2 
- #PRECFOCK  = Fast
 
将上述的INCAR文件与POSCAR、POTCAR和KPOINTS共同放进一个文件夹（opt），运行vasp_std，等待运行完成即可。

## 静态计算（自洽计算）
**在优化结构的基础上，继续对电子进行自洽计算**

将优化结构后的opt文件复制一份并命名复制文件夹（scf）。

打开scf文件夹，将POSCAR删除并将CONTCAR重命名POSCAR。

打开INCAR并修改。

### INCAR
- #Global  parameter
- SYSTEM = BST
- ISTART = 1
- ISPIN  = 1 
- ICHARG = 1
- LWAVE = T 
- LCHARG = T 
- LVTOT = F 
- LELF = F 
- ENCUT = 600 
- LORBIT = 11
- #Electronic Relaxation
- ISMEAR = 0
- SIGMA = 0.05
- NELM = 300
- NELMIN = 6
- EDIFF = 1E-06
- #Ionic Relaxation
- NSW = 0
- IBRION = -1
- ISIF = 3
- EDIFFG = -1E-03
- #HSE06
- #LHFCALC   = .TRUE.
- #HFSCREEN  = 0.2 
- #PRECFOCK  = Fast

保存INCAR，运行vasp_std。计算结束后可以通过VESTA查看CHGCAR中的电荷密度分布。

## 能带计算（非自洽计算）

将自洽计算后的scf文件复制一份并命名复制文件夹（band）。

由于进行能带计算时，需要获得更为密集的高对称性的K点，因此需要借助工具（[vaspkit](https://vaspkit.com)）。

vaspkit获取能带数据操作流程：vaspkit ————— 303 ———— 产生KPATH.in ———— 删除KPOINTS并将KPATH.in命名为KPOINTS。

直接运行vasp——std。计算结束后，使用vaspkit————211————生成band.dat————接下来开始你的画图表演。

## 态密度计算（非自洽计算）

将自洽计算后的scf文件复制一份并命名复制文件夹（dos）。

打开INCAR并修改。

### INCAR
- #Global  parameter
- SYSTEM = BST
- ISTART = 1
- ISPIN  = 1 
- ICHARG = 11
- LWAVE = T 
- LCHARG = T 
- LVTOT = F 
- LELF = F 
- ENCUT = 600 
- LORBIT = 11
- #Electronic Relaxation
- ISMEAR = 0
- SIGMA = 0.05
- NELM = 300
- NELMIN = 6
- EDIFF = 1E-06
- #Ionic Relaxation
- NSW = 0
- IBRION = -1
- ISIF = 3
- EDIFFG = -1E-03
- #DOS
- NEDOS = 3000
- #HSE06
- #LHFCALC   = .TRUE.
- #HFSCREEN  = 0.2 
- #PRECFOCK  = Fast

保存INCAR，运行vasp_std。计算完成后，使用vaspkit画态密度图。

vaspkit获取态密度数据操作流程：关于DOS数据获取的功能，在vaspkit ———— 11都可以获取（例如：vaspkit ————— 111 ———— 产生TDOS.dat），剩下的就看你的画图水平喽。
