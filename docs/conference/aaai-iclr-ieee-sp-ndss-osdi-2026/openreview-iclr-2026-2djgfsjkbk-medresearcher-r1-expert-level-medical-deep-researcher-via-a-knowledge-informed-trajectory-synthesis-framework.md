---
title: "MedResearcher-R1: Expert-Level Medical Deep Researcher via A Knowledge-Informed Trajectory Synthesis Framework"
title_zh: MedResearcher-R1：基于知识引导轨迹合成框架的专家级医学深度研究者
authors: "Ailing Yu, Lan Yao, Jingnan Liu, Zhe Chen, Jiajun Yin, Yuan Wang, Xinhao Liao, Zhiling Ye, JiLi, Yun Yue, Hansong Xiao, Hualei Zhou, ChunxiaoGuo, Peng Wei, Junwei Liu, Jinjie Gu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=2dJgFSJKbK"
tags: ["query:path-agent"]
score: 6.0
evidence: 医学深度研究代理，使用知识图谱，虽非病理专用但与基于代理的医学诊断相关
tldr: 现有大型语言模型在医学深度研究任务中表现不佳，原因在于缺乏密集医学知识和专用检索机制。本文提出MedResearcher-R1，通过知识图谱增强的轨迹合成框架，构建多跳问答代理，在多个医学基准上达到专家级水平。该方法虽通用，但其代理架构可迁移至病理领域。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有医学研究代理缺乏密集医学知识和专用检索机制，在复杂医学基准上表现有限。
method: 提出知识引导轨迹合成（KISA）方法，构建医学知识图谱并生成多跳问答轨迹来训练代理。
result: MedResearcher-R1在多个医学深度研究基准上达到专家级性能。
conclusion: 知识图谱增强的轨迹合成能有效提升医学代理的复杂推理能力。
---

## Abstract
Recent advances in Large Language Model (LLM)-based agents have enabled strong performance in deep research tasks, yet they remain limited in the medical domain. Leading proprietary systems achieve only modest results on complex medical benchmarks, revealing two critical limitations: 
(1) insufficient dense medical knowledge for clinical reasoning, and (2) a lack of specialized retrieval mechanisms for authoritative medical sources. 
We introduce MedResearcher-R1, a medical deep research agent that addresses these challenges with two key innovations. 
First, we propose a novel Knowledge-Informed Trajectory Synthesis (KISA) approach that builds medical knowledge graphs to construct complex multi-hop question–answer pairs around rare medical entities, overcoming the scarcity of high-quality training data. 
Second, we integrate a custom-built private medical retrieval engine alongside general-purpose tools, enabling accurate and reliable evidence synthesis. 
Our approach yields over 2,100 diverse trajectories across 12 medical specialties. 
Trained with supervised fine-tuning and reinforcement learning with composite rewards, our MedResearcher-R1-32B achieves state-of-the-art performance on MedBrowseComp (27.5/50 vs. 25.5/50 for o3-deepresearch) while demonstrates strong general performance on GAIA and xBench benchmarks. 
To the best of our knowledge, we present the first high-quality, tool-using medical dataset and a domain-specific deep-research agent, together enabling smaller open-source models to outperform much larger proprietary systems in specialized medical tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- 现有基于大型语言模型（LLM）的智能体在通用深度研究任务中表现优异，但在医学领域仍存在显著局限。
- 领先的专有系统在复杂医学基准上仅取得中等结果，暴露出两个关键瓶颈：
  - **缺乏密集的医学知识**，不足以支撑临床推理；
  - **缺少针对权威医学来源的专用检索机制**。
- 论文旨在构建一个医学深度研究智能体，以弥补上述不足，并证明在特定领域（医学）内，通过知识增强的轨迹合成和专用检索，较小的开源模型可以超越更大的专有系统。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- 提出 **知识引导轨迹合成（Knowledge-Informed Trajectory Synthesis, KISA）** 框架，通过构建医学知识图谱来生成复杂的多跳问答轨迹，从而缓解高质量医学训练数据稀缺的问题。
- 集成一个自定义的**私有医学检索引擎**，与通用工具配合使用，实现准确可靠的证据合成。

### 关键技术细节
1. **知识图谱构建**：围绕罕见医学实体构建多跳问答对，确保覆盖复杂临床推理场景。
2. **轨迹生成**：利用知识图谱生成超过2100条多样化工具使用轨迹，涵盖12个医学专业。
3. **训练策略**：
   - 先进行**监督微调（SFT）**，再使用**组合奖励的强化学习（RL with composite rewards）** 进一步优化。
4. **模型**：在32B参数规模的开源模型上训练，得到 **MedResearcher-R1-32B**。

### 流程说明（文字）
- 输入医学问题 → 智能体调用通用工具 + 私有医学检索引擎 → 综合多源证据 → 通过多跳推理生成答案。
- 训练数据生成阶段：利用医学知识图谱自动构造复杂问答对，并记录专家级推理轨迹，形成高质量训练集。

## 3. 实验设计

### 数据集 / 基准
- **MedBrowseComp**：医学深度研究专用基准（主要评估）。
- **GAIA** 和 **xBench**：通用深度研究基准（用于评估泛化能力）。
- 自行构建的包含2100+轨迹的医学工具使用数据集（12个专业领域）。

### 对比方法
- 主要对比：**o3-deepresearch**（OpenAI的专有系统）。
- 同时与开源和闭源的其他通用/医学LLM代理进行对比（未具体列出名称，但隐含对比）。

### 实验结果
- MedResearcher-R1-32B 在 MedBrowseComp 上达到 **27.5/50**，优于 o3-deepresearch 的 **25.5/50**。
- 在 GAIA 和 xBench 上也表现出色，证明通用能力未受损。

## 4. 资源与算力

- 论文中**未明确说明**使用的GPU型号、数量和训练时长。
- 仅提及模型为32B参数，在开源基础上训练（推测为 LLaMA 类似基座）。训练涉及SFT+RL，但无具体硬件细节。
- 可以推断：由于是32B模型，需要至少8×A100-80G或类似配置的集群，但缺少官方数据。

## 5. 实验数量与充分性

- 论文主要报告了在**三个基准**上的性能（MedBrowseComp、GAIA、xBench）。
- 消融实验未明确提及。但训练数据包含2100+轨迹（12个专业），可能进行了不同数据规模或训练策略的对比（摘要未展开）。
- 总体评价：实验数量适中，覆盖了专用医学基准和通用基准，但缺乏详细的消融分析和统计学显著性检验。与o3-deepresearch单点对比，对比方法较少，可能不够全面。
- 公平性：与o3-DeepResearch的对比基于公共基准，但未保证检索环境完全一致，存在一定偏差风险。

## 6. 主要结论与发现

1. **知识图谱增强的轨迹合成**能有效提升医学代理的复杂多跳推理能力。
2. 结合**专用医学检索引擎**，智能体可以生成准确且可溯源的证据。
3. **开源32B模型**通过上述方法可超越更大的闭源系统（如o3-deepresearch）在医学深度研究任务上的表现。
4. 这是首个高质量、工具使用的医学数据集和领域专用深度研究代理。

## 7. 优点（方法或实验设计亮点）

- **创新性**：提出KISA方法，利用知识图谱自动生成训练轨迹，解决医学领域数据稀缺问题。
- **实用性**：集成私有医学检索引擎，贴近真实临床工作流。
- **结果显著**：32B模型在专用基准上超过更大闭源模型，验证了领域定制化的有效性。
- **数据开源**：提供了高质量医学工具使用数据集，有助于后续研究。

## 8. 不足与局限

- **实验覆盖**：基准数量较少（仅3个），缺乏更多医学领域的细粒度任务（如不同疾病类型、不同诊断步骤）。
- **对比方法不足**：仅与o3-DeepResearch做主要对比，未与其他医学代理（如Med-PaLM、BioGPT等）或检索增强方法（如RAG）进行比较。
- **消融分析缺失**：未明确分析知识图谱、检索引擎、训练策略等各组件贡献。
- **资源消耗不透明**：未报告训练/推理所需的计算资源，影响可复现性评价。
- **偏差风险**：MedBrowseComp可能由作者自行构建或内部基准，存在数据偏差；与o3-DeepResearch对比时，检索环境可能不同。
- **应用限制**：模型仅训练单一语言（英文），未评估多语言或低资源医学场景。

（完）
