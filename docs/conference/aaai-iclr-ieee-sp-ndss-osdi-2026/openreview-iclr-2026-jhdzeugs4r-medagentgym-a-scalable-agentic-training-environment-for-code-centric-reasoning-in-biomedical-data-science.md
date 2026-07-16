---
title: "MedAgentGym: A Scalable Agentic Training Environment for Code-Centric Reasoning in Biomedical Data Science"
title_zh: MedAgentGym：面向生物医学数据科学中基于代码推理的可扩展智能体训练环境
authors: "Ran Xu, Yuchen Zhuang, Yishan Zhong, Yue Yu, Zifeng Wang, Xiangru Tang, Hang Wu, May Dongmei Wang, Peifeng Ruan, Donghan Yang, Tao Wang, Guanghua Xiao, Xin Liu, Carl Yang, Yang Xie, Wenqi Shi"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=jHDZEUgS4r"
tags: ["query:path-agent"]
score: 5.0
evidence: 用于生物医学推理的智能体训练环境
tldr: "MedAgentGym是一个可扩展的智能体训练环境，包含72,413个任务实例，涵盖129个生物医学类别（涉及病理学）。它提供可执行沙盒、交互反馈和可验证标注，用于训练基于代码的LLM智能体。该系统评测了29种LLM，揭示了开源与商业模型在生物医学数据科学上的性能差异，为开发病理诊断智能体提供了重要的训练基础设施和基准。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 生物医学数据科学任务复杂，缺乏训练LLM智能体的标准化环境。
method: 构建包含72k任务的沙盒环境，支持交互反馈和可扩展训练轨迹生成。
result: 29种LLM的评测显示商业模型显著优于开源模型，验证了环境有效性。
conclusion: 该环境为训练生物医学（包括病理）智能体提供了通用平台。
---

## Abstract
We introduce MedAgentGym, a scalable and interactive training environment designed to enhance coding-based biomedical reasoning capabilities in large language model (LLM) agents. MedAgentGym comprises 72,413 task instances across 129 categories derived from 12 authentic real-world biomedical scenarios. Tasks are encapsulated within executable sandbox environments, each featuring detailed task specifications, interactive feedback mechanisms, verifiable ground truth annotations, and scalable training trajectory generation. Extensive benchmarking of 29 LLMs reveals substantial performance disparities in biomedical data science between commercial and open-source LLMs. Leveraging efficient multi-threaded and multi-turn trajectory sampling in MedAgentGym, Med-Copilot achieves performance gains of +43.02% and +45.28% from offline and online reinforcement learning, respectively, demonstrating MedAgentGym as an effective training ground while establishing itself as a cost-effective, privacy-preserving alternative competitive with proprietary LLMs (gpt-4o). By offering a unified execution environment with a comprehensive benchmark and accessible, extensible training resources, MedAgentGym delivers an integrated platform to develop LLM-based coding assistants for advanced biomedical data science.

---

## 论文详细总结（自动生成）

# MedAgentGym 论文详细中文总结

## 1. 核心问题与整体含义
- **研究动机**：生物医学数据科学任务复杂多变，目前缺乏标准化、可扩展的训练环境来提升大语言模型（LLM）智能体在基于代码的生物医学推理能力。
- **整体含义**：通过构建包含大量真实场景任务的交互式沙盒环境，为训练和评估基于LLM的编码助手提供统一平台，推动低成本、隐私保护型的生物医学智能体发展。

## 2. 方法论
- **核心思想**：设计一个可扩展的智能体训练环境（MedAgentGym），将生物医学任务封装为可执行的沙盒单元，支持交互反馈、可验证标注和可扩展的训练轨迹生成。
- **关键技术细节**：
  - 包含 **72,413 个任务实例**，覆盖 **129 个类别**，源自 **12 个真实的生物医学场景**。
  - 每个任务配备详细的规格说明、交互反馈机制、可验证的真实标注。
  - 采用 **多线程和多轮轨迹采样** 策略高效收集训练数据。
  - 基于该环境训练 **Med-Copilot** 智能体，分别使用 **离线强化学习（offline RL）** 和 **在线强化学习（online RL）** 进行优化。
- **算法流程**（文字说明）：
  1. 从 12 个真实场景中提取并标准化 72k+ 任务。
  2. 将每个任务封装到独立沙盒中，提供初始代码模板和可验证答案。
  3. LLM 智能体在沙盒中执行代码，接收环境反馈（如执行结果、错误信息）。
  4. 根据反馈更新策略，通过 RL 方法（离线/在线）迭代优化智能体的编码推理能力。

## 3. 实验设计
- **数据集/场景**：使用 72,413 个任务实例，涵盖 129 个生物医学类别（包括病理学），来自 12 个真实世界生物医学场景。
- **Benchmark**：以该任务集作为统一的基准，评测 LLM 在生物医学数据科学中的编码推理表现。
- **对比方法**：
  - 对 **29 种 LLM**（包括商业模型和开源模型）进行基准测试，揭示性能差异。
  - 训练 **Med-Copilot** 智能体，与基线 LLM（如 gpt-4o）进行对比。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及使用的 GPU 型号、数量、训练时长等算力细节。仅提到“高效的多线程和多轮轨迹采样”，但未量化。

## 5. 实验数量与充分性
- **实验数量**：
  - 对 29 种 LLM 进行完整基准测试。
  - 训练 Med-Copilot 并评估离线 RL 和在线 RL 两种策略的性能提升（+43.02% 和 +45.28%）。
- **充分性评估**：
  - 覆盖模型种类较广（商业 vs 开源），但未列出具体模型名称，无法判断代表性。
  - 未提及消融实验（如不同任务类型、不同 RL 超参数等），实验设计相对基础。
  - 公平性方面：环境统一、任务标注可验证，但未讨论超参数调优是否对所有模型一致。

## 6. 主要结论与发现
- **性能差距显著**：商业模型在生物医学数据科学任务上明显优于开源模型。
- **MedAgentGym 有效性**：通过离线/在线 RL 训练，Med-Copilot 分别获得 **+43.02%** 和 **+45.28%** 的性能提升，证明该环境是有效的训练场。
- **成本与隐私优势**：Med-Copilot 成为具备成本效益和隐私保护能力的替代方案，性能与 gpt-4o 等专有模型竞争。

## 7. 优点
- **可扩展性**：72k+ 任务实例覆盖 129 个类别，支持持续添加新任务。
- **标准化沙盒**：可执行环境提供即时反馈和可验证标注，便于训练和评估。
- **高效采样**：多线程和多轮轨迹采样降低训练成本。
- **隐私保护**：无需外部 API 调用，可在本地环境完成训练，适合敏感生物医学数据。
- **综合平台**：集成了基准测试、训练和评估功能。

## 8. 不足与局限
- **实验覆盖**：未展示在真实临床部署场景中的表现，仅停留在环境内部评测。
- **偏差风险**：任务来源可能偏向特定生物医学子领域（如病理学），泛化性待验证。
- **资源信息缺失**：未报告算力消耗，难以评估实际训练成本。
- **方法局限**：仅依赖代码推理，未考虑文本理解或多模态输入（如医学影像）。
- **对比公平性**：未说明其他 LLM 是否也经过相同 RL 训练，可能只对比了零样本能力。

（完）
