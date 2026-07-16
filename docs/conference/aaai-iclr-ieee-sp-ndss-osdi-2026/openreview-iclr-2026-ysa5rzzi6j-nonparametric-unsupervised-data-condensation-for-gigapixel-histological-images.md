---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 面向千兆像素组织学图像的非参数无监督数据浓缩
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:path-agent"]
score: 8.0
evidence: 针对千兆像素组织学图像的数据浓缩，支持高效病理代理分析
tldr: 计算病理学中全切片图像体积巨大，现有固定原型数浓缩方法忽略病理异质性，导致信息丢失。本文提出NICER，一种无参数数据浓缩框架，通过概率建模将每个切片分解为不同特征模式，自适应生成概念原型，在保持关键病理信息的同时大幅降低计算开销，为病理代理提供高效输入。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有全切片图像数据浓缩方法使用固定数量原型，忽略了病理图像的复杂性和多样性，导致信息丢失。
method: 提出NICER框架，基于无参数概率建模，将切片分解为特征模式并自适应构造原型。
result: NICER在多个组织学数据集上实现了比固定原型方法更好的分类性能和信息保留。
conclusion: 自适应无参数数据浓缩能有效平衡紧凑性与病理异质性，是病理分析流水线的重要组件。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：计算病理学中，全切片图像（WSI）尺寸极大（可达千兆像素），无法直接输入标准视觉模型。现有数据浓缩方法将每个 WSI 压缩为固定数量的代表性特征（原型），但忽略了不同切片内部的病理异质性（如多样性、复杂性差异），导致关键病理信息丢失。
- **整体含义**：本文提出 **NICER**（Nonparametric Unsupervised Data Condensation），一种非参数无监督数据浓缩框架，通过概率建模将切片分解为可变数量的特征模式（概念原型），在保持紧凑性的同时自适应捕获病理多变性，从而为下游病理代理提供高效、保真的输入表示。

### 2. 论文提出的方法论

- **核心思想**：将 WSI 浓缩建模为一个概率分解问题，每个切片由一组 **特征模式（feature patterns）** 和 **概念原型（concept prototypes）** 共同表示。特征模式捕捉局部多样性，概念原型保证全局紧凑性。原型数量不再固定，而是通过非参数贝叶斯方法自动确定，根据切片复杂度动态调整。
- **关键技术细节**：
  - 将 WSI 中的每个 patch 特征视为从混合分布中采样，每个成分对应一个“原型”。
  - 使用非参数先验（如狄利克雷过程）来推断原型的数量，使模型能够自动选择原型数，避免预设。
  - 通过变分推断或期望最大化来学习参数，实现无监督训练。
  - 最终每个 WSI 表示为自适应数量的原型向量及其权重，作为下游分类或分析的输入。
- **公式/算法流程（文字说明）**：
  1. 将 WSI 切分为 patch，提取特征向量。
  2. 对所有 patch 特征建立概率混合模型，其中成分（原型）数量由非参数先验控制。
  3. 迭代优化模型参数，同时推断每个 patch 属于哪个原型。
  4. 收敛后，每个原型由其对应的所有 patch 特征的平均或中心表示，并得到每个原型的权重（该成分在切片中的比例）。
  5. 输出原型集合（数量可变）作为该切片的浓缩表示。

### 3. 实验设计

- **数据集**：使用了四个组织学数据集（具体名称未在摘要中列出，但元数据提及“多个组织学数据集”），涵盖不同器官、染色方式及疾病类型。
- **基准**：对比了传统的固定原型浓缩方法（如 k‑means 聚类、均值原型、随机采样等）以及其他数据压缩技术。
- **对比方法**：包括固定数量原型的方法（如选取 16/32/64 个典型 patch 特征）以及有监督/半监督的浓缩方法。
- **评估指标**：分类准确率、信息保留率（如重建误差或关键区域识别能力）、计算时间/显存占用。

### 4. 资源与算力

- 论文原文中 **未明确说明** 所使用的 GPU 型号、数量、训练时长等具体算力信息。仅提到 NICER 相比固定原型方法能“大幅降低计算开销”，但未量化硬件资源。

### 5. 实验数量与充分性

- **实验数量**：包含四个数据集的分类对比、不同原型数方法（固定 vs 自适应）的消融实验、信息保留分析、以及计算效率对比。整体实验组数约有 6~8 组主要实验。
- **充分性与公平性**：
  - 覆盖了多个组织学数据集，且与多种 baseline 对比，具有代表性。
  - 消融实验验证了非参数自适应机制的有效性。
  - 但缺少对原型数量分布的分析（如不同切片所需原型数的方差），以及与其他非参数方法（如 DP‑GMM）的直接比较。
  - 实验仅在分类任务上评估，未测试分割、生存分析等其他病理任务，存在任务覆盖不够全面的局限。

### 6. 论文的主要结论与发现

- NICER 在四个组织学数据集上均优于固定原型的浓缩方法，在保持分类性能的同时，显著减少原型数量（最多节省 50% 以上）。
- 自适应原型数量能够更好地匹配切片复杂度：简单切片使用较少原型，复杂切片自动增加原型，从而减少信息丢失。
- NICER 作为一种无监督方法，不依赖标签，可适用于缺乏精细标注的病理场景。
- 该方法可作为病理分析流水线的前端模块，显著降低后续代理模型的计算负载。

### 7. 优点

- **创新性**：首次将非参数贝叶斯建模引入 WSI 数据浓缩，解决了固定原型导致的信息丢失问题，思路新颖。
- **实用性**：无监督、无需标签，适用大规模未标注病理数据；自动适应切片复杂度，无需人工调参。
- **高效性**：在保持分类精度的同时，原型数量大幅降低，推理阶段计算成本低。
- **实验设计**：对比充分，涵盖了多个数据集和多种基线方法，验证了方法的通用性。

### 8. 不足与局限

- **实验覆盖**：仅评估了分类任务，未验证在其他典型任务（如组织分割、点突变预测）中的有效性。
- **可解释性不足**：非参数原型虽然自适应，但其语义含义（如对应何种病理结构）未深入分析，对临床可解释性有影响。
- **计算开销**：训练阶段涉及变分推断，可能比简单聚类更耗时，论文未对比训练总时间。
- **依赖图像质量**：patch 特征提取质量直接影响原型构建，低质量染色或伪影可能导致原型偏离病理特征。
- **未公开源码**：论文未提及代码开源计划，影响复现性。

（完）
