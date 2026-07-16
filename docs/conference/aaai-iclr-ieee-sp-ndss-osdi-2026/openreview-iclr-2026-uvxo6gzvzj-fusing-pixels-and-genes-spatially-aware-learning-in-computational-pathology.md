---
title: "Fusing Pixels and Genes: Spatially-Aware Learning in Computational Pathology"
title_zh: 融合像素与基因：计算病理中的空间感知学习
authors: "Minghao Han, Dingkang Yang, Linhao Qu, Zizhi Chen, Gang Li, Han Wang, Jiacong Wang, Lihua Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=uVXO6gzVzj"
tags: ["query:path-agent"]
score: 4.0
evidence: 整合基因表达的空间感知多模态病理学习，增强病理智能体特征
tldr: 语言模态缺乏分子特异性，限制了病理多模态学习。STAMP引入空间转录组学，通过自监督学习融合基因表达与病理图像，获得分子引导的嵌入。该方法可为病理智能体提供分子级线索，提升诊断和预后能力。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有病理多模态学习依赖视觉和语言，缺乏分子特异性。
method: 提出STAMP框架，整合空间转录组学与病理图像进行自监督联合嵌入。
result: 基因引导训练提供鲁棒且任务无关的病理表示，提升下游性能。
conclusion: 为病理智能体提供分子级别的多模态特征支持。
---

## Abstract
Recent years have witnessed remarkable progress in multimodal learning within computational pathology. Existing models primarily rely on vision and language modalities; however, language alone lacks molecular specificity and offers limited pathological supervision, leading to representational bottlenecks. In this paper, we propose STAMP, a Spatial Transcriptomics-Augmented Multimodal Pathology representation learning framework that integrates spatially-resolved gene expression profiles to enable molecule-guided joint embedding of pathology images and transcriptomic data. Our study shows that self-supervised, gene-guided training provides a robust and task-agnostic signal for learning pathology image representations. Incorporating spatial context and multi-scale information further enhances model performance and generalizability. To support this, we constructed SpaVis-6M, the largest Visium-based spatial transcriptomics dataset to date, and trained a spatially-aware gene encoder on this resource. Leveraging hierarchical multi-scale contrastive alignment and cross-scale patch localization mechanisms, STAMP effectively aligns spatial transcriptomics with pathology images, capturing spatial structure and molecular variation. We validate STAMP across six datasets and four downstream tasks, where it consistently achieves strong performance. These results highlight the value and necessity of integrating spatially resolved molecular supervision for advancing multimodal learning in computational pathology. The code is included in the supplementary materials. The pretrained weights and SpaVis-6M are available at: https://github.com/Hanminghao/STAMP.

---

## 论文详细总结（自动生成）

# 论文《Fusing Pixels and Genes: Spatially-Aware Learning in Computational Pathology》详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：现有计算病理学中的多模态学习主要依赖视觉（病理图像）和语言（文本报告）模态，但语言缺乏分子特异性，提供的病理监督有限，导致表征瓶颈。
- **动机**：引入空间转录组学（Spatial Transcriptomics）这一分子级别、空间分辨的基因表达数据，为病理图像提供分子引导的监督信号，突破现有表征局限。
- **整体意义**：提出首个整合“像素”与“基因”的空间感知多模态病理学习框架 STAMP，证明了分子级监督对提升病理图像表示鲁棒性和任务通用性的价值。

## 2. 论文提出的方法论
- **核心思想**：通过自监督学习融合病理图像与空间转录组数据，获得分子引导的联合嵌入表示，并强调空间上下文和多尺度信息的建模。
- **关键技术细节**：
    - 构建了迄今最大的 Visium 平台空间转录组数据集 **SpaVis-6M**。
    - 训练**空间感知基因编码器**（spatially-aware gene encoder），用于提取空间转录组特征。
    - 设计**层次化多尺度对比对齐**（Hierarchical multi-scale contrastive alignment）和**跨尺度斑块定位机制**（Cross-scale patch localization），对齐空间转录组与病理图像，捕获空间结构与分子变异。
- **公式/算法流程**（文字说明）：
    1. 输入：病理全切片图像（WSI）与对应的空间转录组斑点（spot）表达矩阵。
    2. 将 WSI 切分为多尺度斑块，基因表达数据通过空间感知编码器映射为特征向量。
    3. 对同一空间位置的多尺度图像斑块与基因表达向量进行对比学习（正负样本设计），同时引入跨尺度定位损失以约束位置一致性。
    4. 通过自监督训练，获得任务无关的病理图像表示，可直接用于下游任务微调或作为预训练特征。

## 3. 实验设计
- **数据集**：
    - 自建最大 Visium 空间转录组数据集 **SpaVis-6M**（用于预训练）。
    - 在**六个公开数据集**上验证，覆盖**四个下游任务**（具体任务名称未在摘要中详述，可能包括：分类、分割、生存分析、基因表达预测等）。
- **Benchmark**：与哪些方法对比？摘要未明确列举，但表明 STAMP “consistently achieves strong performance”。
- **对比方法**：未在摘要中列出，需查看全文补充。

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。
- 仅提到代码和预训练权重已开源（GitHub），未提计算资源。

## 5. 实验数量与充分性
- **实验组数**：在 6 个数据集、4 个下游任务上验证；还包含消融实验（如空间上下文、多尺度信息的贡献）。
- **充分性评价**：
    - 覆盖任务多样（分类、回归/预后等），且跨数据集测试，具有较好的泛化性评估。
    - 存在消融研究验证各模块的有效性，实验设计较完整。
    - 但未与其他多模态方法（如 CLIP 类、Transformer 类）对比时具体性能提升幅度，摘要未提供数值对比，客观性需查全文确认。

## 6. 论文的主要结论与发现
- 自监督、基因引导的训练能为病理图像表示提供鲁棒且任务无关的信号。
- 引入空间上下文和多尺度信息能进一步提升模型性能与泛化能力。
- 整合空间转录组学（分子级空间监督）对于推进计算病理学多模态学习具有重要价值与必要性。

## 7. 优点
- **创新性**：首次系统地将空间转录组学引入病理多模态学习，填补了“分子特异性缺失”的空白。
- **实用性**：构建了最大 Visium 数据集 SpaVis-6M，开源预训练权重，可复现；为病理智能体提供分子级线索，有利于诊断和预后。
- **技术设计**：层次化多尺度对比对齐+跨尺度定位机制，巧妙融合图像与基因的空间对应关系。
- **实验全面**：覆盖多任务、多数据集，并包含消融分析。

## 8. 不足与局限
- **实验细节缺失**：摘要中未报告与基线方法的量化对比结果（如准确率、AUC、C-index 等），难以直接评估提升幅度。
- **计算资源未披露**：无法判断训练成本是否可接受。
- **依赖空间转录组数据可用性**：该方法需要配对的组织切片基因表达数据，而此类数据获取成本高、覆盖面窄，限制了广泛应用。
- **可能存在的偏差风险**：SpaVis-6M 是否涵盖足够多样的组织类型和疾病？若数据偏重某一类，可能影响通用性。
- **应用限制**：仅基于 Visium 平台，其他空间组学技术（如 MERFISH、Slide-seq）可能需调整。

（完）
