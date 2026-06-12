---
title: "Transformer"
type: concept
tags: [AI, deep-learning, architecture]
created: 2026-06-12
updated: 2026-06-12
source: "Attention Is All You Need (Vaswani et al., 2017)"
status: growing
related: ["[[注意力机制]]", "[[自注意力]]", "[[多头注意力]]"]
---

# Transformer

## 定义

Transformer 是一种基于**自注意力机制**的深度学习架构，摒弃了传统的 RNN/CNN 结构，完全依赖注意力机制来捕捉序列中的全局依赖关系。

## 核心要点

1. **自注意力机制**：每个位置都能直接关注序列中的所有其他位置
2. **并行计算**：不像 RNN 需要顺序处理，Transformer 可以并行处理整个序列
3. **编码器-解码器结构**：由编码器和解码器两部分组成，各包含多层堆叠

## 工作原理

```
输入 → 嵌入层 → 位置编码 → [编码器 × N] → [解码器 × N] → 线性层 → 输出
```

编码器的每一层包含：
- [[多头注意力]] (Multi-Head Attention)
- 前馈神经网络 (FFN)
- 残差连接 + 层归一化

## 应用场景

- **NLP**: 机器翻译、文本生成、问答系统
- **计算机视觉**: ViT (Vision Transformer)
- **多模态**: CLIP、GPT-4V

## 与其他概念的关系

- 基于 [[注意力机制]]，是其最成功的应用
- 替代了 [[RNN]] 和 [[LSTM]] 在序列建模中的地位
- 衍生出 [[BERT]]（仅编码器）和 [[GPT]]（仅解码器）

---

*状态: growing | 最后更新: 2026-06-12*
