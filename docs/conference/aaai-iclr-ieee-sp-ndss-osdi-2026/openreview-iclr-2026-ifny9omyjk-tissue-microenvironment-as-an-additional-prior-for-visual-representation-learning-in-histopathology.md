---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理学视觉表示学习的额外先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:path-agent"]
score: 6.0
evidence: 利用组织微环境先验的自监督学习，增强病理agent的特征表示
tldr: 自监督学习在组织病理学中表现出色，但现有方法未充分利用组织微环境结构作为先验。本文通过语义掩码生成器识别组织结构，并将其作为增强集成到DINOv2预训练中。在5500万张TCGA组织病理切片上训练视觉Transformer，得到的表示在下游任务中优于基线。该预训练模型可为病理agent提供更强的视觉编码器。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 自监督学习未充分利用组织微环境结构信息。
method: 训练对抗性掩码生成器识别组织结构，在DINOv2中集成语义掩码增强。
result: 预训练模型在多个下游任务上取得最佳性能。
conclusion: 引入组织微环境先验有效提升了病理图像表示质量，有助于病理agent的感知能力。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

# 论文结构化中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：当前自监督学习在组织病理学中虽然表现优异，但现有方法（如 DINOv2）主要基于自然图像设计，**未充分利用组织微环境（Tissue Microenvironment）的固有结构信息**作为先验知识。
- **整体含义**：组织微环境包含细胞、血管、基质等具有生物学意义的空间结构，将其作为额外先验引入自监督预训练，有望提升病理图像的特征表示质量，从而服务于下游诊断任务（如突变预测、分类），并为病理学 AI agent 提供更强的视觉编码器。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：通过语义掩码（Semantic Masking）将组织微环境结构作为数据增强，集成到 DINOv2 自监督学习框架中，迫使模型关注具有生物学意义的区域。
- **关键技术细节**：
  - **语义掩码生成器**：基于 ADIOS 框架，训练对抗性掩码生成器（Adversarial Mask Generator），并加入感知重建损失（perceptual reconstruction loss），以识别组织学结构（如细胞核、腺体、间质等）。
  - **三种增强策略**：
    1. **标准 DINOv2 增强**（baseline）：仅使用裁剪、颜色抖动等标准图像增强。
    2. **混合增强**（DINOv2-mixed）：将标准增强与语义掩码相结合。
    3. **仅语义掩码增强**（DINOv2-semantic）：仅使用语义掩码作为增强。
  - **预训练目标**：视觉 Transformer（ViT）在 5500 万张 TCGA 组织病理切片（224×224 像素，分辨率 0.5 μm/pixel）上使用上述三种策略进行自监督预训练，评估表示质量。

## 3. 实验设计：数据集、基准与对比方法
- **预训练数据**：TCGA（The Cancer Genome Atlas）数据库，共 **5500 万张** 224×224 像素的组织病理图块。
- **下游评估基准**（共 6 个任务）：
  - **4 个图块级分类任务**：PCam、MiDOG、MHIST、BRACS。
  - **2 个全切片级突变预测任务**：LUAD 中的 EGFR 突变预测、BLCA 中的 FGFR3 突变预测。
- **对比方法**：主要将 DINOv2-mixed 与 DINOv2（标准增强）和 DINOv2-semantic 进行比较，同时定性分析 PCA 可视化结果。

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。仅提及在 5500 万张切片上预训练视觉 Transformer，暗示需要较大计算资源，但未给出量化指标。

## 5. 实验数量与充分性
- **数量**：共涉及 **6 个下游任务**（4 个分类 + 2 个突变预测），涵盖图块级和切片级任务；并对增强策略进行了三种变体的消融比较；还提供了 PCA 可视化定性分析。
- **充分性与公平性**：
  - 实验相对充分，覆盖了常见病理基准。
  - 与标准 DINOv2 基线在相同预训练设置下进行公平对比。
  - 但未与其他自监督方法（如 MoCo v3、SimCLR、MAE 等）进行横向比较，也缺乏跨中心或跨数据集泛化测试。
  - 消融实验仅对比了增强策略，未深入分析掩码生成器不同损失或结构的影响。

## 6. 主要结论与发现
- **混合增强策略（DINOv2-mixed）** 在 **全部 6 个下游任务** 上一致优于标准 DINOv2 基线，证明了引入组织微环境先验的有效性。
- 仅语义掩码增强（DINOv2-semantic）效果一般，说明语义掩码必须与标准增广结合才能充分发挥作用。
- **定性结果**：PCA 可视化显示，DINOv2-mixed 能够无监督地将组织分解为细胞结构、血管、基质等生物学可解释成分，特征分离更清晰。
- 结论：领域特定的组织先验能够提升自监督表示学习质量，有助于病理 agent 的感知能力。

## 7. 优点
- **创新性**：首次将组织微环境结构作为可学习的语义掩码先验，并集成到主流自监督框架 DINOv2 中。
- **方法论扎实**：使用对抗训练和感知损失生成语义掩码，而非简单手工设计，增强了对病理结构的适应性。
- **实验设计全面**：覆盖图块级和切片级任务，并包含定性可视化验证。
- **大规模预训练**：使用真实世界大规模 TCGA 数据，提升了结果的可靠性。

## 8. 不足与局限
- **算力成本不透明**：未报告训练所需的 GPU 型号/数量/时长，难以评估方法的经济可行性。
- **比较范围有限**：未与其他代表性的病理自监督方法（如 CTransPath、Phikon、ViTS-256 等）或通用自监督方法对比。
- **潜在偏差风险**：仅使用 TCGA 一个数据源进行预训练，可能缺乏对其它染色、扫描仪或医疗机构的泛化能力。
- **语义掩码质量未量化**：未评估掩码生成器识别组织结构的准确率或覆盖率，也缺乏对掩码策略超参数的敏感性分析。
- **应用限制**：语义掩码需要额外的预训练生成器，增加了流程复杂度；仅评估了分类和突变预测任务，未涵盖分割或生存分析。

（完）
