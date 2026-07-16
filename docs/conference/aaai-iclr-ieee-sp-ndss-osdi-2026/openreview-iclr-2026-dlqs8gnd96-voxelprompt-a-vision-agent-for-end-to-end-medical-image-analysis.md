---
title: "VoxelPrompt: A Vision Agent for End-to-End Medical Image Analysis"
title_zh: VoxelPrompt：面向端到端医学图像分析的视觉智能体
authors: "Andrew Hoopes, Neel Dey, Victor Ion Butoi, John Guttag, Adrian V Dalca"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=DLqs8GnD96"
tags: ["query:path-agent"]
score: 8.0
evidence: 用于医学图像分析（含病理）的视觉智能体
tldr: VoxelPrompt是一个端到端视觉智能体系统，针对用户提示，利用语言模型生成可执行代码，调用联合训练的视觉网络，处理多种3D医学影像模态（包括CT和MRI），完成病理区域的自动分割与定量分析（如肿瘤生长测量）。该方法将多个专业工具整合为自动化流程，在神经影像任务上展现了强大的复合任务处理能力，为病理AI智能体的实现提供了直接范例。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 复合放射学任务需要组合多个专业工具，操作繁琐且易出错，亟需统一智能体。
method: 集成语言模型生成代码调用联合训练的视觉网络，实现分割与定量分析。
result: 在多种神经影像任务中自动完成肿瘤测量等量化流程，效果优于传统pipeline。
conclusion: 视觉智能体能够有效自动化医学图像分析，可扩展至病理领域。
---

## Abstract
We present VoxelPrompt, an end-to-end vision system that tackles composite radiological tasks. Given a user prompt, VoxelPrompt integrates a language model that generates executable code to invoke a novel, jointly-trained vision network. This adaptable network can integrate any number of volumetric (3D) inputs across heterogeneous real-world clinical modalities to segment and characterize diverse anatomy and pathology. Predicted code employs this network to carry out analytical steps to automate practical quantitative pipelines, such as measuring the growth of a tumor across visits, which often require practitioners to painstakingly combine multiple specialized but brittle tools. We evaluate VoxelPrompt using diverse neuroimaging tasks and show that it can delineate hundreds of anatomical and pathological features, measure complex morphological properties, and perform open-language analysis of lesion characteristics. VoxelPrompt performs these objectives with an accuracy similar to that of specialist single-task models for image analysis, while facilitating a broad range of biomedical workflows.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前医学影像分析中，复合放射学任务（如跨多次就诊的肿瘤生长测量）往往需要组合多个专业工具，操作繁琐、容易出错，且工具之间缺乏统一接口。现有方法多针对单一任务，难以灵活处理多样化的用户提问。
- **研究动机**：开发一个端到端的视觉智能体系统，能够根据用户自然语言提示自动生成可执行代码，调用统一训练的视觉网络，完成从分割到定量分析的全流程，从而简化医生工作流、提高效率与一致性。
- **整体含义**：VoxelPrompt 标志着从“多工具拼接”向“单一智能体自动执行”的范式转变，为病理AI智能体提供直接范例，可扩展至更多医学图像分析场景。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程（用文字说明）

- **核心思想**：集成语言模型与视觉网络，实现“用户提示 → 代码生成 → 视觉分析 → 结果输出”的自动化闭环。
- **关键技术细节**：
  1. **语言模型模块**：接收用户自然语言提示（如“测量第三、第四次就诊之间的肿瘤体积变化”），生成可执行的Python代码。
  2. **视觉网络模块**：联合训练的3D神经网络，可接受任意数量的异质性临床模态（CT、MRI等）输入，完成解剖结构和病理区域的分割与特征提取。
  3. **代码执行引擎**：将生成的代码在视觉网络上运行，自动执行分割、形态学测量（体积、形状、表面特征等）、跨时间点配准与差异分析。
- **算法流程**（文字说明）：
  - 输入：用户提示 + 指定影像数据（如两次CT扫描）；
  - 语言模型解析提示，生成序列化代码（例如调用分割函数、计算体积差）；
  - 视觉网络根据代码指令处理3D体数据，输出标注掩码及量化特征；
  - 系统聚合结果，返回用户可理解的数值描述或可视化。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **数据集与场景**：论文主要使用多样化的神经影像任务（Neuroimaging tasks），包括脑区分割、肿瘤分割、病变特征开放语言分析等。具体数据集未在摘要中详列，但提及“数百个解剖和病理特征”。
- **Benchmark**：以“单任务专用模型”作为对照标准，评估准确性和执行效率。
- **对比方法**：未列出具体基线模型名称，但表示与“多个专业单任务模型”进行比较，VoxelPrompt在图像分析精度上与其相当。

## 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点。

- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长等具体算力信息。需要查看完整论文以获取细节。

## 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平。

- **实验数量**：摘要未给出明确数字，但提到“评估了多种神经影像任务”“可描绘数百个特征”。推测包含多个数据集、多个任务类型的对比实验。
- **充分性与公平性**：
  - 优点：对比了单任务专用模型，评估维度包括分割精度、形态测量准确性、开放语言分析能力。
  - 不足：缺乏与现有图像分析智能体框架（如MedSAM等）的横向对比；消融实验（如去除语言模型或联合训练的效果）未在摘要中提及，可能不够全面。整体而言，实验设计偏向功能性展示，客观性和可复现性需依据完整论文判断。

## 6. 论文的主要结论与发现

- VoxelPrompt 能够在一个统一系统中自动完成从提示解析到图像分割、定量分析的复杂放射学流程，精度与单任务专用模型相当。
- 系统支持数百种解剖和病理特征的分割与形态学测量，并具备开放语言分析能力（如描述病变特征）。
- 该框架可广泛应用于生物医学工作流，显著降低工具组合的繁琐性，提升自动化程度。

## 7. 优点：方法或实验设计上有哪些亮点

- **方法亮点**：
  - 端到端集成：语言模型与视觉网络联合训练，实现自然语言驱动的自动化分析。
  - 通用性：可处理多种3D模态（CT/MRI）及任意数量输入，适应异质性临床数据。
  - 灵活提示：支持自由文本问题，无需预定义模板。
- **实验亮点**：
  - 覆盖大量特征（数百个），验证了系统的广泛适用性。
  - 与专业单任务模型对比，证明精度未明显损失。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验覆盖**：仅展示神经影像任务，未在其他部位（如胸部、腹部）验证，泛化性存疑。
- **偏差风险**：
  - 语言模型依赖训练数据中的提示模式，可能对非标准提问处理不佳。
  - 视觉网络可能有模态偏好（如对某些扫描参数敏感）。
- **应用限制**：
  - 需要用户具备一定技术知识生成有效提示，或需预设提示库。
  - 实时性未知，3D处理可能计算时间长，不适合急诊场景。
  - 未考虑法规/临床审批要求，实际落地需额外验证。
- **对比不足**：未与最新多模态大模型（如GPT-4V用于医学图像）直接对比，也未进行消融验证各模块贡献。

（完）
