---
title: Hidden_Markov_Model
date: 2020-10-06 20:55:04
tags:
---
+ **Hidden Markov Model = Markov Random Field + Time** 
  + 动态模型=概率图模型+时间（可以是真正的时间，也可以是序列）
  + GMM高斯混合模型（样本之间独立同分布）；但是动态模型，样本之间不是独立同分布

    <img src="https://github.com/soloistben/images/raw/master/HMM/HMM1.png" alt="HMM1" style="zoom: 67%;" />

  + 图中动态模型包括：横向的时间关系（Time），纵向的混合关系（Mixture，不同变量混合）
  + **若hidden variable是离散的，则动态模型为HMM**；线性连续的，则是Kalmm Filter 卡尔曼滤波器；非线性连续的，则是Partide Filter

  <img src="https://github.com/soloistben/images/raw/master/HMM/HMM2.png" alt="HMM2" style="zoom:75%;" />

+ HMM: param λ = (π, A, B)（π是初始概率分布、A转移矩阵、发射矩阵）
  + **observed variable O**: o~1~, o~2~, ..., o~t~,... → V = {v~1~, ...v~M~} （观察值，观测变量o的值域）
  + **hidden variable I**: i~1~, i~2~, ..., i~t~,... → Q = {q~1~, ...q~N~} （隐变量i的值域）
  + $A = [a_{ij}], a_{ij} = P(i_{t+1}=q_{j}|i_{t}=q_{i})$
  + $B = [b_{j(k)}], b_{j(k)} = P(o_{t}=v_{k}|i_{t}=q_{j})$
+ 两个假设
  + 齐次马尔可夫假设
    + $P(i_{t+1}|i_{t}, i_{t-1}, ..., i_{1}, o_{t}, o_{t-1}, ..., o_{1}) = P(i_{t+1}|i_{t})$
    + 隐状态i~t+1~​只与隐状态​i~t~有关
  + 观测独立假设
    + $P(o_{t}|i_{t}, i_{t-1}, ..., t_{1}, o_{t-1}, ..., o_{1}) = P(o_{t}|i_{t})$
    + 观测状态o~t~只与观测状态i~t~有关
+ HMM解决三个问题（已知参数 λ = (π, A, B)）
  + Evalution → P(O|λ) （已知参数下，求解O现象的概率）→ 前向后向算法
  + Learning → 求解参数，λ = argmax P(O|λ) → EM算法（以前是Baum Welch算法）
  + Decoding → 找到一个状态序列，使 P(I|O)达到最大（I～ = argmax P(I|O)）
    + 预测问题：$P(i_{t+1}|o_{1},...,o_{t-1}, o_{t})$ 已知t个观察序列，预测下一时刻t+1的隐状态
    + **滤波问题**：$P(i_{t}|o_{1},...,o_{t-1}, o_{t})$ 已知t个观察序列，求解当前时刻t的隐状态

  [白板系列](https://www.bilibili.com/video/BV1aE411o7qd?p=82)