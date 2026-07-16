---
title: A Survey of LLM-based Multi-agent Systems in Medicine
title_zh: 医学中基于LLM的多智能体系统综述
authors: "Yanna Lin, Shaojie Xu, Wenshuo Zhang, Yushi Sun, Zixin CHEN, Yanjie Zhang, Rui SHENG"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=MvlBFwAwK8"
tags: ["query:path-agent"]
score: 8.0
evidence: 医学中基于LLM的多智能体系统综述
tldr: 医学领域LLM多智能体系统缺乏结构化设计框架。本文全面综述现有系统，提出涵盖团队组成、医学知识增强和智能体交互三个维度的分类法。调研指向病理学智能体是重要方向，并讨论了人机协作等未来方向。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 医学多智能体系统设计缺乏结构化框架。
method: 系统综述现有医学多智能体系统，提出医学特定分类法。
result: 构建分类法并识别出未来研究方向，包括病理学智能体。
conclusion: 该综述为医学多智能体系统设计提供指南。
---

## Abstract
Large Language Model (LLM)-based multi-agent systems have shown great potential in supporting complex tasks in the medical domain, such as improving diagnostic accuracy and facilitating multidisciplinary collaboration. However, despite the advancement, there is a lack of structured frameworks to guide the design of these systems in medical problem-solving. In this paper, we conduct a comprehensive survey of existing medical multi-agent systems, and propose a medical-specific taxonomy along three key dimensions: team composition, medical knowledge augmentation, and agent interaction. We further outline several future research directions, such as incorporating human–AI collaboration to ensure that human expertise and multi-agent reasoning jointly address complex clinical tasks, designing and evaluating agent profiles, and developing self-evolving systems that adapt to evolving medical knowledge and rapidly changing clinical environments. In summary, our work provides a structured overview of medical multi-agent systems and highlights key opportunities to advance their research and practical deployment.

---

## 论文详细总结（自动生成）

好的，请查收基于提供的论文元数据和摘要生成的详细中文总结。

# 医学中基于LLM的多智能体系统综述 —— 总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：当前医学领域中基于大型语言模型（LLM）的多智能体系统虽然展现出巨大潜力，例如提高诊断准确性和促进多学科协作，但**缺乏一个结构化的设计框架**来指导这些系统在医学问题解决中的开发与评估。
- **研究背景**：随着LLM在医疗应用中的快速发展，多智能体系统能够模拟团队协作，处理复杂临床任务。然而，现有系统设计混乱、缺乏统一标准，阻碍了其可靠部署和临床转化。
- **目标**：通过全面综述现有医学多智能体系统，提出一个**医学特定的分类法**，并指出未来研究方向，从而为系统设计提供指南并推动实际部署。

## 2. 方法论
- **核心思想**：采用系统综述方法，对已发表的医学LLM多智能体系统进行结构化梳理，并构建一个**三维分类法**来捕捉系统设计的关键要素。
- **关键技术细节**：
  - 分类法的三个维度：
    1.  **团队组成（Team Composition）**：描述智能体的角色设定、专业分工和团队结构。
    2.  **医学知识增强（Medical Knowledge Augmentation）**：系统如何整合医学专业知识（如电子病历、医学文献、知识图谱）到智能体推理中。
    3.  **智能体交互（Agent Interaction）**：智能体之间的通信协议、协作机制和决策流程。
- **流程说明**：作者对相关文献进行筛选和归类，基于上述三个维度提取每个系统的设计特征，最终汇总形成结构化综述，并据此识别出尚待探索的研究空白。

## 3. 实验设计
- **数据集/场景**：未在摘要或元数据中明确说明。作为一篇综述，其“实验”通常是对现有文献的分析和分类，而非提出新的模型并在特定数据集上验证。文中提到的场景包括：**提高诊断准确性**、**促进多学科协作**等。
- **Benchmark**：未提及特定benchmark。本文的目的之一是提出分类框架，未来可以作为评估和设计系统的benchmark。
- **对比方法**：无；本文是综述性工作，对比了不同论文中的系统设计思路。

## 4. 资源与算力
- 文中**未提及**任何关于GPU型号、数量、训练时长等算力信息。作为综述论文，这属于正常情况；其资源消耗主要在于文献阅读和人工分析。

## 5. 实验数量与充分性
- 由于这是一篇**综述论文**，没有进行通常意义上的数值实验。其实验相当于**文献覆盖度**和分类的合理性。
- 从元数据看，该论文被标注为“ICLR-2026-Public”，且score为8.0，说明其工作得到了初步认可。但基于现有信息，无法判断其文献搜索范围是否全面、分类是否客观公平。元数据中提到“调研指向病理学智能体是重要方向”，显示综述覆盖了特定领域。

## 6. 主要结论与发现
- **构建了医学特定的多维分类法**：从团队组成、医学知识增强和智能体交互三个维度系统化组织现有系统。
- **识别出未来重要研究方向**：
  - **人机协作（Human-AI collaboration）**：确保人类专家与多智能体推理共同处理复杂临床任务。
  - **智能体画像设计与评估**：如何为不同医学专业设计有效的智能体角色。
  - **自演化系统**：系统能够适应不断更新的医学知识和快速变化的临床环境。
- **提供了结构化综述**：为医学多智能体系统的研究与实践部署指明了关键机遇。

## 7. 优点
- **填补结构空白**：首次为医学领域的LLM多智能体系统提供了系统性的分类框架，具有较高的实用价值和指导意义。
- **视角全面**：分类法覆盖了系统设计的核心维度（角色、知识、交互），有助于研究者快速定位问题。
- **前瞻性强**：提出的未来方向（如人机协作、自演化）切中了该领域发展的关键瓶颈和趋势。

## 8. 不足与局限
- **缺乏定量分析**：作为纯综述性质工作，没有进行任何实验验证或性能对比，无法提供方法优劣的量化证据。对每个系统的对比可能停留在定性描述，缺乏对不同设计选择效果的直接评估。
- **文献覆盖范围有限**：用户提供的仅包括摘要和元数据，无法判断其文献检索策略、纳入排除标准以及是否有偏差（如只关注特定年份或会议）。
- **应用限制**：分类法虽提出，但尚未经过临床部署的检验。在实际应用中，维度之间的权衡（例如知识增强的成本与交互效率）可能需要更深入的分析。
- **未阐述具体构建方法**：例如如何“设计并评估智能体画像”仅停留在方向层面，未给出具体示例或评估指标。

（完）
