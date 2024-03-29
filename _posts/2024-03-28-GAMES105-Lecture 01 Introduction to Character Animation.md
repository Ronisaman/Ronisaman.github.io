---
title: GAMES105-Lecture 01 Introduction to Character Animation
date: 2024-03-28 18:30:00 +0800
categories: [Computer Graphics, GAMES105]
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
pdf地址：[Introduction to Character Animation](https://games-105.github.io/ppt/01%20-%20Introduction.pdf)

## 3D Computer Animation

* Simulation: rigid bodies,deformable solids,ropes, thin shells, cloth,fluid, smoke, sound...Phenomenon
* Character Animation: humans, animals,virtual creatures,hands, robots,crowds...Behavior
* 一般一个角色只有二三十个关节数，50到100+参数
* 把劳动密集型的民工活-> 计算密集型的计算机活
* Character Animation Pipeline

[![pFo6NND.jpg](https://s21.ax1x.com/2024/03/29/pFo6NND.jpg)](https://imgse.com/i/pFo6NND)

* Forward Kinematics
* Inverse Kinematics
* Interpolation
* Motion Capture
* Motion Retargeting
* Motion Graphs/State Machines:重用已有数据，生成新的动作
  * 问题：太复杂，容易出bug
* Motion Matching:不是完整地播放一个动作，而是在更加细粒度的情况下，比如每一帧结束后，通过一个最近邻搜索，去找到一个新的姿态，同时满足要控制的目标、与当前角色的动作不能差太远保证动作连续性
* Learning-based Approaches
* Motion Generative Models
* Cross-Modal Motion Synthesis：跨模态动作生成
* Problems of Kinematic Methods
  * 物理问题，如穿模
  * 与环境交互的意外动作，动作库中没有
* Motion Reconstuction with Sparse
  * 3 Point Tracking
* Proportional-Derivative(PD) Control
* trajectory crafting - NaturalMotion: 设计轨迹，然后再根据类似pd控制的方法去进行物理仿真
* Spacetime/Trajectory Optimization
* Abstract Models-simbicon
* DRL-based Tracking Controllers 


[![pFo6U4e.jpg](https://s21.ax1x.com/2024/03/29/pFo6U4e.jpg)](https://imgse.com/i/pFo6U4e)