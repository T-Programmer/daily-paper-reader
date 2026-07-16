---
title: "Patho-AgenticRAG: Towards Multimodal Agentic Retrieval-Augmented Generation for Pathology VLMs via Reinforcement Learning"
title_zh: "Patho-AgenticRAG: 面向病理视觉语言模型的多模态智能体检索增强生成"
authors: "Wenchuan Zhang, Jingru Guo, Hengzhe Zhang, Penghao Zhang, Jie Chen, Shuwan Zhang, Zhang Zhang, Yuhao Yi, Hong Bu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40239/44200"
tags: ["query:path-agent"]
score: 9.0
evidence: 面向病理视觉语言模型的智能体检索增强生成框架
tldr: 病理视觉语言模型存在幻觉问题，传统文本检索无法利用视觉线索。本文提出Patho-AgenticRAG，构建基于权威病理教材页面级嵌入的多模态检索增强生成框架，通过智能体式检索减少幻觉。实验显示该方法显著提升病理回答的准确性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 病理VLM因超高分辨率和复杂组织结构易产生幻觉。
method: 构建基于病理教材页面级嵌入的多模态RAG框架，用智能体检索融合文本与视觉证据。
result: 在病理问答任务中，减少幻觉，提高回答真实性和临床可信度。
conclusion: 多模态智能体RAG是提升病理VLM可靠性的有效方案。
---

## Abstract
Although Vision Language Models (VLMs) have shown generalization in medical imaging, pathology presents unique challenges due to ultra-high resolution, complex tissue structures, and nuanced semantics. These factors make pathology VLMs prone to hallucinations, i.e., generating outputs inconsistent with visual evidence, which undermines clinical trust. Existing RAG approaches in this domain largely depend on text-based knowledge bases, limiting their ability to leverage diagnostic visual cues. To address this, we propose Patho-AgenticRAG, a multimodal RAG framework with a database built on page-level embeddings from authoritative pathology textbooks. Unlike traditional text-only retrieval systems, it supports joint text–image search, enabling retrieval of textbook pages that contain both the queried text and relevant visual cues, thus avoiding the loss of critical image-based information. Patho-AgenticRAG also supports reasoning, task decomposition, and multi-turn search interactions, improving accuracy in complex diagnostic scenarios. Experiments show that Patho-AgenticRAG significantly outperforms existing multimodal models in complex pathology tasks like multiple-choice diagnosis and visual question answering.

---

## 论文详细总结（自动生成）

# 论文总结：Patho-AgenticRAG

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：病理视觉语言模型（VLM）在超高清、复杂组织结构、细微语义方面存在幻觉问题，即生成与视觉证据不一致的输出，削弱临床信任。
- **背景**：现有RAG方法多依赖纯文本知识库，无法有效利用诊断相关的视觉线索。病理诊断高度依赖图像（组织形态、染色模式、空间结构），纯文本检索会丢失关键的图像信息。
- **目标**：构建一个**多模态智能体检索增强生成框架**，结合图像-文本联合检索、智能体规划与强化学习，减少病理VLM的幻觉，提升诊断准确性与可解释性。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：将权威病理教材页面转换为图像样本，构建多模态向量数据库；通过智能体自主规划多轮检索路径，融合文本与图像模态相似度进行重排序；利用GRPO强化学习训练智能体决策能力。
- **关键技术细节**：
  1. **多模态病理知识库**：收集600+本权威病理教材（约30万页），筛选后保留20多万高质量页面，使用ColQwen2嵌入文本-图像对到统一向量空间，HNSW索引，Milvus存储。
  2. **多模态融合公式（Patho-Fusion）**：结合文本相似度矩阵 \(S_t\) 和图像相似度矩阵 \(S_v\)，通过标准差、峰度（kurtosis）以及文本最大相似度进行重排序。公式强调关注文档中信息集中的部分，抑制均匀但可能噪声高的文档。
  3. **智能体诊断工作流**：
     - **Agentic Router**：解析问题，分解为子任务，决定是否调用RAG、几次查询重写、是否启用组织特异性分类器。
     - **VRAG Agent**：执行多轮检索、重排序、证据聚合，最终生成结构化提示给病理VLM进行对比推理。
  4. **工具集成强化学习（GRPO）**：采用GRPO算法，对智能体生成的决策路径（是否调RAG、重写次数、分类器选择等）进行奖励。分层奖励函数（Algorithm 1）逐步比较每个决策与真实路径的匹配度。奖励范围0~4，组内归一化优势函数后更新策略。

## 3. 实验设计
- **数据集/场景**：
  - 多模态融合评估：100对图像-问题-答案（专家筛选），50%训练/50%测试。
  - 闭端问答：PathVQA、Quilt-VQA（Yes/No），PathMMU、MedXpertQA、OmniMedVQA（多项选择）。
  - 消融研究：SFT数据量（0、400、4k）与GRPO步数（400、4k）组合。
- **基准对比方法**：
  - 多模态融合基线：CoPaLi（仅文本/仅图像）、WeiMoCIR（加权融合）。
  - 病理VLM基线：InternVL2/2.5/3-8B、Llama-3.2-11B-VI、LLaVA-Onevision-7B、Qwen2.5VL-7B、Patho-R1-7B（作者先前的反事实推理模型）。
- **指标**：Recall@K、MRR@K、NDCG@K（检索）；Accuracy（问答）。

## 4. 资源与算力
- **文中未明确提及**：未说明训练所使用的GPU型号、数量、训练时长、显存消耗等信息。仅在代码仓库中可能隐含，但正文未提供。

## 5. 实验数量与充分性
- **实验数量**：
  - 多模态融合实验：1组对比（表1），含5个指标。
  - 智能体RAG评估：表2（PathMMU）和表3（Quilt-VQA等），覆盖7个模型×多个子集。
  - 消融实验：图4展示SFT+GRPO组合在7个数据集上的精度比较。
  - 总体约10+组对比实验。
- **充分性与公平性**：
  - 对比了多种主流通用VLM和病理专用模型，基线充足。
  - 消融覆盖SFT冷启动策略，验证了“小量SFT+GRPO”最优。
  - 但缺乏与开放式问答任务的评测（仅闭端），也未对不同图像分辨率、噪声场景进行鲁棒性测试。实验覆盖偏重定量准确率，缺少对推理过程可解释性的定性分析。

## 6. 主要结论与发现
- **Patho-Fusion**在检索重排序上全面超越CoPaLi和WeiMoCIR，Recall@1达0.720，MRR@1达0.720。
- **Patho-AgenticRAG**在闭端问答上显著优于所有基线：
  - 在Quilt-VQA上比Patho-R1高+13.37%（75.80% vs 64.72%）。
  - 在MedXpertQA上高+38.00%（60.00% vs 22.00%）。
  - 在OmniMedVQA BrightChallenge上高+19.32%（90.11% vs 70.79%）。
- **消融实验**表明：跳过SFT直接GRPO收敛差；大SFT导致过拟合；SFT400+GRPO4k是最优组合。
- **结论**：多模态智能体RAG能有效减少幻觉，提升病理VLM的事实一致性和临床可信度。

## 7. 优点
- **方法亮点**：
  - 创新地将**教材整页图像**作为检索单元，而非仅文本，保留了丰富的组织形态学视觉线索。
  - 多模态融合公式（Patho-Fusion）利用峰度区分信息集中与噪声文档，设计精巧。
  - **工具集成RL**不仅训练模型回答，还训练智能体决策路径（是否检索、如何重写、选分类器），提升自适应能力。
  - 使用GRPO进行组内归一化，训练更稳定。
- **实验亮点**：
  - 消融细致，验证了SFT冷启动的必要性与最佳数据比例。
  - 多数据源覆盖（病理专有、通用医学、多项选择、Yes/No），结果可信度高。

## 8. 不足与局限
- **实验覆盖不完整**：
  - 仅评估闭端问题（多项选择/是/否），未测开放式问答与长篇报告生成。
  - 缺少推理过程的可解释性评估（如证据引用准确率）。
  - 未对知识库规模进行敏感性测试（如不同教科书数量对性能的影响）。
- **偏差风险**：
  - 教材主要来源于西方权威教材，可能引入地域偏差，对罕见病或特殊人群的诊断证据不足。
  - 智能体决策路径依赖人工标注的地面真值（Algorithm 1），标注成本高且可能有主观性。
- **应用限制**：
  - 需要构建和维护大规模病理教材多模态数据库，更新成本高。
  - 实时推理延迟：ColQwen2嵌入+多轮检索+重排序，延迟较高（文中提到CoPaLi 7.22s/page vs 本文0.39s/page，但未说明完整推理总时长）。
  - 模型规模（7B参数）可能无法在边缘设备部署。
- **资源与可复现性**：未公开具体训练超参数、GPU型号、训练时间，影响独立复现。

（完）
