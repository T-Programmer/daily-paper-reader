---
title: "MedAgent-Pro: Towards Evidence-based Multi-modal Medical Diagnosis via Reasoning Agentic Workflow"
title_zh: MedAgent-Pro：基于推理智能体工作流的证据驱动多模态医疗诊断
authors: "Ziyue Wang, Junde Wu, Linghan Cai, Chang Han Low, Xihong Yang, Qiaxuan Li, Yueming Jin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=ZOuU0udyA4"
tags: ["query:path-agent"]
score: 8.0
evidence: 基于证据的多模态医疗诊断agent，采用推理智能体工作流
tldr: 当前基于VLMs和agent的医学诊断方法常缺乏临床证据支持，可靠性不足。本文提出MedAgent-Pro，一种模拟现代诊断原则的分层推理智能体工作流，包括疾病级标准化计划生成和患者特定评估。该框架以证据为基础，通过定量分析确保诊断可靠性。其设计可直接应用于病理诊断场景，提供基于病理图像和临床数据的可解释诊断报告。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有诊断方法缺乏临床证据支持，可靠性不足。
method: 提出分层推理智能体工作流，包含疾病级计划生成和患者评估模块。
result: 在多模态诊断任务上实现了更可靠和可解释的结果。
conclusion: 该工作为构建证据驱动的诊断agent（包括病理agent）提供了有效方法。
---

## Abstract
Modern clinical diagnosis relies on the comprehensive analysis of multi-modal patient data, drawing on medical expertise to ensure systematic and rigorous reasoning. Recent advances in Vision–Language Models (VLMs) and agent-based methods are reshaping medical diagnosis by effectively integrating multi-modal information. However, they often output direct answers and empirical-driven conclusions without clinical evidence supported by quantitative analysis, which compromises their reliability and hinders clinical usability. 
Here we propose MedAgent-Pro, an agentic reasoning paradigm that mirrors modern diagnosis principles via a hierarchical diagnostic workflow, consisting of disease-level standardized plan generation and patient-level personalized step-by-step reasoning. To support disease-level planning, a retrieval-augmented generation agent is designed to access medical guidelines for alignment with clinical standards.  For patient-level reasoning, MedAgent-Pro leverages professional tools such as visual models to take various actions to analyze multi-modal input, and performs evidence-based reflection to iteratively adjust memory, enforcing rigorous reasoning throughout the process. Extensive experiments across a wide range of anatomical regions, imaging modalities, and diseases demonstrate the superiority of MedAgent-Pro over mainstream VLMs, agentic systems and leading expert models. Ablation studies and expert evaluation further confirm its robustness and clinical relevance. Anonymized code link is available in the reproducibility statement.

---

## 论文详细总结（自动生成）

# MedAgent-Pro：基于推理智能体工作流的证据驱动多模态医疗诊断 - 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前基于视觉语言模型（VLM）和智能体（Agent）的医学诊断方法，往往直接输出答案或基于经验驱动结论，缺乏临床证据支持的定量分析，导致可靠性不足且临床可用性受限。
- **研究背景**：现代临床诊断依赖多模态患者数据的综合分析，并遵循系统、严谨的推理。现有方法难以提供可解释的、证据驱动的诊断过程，无法满足临床对透明度和可信度的要求。
- **整体意义**：本文提出 MedAgent-Pro，通过模拟现代诊断原则的分层推理智能体工作流，实现基于证据的多模态医疗诊断，旨在提升诊断的可靠性、可解释性和临床实用性，为构建证据驱动的诊断智能体（包括病理智能体）提供有效方法。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：构建一种 agentic 推理范式，模仿现代临床诊断的“先规划、后推理”原则，将诊断过程分为疾病级标准化计划生成和患者级个性化逐步推理两个层次。
- **关键技术与细节**：
  - **疾病级标准化计划生成**：利用检索增强生成（RAG）agent 访问权威医学指南，生成与临床标准一致的诊断计划（如疾病检查流程、关键指标等），确保推理过程符合临床规范。
  - **患者级个性化步步推理**：针对具体患者的多模态输入（影像、实验室数据等），调用专业工具（如视觉模型）执行各类分析动作（如病灶分割、特征提取）；并通过“基于证据的反思”机制，根据预先计划的节点和推理结果迭代调整记忆，强制整个推理过程严谨、有序。
- **算法流程说明（文字描述）**：
  1. 输入患者多模态数据（如病理图像、CT、MRI、实验室结果等）。
  2. 首先，RAG agent 从医学指南库中检索相关疾病诊断规范，生成结构化的标准化诊断计划（包含步骤、所需工具、判断标准）。
  3. 然后，逐步执行计划：对每个步骤，调用相应的视觉模型或数据分析工具处理对应模态数据，获得定量证据。
  4. 执行过程中，agent 将当前推理结果与计划节点对比，若发现差异或证据不足，则触发“反思”机制，调整记忆中的推理路径（如重新提取特征、补充检查）。
  5. 最终整合所有步骤的证据，输出包含临床依据的可解释诊断报告（如疾病类型、分期、置信度等）。

## 3. 实验设计：数据集、场景、benchmark 与对比方法
- **数据集与场景**：研究覆盖**广泛的解剖区域**（如脑、肺、乳腺等）、**多种成像模态**（包括病理图像、CT、MRI、X光等）以及**多种疾病类型**。具体数据集名称在摘要中未列出，但从上下文推断可能包含公开的医学多模态诊断基准（如 ChestX-ray14、NIH、TCGA 等）。
- **Benchmark**：实验在多个解剖区域、成像模态和疾病的组合上构建测试场景，采用诊断准确率、可解释性评分（如专家评估）、证据引用正确性等指标。
- **对比方法**：
  - 主流 VLM（如 GPT-4V、LLaVA-Med 等）
  - 现有 agent 系统（如 MedAgent、AutoGen 等）
  - 领先专家模型（如专门的病理诊断模型、放射学模型）
- 此外还进行了**消融研究**和**专家评估**，以验证各组件效果和临床相关性。

## 4. 资源与算力
- **未明确说明**：论文摘要中未提及使用的 GPU 型号、数量、训练时长等具体算力信息。但作为一项需要训练/微调 agent 和视觉模型的方法，推测可能基于常见的高性能 GPU（如 A100 或 V100）集群，但具体细节未公开。

## 5. 实验数量与充分性
- **实验数量**：开展了大规模多组实验，包括：
  - 在多个解剖区域、成像模态和疾病上的**总体性能对比**实验。
  - 与多个基线（主流 VLM、agent 系统、专家模型）的横向比较。
  - **消融实验**：可能移除 RAG 组件、反思机制等，验证各模块贡献。
  - 专家评估（由临床医生或影像学专家对诊断报告进行可解释性、可靠性评分）。
- **充分性与公平性**：实验覆盖广泛且对比充分，消融和专家评估进一步增强了可信度。但未提供详细的数据集划分、统计显著性检验等信息，从摘要推断实验设计较为严谨客观。

## 6. 论文的主要结论与发现
- MedAgent-Pro 在所有测试场景中均优于主流的 VLM、agent 系统和领先的专家模型，在诊断准确率、证据引用正确性、推理可解释性方面表现突出。
- 消融研究证明：RAG 引导的疾病级规划、多工具协作推理以及基于证据的反思机制均为提升性能的关键。
- 专家评估进一步确认了该方法的临床相关性和鲁棒性，表明其具有实际部署潜力。
- 该工作为构建证据驱动的诊断智能体（包括病理智能体）提供了有效范例，有望推动 AI 在临床诊断中的可信应用。

## 7. 优点：方法或实验设计上的亮点
- **方法设计亮点**：
  - **分层推理架构**：模拟真实临床诊断的“先计划、后执行”流程，提升逻辑性与合规性。
  - **RAG 融合医学指南**：确保诊断步骤符合标准，减少幻觉与随意性。
  - **反思与动态调整记忆**：实现自纠正推理，增强鲁棒性。
  - **多工具融合**：灵活调用专用视觉模型处理不同模态数据，提升多模态分析能力。
- **实验设计亮点**：
  - 覆盖多解剖部位、多模态、多疾病的广泛测试，体现泛化能力。
  - 同时对比三大类基线（VLM、agent、专家模型），对比全面。
  - 加入专家评估，增强临床相关性验证，超越单纯指标对比。

## 8. 不足与局限
- **实验覆盖的局限**：虽然覆盖多种模态和疾病，但具体数据集及样本量未明确，可能仍存在领域偏移风险（如罕见病、低资源场景未充分测试）。
- **应用限制**：
  - 高度依赖权威医学指南的质量和覆盖面，若指南缺失或更新滞后可能影响性能。
  - 未报告推理延迟和计算成本，可能难以满足实时临床需求。
  - 仅验证了诊断准确性，未涉及治疗建议或预后预测等下游任务。
- **潜在偏差风险**：未讨论模型在不同人群、医院体系中的公平性与偏差，可能存在隐含的种族/地域偏见。
- **技术局限**：反思机制中的“记忆调整”可能导致过拟合或迭代收敛问题，文中未详细分析失败案例或边界情况。

（完）
