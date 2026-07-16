---
title: "PIPA: An Agent for Protein Interaction Identification and Perturbation Analysis"
title_zh: PIPA：用于蛋白质相互作用识别和扰动分析的智能体
authors: "Xiaotao Wang, Kangqing Xu, Wenjing Li, Guangchuan Guo, Zhiyuan Li, Zhidong Zhang, Yiyang Liu, Dan Liu, Nuo Xu, Shuke Zhao, Shuo Ren, Qianlong Du, Zhenjiang Ren, Ziliang Pang, YUYING WANG, YANBIAO DUAN, Haixin Wang, Haisheng Yu, Yingying Chen, Ge Yang, Jiajun Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1fH0nFuvjo"
tags: ["query:path-agent"]
score: 4.0
evidence: 面向病理突变的蛋白质相互作用和扰动分析工具增强智能体
tldr: 蛋白质相互作用在疾病中关键但发现费力。PIPA是一个工具增强智能体，通过计划-选择-执行-反思循环自动完成PPI识别、通路分析和靶点筛选。该智能体可辅助病理学家分析疾病相关突变，加速诊断和治疗靶点发现。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 蛋白质相互作用发现效率低，影响疾病机制研究。
method: 提出工具增强智能体PIPA，自动化PPI发现和病理突变效应预测。
result: PIPA集成多项任务，有效辅助生物学家发现新PPI和病理效应。
conclusion: 为病理分子层面的智能体提供了自动化分析范例。
---

## Abstract
Protein–protein interactions (PPIs) play a fundamental role in the functioning of proteins and the formation of cellular pathways. Given their implication in numerous disease processes, PPIs represent important targets for therapeutic intervention. To enhance the efficacy and efficiency of PPI identification, pathway analysis, and disease target screening, we present PIPA, a tool-augmented intelligent agent that automates the entire PPI-centric discovery pipeline through a structured Plan-Select-Execute-Reflect loop,  to assist biological researchers in discovering novel PPIs and predicting the effects caused by pathological mutations. PIPA integrates multiple tasks, including automated database retrieval, protein interaction identification, pathological mutation annotation, and interface perturbation prediction. To test its scientific discovery capabilities, PIPA was used to investigate the interaction between the proteins of the endoplasmic reticulum (ER) and Dynamin 2 (DNM2). The identified hypo-PPI with dynamin mutation, a potential target for therapeutic intervention of centronuclear myopathy,  was experimentally validated in the wet lab. Furthermore, PIPA autonomously explored numerous PPI and mutation combinations to elucidate disease-related alterations in protein–protein interactions at the proteome scale. The scientific data used in this study has been developed into a benchmark named ER-MITO. As a novel framework for quantitatively evaluating agent capabilities on biologically meaningful tasks, ER-MITO benchmark moves beyond simplistic QA metrics to assess an agent's skill in (i) predicting novel inter-organelle PPIs and (ii) accurately retrieving and associating pathogenic mutations with proteins, further facilitating the evaluation of other AI systems and agents in terms of their capabilities for scientific discovery.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

蛋白质-蛋白质相互作用（PPI）在蛋白质功能及细胞通路形成中起关键作用，且与多种疾病进程密切相关，是治疗干预的重要靶点。然而，传统PPI识别、通路分析和疾病靶点筛选过程耗时费力，效率低下。现有方法缺乏自动化、系统化的分析框架，难以大规模发现新的PPI并预测病理突变带来的扰动效应。因此，论文旨在构建一个工具增强型智能体，自动化完成以PPI为中心的完整发现流程，辅助生物学家高效发现新PPI并评估病理突变的影响，加速疾病机制研究和靶点发现。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出**PIPA**（Protein Interaction Identification and Perturbation Analysis），一个工具增强的智能体。它通过结构化的**Plan-Select-Execute-Reflect循环**自动化PPI发现与分析流程。
- **关键技术细节**：
  - **计划（Plan）**：智能体根据用户问题（如“某蛋白与另一蛋白是否相互作用”）制定分步计划。
  - **选择（Select）**：从工具库中选择合适的工具（如数据库检索、结构预测、突变注释等）执行当前步骤。
  - **执行（Execute）**：调用所选工具获取数据，如从PPI数据库检索已知互作、利用AlphaFold等预测结构、注释病理突变信息。
  - **反思（Reflect）**：检查执行结果是否合理，若需要则调整计划或重新选择工具，形成闭环。
  - **集成任务**：包括自动数据库检索、蛋白质互作识别、病理突变注释、界面扰动预测等。
  - 实验验证了PIPA在**内质网（ER）与发动蛋白2（DNM2）互作**案例中的能力，识别出DNM2突变导致的hypo-PPI（弱相互作用），并经湿实验验证为中央核肌病的潜在治疗靶点。此外，PIPA还自主探索了多种PPI与突变组合，揭示蛋白质组尺度上疾病相关PPI的变化。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **数据集与场景**：
  - 主要研究场景为内质网（ER）与线粒体等细胞器之间的蛋白质互作，特别关注DNM2突变对ER-DNM2互作的影响。
  - 科学数据被整理成基准测试**ER-MITO**，用于评估智能体在生物意义任务上的能力。
- **Benchmark（ER-MITO）**：
  - 两个评估维度：
    1. 预测新型细胞器间PPI的能力；
    2. 精确检索并关联致病突变与蛋白质的能力。
  - 超越了简单的问答指标，侧重于科学发现能力。
- **对比方法**：论文未明确列出具体对比基线方法，但指出该benchmark可用于评估其他AI系统和智能体，暗示未来工作可在此基准上对比不同方法。

## 4. 资源与算力

论文摘要及元数据中**未明确说明**所使用的计算资源（如GPU型号、数量、训练时长等）。因此无法提供具体算力信息。推测训练和推理可能基于通用LLM工具增强框架，算力需求取决于所用基础模型规模。

## 5. 实验数量与充分性

- **实验数量**：论文主要描述了一个代表性案例（ER-DNM2互作及突变效应），并提到自主探索了多种PPI与突变组合，但未提供具体的实验组数或消融实验。
- **充分性与公平性**：
  - 单案例湿实验验证具有实证价值，但缺乏大规模系统对比实验（如不同PPI预测方法、不同智能体架构、不同突变注释工具等）。
  - 提出的ER-MITO基准可促进后续公平对比，但当前实验覆盖范围较窄，主要是概念验证性质。整体实验设计对于全面评估智能体能力而言不够充分，但作为初步工作可行。

## 6. 论文的主要结论与发现

- PIPA能够自动化完成PPI发现、通路分析和靶点筛选，有效辅助生物学家发现新PPI和预测病理突变效应。
- 在ER-DNM2案例中，成功识别出DNM2突变导致的hypo-PPI，并经湿实验验证为中央核肌病的潜在治疗靶点。
- PIPA具备在蛋白质组尺度自主探索PPI与突变组合的能力，揭示疾病相关的互作变化。
- 提出了ER-MITO基准，为定量评估AI智能体在生物学有意义任务上的科学发现能力提供了新框架。

## 7. 优点：方法或实验设计上的亮点

- **流程自动化**：通过Plan-Select-Execute-Reflect循环将复杂多步PPI分析集成到一个智能体中，减少人工干预。
- **工具增强**：整合数据库检索、结构预测、突变注释等多种工具，比单一模型更灵活实用。
- **湿实验验证**：不仅做计算预测，还进行了湿实验验证，增强结果可靠性。
- **新型基准**：ER-MITO设计针对科学发现能力而非简单QA，为领域评估提供了新标准。
- **可扩展性**：框架可应用于其他细胞器间或疾病相关的PPI研究。

## 8. 不足与局限

- **实验覆盖不足**：仅深入验证了一个案例，缺乏多案例、大规模系统性评估，泛化能力存疑。
- **对比方法缺失**：未与现有PPI预测方法、其他智能体或传统流水线进行定量比较，难以量化优势。
- **算力与资源未说明**：不利于复现和资源评估。
- **依赖外部工具与数据库**：智能体性能受限于所调用工具的质量和覆盖度（如数据库是否最新、结构预测精度等）。
- **基准规模较小**：ER-MITO可能仅针对特定细胞器互作，尚未覆盖更广泛的蛋白质组场景。
- **偏差风险**：若工具库或数据库存在偏向性（如某些蛋白研究更多），可能导致结果偏差。

（完）
