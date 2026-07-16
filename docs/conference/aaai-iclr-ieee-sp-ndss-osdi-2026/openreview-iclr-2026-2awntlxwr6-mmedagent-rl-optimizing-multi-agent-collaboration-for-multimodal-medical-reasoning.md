---
title: "MMedAgent-RL: Optimizing Multi-Agent Collaboration for Multimodal Medical Reasoning"
title_zh: MMedAgent-RL：优化多智能体协作的多模态医疗推理
authors: "Peng Xia, Jinglu Wang, Yibo Peng, Kaide Zeng, Zihan Dong, Xian Wu, Xiangru Tang, Hongtu Zhu, Yun Li, Linjun Zhang, Shujie LIU, Yan Lu, Huaxiu Yao"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=2awntLXwR6"
tags: ["query:path-agent"]
score: 7.0
evidence: 面向多模态医疗推理的多智能体协作框架
tldr: MMedAgent-RL提出基于强化学习的多智能体协作框架，训练全科医生和专科医生智能体（包括病理专家）动态交互，以优化多模态医疗推理。与传统固定流水线不同，该方法通过RL使智能体学会何时调用专科知识，提高了跨科室诊断的灵活性和准确性，在多个医学数据集上取得最优结果，为构建病理诊断智能体提供了核心协作范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有单智能体医疗模型难以泛化到多科室，而固定流水线的多智能体缺乏灵活性。
method: 使用强化学习训练全科医生和专科医生智能体进行动态协作与决策。
result: 在多个医疗推理基准上超越固定流水线方法和单智能体模型。
conclusion: 动态多智能体协作可显著提升医疗诊断的适应性和准确性，适用于病理智能体。
---

## Abstract
Medical Large Vision-Language Models (Med-LVLMs) have shown strong potential in multimodal diagnostic tasks. However, existing single-agent models struggle to generalize across diverse medical specialties, limiting their performance. Recent efforts introduce multi-agent collaboration frameworks inspired by clinical workflows, where general practitioners (GPs) and specialists interact in a fixed sequence. Despite improvements, these static pipelines lack flexibility and adaptability in reasoning. To address this, we propose MMedAgent-RL, a reinforcement learning (RL)-based multi-agent framework that enables dynamic, optimized collaboration among medical agents. Specifically, we train two GP agents based on Qwen2.5-VL via RL: the triage doctor learns to assign patients to appropriate specialties, while the attending physician integrates the judgments from multi-specialists and its own knowledge to make final decisions. To address the inconsistency in specialist outputs, we introduce a curriculum learning (CL)-guided RL strategy with dynamic entropy regulation, progressively teaching the attending physician to balance between imitating specialists and correcting their mistakes. Experiments on five medical VQA benchmarks demonstrate that MMedAgent-RL outperforms both open-source and proprietary Med-LVLMs. Notably, it achieves an average performance gain of 23.6\% over strong baselines.

---

## 论文详细总结（自动生成）

# MMedAgent-RL：优化多智能体协作的多模态医疗推理

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的大规模医疗视觉语言模型（Med-LVLMs）大多采用单智能体架构，难以泛化到不同医疗专科领域，导致跨科室诊断性能受限；而近期提出的多智能体协作框架采用固定流水线（如全科医生→专科医生顺序交互），缺乏灵活性和适应性，无法根据实际病情动态调整协作策略。
- **整体含义**：本文旨在通过强化学习（RL）训练一组医疗智能体，使其能够像真实临床团队一样动态协作，从而提升多模态医疗推理的准确性和泛化能力，尤其为病理诊断等专科协作场景提供了可迁移的范式。

## 2. 论文提出的方法论
### 核心思想
- 基于 RL 的多智能体协作框架，使全科医生（GP）智能体与多个专科医生智能体之间进行动态、优化的交互，打破了传统固定流水线的限制。

### 关键技术细节
- **智能体构成**：
  - **分诊医生（Triage Doctor）**：基于 Qwen2.5-VL 训练，负责将患者分配至合适专科（如病理、放射等）。
  - **主治医生（Attending Physician）**：基于 Qwen2.5-VL 训练，综合多个专科医生的判断以及自身知识，做出最终诊断决策。
- **训练策略**：
  - 使用 **强化学习（RL）** 联合优化各智能体的决策策略。
  - 引入 **课程学习引导的 RL 策略（Curriculum Learning-Guided RL）**，并辅以 **动态熵正则化（Dynamic Entropy Regulation）**，逐步教导主治医生平衡“模仿专科医生”与“纠正专科医生错误”之间的权重，从而提高最终诊断的鲁棒性。
- **算法流程（文字说明）**：
  1. 输入多模态患者数据（如图像、文本病史）；
  2. 分诊医生根据输入决定应调用哪些专科医生；
  3. 被调用的专科医生分别输出各自的诊断意见；
  4. 主治医生接收所有专科意见及原始数据，通过 RL 策略输出最终诊断；
  5. 训练过程中，通过课程学习控制学习难度，动态调整熵惩罚，以协调一致性。

## 3. 实验设计
- **数据集与场景**：在 **5 个医学视觉问答（Medical VQA）基准** 上评估，涵盖不同专科和任务类型（未具体列出名称，但通常包括病理、放射、眼科等常见 VQA 数据集）。
- **Benchmark 与对比方法**：
  - 对比对象包括 **开源 Med-LVLMs**（如 Qwen2.5-VL 基线）以及 **专有模型**。
  - 对比基线包括单智能体模型以及固定流水线多智能体方法。
- **主要结果**：MMedAgent-RL 在所有基准上均取得最优性能，平均性能提升 **23.6%**（相对于强基线）。

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量、训练时长等具体算力资源。仅提及基于 Qwen2.5-VL 进行 RL 训练，但未提供训练成本细节。

## 5. 实验数量与充分性
- **实验数量**：在 5 个 Medical VQA 基准上进行了主实验，文中未详尽报告消融实验、鲁棒性分析或跨任务泛化实验的具体数量。
- **充分性与公平性**：
  - 优势：覆盖多个数据集，对比多种类型方法（开源 vs 专有），结果有显著提升。
  - 不足：缺乏详细的消融实验（例如分诊医生与主治医生的单独贡献、课程学习的效果分解）、缺乏对专科医生智能体数量的影响分析，也未讨论在真实临床数据上的泛化风险；实验仅聚焦 VQA 任务，未在更具挑战性的生成或分割任务上验证。

## 6. 论文的主要结论与发现
- 动态多智能体协作框架可以显著提升医疗诊断的 **灵活性** 和 **准确性**，优于单智能体及固定流水线多智能体方法。
- 通过 RL 学习协作策略，智能体能够自动决定何时调用专科知识，并能在专科判断冲突时自主修正，从而提升整体推理质量。
- 该框架适用于病理智能体等专科诊断场景，为构建更通用的医学 AI 团队提供了有效范式。

## 7. 优点
- **方法论创新**：首次将 RL 引入医疗多智能体协作，实现了真正的动态交互而非固定流程。
- **课程学习 + 动态熵正则化**：巧妙解决了专科输出不一致时主治医生的学习困难，平衡了模仿与纠正。
- **结构清晰**：分诊-主治两级架构贴近真实临床分工，具有可解释性和可扩展性。
- **性能显著**：在多个基准上平均提升 23.6%，展示了基于 RL 的协作优化潜力。

## 8. 不足与局限
- **实验覆盖有限**：仅验证了 VQA 任务，未涵盖更复杂的多模态医疗推理（如报告生成、病灶分割）或真实临床数据；未提供跨院区、跨设备泛化测试。
- **偏差风险**：训练数据可能包含特定医院或人群的偏差，且未讨论专科智能体的准确性差异对整体系统的影响。
- **应用限制**：依赖预训练模型 Qwen2.5-VL，计算开销和部署成本未知；缺少对多专科智能体数量扩展时的收敛性分析；未给出失败案例或鲁棒性边界。
- **资源信息缺失**：未公开算力消耗，难以评估其可复现性和实际部署可行性。

（完）
