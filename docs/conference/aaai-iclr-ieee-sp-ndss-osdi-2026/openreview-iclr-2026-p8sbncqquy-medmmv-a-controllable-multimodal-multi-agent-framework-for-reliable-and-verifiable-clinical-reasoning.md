---
title: "MedMMV: A Controllable Multimodal Multi-Agent Framework for Reliable and Verifiable Clinical Reasoning"
title_zh: MedMMV：一种可控的多模态多智能体框架，用于可靠且可验证的临床推理
authors: "Hongjun Liu, Yinghao Zhu, Yuhui Wang, Yitao Long, Zeyu Lai, Dennis Shasha, Lequan Yu, Chen Zhao"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=p8sBNCqQUY"
tags: ["query:path-agent"]
score: 7.0
evidence: 多模态多智能体框架用于可验证的临床推理，可应用于病理诊断
tldr: 多模态大语言模型在临床诊断中存在早期证据解释不稳定和幻觉问题，导致推理轨迹分支和全局不一致。本文提出MedMMV，一个可控的多模态多智能体框架，通过多样化短展开稳定推理，并生成可审计的决策流。该框架提升了临床推理的可靠性和可验证性，可直接支持病理诊断agent的构建，确保诊断过程透明可信。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有临床推理方法存在不稳定和幻觉问题，缺乏可审计性。
method: 提出多模态多智能体框架，通过多样化短展开和可审计决策流来稳定推理。
result: 在多个临床基准上实现了更可靠的推理性能，增强了可解释性。
conclusion: MedMMV为构建安全可靠的医学诊断agent（包括病理agent）提供了有效范式。
---

## Abstract
Recent progress in multimodal large language models (MLLMs) has demonstrated promising performance on medical benchmarks and in preliminary trials as clinical assistants. Yet, our pilot audit of diagnostic cases uncovers a critical failure mode: instability in early evidence interpretation precedes hallucination, creating branching reasoning trajectories that cascade into globally inconsistent conclusions. This highlights the need for clinical reasoning agents that constrain stochasticity and hallucination while producing auditable decision flows. We introduce MedMMV, a controllable multimodal multi-agent framework for reliable and verifiable clinical reasoning. MedMMV stabilizes reasoning through diversified short rollouts, grounds intermediate steps in a structured evidence graph under the supervision of a Hallucination Detector, and aggregates candidate paths with a Combined Uncertainty scorer. On six medical benchmarks, MedMMV improves accuracy by up to 12.7% and, more critically, demonstrates superior reliability. Blind physician evaluations confirm that MedMMV substantially increases reasoning truthfulness without sacrificing informational content. By controlling instability through a verifiable, multi-agent process, our framework provides a robust path toward deploying trustworthy AI systems in high-stakes domains like clinical decision support.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的多模态大语言模型（MLLMs）在临床诊断任务中表现不稳定，早期证据解释易出现幻觉，导致推理轨迹分叉并产生全局不一致的结论。这种不可控性使得模型难以在临床决策等高风险场景中安全部署。
- **研究动机**：需要一种能够约束随机性和幻觉、同时生成可审计决策流的临床推理智能体，以提高推理的可靠性和可验证性。
- **整体含义**：提出 MedMMV 框架，通过多智能体协作、多样化短展开和结构化证据图，实现可控的、可验证的临床推理，为构建可信的医学 AI 系统提供新范式。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将临床推理分解为多个可控步骤，利用多智能体协同机制稳定推理轨迹，并通过可审计的证据图记录中间决策，减少幻觉和全局不一致。
- **关键技术细节**：
  - **多样化短展开（Diversified Short Rollouts）**：对同一诊断案例生成多个短推理路径，避免长链推理的误差累积。
  - **结构化证据图（Structured Evidence Graph）**：在幻觉检测器（Hallucination Detector）监督下，将中间步骤的推理结果映射到证据图中，保证每一步都有依据。
  - **组合不确定性评分器（Combined Uncertainty Scorer）**：聚合所有候选推理路径，通过不确定性度量选择最可靠的最终结论。
  - **多智能体框架**：包含多个专用智能体（如证据提取、推理验证、幻觉检测等），各自负责不同子任务，通过协作完成整体推理。
- **公式/算法流程**（文字说明）：
  1. 输入多模态临床数据（图像、文本等）。
  2. 多智能体并行生成多个短推理路径（每个路径长度有限）。
  3. 每个路径的中间步骤被映射到证据图，并由幻觉检测器评估合理性。
  4. 对所有路径进行不确定性评分，选择得分最优的路径作为最终诊断结论。
  5. 输出可审计的决策流（包括证据图、路径选择理由等）。

### 3. 实验设计：数据集、Benchmark 与对比方法
- **数据集**：使用了六个医学基准数据集（具体名称未在摘要中列出，但元数据提到“six medical benchmarks”），涵盖不同模态和临床任务。
- **Benchmark**：包括准确率、可靠性（如推理一致性、幻觉率）等指标，并额外进行盲法医师评估（Blind physician evaluations）以衡量推理真实性。
- **对比方法**：与多种基线 MLLMs（如通用多模态模型、医学专用模型）进行比较，但具体方法名称未在摘要给出。

### 4. 资源与算力
- 论文中**未明确说明**使用的 GPU 型号、数量或训练时长。仅提及模型设计和实验设置，但未涉及具体算力消耗。若需进一步了解，需查阅完整原论文。

### 5. 实验数量与充分性
- **实验数量**：覆盖六个不同医学基准，并包含盲法医师评估。此外应有消融实验（如作用多样化短展开、幻觉检测器等模块的贡献），但摘要中未详细列出数量。
- **充分性**：实验设计较为全面，既采用自动指标也结合人工评估（医师盲审），能较好验证推理可靠性和真实性。但缺少对跨中心、不同疾病类型的泛化性测试，可能受限于公开基准的规模。

### 6. 论文的主要结论与发现
- MedMMV 在六个基准上准确率最高提升 12.7%，同时展现出更优的可靠性（推理稳定性、低幻觉率）。
- 盲法医师评估表明，MedMMV 在保持信息量的同时显著提高了推理的真实性（truthfulness）。
- 可控的多智能体过程能够有效抑制早期证据解释的不稳定性，为高安全性临床决策支持提供了可行路径。

### 7. 优点：方法或实验设计上的亮点
- **方法论上**：
  - 将推理分解为短展开并引入结构化证据图，使得每一步都可审计，增强了透明度和可信度。
  - 多智能体协作+幻觉检测器的设计，既实现了稳定性又保留了多模态信息的丰富性。
- **实验设计上**：
  - 不仅使用自动指标，还引入盲法医师评估，更贴近真实临床场景。
  - 对比了准确率和可靠性双重指标，突出“可信”这一核心贡献。

### 8. 不足与局限
- **实验覆盖**：仅报告了六个公开基准的结果，未涉及真实临床环境、罕见病或多中心数据，泛化性有待验证。
- **偏差风险**：可能依赖于特定训练集或数据分布，对噪声或未见过的模态组合鲁棒性未知。
- **应用限制**：框架复杂度较高，多智能体协作可能增加推理延迟；幻觉检测器的准确性本身也可能成为新瓶颈。
- **资源细节缺失**：未提供计算资源需求，难以评估落地成本。

（完）
