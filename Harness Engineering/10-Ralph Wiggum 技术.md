---
title: "Ralph Wiggum 技术"
created: 2026-06-02
description: "简单但有效的代理循环技术"
tags:
  - "ralph-wiggum"
  - "loop"
  - "simple"
---

# Ralph Wiggum 技术

## 什么是 Ralph Wiggum？

> "Ralph 是一个技术。在其最纯粹的形式中，Ralph 是一个 Bash 循环。" - [Geoffrey Huntley](https://ghuntley.com/ralph/)

**定义**：Ralph Wiggum 是一种简单但有效的代理循环技术，将代理放在 while 循环中，通过提示调优来改进。

**代码**：
```bash
while :; do cat PROMPT.md | claude-code ; done
```

## 为什么叫 Ralph Wiggum？

Ralph Wiggum 是《辛普森一家》中的角色，以天真、简单和偶尔的愚蠢著称。这个技术之所以叫这个名字，是因为：

- **简单**：技术本身非常简单
- **有效**：尽管简单，但非常有效
- **可调优**：像调吉他一样调优

> "Ralph 有三种状态：未烤熟、烤熟、或烤熟但有未指定的潜在行为（有时相当不错！）" - Geoffrey Huntley

## Ralph 的核心原则

### 1. 单任务循环
> "每次循环只做一件事。我需要重复自己 - 每次循环只做一件事。" - Geoffrey Huntley

**原则**：
- 每次循环只处理一个任务
- 不要一次做太多
- 保持简单

**示例**：
```markdown
# PROMPT.md

你的任务是实现缺失的 stdlib（参见 @specs/stdlib/*）和编译器功能。

## 步骤
1. 阅读 @fix_plan.md 了解当前计划
2. 选择最重要的 10 件事
3. 使用子代理搜索代码库（不要假设未实现）
4. 实现功能
5. 运行测试
6. 更新 @fix_plan.md
```

### 2. 确定性堆栈分配
> "另一个关键点是确定性地分配堆栈，每次循环都相同。" - Geoffrey Huntley

**原则**：
- 每次循环都加载相同的上下文
- 包括计划、规格、标准库
- 保持一致性

**示例**：
```bash
# 每次循环都加载相同的文件
while :; do
  cat PROMPT.md \
    specs/stdlib/* \
    fix_plan.md \
    AGENT.md \
    | claude-code
done
```

### 3. 子代理扩展
> "Ralph 需要一种思维方式，即不分配到主上下文窗口。相反，你应该做的是生成子代理。" - Geoffrey Huntley

**原则**：
- 主上下文窗口作为调度器
- 子代理执行昂贵的工作
- 控制并行度

**示例**：
```markdown
# 使用子代理

你的任务是使用最多 500 个子代理来研究现有源代码。

## 子代理任务
- 搜索文件系统
- 读取和分析代码
- 生成报告

## 限制
- 只有 1 个子代理用于构建/测试
- 最多 500 个子代理用于搜索和分析
```

### 4. 反馈循环
> "你想以 Ralph 可以将自己循环回 LLM 进行评估的方式进行编程。" - Geoffrey Huntley

**原则**：
- 让代理能够自我评估
- 提供反馈信号
- 持续改进

**示例**：
```markdown
# 反馈循环

## 验证步骤
1. 运行测试
2. 检查输出
3. 与规格对比
4. 如果失败，修复问题
5. 重复直到通过

## 反馈信号
- 测试通过：好的
- 测试失败：需要修复
- 编译错误：需要修复
- 性能问题：需要优化
```

## Ralph 的工作流程

### 阶段 1：生成

**目标**：生成代码

**实践**：
- 使用规格和标准库
- 遵循技术模式
- 生成完整实现

**示例**：
```markdown
# 生成阶段

## 输入
- 规格：specs/stdlib/*
- 标准库：src/stdlib/*
- 计划：fix_plan.md

## 输出
- 实现的代码
- 更新的 fix_plan.md
- 测试结果
```

### 阶段 2：反压

**目标**：验证代码质量

**实践**：
- 运行测试
- 检查类型
- 验证架构

**示例**：
```markdown
# 反压阶段

## 验证步骤
1. 运行单元测试
2. 运行集成测试
3. 检查类型安全
4. 验证架构约束

## 反压信号
- 测试通过：继续
- 测试失败：修复
- 类型错误：修复
- 架构违规：修复
```

### 阶段 3：学习

**目标**：从错误中学习

**实践**：
- 记录错误
- 更新规格
- 改进提示

**示例**：
```markdown
# 学习阶段

## 错误记录
- 错误类型：编译错误
- 错误原因：缺少函数
- 修复方案：实现函数

## 规格更新
- 更新 specs/stdlib/FILE.md
- 添加缺失的函数规格

## 提示改进
- 更新 PROMPT.md
- 添加新的指导
```

## Ralph 的最佳实践

### 1. 简单提示
> "没有完美的提示。" - Geoffrey Huntley

**原则**：
- 保持提示简单
- 不要过度复杂
- 专注于核心任务

**示例**：
```markdown
# 简单提示

你的任务是实现缺失的 stdlib。

## 步骤
1. 阅读规格
2. 选择最重要的功能
3. 实现功能
4. 运行测试
5. 更新计划
```

### 2. 渐进式改进
> "每次 Ralph 做了坏事，Ralph 就会被调优 - 像吉他一样。" - Geoffrey Huntley

**原则**：
- 从简单开始
- 逐步增加复杂度
- 持续改进

**示例**：
```markdown
# 渐进式改进

## 第 1 轮
- 实现基本功能
- 运行简单测试

## 第 2 轮
- 添加更多功能
- 运行更全面的测试

## 第 3 轮
- 优化性能
- 修复边界情况
```

### 3. 监控和调优
> "当你醒来发现 Ralph 在做多个实现时，你需要调优这一步。" - Geoffrey Huntley

**原则**：
- 监控代理行为
- 识别问题模式
- 调优提示

**示例**：
```markdown
# 监控和调优

## 监控指标
- 任务完成率
- 错误率
- 代码质量

## 问题模式
- 代理跳过测试
- 代理忽略规格
- 代理重复实现

## 调优策略
- 添加更明确的指导
- 强调测试重要性
- 明确规格要求
```

### 4. 版本控制
> "当测试通过时更新 @fix_plan.md，然后添加更改的代码和 @fix_plan.md，使用 'git add -A'，然后做 'git commit'。" - Geoffrey Huntley

**原则**：
- 每次更改都提交
- 使用描述性提交消息
- 保持历史清晰

**示例**：
```bash
# 版本控制
git add -A
git commit -m "feat: implement user authentication"
git push
```

## Ralph 的变体

### 1. 基础 Ralph

**代码**：
```bash
while :; do cat PROMPT.md | claude-code ; done
```

**特点**：
- 最简单
- 最纯粹
- 最易调试

### 2. 带子代理的 Ralph

**代码**：
```bash
while :; do
  cat PROMPT.md | claude-code --subagents 500
done
```

**特点**：
- 支持并行工作
- 更快完成
- 更复杂

### 3. 带验证的 Ralph

**代码**：
```bash
while :; do
  cat PROMPT.md | claude-code
  npm test || true
done
```

**特点**：
- 自动验证
- 自动修复
- 更可靠

### 4. 带监控的 Ralph

**代码**：
```bash
while :; do
  cat PROMPT.md | claude-code
  echo "$(date): Task completed" >> log.txt
done
```

**特点**：
- 记录进度
- 便于调试
- 可追溯

## Ralph 的挑战

### 1. 循环检测
> "代理可以陷入'doom loop'，做出小变化永远循环。" - [LangChain](https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering)

**问题**：
- 代理可能重复相同错误
- 无法自我纠正
- 浪费时间和资源

**解决方案**：
- 循环检测中间件
- 添加上下文提醒
- 强制重新考虑计划

**示例**：
```python
class LoopDetectionMiddleware:
    def on_tool_call(self, file_path):
        self.edit_counts[file_path] += 1
        
        if self.edit_counts[file_path] > N:
            # 添加上下文提醒
            return "...consider reconsidering your approach"
```

### 2. 质量控制
> "不要实现占位符或简单实现。我们想要完整实现。" - Geoffrey Huntley

**问题**：
- 代理可能生成低质量代码
- 可能使用占位符
- 可能跳过测试

**解决方案**：
- 强调质量要求
- 使用强提示
- 添加验证步骤

**示例**：
```markdown
# 质量控制

## 要求
- 不要实现占位符
- 不要使用简单实现
- 我们想要完整实现

## 验证
- 运行所有测试
- 检查代码质量
- 验证功能完整性
```

### 3. 成本控制
> "Ralph 可以替代大多数公司的外包。" - Geoffrey Huntley

**问题**：
- 代理运行有成本
- 可能消耗大量 tokens
- 需要成本控制

**解决方案**：
- 监控 token 使用
- 设置预算限制
- 优化提示效率

**示例**：
```bash
# 成本控制
while :; do
  # 限制 token 使用
  cat PROMPT.md | claude-code --max-tokens 10000
  
  # 检查成本
  cost=$(calculate_cost)
  if [ "$cost" -gt "$BUDGET" ]; then
    echo "Budget exceeded"
    break
  fi
done
```

## Ralph 的实际案例

### Geoffrey Huntley 的 CURSED 项目

**场景**：构建新的编程语言

**实践**：
1. 使用 Ralph 循环构建编译器
2. 使用子代理并行工作
3. 使用规格和标准库指导

**结果**：
- 成功构建了新的编程语言
- 代理能够编程在该语言中
- 语言不在 LLM 训练数据中

**提示示例**：
```markdown
# CURSED 编译器提示

你的任务是实现缺失的 stdlib 和编译器功能。

## 步骤
1. 学习 specs/* 了解编译器规格
2. 学习 fix_plan.md 了解当前计划
3. 使用最多 500 个子代理研究源代码
4. 选择最重要的 10 件事
5. 实现功能
6. 运行测试
7. 更新 fix_plan.md
```

### Y Combinator 黑客马拉松

**场景**：使用 Ralph 构建多个仓库

**实践**：
1. 将代理放在 while 循环中
2. 让代理自主工作
3. 监控进度

**结果**：
- 一夜之间发布了 6 个仓库
- 代理能够自主完成工作
- 证明了 Ralph 的有效性

## Ralph 的哲学

### 1. 最终一致性
> "构建软件需要大量的信念和对最终一致性的信念。" - Geoffrey Huntley

**原则**：
- 相信代理最终会做对
- 不要期望完美
- 接受错误和修复

### 2. 调优而非放弃
> "每次 Ralph 做了坏事，Ralph 就会被调优 - 像吉他一样。" - Geoffrey Huntley

**原则**：
- 不要放弃代理
- 调优提示和环境
- 持续改进

### 3. 简单而非复杂
> "Ralph 是单体的。Ralph 作为单个进程在单个仓库中自主工作。" - Geoffrey Huntley

**原则**：
- 保持简单
- 避免过度工程
- 专注于核心任务

## 相关文章

- [[Ralph Wiggum as a software engineer]] - 原始文章
- [[02-长时间运行代理设计]] - 长时间运行代理
- [[05-多代理架构]] - 多代理协调

## 关键要点

1. **简单有效**：Ralph 是一个简单的 while 循环
2. **单任务循环**：每次循环只做一件事
3. **确定性分配**：每次循环加载相同上下文
4. **子代理扩展**：使用子代理并行工作
5. **持续改进**：调优提示和环境

## 下一步

- 阅读 [[01-Harness 定义与核心概念]] 回顾基础
- 阅读 [[HOME|Harness Engineering Wiki]] 返回主页
- 阅读 [[Ralph Wiggum as a software engineer]] 了解更多细节

---

**相关概念**：[[HOME|Harness Engineering Wiki]]
