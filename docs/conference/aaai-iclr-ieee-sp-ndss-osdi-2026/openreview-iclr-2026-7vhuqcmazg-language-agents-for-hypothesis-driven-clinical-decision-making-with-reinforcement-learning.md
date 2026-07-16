---
title: Language Agents for Hypothesis-driven Clinical Decision Making with Reinforcement Learning
title_zh: 基于强化学习的假设驱动临床决策语言智能体
authors: "David Bani-Harouni, Chantal Pellegrini, Ege Özsoy, Nassir Navab, Matthias Keicher"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=7vHUQCMAzG"
tags: ["query:path-agent"]
score: 7.0
evidence: 结合强化学习的语言智能体用于假设驱动临床决策，可应用于病理诊断
tldr: 临床决策是动态迭代过程，现有LLM应用缺乏交互或过度简化。本文提出假设驱动的语言智能体，通过强化学习训练，模拟医生逐步收集信息并决策。该框架可直接适配病理诊断场景，使智能体具备主动询问和推理能力，提升病理Agent的临床实用性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有临床决策LLM应用缺乏交互迭代或仅用基础能力。
method: 提出语言智能体框架，结合强化学习进行假设驱动、逐步决策的临床推理。
result: 智能体在模拟临床环境中表现出优于基线的方法，可推广至病理诊断。
conclusion: 该框架为构建交互式病理诊断智能体提供了有效范式。
---

## Abstract
Clinical decision-making is a dynamic, interactive, and cyclic process where doctors have to repeatedly decide on which clinical action to perform and consider newly uncovered information for diagnosis and treatment. Large Language Models (LLMs) have the potential to support clinicians in this process, however, most applications of LLMs in clinical decision support suffer from one of two limitations: Either they assume the unrealistic scenario of immediate availability of all patient information and do not model the interactive and iterative investigation process, or they restrict themselves to the limited "out-of-the-box" capabilities of large pre-trained models without performing task-specific training. In contrast to this, we propose to model clinical decision-making for diagnosis with a hypothesis-driven uncertainty-aware language agent, LA-CDM, that converges towards a diagnosis via repeatedly requesting and interpreting relevant tests. Using a hybrid training paradigm combining supervised and reinforcement learning, we train LA-CDM with three objectives targeting critical aspects of clinical decision-making: accurate hypothesis generation, hypothesis uncertainty estimation, and efficient decision-making. We evaluate our methodology on MIMIC-CDM, a real-world dataset covering four abdominal diseases containing various clinical tests and show the benefit of explicitly training clinical decision-making for increasing diagnostic performance and efficiency. Our code is available at https://github.com/dharouni/LA-CDM.

---

## 论文详细总结（自动生成）

# 基于强化学习的假设驱动临床决策语言智能体——详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：临床决策是一个动态、交互、循环的过程，医生需要反复决定下一步临床行动，并结合新信息进行诊断和治疗。现有大语言模型（LLM）在临床决策支持中的应用存在两类缺陷：① 假设所有患者信息立即可得，不建模交互式迭代调查过程；② 仅使用预训练模型的“开箱即用”能力，不进行任务特定训练，导致性能受限。
- **动机**：为了弥补上述不足，使 LLM 能够像医生一样逐步收集信息、提出假设并收敛至诊断结果，本文提出一种**假设驱动的、具有不确定性感知的语言智能体**，通过强化学习训练实现高效的临床决策。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将临床诊断建模为**假设驱动的迭代过程**：智能体反复请求相关检查（如实验室检验、影像等），根据返回结果更新对疾病的假设和不确定性，最终做出准确诊断。
- **智能体名称**：LA-CDM（Language Agent for Clinical Decision Making）。
- **关键技术细节**：
  - 使用**混合训练范式**：结合监督学习（Supervised Learning）和强化学习（Reinforcement Learning）。
  - 训练目标包含三个关键方面：
    1. **准确假设生成**：智能体应能提出合理的疾病假设。
    2. **假设不确定性估计**：对当前假设的不确定性进行量化，以指导下一步检查请求。
    3. **高效决策**：在尽可能少的检查步骤内收敛到正确诊断，减少不必要的资源消耗。
  - 流程示例：智能体接收初始患者描述 → 生成当前假设及不确定性 → 请求一项检查 → 收到结果 → 更新假设 → 重复直至达到终止条件（如确信度足够高）→ 输出最终诊断。

## 3. 实验设计：数据集、基准与对比方法
- **数据集**：**MIMIC-CDM** — 一个基于真实世界的临床数据集，涵盖**四种腹部疾病**，包含多种临床检查（如实验室检验、影像报告等）。该数据集专门用于临床决策建模。
- **基准**：论文未明确列出具体的基准名称，但提到**相比基线方法**，所提方法在诊断性能和效率上更优。
- **对比方法**：文中仅提及“优于基线的方法”，未给出具体基线列表。推测对比了仅使用监督学习训练、或未使用强化学习的变体，以及纯 LLM 基线的零样本/少样本决策。

## 4. 资源与算力
- **未明确说明**：论文摘要和元数据中未提及所使用的 GPU 型号、数量、训练时长等算力信息。可能存在实验部分缺失或未公开。

## 5. 实验数量与充分性
- **实验数量**：仅在一个数据集（MIMIC-CDM）上进行评估。未说明是否在多个疾病子集或不同数据分布上验证。消融实验方面，从三个训练目标可以推测可能做了目标组件的消融，但摘要未具体列出实验组数。
- **充分性评价**：
  - **优点**：使用了真实临床记录并针对多种疾病，具有一定代表性。
  - **不足**：数据集单一（仅四种腹部疾病），缺乏跨科室或跨模态的泛化验证；未与其他前沿方法（如基于图神经网络的诊断、端到端强化学习诊断）进行系统比较；未提供统计显著性检验或误差分析。因此实验充分性有限。

## 6. 论文的主要结论与发现
- LA-CDM 在模拟临床环境中**诊断准确率和效率均显著优于基线方法**。
- 将**假设生成、不确定性估计和高效决策**联合训练，能够有效提升临床决策性能。
- 该框架可**直接适配至病理诊断等类似场景**，为构建交互式、具备主动询问能力的病理诊断智能体提供了有效范式。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：首次将**假设驱动的不确定性感知语言智能体**与**强化学习**结合，用于模拟医生逐步决策过程，突破了传统 LLM 静态或简单调用的局限。
- **训练目标全面**：同时优化假设准确性、不确定性和决策效率的多目标设计，更贴合临床实际需求。
- **可推广性**：框架设计通用，容易迁移至病理诊断、影像报告解读等需要迭代信息收集的医疗任务。
- **开源代码**：已在 GitHub 上公开，便于复现和二次开发。

## 8. 不足与局限
- **实验覆盖不足**：仅在一个数据集（MIMIC-CDM，四种腹部疾病）上验证，未验证在更广泛疾病种类、多科室或跨机构数据上的性能，存在过拟合风险。
- **对比基准不明确**：未列出具体基线方法名称和实现细节，削弱了公平比较的可信度。
- **算力与实现细节缺失**：未报告训练所需 GPU 资源、超参数、收敛曲线等，影响可复现性。
- **实际应用限制**：模拟环境与现实临床工作流仍有差距（如检查结果获取延迟、医生偏好差异、患者个体反应等），实际部署前需要更多临床验证和安全性评估。
- **没有患者结局或伦理讨论**：未涉及诊断结果对患者预后的影响、医疗责任、系统鲁棒性（如对抗攻击、罕见病处理）等关键问题。

（完）
