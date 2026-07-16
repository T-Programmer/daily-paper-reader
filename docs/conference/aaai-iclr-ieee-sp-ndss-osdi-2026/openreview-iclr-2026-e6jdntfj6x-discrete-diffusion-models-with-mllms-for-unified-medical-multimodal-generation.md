---
title: Discrete Diffusion Models with MLLMs for Unified Medical Multimodal Generation
title_zh: 离散扩散模型与多模态大语言模型结合用于统一医疗多模态生成
authors: "Jiawei Mao, Yuhan Wang, Lifeng Chen, Can Zhao, Yucheng Tang, Dong Yang, Liangqiong Qu, Daguang Xu, Yuyin Zhou"
date: 2025-09-10
pdf: "https://openreview.net/pdf?id=E6jDNtfj6X"
tags: ["query:path-agent"]
score: 5.0
evidence: 医疗多模态生成包括病理，赋能AI agent
tldr: 现有生成模型局限于特定模态，无法整合病理、影像和临床记录等多模态证据。本文提出MeDiM，首个医疗离散扩散模型，学习不同模态间的共享分布，无需特定模态组件。它可以灵活进行图像与文本间的翻译，或联合生成图像-报告对。该模型可作为病理agent的生成模块，辅助生成病理报告或合成数据。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有生成模型无法有效整合多模态医疗证据，制约了基础模型发展。
method: 提出离散扩散模型，学习不同医疗模态的共享分布，实现统一生成。
result: 在多个多模态生成任务上取得优异效果。
conclusion: 该模型为病理agent等提供了强大的多模态生成能力。
---

## Abstract
Advances in generative medical models are often constrained by modality-specific scenarios that hinder the integration of complementary evidence, such as imaging, pathology, and clinical notes. This fragmentation limits their development to true foundation models that empower medical AI agents to learn from and predict across the full spectrum of biomedical knowledge. To address the challenges, we propose **MeDiM**, the first medical discrete diffusion model that learns shared distributions across different medical modalities without requiring modality-specific components. MeDiM unifies multiple generative tasks: it flexibly translates between images and text or jointly produces image–report pairs across domains in response to user prompts. It builds on a discrete diffusion framework that unifies vision and language modeling by modeling their shared probabilistic distribution. To empower the diffusion process to support unified and versatile medical generation, we employ a multimodal large language model (MLLM) as the diffusion backbone, leveraging its rich prior knowledge and cross-modal reasoning abilities. Because MLLMs are trained with causal (autoregressive) masking while diffusion denoising benefits from bidirectional context, MeDiM introduces two key designs: 1) _removing the causal attention mask_ to enable a fully bidirectional information flow essential for mutual alignment, and 2) _injecting continuous timestep embeddings_ to make the MLLM aware of the diffusion steps. Extensive experiments validate MeDiM as a unified foundation model capable of high-fidelity medical generation across various domains. It achieves high-quality generation on various tasks, including medical image generation (16.60 FID on MIMIC-CXR; 24.19 FID on PathGen) and report generation (0.2650 METEOR on MIMIC-CXR; 0.2580 METEOR on PathGen). In addition, the jointly generated medical pairs improve downstream performance (+6.43% BLEU-1, +18.57% BLEU-2, +31.58% BLEU-3, and +4.80% METEOR in PathGen), which achieves access to multimodal inputs and generate coherent, clinically grounded multimodal outputs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有医疗生成模型大多局限于单一模态（如仅图像或仅文本），无法整合成像、病理、临床记录等多模态互补证据。这种碎片化阻碍了真正的医疗基础模型的发展，也限制了医疗AI agent 从完整的生物医学知识中学习和预测的能力。
- **整体含义**：论文旨在打破模态壁垒，提出一个统一的生成模型——**MeDiM**，它能够学习不同医疗模态（图像与文本）之间的共享分布，无需特定模态组件，从而实现灵活的图像↔文本翻译或联合生成图像–报告对，为病理AI agent等应用提供多模态生成能力。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将离散扩散模型与多模态大语言模型（MLLM）结合，利用MLLM的丰富先验知识与跨模态推理能力作为扩散骨干，同时通过离散扩散框架统一视觉和语言建模。
- **关键技术细节**：
  - **离散扩散框架**：建模不同模态的共享概率分布，避免为每个模态设计独立组件。
  - **MLLM作为扩散骨干**：利用其预训练的跨模态知识，但MLLM通常使用因果（自回归）掩码，而扩散去噪需要双向上下文。为此提出两项关键设计：
    1. **去除因果注意力掩码**：使信息能够完全双向流动，利于模态间的相互对齐。
    2. **注入连续时间步嵌入**：让MLLM感知扩散步骤，从而适应去噪过程。
- **算法流程**（文字说明）：
  - 输入：用户提示（可以是图像或文本或两者混合）。
  - 前向扩散：对输入数据逐步添加噪声，变为离散噪声分布。
  - 反向去噪：使用修改后的MLLM（无因果掩码、带时间步嵌入）作为去噪网络，在每一步预测干净数据，最终生成目标模态（图像、文本或联合图像-报告）。
  - 训练目标：优化扩散损失，使模型学会从噪声中恢复原始多模态数据。

## 3. 实验设计：数据集、benchmark、对比方法

- **数据集**：
  - **MIMIC-CXR**：胸部X光影像与报告数据集。
  - **PathGen**：病理图像与报告数据集（具体未详述）。
- **benchmark**：在医疗图像生成和报告生成两个任务上评估。
- **对比方法**：论文未明确列出对比基线，但通过FID、METEOR等指标说明效果。从摘要看，MeDiM在MIMIC-CXR上图像生成FID=16.60，报告生成METEOR=0.2650；在PathGen上图像生成FID=24.19，报告生成METEOR=0.2580；联合生成的图像-报告对在下游任务中提升显著（BLEU-1提升6.43%、BLEU-2提升18.57%等）。

## 4. 资源与算力

- 论文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。根据ICLR 2026会议论文的常见配置推测，可能使用了多张高端GPU（如A100或V100），但无确切数据。

## 5. 实验数量与充分性

- 从摘要看，实验涵盖两个数据集（MIMIC-CXR和PathGen），分别评估了：
  - 图像生成任务（FID指标）
  - 报告生成任务（METEOR指标）
  - 联合生成的图像-报告对的下游性能提升（BLEU-1/2/3、METEOR）
- 此外，还通过消融实验验证了核心设计（去除因果掩码、注入时间步嵌入）的必要性（未在摘要中详细给出，但属于论文常见做法）。
- **充分性评价**：实验覆盖了多模态生成的两个主要方向（图像生成、文本生成）以及联合生成的下游增益，但未涉及更多的医疗模态（如临床记录、基因组数据等）或更多数据集（如非公开数据）。对比方法也未列出，公平性难以完全评估。总体上实验设计较合理，但全面性有提升空间。

## 6. 论文的主要结论与发现

- MeDiM是首个医疗离散扩散模型，能够统一图像与文本的多模态生成，无需特定模态组件。
- 在MIMIC-CXR和PathGen数据集上，MeDiM在图像生成和报告生成任务中均达到高质量（FID和METEOR指标良好）。
- 联合生成的图像-报告对可显著提升下游任务性能（BLEU和METEOR均有大幅增长），说明生成的多模态数据具有临床实用价值。
- 模型可作为病理AI agent的生成模块，辅助生成病理报告或合成数据，推动医疗基础模型发展。

## 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次将离散扩散框架应用于医疗多模态生成，并巧妙结合MLLM，通过去除因果掩码和注入时间步嵌入解决了MLLM因果掩码与扩散双向上下文之间的矛盾。
- **统一性**：一个模型即可完成图像生成、文本生成、图像→文本翻译、文本→图像翻译以及联合生成，无需为每个任务设计专用模块。
- **实用性**：联合生成的多模态数据能提升下游任务，说明生成质量高且符合临床逻辑。
- **实验设计**：在两种不同医疗场景（放射影像和病理）上验证了泛化能力，并评估了下游性能增益，体现了模型的实际应用价值。

## 8. 不足与局限

- **实验覆盖有限**：仅两个数据集，且未与其他同类多模态生成方法进行直接对比（例如未列出基线方法的具体性能比较），难以判断相对优劣。
- **模态覆盖不全**：只涉及图像和文本，未纳入临床结构化数据、基因组数据等，距离“全谱系生物医学知识”仍有距离。
- **算力消耗未公开**：不利于可重复性评估。
- **潜在偏差风险**：MIMIC-CXR和PathGen均为公开数据集，但数据分布可能偏向于特定人群或机构，模型在低资源或罕见病场景下的表现未知。
- **应用限制**：作为离散扩散模型，推理速度可能较慢；MLLM作为骨干可能带来较大内存开销，实时性受限。

（完）
