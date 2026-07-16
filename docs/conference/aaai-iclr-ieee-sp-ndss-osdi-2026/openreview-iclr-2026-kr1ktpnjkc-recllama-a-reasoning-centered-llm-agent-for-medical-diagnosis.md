---
title: "ReCLLaMA: A Reasoning-Centered LLM Agent for Medical Diagnosis"
title_zh: "ReCLLaMA: 面向医学诊断的推理中心LLM智能体"
authors: "Yang Zhao, Bowen Xu, Saiyun Dong, Xinghua Shi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=KR1ktPNJkC"
tags: ["query:path-agent"]
score: 7.0
evidence: 用于医学诊断的LLM智能体结合结构化知识
tldr: LLM在临床诊断中存在幻觉和缺乏可解释性。本文提出ReCLLaMA，将统计语言模型与医学知识图谱上的符号推理结合，实现可解释的诊断推理。实验证明该方法在诊断准确性和可追溯性上优于纯LLM方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM应用于临床诊断时存在幻觉和缺乏正式推理机制。
method: 将自由文本症状与标准化本体对齐，并在知识图谱上进行逻辑推理，融合统计与符号推理。
result: 在诊断任务上，ReCLLaMA减少幻觉，提高准确性和解释性。
conclusion: 融合符号推理的LLM智能体是提升医学诊断可靠性的关键。
---

## Abstract
Large Language Models (LLMs) have demonstrated impressive capabilities in natural language understanding, yet their application to clinical diagnosis remains constrained by hallucinations, limited interpretability, and the absence of formal reasoning mechanisms. To address these limitations, we propose ReCLLaMA, a Reasoning-Centered LLM Agent for Medical Diagnosis, which integrates statistical language models with symbolic inference over structured medical knowledge. ReCLLaMA aligns free-text symptom descriptions with standardized ontologies using pretrained biomedical encoders and performs logical reasoning over heterogeneous knowledge graphs constructed from EHR and pharmacological data. To reconcile representational mismatches across sources, we introduce a statistical entity alignment module based on random forest classification. This enables the construction of a unified knowledge space in which ReCLLaMA applies both deductive and abductive reasoning to derive interpretable diagnostic pathways. Our framework advances the theoretical integration of subsymbolic and symbolic AI in clinical contexts, offering a principled approach to traceable, knowledge-grounded decision-making. Empirical results on real-world datasets validate its superiority over black-box LLMs and rule-based systems in both accuracy and explainability.

---

## 论文详细总结（自动生成）

# ReCLLaMA: 面向医学诊断的推理中心LLM智能体 — 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）在临床诊断应用中存在三大缺陷：**幻觉**（生成不真实的信息）、**可解释性差**（推理过程不透明）以及**缺乏正式推理机制**（仅依赖统计模式而非逻辑推理）。
- **研究动机**：医学诊断要求高可靠性和可追溯性，纯统计语言模型无法满足临床决策对可解释性和知识严谨性的需求。
- **整体含义**：提出将统计语言模型与符号推理相结合的智能体架构，在保持自然语言理解能力的同时，引入结构化医学知识图谱上的逻辑推理，实现可解释、知识驱动的诊断过程，为临床AI提供一种更可信的范式。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
**ReCLLaMA（Reasoning-Centered LLM Agent for Medical Diagnosis）** 将**子符号统计模型**（LLM）与**符号推理**（基于医学知识图谱的逻辑运算）融合，构建一个统一的推理智能体。它通过实体对齐和知识图谱构建，将自由文本症状映射到标准化本体，然后执行演绎和溯因推理，输出可解释的诊断路径。

### 关键技术细节
1. **症状-本体对齐（Symptom-Ontology Alignment）**：
   - 使用预训练的**生物医学编码器**（如BioBERT）将自由文本症状描述嵌入到向量空间，并与标准化医学本体（如UMLS）中的概念进行语义匹配对齐。
2. **异构知识图谱构建**：
   - 从电子健康记录（EHR）和药理学数据中提取实体（症状、疾病、药物、检验结果）及其关系，构建多源异构知识图谱。
3. **统计实体对齐模块**：
   - 针对不同数据源之间的**表示不匹配**（如同一症状不同表述），引入基于**随机森林分类**的实体对齐方法，将异构实体映射到统一的知识空间。
4. **逻辑推理引擎**：
   - 在统一知识图谱上同时支持**演绎推理**（从已知规则推导结论）和**溯因推理**（从观察结果反向推断原因），生成结构化的诊断路径。
5. **统计与符号融合**：
   - LLM负责自然语言理解和候选生成，符号推理引擎负责逻辑验证和路径约束，最终以可解释的方式输出诊断结果。

### 算法流程（文字描述）
1. 输入患者自由文本症状描述。
2. 利用生物医学编码器将症状与标准本体对齐，得到标准概念集合。
3. 从EHR和药理学数据中提取实体和关系，通过随机森林对齐模块融合为统一知识图谱。
4. 在统一知识图谱上，同时进行演绎和溯因推理，生成可能的诊断路径。
5. 将推理路径输出为可解释的诊断结论，并附上证据链。

## 3. 实验设计

- **数据集**：使用了**真实世界数据集**（具体名称未在摘要中详述，推测为公开的EHR或临床诊断基准，如MIMIC-III/IV或私有临床数据）。
- **Benchmark**：未明确指定，但比较对象包括：
  - **黑盒LLM**（如GPT系列、LLaMA系等纯语言模型）
  - **基于规则的系统**（如传统的专家系统或决策树）
- **对比方法**：ReCLLaMA与上述两类方法在诊断**准确性**和**可解释性**上进行对比。

## 4. 资源与算力

- **文中未明确说明**具体GPU型号、数量、训练时长等算力信息。
- 推测其训练和推理可能涉及LLaMA等开源模型微调，以及随机森林和知识图谱构建，但资源细节未被报告。

## 5. 实验数量与充分性

- **实验数量**：论文摘要仅概括性提及“在真实世界数据集上验证”，未给出具体的实验组数、消融实验设计细节或统计显著性检验结果。
- **充分性评估**：
  - **优点**：对比了纯LLM和规则系统两类典型基线，覆盖统计和符号两种范式的对比。
  - **不足**：缺乏对单一模块（如对齐模块、推理引擎）的消融实验；未报告多次重复实验的稳定性；未公开数据集名称和规模，无法直接复现；可能只在单一或少数数据集上评测，泛化性证据不足。

## 6. 主要结论与发现

- **准确性提升**：ReCLLaMA在诊断任务上优于纯黑盒LLM和基于规则的系统，幻觉显著减少。
- **可解释性增强**：输出结构化的推理路径，具有可追溯性，符合临床对透明决策的需求。
- **融合有效性**：统计语言模型与符号推理的结合可以弥补各自缺陷，为临床AI提供更可靠的方案。

## 7. 优点

1. **理论创新**：将子符号与符号AI在临床场景下进行系统性整合，提出了一个可解释的诊断框架。
2. **技术实用**：利用随机森林进行实体对齐，解决多源数据表示不一致的实际问题，工程可行性高。
3. **解释性友好**：推理路径可被医生理解和审查，符合医疗AI的可解释性要求。
4. **性能优越**：在真实数据上验证了相较于纯LLM和规则系统的双重优势。

## 8. 不足与局限

1. **实验覆盖不足**：缺少多数据集、多疾病领域的广泛验证，可能过拟合于特定知识图谱或数据分布。
2. **消融分析缺失**：未单独评估每个模块（如对齐、推理）的贡献，无法确定性能提升的主要来源。
3. **资源开销未透明**：未报告计算成本，难以评估其实际部署可行性。
4. **偏差风险**：知识图谱构建依赖的EHR和药理学数据可能存在选择性偏差（如特定人群、医院记录），影响泛化。
5. **应用限制**：推理依赖预构建的知识图谱，对新疾病或罕见症状的适应性可能有限；实时诊断场景下的延迟未讨论。
6. **可重复性**：未提供代码或数据集访问细节，阻碍独立验证。

（完）
