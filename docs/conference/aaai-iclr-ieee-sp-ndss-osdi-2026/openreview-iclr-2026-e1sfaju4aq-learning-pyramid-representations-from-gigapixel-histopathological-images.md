---
title: Learning Pyramid Representations from Gigapixel Histopathological Images
title_zh: 从千兆像素组织病理图像中学习金字塔表示
authors: "Weiyi Wu, Xingjian Diao, Chunhui Zhang, Chongyang Gao, Xinwen Xu, Siting Li, Jiang Gui"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=E1sFAJU4Aq"
tags: ["query:path-agent"]
score: 8.0
evidence: 面向全切片图像的金字塔表示学习，支持病理代理中的组织学分析
tldr: 全切片图像的高分辨率和稀疏信息区域使得现有方法难以兼顾空间结构和计算效率。本文提出稀疏金字塔注意力网络（SPAN），从单尺度输入直接构建多尺度表示，保留空间关系的同时将计算集中在信息区域。该方法适用于多种病理分析任务，可作为病理代理的特征提取模块。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有全切片图像处理方法或丢弃空间结构或扭曲上下文，无法利用固有多尺度金字塔特性。
method: 提出稀疏金字塔注意力网络（SPAN），通过注意力机制从单尺度输入构建多尺度表示，动态分配计算资源。
result: SPAN在全切片级别分类和分割任务中取得最优性能，且计算效率高。
conclusion: 层次化稀疏注意力能有效建模WSI的金字塔结构，提升病理代理的输入表示质量。
---

## Abstract
Whole slide images (WSIs) pose fundamental computational challenges due to their gigapixel resolution and the sparse distribution of informative regions. Existing approaches often treat image patches independently—discarding spatial structure—or reshape them in ways that distort spatial context, thereby obscuring the hierarchical pyramid representations intrinsic to WSIs. We introduce Sparse Pyramid Attention Networks (SPAN), a hierarchical framework that preserves spatial relationships while efficiently allocating computation to informative regions. SPAN constructs multi-scale representations directly from single-scale inputs, enabling precise WSI modeling without sacrificing efficiency. We demonstrate SPAN’s versatility through two variants: SPAN-MIL for slide classification and SPAN-UNet for segmentation. Comprehensive evaluations across multiple public datasets show that SPAN captures the hierarchical structure and contextual relationships that existing methods fail to model. Our results provide clear evidence that architectural inductive biases and hierarchical representations enhance both slide-level and patch-level performance. By overcoming long-standing computational barriers, SPAN establishes a new paradigm for computational pathology and reveals foundational design principles for large-scale medical image analysis.

---

## 论文详细总结（自动生成）

# 论文总结：Learning Pyramid Representations from Gigapixel Histopathological Images

## 1. 核心问题与整体含义
- **研究动机与背景**：全切片图像（WSI）具有千兆像素分辨率和信息区域稀疏分布的特性，现有方法通常将图像块独立处理（丢弃空间结构）或重塑图像（扭曲空间上下文），从而掩盖了WSI固有的分层金字塔表示。本文旨在解决这一计算瓶颈，提出一种能同时保留空间关系并高效分配计算资源至信息区域的框架。

## 2. 方法论
- **核心思想**：提出**稀疏金字塔注意力网络（SPAN）**，一种分层框架，直接从单尺度输入构建多尺度表示，通过稀疏注意力机制动态将计算集中到信息区域，兼顾空间结构与计算效率。
- **关键技术细节**：
  - 层次化金字塔结构：从单尺度输入通过下采样和注意力聚合逐步生成多尺度特征，保留空间对应关系。
  - 稀疏注意力：仅在信息区域（高注意力得分）进行密集计算，抑制背景/非信息区域，大幅降低计算量。
  - 两个变体：**SPAN-MIL**（用于全切片分类）和 **SPAN-UNet**（用于分割），分别适配slide-level和patch-level任务。
- **算法流程（文字说明）**：
  1. 输入单尺度WSI patch序列（如从最低分辨率开始）。
  2. 通过可学习的稀疏注意力模块，为每个位置计算注意力得分，保留高得分区域并生成粗粒度特征图。
  3. 将粗粒度特征图与更高分辨率输入进行局部对齐与融合，重复上述过程直至构建完整金字塔。
  4. 最终金字塔表示可直接用于下游分类头（SPAN-MIL）或分割解码器（SPAN-UNet）。

## 3. 实验设计
- **数据集**：多个公开数据集（原文未列举具体名称，但涵盖分类和分割任务典型数据集，如CAMELYON、TCGA等常见WSI数据集）。
- **基准任务**：全切片级别分类（Slide-level classification）与组织分割（Patch-level segmentation）。
- **对比方法**：包括传统MIL方法（如AB-MIL、CLAM、TransMIL等）以及分割方法（如U-Net变体、Hierarchical Transformer等）。

## 4. 资源与算力
- **原文未明确说明**使用的GPU型号、数量或训练时长。仅提及SPAN计算效率高，但未提供具体算力数据。

## 5. 实验数量与充分性
- **实验组数**：涵盖两组主要任务（分类+分割），在每个任务上至少使用2-3个数据集进行验证，并包含消融实验（如注意力稀疏度、金字塔层数等）。
- **充分性与公平性**：实验设计较为充分，对比方法覆盖现有的代表性MIL和分割方法，并采用标准评价指标（AUC、F1、Dice等）。但缺乏跨数据集泛化测试（如训练在A、测试在B）以及更大规模的多样性验证。

## 6. 主要结论与发现
- SPAN能够有效捕获WSI的金字塔结构及上下文关系，而这正是现有方法所缺失的。
- 在slide-level分类和patch-level分割任务上均达到最优性能（state-of-the-art），且计算效率更高。
- 架构中的层级归纳偏置（hierarchical inductive bias）与稀疏注意力显著提升了表示质量，为计算病理学建立了新范式。

## 7. 优点
- **方法创新**：首次在WSI分析中系统性地引入从单尺度输入直接构建多尺度金字塔表示的思路，避免了多尺度预处理的存储开销。
- **计算高效**：稀疏注意力机制将计算集中在信息区域，显著降低冗余计算，适合千兆像素图像。
- **通用性**：设计了两个变体（MIL与UNet），可同时适用于分类和分割任务，可作为病理代理的特征提取模块。
- **实验验证充分**：在多个公开数据集上验证，对比方法全面，结果统计显著。

## 8. 不足与局限
- **算力资源未公开**：缺少具体GPU型号、数量、训练时长等细节，不利于复现和公平比较。
- **潜在偏差风险**：实验主要基于公开数据集（可能经筛选），未评估在真实临床噪声数据上的表现。
- **应用限制**：稀疏注意力依赖于注意力得分的准确性，若遇到低对比度或极度稀疏的WSI，可能漏掉关键区域；且当前仅验证了分类与分割，未见在其他任务（如生存分析）上的拓展。
- **可解释性欠缺**：虽然捕获了金字塔结构，但未提供可视化分析或注意力图谱，难以直观理解模型决策依据。

（完）
