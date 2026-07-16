---
title: "MedSimSearch: Sim2Real Agentic Learning for Medical Visual Reasoning"
title_zh: MedSimSearch：面向医学视觉推理的Sim2Real智能体学习
authors: "Tao Fang, Jiayan Guo, Mingkun Xu, Yuanzhe Zhao, Shangyang Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ggqNAGLQjR"
tags: ["query:path-agent"]
score: 6.0
evidence: 面向医学视觉推理的Sim2Real智能体学习，可应用于病理
tldr: 在真实临床环境中训练自主医学视觉推理agent因隐私和数据限制几乎不可行。本文提出MedSimSearch，基于Sim2Real智能体学习，利用生成式大模型构建高保真模拟检索环境，在安全的纯文本仿真中学习搜索和推理策略，避免了真实世界暴露。该框架可直接迁移到病理诊断agent的训练中，实现从仿真到真实场景的知识迁移。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实临床环境训练agent不可行，现有方法依赖不可行的多模态索引。
method: 利用生成式大模型构建仿真环境，在纯文本模拟中学习搜索和推理策略。
result: 在医学视觉推理任务上取得鲁棒的策略，无需真实暴露。
conclusion: 该框架为病理agent提供了一个安全有效的训练范式。
---

## Abstract
Developing autonomous agents for complex Medical Visual Reasoning is a critical goal, yet training them in real-world clinical settings is largely infeasible due to severe privacy, data, and safety constraints. While retrieval-augmented methods exist, they often depend on impractical multimodal indexing or fail to address the core challenge of learning interactive policies without real-world exposure.
To bridge this gap, we introduce MedSimSearch, a novel framework based on Sim2Real Agentic Learning. The core innovation lies in leveraging a generative large multimodal model (LMM) to create a high-fidelity simulated retrieval environment. Within this safe, text-only simulation, our agent learns a robust search and reasoning policy, eliminating the need for multimodal data indexing while preserving patient privacy.
To validate our approach, we evaluate the agent trained in simulation on realistic medical benchmarks using a curated private text corpus. Extensive experiments on VQAMed2019 and OmniMedVQA demonstrate that MedSimSearch significantly surpasses strong retrieval-augmented generation (RAG) baselines and shows enhanced robustness against hallucinations, paving a viable path for deploying trustworthy medical AI agents.

---

## 论文详细总结（自动生成）

# MedSimSearch：面向医学视觉推理的Sim2Real智能体学习——详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：在真实临床环境中训练自主医学视觉推理Agent几乎不可行——隐私、数据和安全性约束严重限制了真实世界的交互训练；现有的检索增强方法（RAG）通常依赖不切实际的多模态索引，或未能解决在无真实世界暴露条件下学习交互策略的核心挑战。
- **研究动机**：填补“无法在真实环境训练”与“现有方法依赖多模态数据标注”之间的空白，寻求一种安全、高效的Agent训练范式，使其能够学习搜索与推理策略，并迁移至真实临床任务。
- **整体含义**：提出一种基于Sim2Real（仿真到真实）的Agent学习框架，通过生成式大模型构建高保真模拟环境，使Agent在纯文本仿真中学习策略，避免隐私泄露和对多模态数据索引的依赖，为部署可信医学AI Agent开辟可行路径。

## 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：Sim2Real Agentic Learning——在安全的纯文本仿真模拟环境中训练Agent，再将其策略直接迁移到真实世界场景，实现从仿真到真实的知识泛化。
- **关键技术细节**：
  - **高保真模拟检索环境**：利用生成式大语言模型（LMM，即Large Multimodal Model）构建模拟环境，该环境能够基于纯文本描述模拟医学视觉检索和推理交互，无需真实的多模态图像和敏感数据。
  - **纯文本仿真**：Agent在仿真环境中以文本形式进行搜索和推理（如提出检索查询、接收返回的文本信息、做出诊断决策），完全避免对真实图像和多模态索引的依赖。
  - **策略学习**：Agent在仿真环境中通过强化学习或类似试错机制学习“搜索”和“推理”的联合策略，目标是最大化检索准确率和推理正确性，同时保持对幻觉的鲁棒性。
- **算法/流程说明**（文字描述）：
  1. 构建一个由LMM驱动的模拟器，该模拟器接收Agent的文本查询，生成模拟的上下文文本（如病理描述、检查结果等）。
  2. Agent在模拟环境中执行动作（如选择下一个问题、指定检索关键词）。
  3. 模拟器根据Agent动作返回观察（文本形式的检索结果列表）和奖励（如是否接近正确答案）。
  4. Agent更新策略，重复步骤2-3直至策略收敛。
  5. 将学到的策略直接部署到真实场景：用户输入视觉问题 → Agent以文本形式搜索私有文本语料库 → 返回答案。

## 3. 实验设计
- **使用的数据集/场景**：
  - **VQAMed2019**：医学视觉问答基准。
  - **OmniMedVQA**：综合性医学视觉问答基准。
- **Benchmark**：上述两个标准医学VQA数据集作为性能评估基准。
- **对比方法**：与强基线检索增强生成（RAG）方法进行对比，具体基线类型未在摘要中详列，但强调“significantly surpasses strong RAG baselines”。
- **评价指标**：未明确列出，通常涉及答案准确率、F1、Hallucination鲁棒性等。摘要特别指出“enhanced robustness against hallucinations”。

## 4. 资源与算力
- **资源与算力**：论文内容（摘要及元数据）中**未明确说明**使用的GPU型号、数量或训练时长。仅提及利用了生成式大模型（LMM），但未提供具体模型参数量或计算资源细节。

## 5. 实验数量与充分性
- **实验数量**：摘要仅提到两个医学VQA基准实验，未提及消融实验、参数敏感性分析、Sim2Real迁移效果定量测试等。实验组数较少（至少2组主要对比实验）。
- **充分性与公平性**：
  - **充分性**：实验覆盖了多个主流医学VQA数据集，但缺少消融研究（如不同模拟环境保真度的影响、不同Agent架构的对比）和跨领域泛化实验，整体实验不够全面。
  - **客观性与公平性**：对比了强RAG基线，但未明确基线具体实现和参数是否优化一致；未展示重复多次实验的统计显著性。结论初步可信，但证据力度有限。

## 6. 主要结论与发现
- **主要结论**：
  1. MedSimSearch框架能够使Agent在纯文本仿真中学习到鲁棒的搜索和推理策略，且无需真实世界暴露。
  2. 在VQAMed2019和OmniMedVQA上，仿真训练的Agent显著优于强RAG基线方法。
  3. 该方法对幻觉（hallucination）具有更强的鲁棒性，有助于构建更可信的医学AI Agent。
  4. 该框架为病理Agent的训练提供了一个安全有效的范式，可直接迁移到病理诊断等任务中。

## 7. 优点
- **创新性**：首次将Sim2Real学习范式引入医学视觉推理Agent训练，解决真实环境不可达的瓶颈。
- **隐私保护**：训练过程完全不使用真实患者数据或图像，极大降低隐私泄露和伦理风险。
- **无需多模态索引**：仅依赖纯文本交互，避免了对大规模多模态数据索引的依赖（现有方法通常不可行）。
- **抗幻觉能力**：通过仿真环境中的策略学习增强Agent对错误信息的抵抗能力。
- **可迁移性**：学到的策略可直接部署到真实临床场景中的私有文本语料库，实现零成本迁移。

## 8. 不足与局限
- **实验覆盖有限**：仅有两个医学VQA数据集，缺乏对更多类型医学推理任务（如放射报告生成、病理切片诊断）的验证；未包含消融实验或与端到端多模态模型的对比。
- **仿真保真度风险**：依赖生成式大模型构建仿真环境，若模拟器不能准确反映真实临床交互的复杂性（如视觉线索的模糊性、医生提问的顺序策略），策略迁移效果可能打折扣。
- **未涉及多模态维度**：Agent在仿真环境中仅处理文本，但真实医学推理往往需要同时分析图像和文本，该框架将视觉信息完全转化为文本描述，可能丢失重要视觉细节。
- **资源与可重复性**：论文未公开仿真环境构建细节、超参数设置和算力要求，增加了复现难度。
- **实验客观性**：仅对比RAG基线，未与最先进的医学VQA模型（如直接多模态推理模型）比较；未报告方差或置信区间，统计显著性不足。
- **应用限制**：该方法适用于已有结构化文本语料库的场景；对于完全无文本说明的原始图像（如病理切片），仍需额外的视觉转文本模块，可能引入噪音。

（完）
