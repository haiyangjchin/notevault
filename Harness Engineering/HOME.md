---
title: "Harness Engineering Wiki"
created: 2026-06-02
description: "Wiki 主页 - 关于 AI 代理 Harness 工程的综合知识库"
tags:
  - "wiki"
  - "harness-engineering"
  - "index"
---

# Harness Engineering Wiki

欢迎来到 **Harness Engineering** 知识库！这是一个关于 AI 代理 Harness 工程的综合 Wiki，汇集了来自 Anthropic、OpenAI、LangChain 等领先机构的最新研究成果和实践经验。

## 核心概念

| 概念 | 说明 | 相关文章 |
|------|------|----------|
| [[01-Harness 定义与核心概念]] | Harness 是什么？为什么需要它？ | 所有文章 |
| [[02-长时间运行代理设计]] | 如何设计能够跨多个上下文窗口工作的代理 | Anthropic, OpenAI |
| [[03-上下文工程]] | 如何管理和优化代理的上下文 | LangChain, Anthropic |
| [[04-自验证与测试]] | 让代理自我验证和改进的技术 | Anthropic, LangChain |
| [[05-多代理架构]] | 多代理系统的设计和协调 | OpenAI, Anthropic |
| [[06-工具与沙箱]] | 代理需要的工具和执行环境 | LangChain, OpenAI |
| [[07-代码仓库作为知识源]] | 如何让代码仓库对代理可读 | OpenAI |
| [[08-代理可读性]] | 提高应用程序对代理的可见性 | OpenAI |
| [[09-熵与垃圾收集]] | 管理代理生成的代码质量 | OpenAI |
| [[10-Ralph Wiggum 技术]] | 简单但有效的代理循环技术 | Geoffrey Huntley |

## 关键主题

### 1. Harness 的本质
Harness 是 **Agent = Model + Harness** 中除了模型之外的一切。它包括：
- 系统提示和指令
- 工具和环境
- 状态管理和记忆
- 验证和反馈循环
- 权限和安全控制

**相关文章**：
- [[The Anatomy of an Agent Harness]]
- [[What Harness Engineering Actually Means]]
- [[Harness engineering for coding agent users]]

### 2. 长时间运行代理的核心挑战
- **上下文窗口限制**：代理必须在离散的会话中工作
- **状态丢失**：每个新会话从零开始
- **一致性问题**：代理可能做出矛盾的决策
- **验证困难**：如何确保代理正确完成任务

**相关文章**：
- [[Effective harnesses for long-running agents]]
- [[Harness design for long-running application development]]

### 3. 解决方案模式

#### 初始化代理 + 编码代理
- **初始化代理**：设置初始环境、功能列表、进度文件
- **编码代理**：增量式工作，一次一个功能

**相关文章**：
- [[Effective harnesses for long-running agents]]

#### 生成器-评估器模式（GAN 启发）
- **规划器**：将简单提示扩展为完整产品规格
- **生成器**：按 sprint 实现功能
- **评估器**：验证工作质量

**相关文章**：
- [[Harness design for long-running application development]]

#### Ralph Wiggum 循环
- 将代理放在 while 循环中
- 每次循环只做一件事
- 通过提示调优来改进

**相关文章**：
- [[Ralph Wiggum as a software engineer]]

### 4. 上下文工程最佳实践

#### 渐进式披露
- 不要一开始就加载所有信息
- 使用 AGENTS.md 作为"地图"而非"百科全书"
- 深层信息按需加载

**相关文章**：
- [[工程技术：在智能体优先的世界中利用 Codex]]

#### 环境上下文注入
- 目录结构和工具发现
- 时间预算管理
- 测试要求说明

**相关文章**：
- [[Improving Deep Agents with harness engineering]]

### 5. 验证与反馈循环

#### 自验证循环
1. 构建功能
2. 运行测试
3. 检查结果
4. 修复问题

**相关文章**：
- [[Improving Deep Agents with harness engineering]]
- [[Effective harnesses for long-running agents]]

#### 计算型 vs 推理型传感器
- **计算型**：确定性、快速（测试、linter、类型检查）
- **推理型**：语义分析、AI 代码审查（更慢、更贵）

**相关文章**：
- [[Harness engineering for coding agent users]]

### 6. 架构与约束

#### 分层架构强制执行
- Types → Config → Repo → Service → Runtime → UI
- 通过自定义 linter 和结构测试强制执行
- 允许边界内自由，强制执行边界

**相关文章**：
- [[工程技术：在智能体优先的世界中利用 Codex]]

#### Harness 可读性
- 代码库对代理可读
- 文档版本化
- 执行计划作为一流工件

**相关文章**：
- [[工程技术：在智能体优先的世界中利用 Codex]]

## 实践案例

### OpenAI 的实践
- 100 万行代码，零人工编写
- 3 名工程师，1500 个 PR
- 每位工程师每天 3.5 个 PR

**相关文章**：
- [[工程技术：在智能体优先的世界中利用 Codex]]

### Anthropic 的实践
- Claude 代理 SDK
- 多上下文窗口工作流
- 初始化代理 + 编码代理模式

**相关文章**：
- [[Effective harnesses for long-running agents]]
- [[Harness design for long-running application development]]

### LangChain 的实践
- Terminal Bench 2.0 排名从 Top 30 提升到 Top 5
- 只改变 harness，不改变模型
- 自验证和追踪是关键

**相关文章**：
- [[Improving Deep Agents with harness engineering]]

## 工具与技术栈

### 代理框架
- Claude Agent SDK
- LangChain Deep Agents
- Codex CLI

### 验证工具
- Playwright MCP（浏览器自动化）
- Chrome DevTools Protocol
- Puppeteer MCP

### 监控与追踪
- LangSmith
- OpenTelemetry
- LogQL / PromQL

## 学习路径

### 入门
1. 阅读 [[What Harness Engineering Actually Means]] 了解基本概念
2. 阅读 [[The Anatomy of an Agent Harness]] 了解核心组件
3. 阅读 [[Harness engineering for coding agent users]] 了解用户视角

### 进阶
4. 阅读 [[Effective harnesses for long-running agents]] 了解长时间运行代理
5. 阅读 [[Harness design for long-running application development]] 了解多代理架构
6. 阅读 [[Improving Deep Agents with harness engineering]] 了解性能优化

### 高级
7. 阅读 [[工程技术：在智能体优先的世界中利用 Codex]] 了解工业级实践
8. 阅读 [[Ralph Wiggum as a software engineer]] 了解简单但有效的技术

## 开放问题

1. **行为 Harness**：如何确保应用程序按预期运行？
2. **Harness 一致性**：如何保持指南和传感器同步？
3. **Harness 覆盖度**：如何评估 harness 的质量？
4. **模型演进**：随着模型改进，harness 如何适应？

## 参考资源

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

本 Wiki 基于以下 10 篇核心文章构建：

1. [[Building Effective AI Coding Agents for the Terminal Scaffolding, Harness, Context Engineering, and Lessons Learned]]
2. [[Effective harnesses for long-running agents]]
3. [[Harness design for long-running application development]]
4. [[Harness engineering for coding agent users]]
5. [[Improving Deep Agents with harness engineering]]
6. [[OpenAI's Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]
7. [[Ralph Wiggum as a software engineer]]
8. [[The Anatomy of an Agent Harness]]
9. [[What Harness Engineering Actually Means]]
10. [[工程技术：在智能体优先的世界中利用 Codex]]

---

**最后更新**: 2026-06-02
**维护者**: Claudian (AI Assistant)
