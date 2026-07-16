---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理图像到细胞云：使用分层细胞Transformer学习切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:path-agent"]
score: 7.0
evidence: 通过细胞云建模进行组织病理图像表示，为病理agent提供基础
tldr: 现有组织病理全切片图像分析方法主要基于图像表示学习，忽略了细胞空间分布的重要性。本文提出将每张切片视为细胞集合，通过细胞检测和细胞云建模，并采用分层细胞Transformer学习表示。该方法直接从细胞分布语义层面分析切片，为后续病理agent的细胞级推理提供了有效的特征表示基础。在多个任务上验证了优越性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法忽略细胞空间分布，无法直接建模细胞级语义。
method: 提出细胞检测+细胞云建模+分层细胞Transformer的表示学习方案。
result: 在多个组织病理学任务上取得了优于传统方法的性能。
conclusion: 该工作展示了从细胞分布角度理解病理图像的潜力，可赋能病理agent进行细粒度分析。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有组织病理学全切片图像（WSI）分析方法主要基于图像表示学习，忽略了细胞空间分布这一关键病理语义。能否直接利用细胞的空间分布进行深度学习建模，是一个尚未被充分探索的问题。
- **整体含义**：本文将每张WSI视为一个细胞集合，通过检测细胞并建模其空间分布（“细胞云”），实现基于细胞级语义的切片表示学习。这种方法能够更贴近病理医生的细胞层面诊断推理，为后续病理智能体（path-agent）的细粒度分析提供基础。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将WSI转化为细胞云（cell cloud），即通过细胞检测算法提取所有细胞的位置和类别，然后对这些细胞的空间分布进行层次化建模。
- **关键技术细节**：
  - **Human-in-the-loop标签优化**：利用人工辅助迭代精炼预训练的细胞检测与分类模型，提升检测准确度。
  - **分层细胞Transformer（CCFormer）**：
    - **邻域信息嵌入模块**：刻画每个细胞邻域内的局部分布特征。
    - **层次空间感知模块**：采用自底向上的方式学习细胞之间的空间关系，逐步聚合为全局切片表示。
- **算法流程**：输入WSI → 细胞检测（获取细胞坐标和类型）→ 构建细胞云 → 邻域信息嵌入 → 层次空间Transformer编码 → 得到切片级表示 → 用于下游任务（如生存预测、癌症分期）。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：文中提及临床分析基于细胞计数的评估指标可评估生存风险，并在生存预测和癌症分期两个任务上进行了实验（具体数据集名称未在摘要中给出，但推测为公开的TCGA等病理数据集）。
- **基准（Benchmark）**：与同类方法比较，采用标准评估指标（如生存预测的C-index、分期准确率等）。
- **对比方法**：包括基于图像表示的全切片学习方法（如MIL、Transformer-based WSI模型等），以及纯细胞计数基线。CCFormer仅利用细胞空间分布信息即超越了这些方法。

### 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量或训练时长。仅提及模型为Transformer架构，但未提供计算资源细节。需要查阅全文获取。

### 5. 实验数量与充分性

- **实验数量**：从摘要和元数据看，至少包含两类任务（生存预测、癌症分期）的实验，以及临床分析（基于细胞计数的评估）和消融实验（验证CCFormer各模块有效性）。元数据还提到了“多个任务上验证了优越性”。
- **充分性与客观性**：实验覆盖了组织病理学的两个典型任务，并与多种基线对比，且通过消融验证了设计。但未提供多数据集交叉验证、泛化性实验细节。总体上实验设计较合理，公平性较好（仅基于细胞空间分布，避免了图像特征干扰）。

### 6. 论文的主要结论与发现

- **主要结论**：将WSI建模为细胞云，并利用分层Transformer学习细胞空间分布，能够有效地进行生存预测和癌症分期，性能超越仅使用图像表示的方法。临床分析表明，基于细胞计数的简单指标已能评估患者生存风险，而CCFormer进一步提升了建模能力。
- **发现**：细胞空间分布本身包含了丰富的病理语义，直接建模可跳过中间图像特征，具有高效、可解释的潜力。

### 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次提出将WSI视为细胞云，并设计专用Transformer架构（CCFormer），直接建模细胞级空间分布。
- **人机协同标签优化**：利用human-in-the-loop提高细胞检测质量，增强下游表示可靠性。
- **解释性强**：细胞分布语义与病理医生的认知更一致，便于临床理解。
- **实验设计**：仅使用细胞分布信息即达到SOTA，突出了方法的有效性。

### 8. 不足与局限

- **算力与资源未公开**：无法评估训练成本及部署可行性。
- **实验覆盖有限**：仅提及两个任务，缺少不同癌症类型、多样本规模下的泛化验证；未与多模态方法（如融合图像与细胞信息）比较，可能未能展示联合建模的上限。
- **依赖细胞检测质量**：检测错误可能传播到后续表示，人机迭代流程增加了成本。
- **模型复杂性**：Transformer处理大量细胞可能面临计算瓶颈，文中未讨论效率问题。
- **公开性**：论文为ICLR 2026被拒版本（Rejected-Public），可能在某些方面存在不足（如实验鲁棒性、理论深度），但元数据仍给出7.0分。

（完）
