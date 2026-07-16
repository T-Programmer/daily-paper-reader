---
title: "RareAgents: Autonomous Multi-disciplinary Team for Rare Disease Diagnosis and Treatment"
title_zh: RareAgents：面向罕见病诊断与治疗的自主多学科团队
authors: "Xuanzhong Chen, Ye Jin, Xiaohao Mao, Lun Wang, Shuyang Zhang, Ting Chen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/36969/40931"
tags: ["query:path-agent"]
score: 5.0
evidence: 多学科代理团队用于罕见病诊断，与病理学有间接关联
tldr: 罕见病涉及多器官系统，但当前代理框架未适应真实临床场景。本文提出RareAgents，一个由大型语言模型驱动的多学科代理团队，通过协调不同专科代理（可能包含病理学）实现罕见病的诊断和治疗建议。尽管不是专门针对病理，但其多代理协作框架对构建病理诊断代理团队有启发意义。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 罕见病诊断因多学科协作困难和专业医生短缺，现有代理框架不适应真实临床场景。
method: 构建基于LLM的多学科代理团队，包括各类专科代理，通过协作完成罕见病的诊断和治疗建议。
result: RareAgents在罕见病诊断数据集上优于单一代理和直接提示方法。
conclusion: 多学科代理协作能更有效地处理复杂罕见病的诊断需求。
---

## Abstract
Rare diseases, despite their low individual incidence, collectively impact around 300 million people worldwide due to the vast number of diseases. The involvement of multiple organs and systems, and the shortage of specialized doctors with relevant experience, make diagnosing and treating rare diseases more challenging than common diseases. Recently, agents powered by large language models (LLMs) have demonstrated notable applications across various domains. In the medical field, some agent methods have outperformed direct prompts in question-answering tasks from medical examinations. However, current agent frameworks are not well-adapted to real-world clinical scenarios, especially those involving the complex demands of rare diseases. To bridge this gap, we introduce RareAgents, the first LLM-driven multi-disciplinary team decision-support tool designed specifically for the complex clinical context of rare diseases. RareAgents integrates advanced Multidisciplinary Team (MDT) coordination, memory mechanisms, and medical tools utilization, leveraging Llama-3.1-8B/70B as the base model. Experimental results show that RareAgents outperforms state-of-the-art domain-specific models, GPT-4o, and current agent frameworks in diagnosis and treatment for rare diseases. Furthermore, we contribute a novel rare disease dataset, MIMIC-IV-Ext-Rare, to facilitate further research in this field.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：罕见病虽然单一发病率低，但总数超过7000种，全球影响约3亿患者。罕见病常涉及多器官系统，症状复杂且与常见病重叠，导致诊断延迟（“诊断奥德赛”）。同时，具备相关经验的专科医生稀缺，使得罕见病的诊断和治疗比常见病更具挑战。
- **现有局限**：当前基于大语言模型（LLM）的医疗代理框架（如MedAgents、MDAgents）主要针对多项选择题或有限回答场景，不适用于开放式的真实临床决策。此外，这些框架往往依赖LLM自行生成角色定义，易产生幻觉；在记忆机制和工具使用方面也较弱。
- **本文目标**：提出RareAgents，第一个专为罕见病复杂临床背景设计的LLM驱动多学科团队（MDT）决策支持工具，旨在提升诊断和治疗的准确性。

## 2. 论文提出的方法论：核心思想与关键技术细节
- **核心思想**：患者为中心，由主治医师代理（Attending Physician Agent）根据患者症状自动组建多学科团队（MDT），团队成员基于预定义的41个专科（如神经科、血液科、消化科等）进行多轮讨论，最终达成一致意见并生成报告。每个医生代理具备动态长期记忆和医疗工具使用能力。
- **关键技术细节**：
  - **MDT协作**：分为三个阶段：(i) MDT形成：主治医师从预定义专科池中选择相关专科构成MDT；(ii) 专家共识：专科代理进行最多R轮讨论，逐步提出并综合意见；(iii) 报告生成：主治医师汇总所有意见生成最终讨论报告。
  - **动态长期记忆**：每个代理维护个性化长期记忆，可存储、检索和更新。诊断时检索最相似的top-k历史病例（k=5）；治疗时检索该患者之前住院记录。
  - **医疗工具使用**：代理可调用外部工具如Phenomizer、LIRICAL、Phenobrain（诊断工具）以及DrugBank、DDI-graph（治疗工具），增强临床推理。
  - **基础模型**：使用Llama-3.1-8B/70B作为底层LLM，利用其增强的上下文窗口（128K tokens）和函数调用能力。
  - **最终决策**：综合MDT共识、记忆检索结果和工具反馈，由LLM生成最终诊断或治疗建议。

## 3. 实验设计
- **数据集**：
  - **RareBench-Public**：多中心罕见病患者数据，共1197例，用于鉴别诊断任务。提供症状和相应诊断。
  - **MIMIC-IV-Ext-Rare**：从MIMIC-IV（版本3.0）中提取的罕见病患者子集，共4760名患者，18522次入院记录，用于药物推荐任务。通过映射ICD代码至OMIM/Orphanet并过滤得到。
- **Benchmark与对比方法**：
  - **领域特定SOTA**：诊断模型（Phenomizer, LIRICAL, Phen2Disease, Phenobrain等）；治疗模型（LEAP, G-Bert, SafeDrug, MoleRec, RAREMed等）。
  - **通用/医学LLM**：GPT-4o, GPT-3.5, UltraMedical-70B/8B, OpenBioLLM-70B/8B等，零样本+链式思考。
  - **o1-like LLM**：DeepSeek-R1-Distill-Llama-70B/8B, Baichuan-M1-14B, HuatuoGPT-o1-70B。
  - **开源医学多代理框架**：MedAgents, MDAgents，均适配至本地Llama-3.1运行。
  - **消融设置**：RareAgents的三种变体（去除MDT、去除记忆、去除工具）。
- **评估指标**：
  - 鉴别诊断：Hit@k（k=1,3,10）、Median Rank（MR）。
  - 药物推荐：Jaccard系数、F1分数、药物-药物相互作用率（DDI）、推荐药物数量（#MED）。

## 4. 资源与算力
- **文中未明确说明**：论文未提及训练或推理所使用的具体GPU型号、数量、训练时长、内存等算力信息。仅提到使用Llama-3.1-8B/70B作为基础模型，但未说明模型是直接推理还是经过微调、硬件配置如何。因此无法评估算力需求。

## 5. 实验数量与充分性
- **实验数量**：主要实验包括主表（Table 3）涵盖2个任务、2种模型大小（8B/70B）下20+个基线；消融实验（Table 4）比较3个模块的贡献；额外分析实验（Figure 3-5）探讨MDT代理数量、MDT定义策略（3种）、记忆检索策略（2种）的影响。总计约10+组独立实验。
- **充分性与公平性**：
  - 基线选择全面，覆盖领域模型、通用LLM、医学LLM、o1-like模型和现有代理框架。
  - 对开源代理框架进行了适配（从GPT-4 API转换到本地Llama-3.1），保证公平比较。
  - 药物推荐任务采用5折交叉验证，减少了随机性影响。
  - 消融实验清晰展示了各模块的贡献，验证了设计的必要性。
  - **不足**：未在更多LLM基础模型上验证（如GPT-4o作为代理的变体）；未报告统计显著性检验；未在真实临床环境中测试。

## 6. 论文的主要结论与发现
- **总体性能**：RareAgents（基于Llama-3.1-70B）在鉴别诊断和药物推荐任务上均超越所有基线，包括GPT-4o和现有代理框架。
- **模块重要性**：消融实验表明，所有三个模块（MDT、记忆、工具）均带来提升，其中记忆模块对性能影响最大（诊断Hit@1下降22.4%）；工具模块能显著降低DDI率。
- **MDT有效性**：RareAgents中的MDT（仅MDT，不含记忆和工具）已经优于MedAgents和MDAgents；基于预定义专科相关性的MDT定义策略优于随机或LLM自生成策略；MDT性能在约12-22个专科时最优。
- **动态记忆优势**：动态检索相关历史病例/记录远优于随机检索，且随着检索数量增多优势更明显。
- **新数据集贡献**：MIMIC-IV-Ext-Rare首次将LLM代理框架应用于药物推荐任务，为罕见病研究提供了有价值资源。

## 7. 优点
- **任务针对性强**：首次针对罕见病复杂真实临床场景设计LLM代理框架，突破现有方法仅适用于选择题/有限回答的局限。
- **模块化可插拔设计**：MDT、记忆、工具三个组件均可独立替换，易于扩展至其他医疗决策场景。
- **角色定义专业**：采用人类专科医生指导的41个预定义专科，避免LLM自行定义角色带来的幻觉和不确定性。
- **实验全面细致**：不仅报告主结果，还深入分析各模块贡献、策略选择、超参数影响，结论扎实。
- **数据资源贡献**：提供了MIMIC-IV-Ext-Rare数据集，填补了LLM代理框架在罕见病药物治疗任务上的数据空白。

## 8. 不足与局限
- **算力与部署未报告**：未说明训练/推理所需GPU型号、时长、成本，不利于可重复性和实际部署评估。
- **模型泛化性有限**：仅基于Llama-3.1模型，未在GPT-4、Claude等其他强大LLM上验证RareAgents框架的通用性。
- **DDI指标未最优**：在药物推荐任务中DDI值低于部分基线（如OpenBioLLM），但OpenBioLLM以牺牲Jaccard/F1为代价；需进一步平衡安全性与有效性。
- **数据集偏差**：MIMIC-IV-Ext-Rare仅来自美国单一医院系统，可能不具有全球代表性；RareBench-Public虽为多中心，但病例数有限。
- **缺乏真实临床验证**：所有评估基于静态数据集，未在真实医生-患者交互环境中测试，可能低估实际应用中的复杂性和不确定性。
- **未见伦理与安全性讨论**：罕见病诊断错误后果严重，论文未讨论AI代理的临床责任、可解释性、纠错机制等关键问题。

（完）
