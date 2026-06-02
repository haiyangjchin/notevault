---
title: "Harness 定义与核心概念"
created: 2026-06-02
description: "理解 Harness 的本质：它是什么，为什么重要，以及它的核心组件"
tags:
  - "harness"
  - "concepts"
  - "fundamentals"
---

# Harness 定义与核心概念

## 什么是 Harness？

Harness 是 **AI 代理系统中除了模型之外的一切**。

> **Agent = Model + Harness**

这个简洁的公式来自 [LangChain 的定义](https://blog.langchain.com/the-anatomy-of-an-agent-harness/)，它清楚地表明：代理的智能来自模型，但模型的实用性来自 harness。

## 为什么需要 Harness？

模型（通常）只能处理文本输入并输出文本。它们无法：
- 维护跨交互的持久状态
- 执行代码
- 访问实时知识
- 设置环境和安装包

这些都是 **harness 级别的功能**。Harness 是将模型的"尖峰智能"塑造成可用工具的系统。

## Harness 的三个层次

根据 [Birgitta Böckeler 的分析](https://martinfowler.com/articles/harness-engineering.html)，Harness 可以分为三个同心圆：

### 1. 模型层（核心）
- 模型的内在能力
- 训练数据和知识
- 推理能力

### 2. 构建者 Harness（中间层）
- 系统提示
- 代码检索机制
- 编排系统
- 工具和环境

### 3. 用户 Harness（外层）
- 用户特定的配置
- 自定义工具和脚本
- 项目特定的指南
- 反馈传感器

## Harness 的核心组件

根据 [LangChain 的分析](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness)，一个完整的 harness 包含：

### 1. 文件系统
**目标**：提供持久存储和上下文管理

- 工作空间：读取数据、代码和文档
- 增量工作：可以逐步添加和卸载信息
- 协作表面：多个代理和人类可以通过共享文件协调

**Git** 为文件系统添加版本控制，使代理可以跟踪工作、回滚错误和分支实验。

### 2. Bash + 代码执行
**目标**：让代理自主解决问题，无需预先设计每个工具

代理的主要执行模式是 [ReAct 循环](https://docs.langchain.com/oss/python/langchain/agents)，模型推理、通过工具调用采取行动、观察结果，然后重复。但 harness 只能执行它有逻辑的工具。

**解决方案**：给代理一个通用工具（如 bash），让它通过编写和执行代码来解决问题。

### 3. 沙箱和执行环境
**目标**：提供安全的操作环境

- 安全隔离：本地执行风险高，沙箱提供隔离
- 可扩展性：按需创建环境，工作完成后销毁
- 默认工具：预安装语言运行时、包、CLI 工具

### 4. 验证工具
**目标**：让代理能够观察和分析工作

- 浏览器：Web 交互和验证
- 日志：运行时信息
- 截图：视觉验证
- 测试运行器：自动化测试

这些工具创建 **自验证循环**：编写应用代码 → 运行测试 → 检查日志 → 修复错误。

## Harness 的设计原则

### 1. 最小复杂度
> "找到最简单的解决方案，只在需要时增加复杂度" - Anthropic

### 2. 渐进式披露
- 不要一开始就加载所有信息
- 使用简短的"地图"而非"百科全书"
- 深层信息按需加载

### 3. 确定性优先
- 计算型控制（测试、linter）便宜、快速、确定性
- 推理型控制（AI 审查）更贵、更慢、非确定性
- 优先使用计算型，必要时才用推理型

### 4. 反馈循环
- 每次错误都是改进 harness 的机会
- 将人类品味编码到系统中
- 持续迭代和改进

## Harness vs 提示工程 vs 上下文工程

| 概念 | 定义 | 范围 |
|------|------|------|
| **提示工程** | 问什么 | 单次交互 |
| **上下文工程** | 发送什么给模型 | 上下文窗口 |
| **Harness 工程** | 整个系统如何运作 | 整个代理系统 |

> "提示工程是问什么，上下文工程是发送什么给模型以便它能自信地回答，Harness 工程是整个系统如何运作。" - [Louis-François Bouchard](https://www.youtube.com/watch?v=zYerCzIexCg)

## Harness 的类比

### 汽车类比
- **模型** = 引擎（你不能没有它）
- **上下文** = 燃料、机油、仪表信息（你可以轻松优化和控制）
- **Harness** = 方向盘、刹车、车道边界、维护计划、警告灯（其余一切）

> "如果你只关注引擎和燃料，你仍然可以造出一辆糟糕的车。你会开车，但可能很危险。" - Louis-François Bouchard

### 网络服务类比
- **模型** = 业务逻辑
- **Harness** = 基础设施（服务器、数据库、监控、CI/CD）

## 相关文章

- [[The Anatomy of an Agent Harness]] - Harness 的解剖学
- [[What Harness Engineering Actually Means]] - Harness 工程的真正含义
- [[Harness engineering for coding agent users]] - 面向编码代理用户的 Harness 工程

## 关键要点

1. **Harness 是必要的**：模型本身无法完成有用的工作
2. **Harness 是系统性的**：包括工具、环境、状态、验证、反馈
3. **Harness 是演进的**：随着模型改进，harness 也需要调整
4. **Harness 是可工程化的**：可以系统地设计和优化

## 下一步

- 阅读 [[02-长时间运行代理设计]] 了解如何设计跨会话工作的代理
- 阅读 [[03-上下文工程]] 了解如何优化代理的上下文
- 阅读 [[04-自验证与测试]] 了解如何让代理自我验证

---

**相关概念**：[[HOME|Harness Engineering Wiki]]
