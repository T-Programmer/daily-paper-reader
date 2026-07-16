---
title: An AI Agent for Immune Receptor Fingerprint‑Based Diagnosis of Infection of Unknown Origin
title_zh: 基于免疫受体指纹的未知感染诊断AI智能体
authors: "Jiahao MA, Hongzong LI, Ye-Fan Hu, Jian-Dong Huang"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=15HYjY5ol7"
tags: ["query:path-agent"]
score: 4.0
evidence: 基于免疫受体指纹的诊断AI智能体，方法可迁移至病理诊断
tldr: 面对未知病原体感染诊断困境，本文提出一种AI智能体，通过读取免疫受体指纹推断抗原并定位病原。设计了多任务预训练Transformer模型和端到端临床智能体。方法虽面向感染，但agent框架和表示学习思路可直接迁移至病理诊断智能体开发。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 常规检测无法诊断未知感染，本文利用免疫受体指纹进行AI诊断。
method: 提出Transformer多序列表示学习模型及端到端临床智能体，进行抗原推断和病原定位。
result: 模型在六个任务上达到最佳或次佳性能，智能体具备临床实用性。
conclusion: 该智能体框架可扩展至病理诊断，为病理Agent提供方法参考。
---

## Abstract
When routine tests fail to find a pathogen, diagnosing infections of unknown origin stalls. We instead read the patient's immune response for AI-readable clues. We formalize a new machine learning task: inferring plausible epitopes directly from immune-receptor repertoires and localizing their pathogen sources. To address this problem, we introduce a Transformer-based multi-sequence novel representation-learning model that jointly models T-cell receptors, human leukocyte antigen , and antigenic peptides, and we pretrain it across six tasks; the model achieves best or second-best performance across all six tasks against strong baselines. Building on this, we develop an end-to-end, clinically oriented agent that operates in a perceive--plan--act loop, orchestrating epitope generation, HLA-personalized filtering, consistency checks, and retrieval, with clinician-in-the-loop threshold adaptation; when evidence conflicts, it performs calibrated abstention and logs an interpretable decision trace. End-to-end on clinical-style repertoires with diagnostic report generation, the agent outperforms discriminative-pairing and direct-retrieval baselines. Upon publication, we will release all code, models, and pathogen indices under a research license, together with de-identified evaluation data.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文元数据和摘要（注意：实际PDF内容为浏览器验证页面，因此以下分析完全基于您给出的元数据、摘要及tldr）生成的结构化中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当常规检测（如PCR、培养）无法识别病原体时，临床对“未知感染”的诊断陷入停滞。现有方法依赖已知病原体序列，难以应对新发、罕见或变异病原体。
- **整体含义**：提出一种全新的诊断范式——不直接检测病原体，而是“读取”患者免疫应答中留下的**免疫受体指纹**（T细胞受体和B细胞受体库），通过AI推断出致病抗原表位，并定位其病原来源。该方法有望突破传统病原检测的局限，实现无需先验知识的感染诊断。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将免疫受体库（TCR序列）、人类白细胞抗原（HLA）和抗原肽三者联合建模，利用Transformer架构进行多序列表示学习，再构建一个端到端的临床智能体，在“感知-规划-行动”循环中完成诊断。
- **关键技术细节**：
    - **多任务预训练Transformer模型**：同时建模TCR、HLA和抗原肽三个模态的序列，设计六个预训练任务（具体任务未在元数据中列举，推测包括配对预测、掩码重建等），以学习三者间的免疫结合规律。
    - **端到端临床智能体**：
        - 采用 `perceive-plan-act` 循环。
        - 步骤：**表位生成** → **HLA个性化过滤**（考虑患者特定的HLA类型） → **一致性检查**（确保生成的表位与免疫受体库逻辑一致） → **病原体检索**（与已知病原表位库比对）。
        - 支持“临床医生在环”（clinician-in-the-loop）的阈值自适应。
        - 当证据冲突时，执行 **校准后的弃权**（calibrated abstention）并记录可解释的决策轨迹（interpretable decision trace）。
- **公式/算法流程**（文字说明）：输入患者免疫受体库序列 → Transformer编码器提取多模态联合表示 → 解码器生成候选表位 → HLA模块过滤与患者MHC相容的表位 → 一致性验证模块校验表位-受体交互的合理性 → 检索模块在病原数据库中找到最匹配的病原体 → 若置信度不足则弃权并输出推理日志。

### 3. 实验设计：数据集/场景、基准、对比方法

- **数据集与场景**：
    - 训练数据：推测使用了公开的免疫受体-抗原配对数据（如VDJdb、IEDB等）。
    - 评估场景：**临床风格**的免疫受体库（模拟真实感染患者），并生成诊断报告。
- **基准（Benchmark）**：在**六个**不同的子任务上进行了评估（具体任务未列出，可能包括表位预测、TCR-肽结合预测、病原体分类等）。
- **对比方法**：与两类基线对比：
    - **判别式配对方法**（discriminative-pairing）：直接学习TCR-肽是否结合。
    - **直接检索方法**（direct-retrieval）：在已知数据库中进行序列比对检索。
- 结果：模型在所有六个任务上达到**最佳或次佳**性能，且端到端智能体在临床风格数据上优于上述基线。

### 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量或训练时长。仅承诺在发表后开源代码和模型。因此无法评估其算力消耗。

### 5. 实验数量与充分性

- **实验数量**：主要涉及**六项**子任务的对比实验 + 一项端到端临床智能体的整体评估（含诊断报告生成）。
- **充分性判断**：实验覆盖了模型本身的表示学习能力（多任务对比）以及下游临床应用（智能体管道）。对比方法包括两类主流范式，具有一定代表性。但缺少以下维度的验证：
    - 未提及在真实临床患者数据上的验证（仅说“临床风格”数据，可能为模拟或回顾性数据）。
    - 未进行跨病原类型（病毒、细菌、真菌）的消融分析。
    - 未详细报告假设检验或方差分析。
    - **总体尚可，但不算非常充分**，尤其缺乏真实临床前瞻性验证。

### 6. 论文的主要结论与发现

- **主要结论**：
    - 免疫受体指纹可以作为一种AI可读的诊断信号，用于未知感染的病原定位。
    - 所提出的多任务预训练Transformer模型能够有效学习TCR、HLA、抗原肽的联合表示，在多任务上达到领先性能。
    - 构建的端到端临床智能体具备临床实用性，能生成可解释的诊断报告，且在冲突时能合理弃权。
    - **该智能体框架具有可迁移性**，可推广至病理诊断等其他基于序列特征的医疗AI场景。

### 7. 优点

- **方法创新性**：首次将免疫受体指纹用于未知病原体诊断，提出表位生成-过滤-检索的端到端框架。
- **多任务学习策略**：通过六个预训练任务联合建模TCR-HLA-肽三元关系，提升了表征鲁棒性。
- **可解释性与临床安全性**：智能体具有可解释的决策轨迹，且在低置信度时主动弃权，符合临床对高风险决策的谨慎要求。
- **框架可迁移性**：tldr明确指出方法可迁移至病理诊断，为其他医学Agent开发提供范本。

### 8. 不足与局限

- **数据偏差风险**：训练数据主要来自公共数据库（可能偏向常见病原体），对罕见病或新发病原的表位覆盖可能不足。
- **临床验证不足**：仅在“临床风格”数据上评估，未提及真实世界前瞻性队列结果，实际诊断准确率未知。
- **算力与可复现性**：未披露训练资源，可能影响其他团队复现。虽然承诺开源，但依赖的病原索引文件可能包含版权或隐私问题。
- **应用限制**：智能体要求患者具有足够的免疫应答（如T细胞库多样性），对于免疫抑制患者可能失效。
- **方法论局限**：模型依赖HLA分型的准确性（需先验HLA信息），且表位生成可能产生大量假阳性，依赖后续过滤和检索，存在误差累积。

（完）
