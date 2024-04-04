---
layout: post
title: "INCAR常用参数含义"
date:   2023-10-3
tags: [VASP]
comments: true
author: Zhangxx
---

INCAR文件控制vasp将进行何种性质的计算，我们需设置一些重要参数。而我们日常计算可分为以下几大模块，例如计算类型与输出文件（如电荷以及波函数）、离子实或原子的优化、电子的优化等。

接下来开始认识INCAR中的一些参数！！！

<!-- more -->

## INCAR常用参数含义（持续更新中...）

**\# Global Parameters**

SYSTEM = BT    \# 随便取名

ISTART = 1     \# 有0，1，2。0代表从头开始计算，不读入波函数文件；1代表读入已有波函数，并继续计算，此时新计算的原胞大小和形状可以和已有波函数中的不同，截断能也可以不同;2也代表读入已有波函数，但截断能和原胞都不能改变。

ISPIN  =  1   \# 有1，2。1代表做非磁性计算；2代表做磁性计算；当设置LNONCOLLINEAR = T时（非共线磁结构计算），ISPIN不设置。       

ICHARG =  11  \# 代表是否读入电荷密度。0代表产生初始波函数；1代表读入CHGCAR并同原子密度进行线性插值；2代表构建原子密度；11代表读入自洽的CHGCAR，并进行**能带计算或态密度的非自洽计算**；12代表非自洽的原子密度计算。   

LWAVE  = T \# 是否在WAVECAR写波函数，默认为T。

LCHARG = T \# 是否在CHGCAR和CHG写电荷密度，默认为T。

LVTOT = F \# 是否在LOCPOT中写总的局域势，默认为F。

LELF = F \# 是否在ELFCAR中写电子局域函数，默认为F。

ENCUT = 500 \# 平面波的截面能，为POTCAR中最大值的1.3~1.5倍。

LORBIT = 11 \# 画投影态密度，一般为11。

GGA = PE \# PE为PBE泛函；默认为LDA泛函；如果杂化泛函HSE06，不用设置GGA，添加以下内容：

- LHFCALC = T

- HFSCREEN = 0.2

- PRECFOCK = Fast

**\# Electronic Relaxation**

ISMEAR =  0 

SIGMA  =  0.05 \# 以上两个参数为确定弥散（smearing）的方法和展宽的参数。ISMEAR有-1、0、1、2和-5。-1表示fermi smearing方法；0表示使用Gaussian展宽，一般用于半导体或绝缘体,同时设置展宽大小SIGMA为一个较小的值，如 0.05 eV。ISMEAR=1或者2表示Methfessel-Paxton方法，一般用于金属体系，同时可设置一个较大的SIGMA值，如0.2eV,保证VASP计算的熵一项的值小于1 meV/atom。在半导体和绝缘体中避免使用ISMEAR>0. ISMEAR=-5表示四面体积分，一般适合于高精确的总能量和态密度计算。

NELM =  300 \# 电子自洽最大步数。默认值为60。

NELMIN =  6 \# 电子自洽最小步数。默认值为2

EDIFF = 1E-06 \# 电子自洽的收敛标准。默认值为E-04。

ALGO = Normal \# Normal为blocked Davidson迭代法；very_Fast为RMM-DIIS方法；Fast 为前两者的混合，即前面几步使用IDavidson方法,后面采用RMM-DIIS方法。Conjuggate或All为共轭梯度算法。Exact为严格对角化方法。

**\# Ionic Relaxation**

NSW =  0 \# 离子运动的最大步数，在做**结构优化或者分子动力学中**设置。默认值为0，即离子不动。

IBRION =  -1 \# IBRION=-1，离子不移动;IBRION=0，标准从头算分子动力学;IBRION=1，采用准牛顿（可变度量）算法来结构优化;IBRION=2，采用共轭梯度算法松弛离子;IBRION=3，阻尼分子动力学;IBRION=5、6，确定二阶导数（Hessian矩阵和声子频率）;IBRION=7、8，利用密度泛函微扰理论计算导数，当IBRION = 8时，可进行光学性能分析。

ISIF =  3 \# 决定了是否计算应力以及如何对结构进行优化。ISIF=0表示只计算原子所受的力和原子位置弛豫，其他不优化。当ISIF=1,除了计算ISIF=0中的两相，还追踪原胞的应力，不改变原胞的体积和形状。ISIF=2表示只优化离子位置,不改变原胞的体积和形状; ISIF=3表示同时优化离子位置、原胞形状和体积; ISIF=4表示同时优化离子位置和原胞形状，但保持原胞体积不变; ISIF=5 表示不优化离子位置和原胞体积，只改变原胞形状; ISIF=6表示不优化离子位置,优化原胞形状和体积; ISIF=6 表示不优化离子位置和原胞形状，只优化原胞体积。在结构优化过程中比较常用的是ISIF=2或3。对于**原胞体积变化的计算需要增加平面波截断能**。

EDIFFG = -1E-03 \# 设定结构优化的精度。

ISYM =  0 \# ISYM表示是否打开对称性，ISYM=1,2,3表示打开对称性，ISYM=-1,0,表示关闭对称性。

POTIM = 0.2 \# 为控制离子移动的距离。

**\# DOS**

NEDOS = 1000-3000 \# 默认值为301点

**\# BANDS**

NBANDS = XX \# 表示能带数目，通常不用设置，但在有的计算中，如计算光学性质时，需要手动增加能带数。

**\# Dielectric property**

LEPSILON = T \# 使用密度泛函微扰理论计算静态介电常数、压电张量和玻恩有效电荷。

LOPTICS = T  \# 计算频率依赖的介电函数的实部和虚部。

LPTAD = T

IBRION = 8

EFIELD_PEAD = Ex Ey Ez（eV/Å） \# 对绝缘体加均匀电场。



