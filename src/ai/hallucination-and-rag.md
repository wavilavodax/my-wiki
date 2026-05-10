# AI 幻觉与 RAG

来源：[Why does AI lie? Hallucinations explained simply](https://dev.to/aws/why-does-ai-lie-hallucinations-explained-simply-1c7g)

## 本质
AI 不是故意撒谎，而是天生会填充自己不知道的东西。LLM 的训练目标是生成“听起来合理的回答”，而非判断真假。

> 幻觉不是 bug，是架构特性。

## RAG
RAG = 给模型指定资料，只从资料里回答。
- 企业知识库、内部文档问答的标配方案
- 检索质量决定回答质量
- 可追溯、可控、可更新

对比 RAG vs 联网搜索：RAG 数据源是你给的文档，可控；搜索数据源是互联网，实时但不可控。
