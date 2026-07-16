---
title: "FedAgentBench: Towards Automating Real-world Federated Medical Image Analysis with Server–Client LLM Agents"
title_zh: FedAgentBench：基于服务器-客户端LLM智能体实现自动化联邦医学图像分析
authors: "Pramit Saha, Joshua Strong, Divyanshu Mishra, Cheng Ouyang, Alison Noble"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=kCnokG3SfU"
tags: ["query:path-agent"]
score: 4.0
evidence: 基于LLM智能体的联邦医学图像分析
tldr: FedAgentBench提出使用服务器-客户端LLM智能体自动化联邦医学图像分析中的操作挑战，包括客户端选择、数据预处理、标签协调和算法选择。该系统将人类操作移植到智能体，减少了跨站点协调的人力。虽然主要面向放射学等影像，但其智能体协作和数据工程方法可迁移至多站点病理学场景，助力病理智能体在实际部署中解决数据异构性难题。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 联邦医学图像分析部署面临客户端协调和数据工程等大量人工操作。
method: 设计服务器和客户端LLM智能体，自动完成客户端选择、数据预处理、标签统一和算法选择。
result: 在多个联邦医学影像任务上减少人工干预，保持模型性能。
conclusion: 智能体能有效自动化联邦学习运维流程，可扩展至病理数据协作。
---

## Abstract
Federated learning (FL) allows collaborative model training across healthcare sites without sharing sensitive patient data. However, real-world FL deployment is often hindered by complex operational challenges that demand substantial human efforts in cross-client coordination and data engineering. This includes: (a) selecting appropriate clients (hospitals), (b) coordinating between the central server and clients, (c) client-level data pre-processing, (d) harmonizing non-standardized data and labels across clients, and (e) selecting FL algorithms based on user instructions and cross-client data characteristics. However, the existing FL works overlook these practical orchestration challenges. These operational bottlenecks motivate the need for autonomous, agent-driven FL systems, where intelligent agents at each hospital client and the central server agent collaboratively manage FL setup and model training with minimal human intervention. To this end, we first introduce: (i) an agent-driven FL framework that captures key phases of real-world FL workflows from client selection to training completion, and (ii) a benchmark dubbed FedAgentBench that evaluates the ability of LLM agents to autonomously coordinate healthcare FL. Our framework incorporates 40 FL algorithms, each tailored to address diverse task-specific requirements and cross-client characteristics. Furthermore, we introduce a diverse set of complex tasks across 201 carefully curated datasets, simulating 6 modality-specific real-world healthcare environments, viz., Dermatoscopy, Ultrasound, Fundus, Histopathology, MRI, and X-Ray. We assess the agentic performance of 14 open-source and 10 proprietary LLMs spanning small, medium, and large model scales. While some agent cores such as GPT-4.1 and DeepSeek V3 can automate various stages of the FL pipeline, our results reveal that more complex, interdependent tasks based on implicit goals remain challenging for even the strongest models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：联邦学习（FL）在医疗影像领域的实际部署面临大量人工操作瓶颈，包括客户端选择、数据预处理、标签协调和算法选择等跨站点协调与数据工程任务。现有FL研究忽视了这些实际编排挑战。
- **研究动机**：为了减少人工干预，提出利用LLM（大语言模型）智能体构建自动化联邦学习系统，使服务器端和客户端智能体协作完成FL工作流。
- **整体含义**：该工作旨在将繁琐的运维操作移植给智能体，实现联邦医疗图像分析从客户端选择到训练完成的全自动化，从而加速FL在真实多站点场景中的落地。

### 2. 论文提出的方法论
- **核心思想**：设计服务器–客户端双角色LLM智能体架构，智能体基于自然语言指令自动执行FL流程中的关键步骤。
- **关键技术细节**：
  - 框架涵盖：客户端选择（医院选择）、服务器与客户端协调、客户端数据预处理、非标准化标签统一、根据用户指令和跨客户端数据特征选择FL算法。
  - 集成了40种FL算法，每种算法针对不同任务需求和跨客户端数据分布特性进行定制。
  - 智能体核心使用LLM（包括开源和闭源模型），通过上下文理解用户任务描述，自主决策并执行操作。
- **算法流程（文字说明）**：用户给出高层目标（如“在5家医院上训练分类模型”），服务器端智能体解析指令 → 选择参与客户端 → 与各客户端智能体通信 → 客户端智能体完成本地数据预处理和标签映射 → 服务器智能体根据数据异构性自动选取合适的FL算法（如FedAvg、FedProx等） → 启动迭代训练 → 训练完成后汇总结果。

### 3. 实验设计
- **数据集/场景**：共201个精心整理的数据集，模拟6种模态的真实医疗环境：皮肤镜（Dermatoscopy）、超声（Ultrasound）、眼底（Fundus）、组织病理（Histopathology）、MRI、X光。
- **Benchmark**：FedAgentBench，用于评估LLM智能体自主协调医疗FL的能力。
- **对比方法**：
  - 14个开源LLM + 10个闭源LLM（共24个模型），涵盖小、中、大模型规模。
  - 重点比较了GPT-4.1、DeepSeek V3等强模型与较弱模型的表现。
- **任务复杂度**：包括简单独立任务和基于隐式目标的复杂、相互依赖任务。

### 4. 资源与算力
- 论文中**未明确说明**使用的GPU型号、数量或训练时长。只提及评估了24个LLM（包括闭源API调用和开源模型推断），未披露具体硬件配置和耗时。需要指出这一信息缺失。

### 5. 实验数量与充分性
- **实验数量**：在201个数据集、6种模态上，使用24个LLM核心进行评估，实验规模较大。
- **充分性与公平性**：
  - 覆盖了多种医疗影像模态和联邦场景，比较了不同规模的开源与闭源模型，具有一定的全面性。
  - 但论文未详细说明每个任务的具体评价指标（如准确性、自动化完成率、人工干预次数等），也未提供消融实验（如移除智能体某组件的影响）。公平性方面，闭源模型API版本可能影响复现，开源模型均在同条件设置下比较。整体实验设计合理，但消融和敏感性分析欠缺。

### 6. 论文的主要结论与发现
- GPT-4.1和DeepSeek V3等强LLM核心能够自动化FL管道的多个阶段。
- 然而，对于更复杂、相互依赖且基于隐式目标的任务，即使最强模型仍然存在挑战。
- 智能体框架有效减少了人工干预，保持了模型性能，并具有扩展到病理数据协作的潜力。

### 7. 优点
- **系统性**：首次将LLM智能体引入联邦医疗图像分析的全流程自动化，填补了现有FL研究忽视运维编排的空白。
- **大规模benchmark**：构建了FedAgentBench，含201个数据集、6种模态、40种FL算法，评估了24种LLM，为后续研究提供标准化测试平台。
- **实用性**：直接面向真实多站点协作痛点，自动化客户端选择和标签协调，可迁移至病理等场景。

### 8. 不足与局限
- **实验覆盖**：未提供消融实验和详细的错误分析，未能区分不同LLM在不同子任务上的具体表现差异。
- **偏差风险**：依赖LLM的决策可能存在幻觉或错误，尤其在处理非结构化医疗数据或敏感标签时，论文未评估安全性或鲁棒性。
- **应用限制**：仅针对医疗影像（放射学、病理等），未验证在其他领域（如电子病历、基因组学）的通用性；此外，闭源模型如GPT-4.1的API成本高，实际部署受限。
- **资源信息缺失**：未报告计算资源，不利于复现和成本评估。

（完）
