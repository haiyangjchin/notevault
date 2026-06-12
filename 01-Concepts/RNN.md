---
title: "RNN"
type: concept
tags: [AI, deep-learning, architecture, sequence-modeling]
created: 2026-06-12
updated: 2026-06-12
source: "Learning long-term dependencies with gradient descent is difficult (Bengio et al., 1994)"
status: seed
related: "[[LSTM]]", "[[Transformer]]", "[[梯度消失]]"
---

# RNN（循环神经网络）

## 定义

RNN（Recurrent Neural Network，循环神经网络）是一类具有**循环连接**的神经网络，能够处理**序列数据**。它通过将前一时间步的隐藏状态作为当前时间步的输入之一，来捕捉序列中的时序依赖关系。

## 核心要点

1. **参数共享**：同一组权重在所有时间步复用，大幅减少参数量
2. **隐藏状态**：$h_t = f(W_h h_{t-1} + W_x x_t + b)$，隐藏状态 $h_t$ 充当网络的"记忆"
3. **变长输入**：理论上可以处理任意长度的序列
4. **信息瓶颈**：所有历史信息被压缩到固定维度的隐藏向量中

## 工作原理

```
x₁ → [RNN Cell] → h₁
x₂ → [RNN Cell] → h₂
x₃ → [RNN Cell] → h₃
...
xₜ → [RNN Cell] → hₜ → Output
```

展开后等价于一个很深的前馈网络，每个时间步共享参数。

**前向传播：**
- $h_t = \tanh(W_{hh} h_{t-1} + W_{xh} x_t + b_h)$
- $y_t = W_{hy} h_t + b_y$

## 关键局限

- **梯度消失 / 梯度爆炸**：反向传播需要穿越所有时间步（BPTT），梯度随序列长度指数衰减或膨胀，导致难以学习长距离依赖
- **顺序计算**：无法并行处理不同时间步，训练效率低
- **长程记忆弱**：隐藏状态容量有限，早期信息容易被后期信息覆盖

这些问题催生了 [[LSTM]] 和 [[GRU]] 等门控变体，以及彻底抛弃循环结构的 [[Transformer]]。

## 应用场景

- **自然语言处理**：语言模型、命名实体识别、机器翻译（早期 Seq2Seq）
- **语音识别**：声学模型建模
- **时间序列预测**：股票价格、气象数据

## 与其他概念的关系

- [[LSTM]] 和 [[GRU]] 是 RNN 的门控改进版本，缓解了 [[梯度消失]] 问题
- [[Transformer]] 完全替代了 RNN 的循环结构，通过 [[自注意力]] 实现并行计算
- [[Seq2Seq]] 模型最初基于 RNN 编码器-解码器架构

---

*状态: seed | 最后更新: 2026-06-12*
