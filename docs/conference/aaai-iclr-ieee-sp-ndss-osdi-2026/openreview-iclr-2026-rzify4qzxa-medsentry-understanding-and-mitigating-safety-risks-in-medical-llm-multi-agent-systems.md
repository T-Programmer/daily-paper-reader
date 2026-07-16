---
title: "MedSentry: Understanding and Mitigating Safety Risks in Medical LLM Multi-Agent Systems"
title_zh: MedSentry：理解并缓解医疗大语言模型多智能体系统中的安全风险
authors: "Kai Chen, Taihang Zhen, Hewei Wang, Kailai Liu, Xinfeng Li, Jing Huo, Tianpei Yang, Jinfeng Xu, Wei Dong, Yang Gao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=RZIfy4Qzxa"
tags: ["query:path-agent"]
score: 6.0
evidence: 医疗多智能体安全评估框架，可用于病理agent
tldr: 当前医疗大语言模型多智能体系统的安全性研究不足，尤其是在病理诊断等关键场景中。本文提出MedSentry，一种端到端的攻击-防御评估工作流，系统分析了四种多智能体拓扑结构在面对恶意攻击时的行为差异。通过构建包含5000个对抗性医疗提示的数据集，揭示了不同架构在信息污染和鲁棒决策方面的脆弱性。该工作为构建安全的病理agent提供了重要的评估方法和设计指导。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 医疗大语言模型多智能体系统在应用中面临严重安全风险，缺乏系统评估方法。
method: 提出端到端攻击-防御评估工作流，分析四种多智能体拓扑结构在攻击下的行为。
result: 揭示了不同架构在信息污染和鲁棒决策上的脆弱性差异。
conclusion: 该工作为医疗多智能体系统安全提供了评估基准和设计启示，可推广至病理agent领域。
---

## Abstract
As large language models are increasingly adopted in healthcare, ensuring their safety is critical, particularly in collaborative multi-agent settings. This paper develops an end-to-end attack–defense evaluation workflow to systematically analyze how four representative multi-agent topologies (Layers, SharedPool, Centralized, and Decentralized) behave under attacks from ``dark-personality'' agents. To support the evaluation, we curate MedSentry, a data resource containing 5,000 adversarial medical prompts that span 25 threat topics and 100 subtopics. Our study reveals critical differences in how these architectures handle information contamination and maintain robust decision-making, exposing their underlying vulnerability mechanisms. For example, SharedPool is highly susceptible due to open information sharing, whereas Decentralized exhibits stronger resilience owing to inherent redundancy and isolation. To mitigate these risks, we propose a personality-scale detection and correction mechanism that identifies and rehabilitates malicious agents, restoring safety to near-baseline levels. Taken together, MedSentry provides a rigorous evaluation framework alongside actionable defense strategies, offering guidance for the design of safer LLM-based multi-agent systems in medical contexts.

---

## 论文详细总结（自动生成）

# MedSentry：理解并缓解医疗大语言模型多智能体系统中的安全风险

## 1. 核心问题与整体含义（研究动机和背景）

大语言模型（LLM）在医疗领域的应用日益广泛，但安全性问题至关重要，尤其是在多智能体协作场景中。现有研究缺乏对医疗多智能体系统在对抗攻击下安全性的系统评估。本文旨在填补这一空白，系统分析不同多智能体拓扑结构在面对“暗人格”智能体攻击时的行为差异，并设计缓解策略，为构建安全的医疗大语言模型多智能体系统提供理论指导和实践框架。

## 2. 论文提出的方法论

- **核心思想**：提出端到端的攻击-防御评估工作流，覆盖从攻击生成、多智能体系统执行到防御缓解的完整过程。
- **关键技术细节**：
  - 设计四种代表性多智能体拓扑结构：**Layers**（层级结构）、**SharedPool**（共享池）、**Centralized**（中心化）、**Decentralized**（去中心化）。
  - 构建包含 **5,000个对抗性医疗提示** 的数据集（MedSentry），涵盖25个威胁主题和100个子主题，用于模拟恶意攻击。
  - 提出**人格尺度检测与修正机制**：通过检测恶意智能体的异常行为（如偏离任务目标、输出有害信息）并实施“修正”操作（重置或重新训练），将系统安全性恢复至接近基线水平。
- **算法/流程说明**（文字描述）：
  1. 生成对抗性医疗提示数据（MedSentry数据集）。
  2. 将对抗性提示输入四种拓扑结构的多智能体系统中，其中部分智能体被设定为“暗人格”（即故意输出错误或有害信息）。
  3. 监控各拓扑结构在信息污染和决策鲁棒性方面的表现，记录脆弱性。
  4. 应用人格尺度检测机制识别恶意智能体，并通过修正机制恢复其正常行为。
  5. 评估修正后的系统安全水平。

## 3. 实验设计

- **数据集/场景**：
  - 使用自建的 **MedSentry数据集**（5000个对抗性医疗提示，涵盖25个威胁主题和100个子主题）。
  - 场景为医疗多智能体协作环境，可能包括诊断、用药建议、患者咨询等医疗任务。
- **Benchmark**：
  - 无现有公开基准，本文将MedSentry本身作为评估框架和基准。
- **对比方法**：
  - 对比四种拓扑结构（Layers、SharedPool、Centralized、Decentralized）在无攻击、有攻击以及攻击+防御三种条件下的安全性表现。

## 4. 资源与算力

论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。可能由于论文重点在评估框架而非训练成本，故未提供具体算力细节。

## 5. 实验数量与充分性

- **实验数量**：至少涉及三种条件（无攻击、攻击、攻击+防御）×四种拓扑结构×5000个对抗提示，因此实验组数可观。但具体消融实验、超参数敏感性分析等细节未在摘要中体现。
- **充分性评价**：从摘要看，实验覆盖了多种拓扑结构和广泛威胁类别，具有一定充分性。然而，缺少模型规模、成本、真实临床环境等变量，且仅基于对抗提示而非真实攻击场景，可能影响泛化性。整体而言，实验设计客观，但充分性有待验证（需阅读全文）。

## 6. 论文的主要结论与发现

- **关键发现**：
  - **SharedPool拓扑结构**因信息开放共享，极易受到攻击（恶意信息快速传播）。
  - **Decentralized拓扑结构**由于内在的冗余和隔离性，展现出更强的鲁棒性。
  - 提出的**人格尺度检测与修正机制**能将系统安全性恢复至接近基线水平。
- 不同架构在信息污染和鲁棒决策方面存在脆性差异，揭示了底层脆弱性机制。

## 7. 优点

- **方法层面**：首次提出端到端的攻击-防御评估工作流，专门针对医疗多智能体系统，为相关安全研究提供了可复用的框架。
- **数据层面**：构建了大规模、细粒度的对抗性医疗提示数据集（MedSentry），覆盖25个主题和100个子主题，为后续研究奠定基础。
- **分析层面**：系统对比四种常见拓扑结构，揭示不同架构的脆弱性差异，并提供实际缓解方案，兼具理论与实践价值。
- **伦理价值**：强调医疗AI安全，具有重要的社会意义。

## 8. 不足与局限

- **实验覆盖不足**：仅考察了四种固定拓扑结构，未覆盖动态拓扑、异构智能体、多层协作等复杂场景。
- **偏差风险**：对抗提示由人工生成，可能无法完全模拟真实攻击行为，存在分布偏移风险。
- **应用限制**：
  - 仅在模拟环境中验证，未在真实临床系统或生产环境中测试。
  - 未讨论防御机制的计算开销及对正常性能的影响。
  - 未考虑模型规模、训练数据来源等可能影响安全性的因素。
- **资源信息缺失**：缺乏算力成本对比，难以评估方案的可部署性。

（完）
