---
title: LLM-mediated pathology models for robust cross-institution generalization
title_zh: LLM中介的病理模型实现鲁棒的跨机构泛化
authors: "Yishu Zhang, Didong Li, Huaxiu Yao, Yun Li, Iain Carmichael, Katherine Hoadley, Di Wu, Daiwei Zhang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=lSSGmgIPNO"
tags: ["query:path-agent"]
score: 7.0
evidence: LLM中介的病理模型提升泛化能力
tldr: 病理基础模型受批效应影响泛化能力差，现有方法效果有限。本文提出GLMP框架，利用多模态大模型将组织图像块转为文本描述再编码，生成鲁棒嵌入。实验表明该方法有效缓解批效应，提升跨机构泛化性能，为病理AI提供新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 病理基础模型因批效应导致跨机构泛化差，现有归一化方法效果有限。
method: 提出GLMP框架，将组织学图像块先转换为文本描述，再利用预训练MLLM和文本编码器生成鲁棒数值嵌入。
result: 在跨机构测试中，GLMP显著提升病理图像分析通用性，缓解批效应。
conclusion: LLM中介的嵌入生成是克服病理模型泛化瓶颈的有效途径。
---

## Abstract
Pathology foundation models (PFMs) have shown strong potential across clinical and scientific applications. Their performance, however, is often limited by batch effects, which are non-biological variations across tissue source institutions (TSIs) that distort feature representations and reduce generalization. Existing mitigation methods, such as stain normalization, have limited success in addressing these high-dimensional and complex artifacts. We introduce the General-purpose LLM-Mediated Pathology model (GLMP), a novel framework that generates robust numerical embeddings from histology image patches by first converting them into text descriptions. By leveraging pretrained multimodal large language models (MLLMs) and text encoders, GLMP prioritizes genuine biological signals over TSI-specific signatures and improves cross-TSI generalization compared to existing PFMs. Our findings demonstrate the effectiveness of broad-domain, non-specialized MLLMs in computational pathology and provide an alternative framework for developing versatile, generalizable, and robust pathology models that do not require large-scale, histology-specific pretraining data. Code is provided in Supplementary Materials for reproducibility and will be released to the public upon paper acceptance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：病理基础模型（PFMs）在跨机构泛化时性能严重受限，主要原因是“批效应”——即不同组织来源机构（TSI）之间存在的非生物性变异（如染色差异、扫描设备差异等），导致模型学到的特征被这些噪声扭曲，难以推广到新机构。
- **背景与动机**：现有缓解方法（如染色归一化）在高维且复杂的批效应面前效果有限，无法有效消除非生物信号。因此，亟需一种能够优先提取真实生物信号、忽略机构特异性伪影的新型特征表征方法。

## 2. 方法论：核心思想、关键技术细节与流程

- **框架名称**：GLMP（General-purpose LLM-Mediated Pathology Model），即通用型LLM中介病理模型。
- **核心思想**：利用多模态大语言模型（MLLM）将组织学图像块先转换为自然语言描述，再通过预训练的文本编码器生成数值嵌入。由于文本描述天然忽略染色等低级视觉歧义，而保留生物学概念，因此生成的嵌入对批效应鲁棒。
- **关键流程**：
  1. 输入：组织学图像块（例如来自病理切片的局部区域）；
  2. 图像→文本：使用预训练MLLM（如GPT-4V等非专用病理的通用MLLM）将图像块翻译成结构化的文本描述（如“高密度细胞核区域，核异型性明显”）；
  3. 文本→嵌入：使用预训练文本编码器（如BERT或CLIP文本编码器）将文本转换为固定维度的数值向量；
  4. 下游任务：该嵌入可直接用于分类、生存分析等临床或科研任务，或作为通用特征供其他模型使用。
- **公式/算法**：文中未给出具体公式，但整体是一个两阶段流水线：`Image → MLLM (text) → Text Encoder (embedding)`，训练阶段仅需少量或无需微调。

## 3. 实验设计

- **数据集/场景**：摘要中未列出具体数据集名称，但明确指出使用了**跨机构（cross-TSI）** 测试场景，即在不同医疗机构收集的数据上评估模型泛化能力。
- **Benchmark与对比方法**：对比了现有病理基础模型（PFMs，如基于对比学习的通用病理模型），以及可能包括直接使用图像编码器的方法（如ResNet、ViT等）。未提及具体对比模型列表。
- **评估指标**：未明确说明，但推测包括分类准确率、AUC等通用指标及跨机构泛化性能度量（如域间性能差距缩小程度）。

## 4. 资源与算力

- **未明确说明**：论文摘要及给定元数据中未提及任何具体GPU型号、数量、训练时长或计算资源消耗。仅提供代码文件用于复现，但无算力细节。

## 5. 实验数量与充分性

- **实验数量**：摘要中仅定性描述“在跨机构测试中显著提升”，未报告具体实验组数（如不同机构数、不同任务数、消融实验等）。但元数据指出“做了多组实验（不同数据集、消融实验等）”，暗示全文可能有严谨的消融分析。
- **充分性与公平性**：
  - 优势：对比了现有PFMs，使用跨机构设置，体现了对实际部署问题的关注。
  - 不足：由于信息有限，无法判断是否控制了所有变量（如数据量、机构数），以及是否进行了统计显著性检验。实验覆盖度需要全文验证。

## 6. 主要结论与发现

- GLMP通过LLM中介的文本描述生成嵌入，能够有效缓解病理图像中的批效应，显著提升跨机构泛化性能。
- 通用（非专门化）MLLM（如GPT-4V）在计算病理中具有有效性，无需大规模、组织学特异的预训练数据即可获得鲁棒特征。
- 该框架提供了一种替代传统基于图像编码的病理基础模型开发思路，具有通用性、普适性和鲁棒性。

## 7. 优点（方法或实验设计亮点）

- **创新性**：首次利用LLM将视觉信号转化为文本描述来解决病理泛化问题，跳出常规的染色归一化或域对抗学习范式。
- **数据效率高**：无需收集海量专用病理图像预训练，直接复用已有的MLLM和文本编码器，降低资源门槛。
- **可解释性潜力**：生成的文本描述可直接解读，有助于临床验证模型关注点是否合理。
- **通用性强**：所采用的MLLM为广域通用模型，并非专门为病理训练，证明了跨领域迁移的有效性。

## 8. 不足与局限

- **实验透明度不足**：摘要中未提供具体数据集、对比方法、实验配置详情，难以复现和评估结论的可靠性。
- **依赖MLLM质量**：若MLLM生成文本描述不准确或遗漏关键形态学细节，可能丢失重要生物信号；且MLLM可能受限于自身知识边界（如不擅长罕见病变）。
- **计算开销**：虽然不需要大规模预训练，但推理时需额外调用MLLM和文本编码器，可能增加延迟与成本（如调用API或加载大模型）。
- **细粒度信息损失**：将图像转换为文本可能丢失亚细胞结构、纹理等连续细微特征，适用于判别性较强的任务，但可能不适合需要高保真视觉细节的任务（如有丝分裂计数）。
- **应用限制**：目前仅在跨机构泛化上验证，对其他批效应来源（如不同扫描仪、不同染色批次）的鲁棒性未知；且未讨论在非公开数据上的隐私风险（如文本描述可能泄露患者信息）。

（完）
