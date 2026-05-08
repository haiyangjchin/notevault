相关的术语：
AI agent、AI Tool、LLM、Function Calling、MCP(server、client)、RAG
Prompt User prompt/System prompt SillyTavern
Prompt Engineering
Zero-shot/Few-shot/Chain-of-Thought(CoT)思维链（引导方式帮助AI回答问题）
Context、Context Window、Context Engineering

RAG流程
1、用户提问前（准备）：①分片（按字数、段落、章节、页码分）、②索引（通过Embedding将片段文本转为向量、将片段文本和片段向量存入向量数据库中）
2、用户提问后（回答）：①召回（搜索与用户问题相关的片段，计算向量相似度（余弦相似度、欧氏距离、点积），成本低、耗时短、准确率低、适合初步筛选，类似简历筛选）、②重排（与召回类似，cross-encoder，成本高、耗时长、准确率高、适合精挑细选，类似面试）、③生成（将经过召回和重排后的相关片段与用户问题交给大模型生成最后的答案）

Context-模型输入
Context Window-模型输入的容量上限：Token（1Token≈0.75个单词/1.5汉字）
Context Engineering-精心设计给模型的输入内容
Context Engineering的实现方法：①保存Context、②选择Context、③压缩Context、④隔离Context
1、保存Context：Context筛选总结然后保存到内存/硬盘
2、选择Context：①静态选择（所有内容全部放入Context中，如claude的CLAUDE.md）、②动态选择（选择与用户问题最相关的内容放入Context中、如RAG）
3、压缩Context：对模型输入文本和工具执行结果进行压缩（如claude的auto-compact）
4、隔离Context：不同模块之间的Context是互相隔离的、互不干扰（如claude的Multi-Agent：Lead Agent与若干Subagent）