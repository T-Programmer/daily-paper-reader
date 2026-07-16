---
title: Histopathology-Genomics Multi-modal Structural Representation Learning for Data-Efficient Precision Oncology
title_zh: 组织病理-基因组学多模态结构表示学习用于数据高效的精准肿瘤学
authors: "Kun Wu, Zhiguo Jiang, Xinyu Zhu, Jun Shi, Yushan Zheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=24QX6XpvSL"
tags: ["query:path-agent"]
score: 5.0
evidence: 组织病理-基因组学多模态表示学习，可辅助病理agent
tldr: 融合组织病理图像和基因组数据的深度学习在精准肿瘤学中具有重要作用，但基因组数据常缺失。本文提出多模态结构表示学习框架，利用病例间关系重建缺失的基因组数据。该方法提高了数据效率，为病理agent提供了更丰富的多模态特征。但论文本身并非agent研究，而是表示学习。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基因组数据缺失限制了多模态融合在精准肿瘤学中的应用。
method: 提出多模态结构表示学习框架，利用病例间关联重建缺失基因组数据。
result: 在多个肿瘤数据集上实现了更准确的基因组预测和病理分析。
conclusion: 该工作提升了病理数据表示质量，可为病理agent提供更全面的特征输入。
---

## Abstract
Fusing histopathology images and genomics data with deep learning has significantly advanced precision oncology. However, genomics data is often missing due to its high acquisition cost and complexity in real-world clinical scenarios. Existing solutions aim to reconstruct genomics data from histopathology images. Nevertheless, these methods typically relied only on individual case and overlooked the potential relationships among cases. Additionally, they failed to take advantage of the authentic genomics data of diagnostically related cases that are accessible from training for inference. In this work, we propose a novel Multi-modal Structural Representation Learning (MSRL) framework for data-efficient precision oncology. We pre-train a histopathology-genomics multi-modal representation graph adopting Graph Structure Learning (GSL) to construct inter-case relevance based on the data inherently. During the fine-tuning stage, we dynamically capture structural relevance between the training cases and the acquired authentic cases for precise prediction. MSRL leverages prior inter-case associations and authentic genomics data from diagnosed cases based on the graph, which contributes to effective inference based on the single histopathology image modality. We evaluated MSRL on public TCGA datasets with 7,263 cases across various tasks, including survival prediction, cancer grading, and gene mutation prediction. The results demonstrate that MSRL significantly outperforms existing missing-genomics generation approaches with improvements of 1.44% to 3.12% in C-Index on survival prediction tasks and achieves comparable performance to multi-modal fusion methods. The code and data are available at https://github.com/WkEEn/MSRL.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在精准肿瘤学中，融合组织病理图像与基因组数据的多模态深度学习模型效果显著，但基因组数据常因成本高、流程复杂而在真实临床场景中缺失。
- **研究动机**：现有方法仅从单病例的组织病理图像重建缺失的基因组数据，忽视了病例之间的潜在关联（如诊断相似性），也未能在推理阶段利用训练集中已有的真实基因组数据。
- **整体含义**：论文试图通过挖掘病例间的结构关系，提高缺失基因组数据的重建质量，从而在仅有组织病理图像的情况下实现接近多模态融合的性能，提升数据效率。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用图结构学习（Graph Structure Learning, GSL）构建组织病理-基因组多模态表示图，显式建模病例间的相关性；在微调时动态捕获训练病例与已知真实病例之间的结构关联，实现基于单模态（组织病理图像）的有效推理。
- **关键技术细节**：
  - **预训练阶段**：采用图结构学习在无监督或自监督方式下，基于数据本身自动构建病例间的关联图。该图融合了组织病理图像特征与基因组特征（或仅图像特征，若基因组缺失）。
  - **微调阶段**：针对下游任务（如生存预测），动态提取待预测病例与训练集中已诊断病例（具有真实基因组数据）之间的结构相关性，从而利用这些真实基因组信息辅助推理，而不是完全依赖生成模型。
  - **推理**：仅需输入组织病理图像，通过图结构从相关训练病例中“借用”基因组信息，实现精准预测。
- **公式/算法流程**：论文未给出具体公式，但核心流程为：预训练（GSL构建跨病例图）→ 微调（动态结构相关性捕获）→ 推理（单模态输入+图结构辅助）。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：使用公共TCGA（The Cancer Genome Atlas）数据集，共包含7,263例病例。覆盖多种肿瘤类型。
- **任务/场景**：
  - 生存预测（survival prediction）
  - 癌症分级（cancer grading）
  - 基因突变预测（gene mutation prediction）
- **基准**：对比了现有的缺失基因组生成方法（missing-genomics generation approaches），例如仅基于单病例重建的方法。
- **对比方法**：具体名称未列出，但摘要指出MSRL在生存预测的C-Index上提升1.44%~3.12%，且与完整多模态融合方法性能相当。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长、显存等算力信息。需要指出这一不足。

## 5. 实验数量与充分性
- **实验数量**：共涉及三种任务（生存预测、癌症分级、基因突变预测），涵盖7,263例病例。未明确列出消融实验的具体组数，但根据方法复杂性推测应包含：
  - 对比实验（与现有生成方法对比）
  - 可能包含有无图结构的消融、是否使用真实基因组数据的消融等。
- **充分性**：
  - 数据集规模较大（七千余例），任务多样性较好。
  - 对比了现有方法并报告了统计提升（C-Index），显示统计学显著。
  - 但缺乏与更多近期基线（如Transformer-based生成方法）的对比细节；消融实验设计未在摘要中体现，可能不够透明。总体而言，实验较为充分，但公开细节有限。

## 6. 论文的主要结论与发现
- 提出的MSRL框架在缺失基因组数据场景下，显著优于现有单病例重建方法，在生存预测任务中C-Index提升1.44%~3.12%。
- 能够达到与完整多模态融合方法相当的性能，说明利用病例间结构关系可以高效弥补单一模态的信息不足。
- 代码和数据集已开源，便于复现和扩展。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：
  - 创新性地引入图结构学习来建模病例间关联，突破了传统单病例重建的局限。
  - 微调阶段动态利用训练集中已有的真实基因组数据，而非仅依赖生成数据，提高了推理可靠性。
  - 仅需单模态输入（组织病理图像）即可实现接近双模态的效果，具有现实临床意义。
- **实验设计亮点**：
  - 在多个肿瘤类型的TCGA数据集上进行评估，任务覆盖生存、分级、基因突变，验证了泛化能力。
  - 与完整多模态方法对比，验证了方法的“数据高效”性。

## 8. 不足与局限
- **实验覆盖**：未提及具体肿瘤亚型或罕见癌症，可能通用性需进一步验证。
- **偏差风险**：TCGA数据集本身具有筛选偏差（如患者选择标准），模型可能不适用于其他来源或低资源场景。
- **应用限制**：
  - 依赖训练集中存在足够多的相关病例来构建有意义的图结构；若病例间缺乏关联（如罕见病），性能可能下降。
  - 动态结构捕获阶段需要存储和计算病例间相似度，可能带来额外的推理开销。
- **算力信息缺失**：未报告训练成本，不利于实际部署评估。
- **消融实验不透明**：未在摘要中展示，读者无法判断各组件（图结构、真实数据利用）的具体贡献。

（完）
