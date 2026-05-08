AI agent、AI Tool、LLM、Function Calling、MCP(server、client)
Prompt User prompt/System prompt SillyTavern
Prompt Engineering
Zero-shot/Few-shot/Chain-of-Thought(CoT)思维链（引导方式帮助AI回答问题）
Context
Context Engineering

RAG流程
用户提问前（准备）：分片（按字数、段落、章节、页码分）、索引（通过Embedding将片段文本转为向量、将片段文本和片段向量存入向量数据库中）
用户提问后（回答）：召回（搜索与用户问题相关的片段，计算向量相似度（余弦相似度、欧氏距离、点积），成本低、耗时短、准确率低、适合初步筛选，类似简历筛选）、重排（与召回类似，cross-encoder，成本高、耗时长、准确率高、适合精挑细选，类似面试）、生成