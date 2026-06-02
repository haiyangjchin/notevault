---
title: "Harness Engineering Wiki - 结构概览"
created: 2026-06-02
description: "Wiki 的整体结构和导航指南"
tags:
  - "readme"
  - "navigation"
  - "overview"
---

# Harness Engineering Wiki

欢迎来到 **Harness Engineering** 知识库！这是一个关于 AI 代理 Harness 工程的综合 Wiki。

## 快速导航

### 核心概念（推荐顺序）

1. [[01-Harness 定义与核心概念]] - 理解 Harness 的本质
2. [[02-长时间运行代理设计]] - 跨会话代理设计
3. [[03-上下文工程]] - 上下文管理和优化
4. [[04-自验证与测试]] - 代理自我验证技术
5. [[05-多代理架构]] - 多代理协调和通信
6. [[06-工具与沙箱]] - 工具和执行环境
7. [[07-代码仓库作为知识源]] - 代码仓库管理
8. [[08-代理可读性]] - 应用程序可见性
9. [[09-熵与垃圾收集]] - 代码质量维护
10. [[10-Ralph Wiggum 技术]] - 简单有效的循环技术

### 主入口

- [[HOME]] - Wiki 主页（综合索引）

### 原始资料（10 篇文章）

#### Anthropic
1. [[Effective harnesses for long-running agents]] - 长时间运行代理的 Harness
2. [[Harness design for long-running application development]] - 长时间应用开发的 Harness 设计

#### OpenAI
3. [[工程技术：在智能体优先的世界中利用 Codex]] - OpenAI 的实践

#### LangChain
4. [[Improving Deep Agents with harness engineering]] - 改进深度代理
5. [[The Anatomy of an Agent Harness]] - Agent Harness 的解剖学

#### Martin Fowler
6. [[Harness engineering for coding agent users]] - 面向编码代理用户的 Harness 工程

#### 其他
7. [[Building Effective AI Coding Agents for the Terminal Scaffolding, Harness, Context Engineering, and Lessons Learned]] - 终端 AI 编码代理
8. [[OpenAI's Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]] - 访谈
9. [[Ralph Wiggum as a software engineer]] - Ralph Wiggum 技术
10. [[What Harness Engineering Actually Means]] - Harness 工程的真正含义

## Wiki 结构

```
Harness Engineering/
├── README.md                                    # 本文件
├── HOME.md                                      # Wiki 主页
├── 01-Harness 定义与核心概念.md                  # 核心概念
├── 02-长时间运行代理设计.md                      # 代理设计
├── 03-上下文工程.md                              # 上下文管理
├── 04-自验证与测试.md                            # 验证技术
├── 05-多代理架构.md                              # 多代理
├── 06-工具与沙箱.md                              # 工具环境
├── 07-代码仓库作为知识源.md                      # 代码仓库
├── 08-代理可读性.md                              # 可见性
├── 09-熵与垃圾收集.md                            # 质量维护
├── 10-Ralph Wiggum 技术.md                      # 循环技术
├── Building Effective AI Coding Agents...md     # 原始资料
├── Effective harnesses for long-running...md    # 原始资料
├── Harness design for long-running...md         # 原始资料
├── Harness engineering for coding agent...md    # 原始资料
├── Improving Deep Agents with harness...md      # 原始资料
├── OpenAI's Michael Bolin on Codex...md         # 原始资料
├── Ralph Wiggum as a software engineer.md       # 原始资料
├── The Anatomy of an Agent Harness.md           # 原始资料
├── What Harness Engineering Actually Means.md   # 原始资料
└── 工程技术：在智能体优先的世界中利用 Codex.md  # 原始资料
```

## 学习路径

### 入门路径（推荐）
1. 阅读 [[HOME]] 了解整体概览
2. 阅读 [[01-Harness 定义与核心概念]] 理解基础
3. 阅读 [[02-长时间运行代理设计]] 了解代理设计
4. 阅读 [[03-上下文工程]] 了解上下文管理

### 进阶路径
5. 阅读 [[04-自验证与测试]] 了解验证技术
6. 阅读 [[05-多代理架构]] 了解多代理协调
7. 阅读 [[06-工具与沙箱]] 了解工具环境

### 高级路径
8. 阅读 [[07-代码仓库作为知识源]] 了解代码仓库管理
9. 阅读 [[08-代理可读性]] 了解应用程序可见性
10. 阅读 [[09-熵与垃圾收集]] 了解质量维护
11. 阅读 [[10-Ralph Wiggum 技术]] 了解简单有效的技术

## 关键概念

### Harness 的本质
- **定义**：Agent = Model + Harness
- **组成**：工具、环境、状态、验证、反馈
- **目标**：使模型的智能变得有用

### 核心挑战
- 上下文窗口限制
- 状态丢失
- 验证困难
- 质量维护

### 解决方案
- 增量式工作
- 结构化交接
- 自验证循环
- 多代理协调

## 实践案例

### OpenAI
- 100 万行代码，零人工编写
- 3 名工程师，1500 个 PR
- 代码仓库作为"记录系统"

### Anthropic
- Claude Agent SDK
- 多上下文窗口工作流
- 初始化代理 + 编码代理模式

### LangChain
- Terminal Bench 2.0 排名从 Top 30 提升到 Top 5
- 只改变 harness，不改变模型
- 自验证和追踪是关键

## 工具和技术

### 代理框架
- Claude Agent SDK
- LangChain Deep Agents
- Codex CLI

### 验证工具
- Playwright MCP
- Chrome DevTools Protocol
- Puppeteer MCP

### 监控工具
- LangSmith
- OpenTelemetry
- LogQL / PromQL

## 开放问题

1. **行为 Harness**：如何确保应用程序按预期运行？
2. **Harness 一致性**：如何保持指南和传感器同步？
3. **Harness 覆盖度**：如何评估 harness 的质量？
4. **模型演进**：随着模型改进，harness 如何适应？

## 相关资源

### 官方文档
- [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview)
- [LangChain Deep Agents](https://docs.langchain.com/oss/python/deepagents/overview)
- [OpenAI Codex](https://openai.com/codex)

### 研究论文
- [Building Effective AI Coding Agents](https://arxiv.org/abs/2603.05344)
- [Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

### 社区资源
- [Agent Skills Specification](https://agentskills.io/specification)
- [Terminal Bench 2.0](https://www.tbench.ai/)

## Wiki 维护

**最后更新**: 2026-06-02
**维护者**: Claudian (AI Assistant)
**文章数量**: 10 篇核心概念 + 10 篇原始资料

---

**开始学习**: [[HOME|Harness Engineering Wiki]]
