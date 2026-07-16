---
title: "MedLA: A Logic-Driven Multi-Agent Framework for Complex Medical Reasoning with Large Language Models"
title_zh: MedLA：基于大语言模型的逻辑驱动多智能体复杂医学推理框架
authors: "Siqi Ma, Jiajie Huang, Fan Zhang, Jinlin Wu, Yue Shen, Guohui Fan, Zhu Zhang, Zelin Zang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37052/41014"
tags: ["query:path-agent"]
score: 8.0
evidence: 逻辑驱动的多智能体医学推理框架，可直接应用于病理诊断
tldr: 复杂医学推理需要多视角逻辑一致性。现有多智能体方法角色固定、交互浅。MedLA让每个智能体将推理组织为三段论逻辑树，并通过图引导讨论迭代精炼。该方法可直接部署于病理诊断问答和决策，提升推理可信度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有医学多智能体方法缺乏细粒度逻辑一致性检测。
method: 提出逻辑驱动多智能体框架，每个智能体构建三段论逻辑树并进行图引导讨论。
result: 在复杂医学推理任务上超越基线，提供透明推理过程。
conclusion: 为病理诊断智能体提供结构化多视角推理能力。
---

## Abstract
Answering complex medical questions requires not only domain expertise and patient-specific information, but also structured and multi-perspective reasoning. Existing multi-agent approaches often rely on fixed roles or shallow interaction prompts, limiting their ability to detect and resolve fine-grained logical inconsistencies. To address this, we propose MedLA, a logic-driven multi-agent framework built on large language models. Each agent organizes its reasoning process into an explicit logical tree based on syllogistic triads (major premise, minor premise, and conclusion), enabling transparent inference and premise-level alignment. Agents engage in a multi-round, graph-guided discussion to compare and iteratively refine their logic trees, achieving consensus through error correction and contradiction resolution. We demonstrate that MedLA consistently outperforms both static role-based systems and single-agent baselines on challenging benchmarks such as MedDDx and standard medical QA tasks. Furthermore, MedLA scales effectively across both open-source and commercial LLM backbones, achieving state-of-the-art performance and offering a generalizable paradigm for trustworthy medical reasoning.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义

- **研究动机**：大型语言模型（LLM）在医学推理中展现潜力，但回答复杂临床问题时仍面临三大挑战：需要整合领域知识、患者信息和显式逻辑推理。现有多智能体方法（如固定角色、浅层交互提示）难以检测和解决细粒度的逻辑不一致（如诊断矛盾、规则误用）。
- **研究目标**：提出一种逻辑驱动的多智能体框架 **MedLA**，通过将每名智能体的推理显式组织为三分逻辑树（大前提-小前提-结论），并引入多轮图引导讨论，实现跨智能体错误修正和一致性收敛，从而提升复杂医学推理的可信度与准确性。
- **整体含义**：为医学QA和鉴别诊断提供了一种无需微调或外部检索、结构透明、可验证的通用推理范式，显著优于静态角色基线和单智能体基线。

### 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：以古典三段论（Syllogism）为最小推理单元，将每名智能体的思考过程组织为**逻辑树**（Logical Tree）：树节点为三段论（大前提、小前提、结论），边为推理前提/结论的依赖关系。通过多智能体间逻辑树的对比与迭代修正，实现细粒度的逻辑冲突检测与纠正。
- **关键技术细节**：
  - **前提智能体（P-Agent）**：从问题和外部知识库中提取大前提集合 \( P_{\text{maj}} \)（医学规则）和小前提集合 \( P_{\text{min}} \)（患者事实）。
  - **分解智能体（D-Agent）**：递归地将原始问题分解为原子子问题，构建问题树。对于选择题，对每个候选答案执行淘汰式推理。
  - **医学智能体（M-Agent）**：并行运行多个M-Agent，每个独立基于 \( P_{\text{maj}}, P_{\text{min}} \) 和子问题生成局部逻辑树。输出包含节点集 \( V \)（三段论文本块）和有向边集 \( E \)。
  - **可信度智能体（C-Agent）**：评估每个节点的置信度（高/中/低），低置信节点标记为待讨论项。
- **算法流程（三阶段）**：
  - **Phase A：前提提取与问题分解**：P-Agent提取大小前提，D-Agent分解问题。
  - **Phase B：逻辑树生成、校准与讨论**：多个M-Agent并行生成局部逻辑树；C-Agent评估置信度；低置信节点进入多轮图引导讨论，各M-Agent交换逻辑树、对比差异、修正节点并重新评分；重复直至收敛。
  - **Phase C：逻辑决策**：合并所有局部逻辑树，遍历生成最终答案及推理解释。

### 3. 实验设计

- **数据集 / 场景**：
  - **MedDDx**：鉴别诊断基准，分Basic/Intermediate/Expert三级难度。
  - **Multi-choice medical QA benchmarks**：包括MMLU-Med、MedQA-US、BioASQ-Y/N，测试通用医学知识。
  - **MedXpertQA**：专家级医学推理和理解基准。
- **基准对比方法**：
  - **图方法**：QAGNN、JointLK、DRAGON。
  - **多智能体投票**：Majority Voting、DyLAN、MedAgents、MDAgents。
  - **单LLM基线**：LLaMA-2/3、Mistral、MedAlpaca、PMC-LLaMA等，及CoT变体。
  - **RAG方法**：Self-RAG、KG-Rank、KG-RAG、MedRAG。
- **评价指标**：Accuracy ± 标准差（3次独立随机运行，每次打乱顺序并重置采样状态）。

### 4. 资源与算力

- **硬件**：8卡 A100-80GB GPU。
- **软件**：vLLM v0.7.2，使用官方预训练模型权重（无需额外微调）。
- **时间消耗**（以BioASQ-Y/N为例）：MedLA总耗时3,657秒（纯推理，不含微调或检索），约为主流多智能体方法的2倍，但低于需要离线训练的KGAREVION（10k+秒）。文中未报告训练耗时（因不需训练），仅报告推理时延。

### 5. 实验数量与充分性

- **实验数量**：
  - 主性能评估：在3个基准（MedDDx的三个难度子集 + 多任务QA + MedXpertQA）下对比20+种基线。
  - 消融实验：逐步剔除Revision loop、Credibility Agent、Logic Tree，在MedQA-US和MedDDx上评测。
  - 规模扩展实验：评估8B vs 70B模型下的增益；商业模型（DeepSeek-r1/v3）上的对比。
  - 难度分析：在MedDDx三级难度上分别报告相对提升。
- **充分性与客观性**：
  - 所有基线结果直接引用原始论文或复现，控制随机种子、解码参数一致，避免不公平因素。
  - 消融实验设计完整，验证了每个模块的贡献。
  - 实验覆盖多难度、多类型任务，且同时测试开源与商业模型，普遍性高。
- **潜在不足**：未在中文语料或多模态（如影像+文本）任务上验证；消融实验仅在一个QA数据集和一个诊断数据集上进行，略少。

### 6. 主要结论与发现

- **MedLA在所有基准上显著超越所有基线**，尤其在困难任务上提升最大（MedDDx-Expert提升+11.1个百分点）。
- **无需外部知识或微调**：仅通过逻辑树结构和多智能体讨论即可超越依赖检索或图的方法。
- **每个模块都有正向贡献**：消融实验表明，移除逻辑树支架导致最大性能下降（~4.5pp），可信度校准和修正循环分别贡献1~2pp。
- **强泛化性**：在商业LLM（DeepSeek）上也取得一致优势，证明逻辑驱动方法不依赖于特定基座模型。
- **时间开销可接受**：推理耗时约为简单投票的2倍，但显著低于需离线训练的方法，在实用场景中可行。

### 7. 优点

- **方法创新**：首次将显式三段论逻辑树引入多智能体医学推理，实现推理步骤的完全可追溯和前提级冲突检测。
- **设计精巧**：通过多层智能体（前提、分解、医学、可信度）划分职责，并设计多轮图引导讨论机制，实现跨智能体错误修正。
- **实用性强**：无需微调、无外部检索依赖，直接运行在现有LLM上，易于部署。
- **实验全面且客观**：覆盖多个难度级别、多种范式基线，并进行了充分的消融和泛化分析。

### 8. 不足与局限

- **依赖LLM输出质量**：逻辑树的构建依赖LLM对三段论提示的理解，若基座模型本身存在系统性偏差（如对特定疾病过度自信），可能难以被讨论纠正。
- **成本仍偏高**：相比单模型，MedLA需要多次调用LLM（多个M-Agent并行+多轮讨论），推理时间与token消耗约为简单投票的2倍，在超大规模部署时可能受限。
- **局限性覆盖**：未涉及多模态（如图像+文本）场景，也未在中文或其他非英语医学数据上测试。讨论机制可能无法处理所有类型的逻辑矛盾（如多个智能体共享相同错误。
- **单点故障风险**：所有智能体基于同一基座模型，若基座模型存在全局性知识缺失，可能影响整个框架。未来可考虑引入异构模型增强鲁棒性。

（完）
