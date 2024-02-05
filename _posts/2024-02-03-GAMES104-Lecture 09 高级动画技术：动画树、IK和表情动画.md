---
title: GAMES104-Lecture 09 高级动画技术：动画树、IK和表情动画
date: 2024-02-03 16:48:00 +0800
categories: [Computer Graphics, GAMES104]
tags: [图形学, 学习笔记]

pin: false
author: 
    name: CALL1CE
    link: https://space.bilibili.com/9330604
toc: true
comments: true
math: true
mermaid: true

---

## Advanced Animation Technology

### Animation Blend

* LERP：插值，在两种动画（clips）之间插值

[![pFlZntP.jpg](https://s11.ax1x.com/2024/02/03/pFlZntP.jpg)](https://imgse.com/i/pFlZntP)

* 根据两个动画的速度计算权重

* Align Blend Timeline：把两个循环动画的时间归一化再插值

[![pFlZZTI.jpg](https://s11.ax1x.com/2024/02/03/pFlZZTI.jpg)](https://imgse.com/i/pFlZZTI)

#### Blend Space

* 1D Blend Space：Directional Movement
  
  * 多个采样点进行插值

* 2D Blend Space：两个1D正交
  
  * 因为多个动画clips进行blend会比较费，所以选取离当前点最近的三个动画clips，然后使用重心坐标进行插值

[![pFlZV0A.jpg](https://s11.ax1x.com/2024/02/03/pFlZV0A.jpg)](https://imgse.com/i/pFlZV0A)

#### Skeleton Masked Bleding

* 有些动作只会影响上半身或者下半身

* 将两种动画拼在一起

#### Additive Blending

* 在这个动画中，不仅作用到动画的局部，而且只存动画的变化量，而不存绝对量

* 作为修饰

* 但Additive Blending很容易造成不正常的结果

### Animation State Machine(ASM)

* 比如跳跃情况，有三个状态，起跳，空中（jump loop），落地

* ASM Definition

[![pFlZF6e.jpg](https://s11.ax1x.com/2024/02/03/pFlZF6e.jpg)](https://imgse.com/i/pFlZF6e)

[![pFlZilD.jpg](https://s11.ax1x.com/2024/02/03/pFlZilD.jpg)](https://imgse.com/i/pFlZilD)

* Cross Fades：平滑切换、frozen切换

* Cross Fades Curve

* Layered ASM：多层次状态机：角色身体的不同部分做不同的动画状态机

[![pFlZkOH.jpg](https://s11.ax1x.com/2024/02/03/pFlZkOH.jpg)](https://imgse.com/i/pFlZkOH)

#### Animation Blend Tree

* 使用树来做运算

* LERP Blend Node

* Additive Blend Node

* 使用blend tree来计算当前ASM下的一个pose

[![pFlZEmd.jpg](https://s11.ax1x.com/2024/02/03/pFlZEmd.jpg)](https://imgse.com/i/pFlZEmd)

* Blend Tree Control Parameters：node search、named variable、control structure

### Animation Kinematics

#### Inverse Kinematics(IK)

- Forward Kinematics(FK)正向运动学：是在给定所有关节角度的情况下计算链接结构（如一节人体的关节）的末端的空间位置的过程。这个过程比较简单，且是具有唯一解的

- Inverse Kinematics反向运动学： 它是在给定末端的空间位置的前提下，求解关节需要成多少角度。 这个过程就较为困难，一般情况下，逆运动学问题没有解析解，而是会有很多或无限多个解（比如确定一个手的位置，然后反向去算其他joint的位置）

- End-effector：添加到一个骨骼上，使得这个骨骼可以一直在一个期望的位置（比如贴地的效果）

- Two Bones IK：两个骨骼的IK，大腿和小腿作为two bones，问题是会有多个解；解决方式是添加一个reference vector，在这个方向去找解

[![pFlZmkt.jpg](https://s11.ax1x.com/2024/02/03/pFlZmkt.jpg)](https://imgse.com/i/pFlZmkt)

- 多joint的IK很复杂，自由度太高，高维非线性方程很难实时运算、可能有很多解、单一解、无解
  
  * 首先判断能否到达终点
  
  * Constraints of Joints：人形骨骼的运动范围是有一个约束的

[![pFlGuh4.jpg](https://s11.ax1x.com/2024/02/04/pFlGuh4.jpg)](https://imgse.com/i/pFlGuh4)

#### Heuristics Algorithm启发式算法

- CCD(Cyclic Coordinate Decent)：依次固定除了end-effector的每个joint，然后使end-effector变换到最接近target的位置
  
  * Optimized CCD1：对每个joint添加tolerance regions
  
  * Optimized CCD2：越靠近叶节点旋转复度越大，越靠近根节点，旋转复度越小

[![pFlGM9J.jpg](https://s11.ax1x.com/2024/02/04/pFlGM9J.jpg)](https://imgse.com/i/pFlGM9J)

- FABRIK (Forward And Backward Reaching Inverse Kinematics)
  
  * 先强行把end-effector拉到目标点，然后更改骨骼的方向，然后依次修改对应的joint和骨骼直到根节点，这是一次forward
  
  * backward就是再把根节点拉回原来的位置，再做类似上面的操作
  
  * 迭代多次
  
  * 都要设置一个tolerance
  
  * FABRIK with Constraints：为每个joint设置一个可以旋转的角度范围，然后强行拉点的时候呢，不一定拉到target，而是拉到这个角度范围在target平面上投影的一点

#### Multiple End-Effectors

* IK with Multiple End-Effectors：使用上面那个方法会使得骨骼偏来偏去

* Jacobian Matrix：是个逐渐逼近的过程（会在物理那一part详细讲）

#### Other IK Solutions

[![pFlGVBV.jpg](https://s11.ax1x.com/2024/02/04/pFlGVBV.jpg)](https://imgse.com/i/pFlGVBV)

### Animation Pipeline

[![pFlGmAU.jpg](https://s11.ax1x.com/2024/02/04/pFlGmAU.jpg)](https://imgse.com/i/pFlGmAU)

### Facial Animation

[![pFlGnNF.jpg](https://s11.ax1x.com/2024/02/04/pFlGnNF.jpg)](https://imgse.com/i/pFlGnNF)

* Key Pose Blending

* Morph Target Animation：记录下每个部分相对于中性表情的位置，这样就可以自由地组合

[![pFlGEn0.jpg](https://s11.ax1x.com/2024/02/04/pFlGEn0.jpg)](https://imgse.com/i/pFlGEn0)

* facial skeleton

* UV Texture Facial Animation

* Muscle Model Animation

### Retargeting

* 采集一套动画可以应用到很多模型上

* 忽略骨骼之间的offset

* apply的是相对于原始的binding的joint的位移

* Align Movement by Pelvis Height

[![pFlGZ7T.jpg](https://s11.ax1x.com/2024/02/04/pFlGZ7T.jpg)](https://imgse.com/i/pFlGZ7T)

* Retargeting with different skeleton hierarchy：在两个相同骨骼之间的所有骨骼进行一个映射

* Unresolved problems
  
  * 模型自穿插问题
  
  * 自我接触约束问题（如鼓掌需要双手接触）
  
  * target character的平衡

* Morph  Animation Retargeting
