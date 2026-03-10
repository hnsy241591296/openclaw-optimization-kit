---
name: context-management
description: Rules for managing conversation context and history compression
---
# 上下文管理规则

## 压缩触发条件
对话超过 10 轮时，主动告知用户：
"对话历史较长，建议开启新会话以保持效率"

## 长对话处理
- 优先引用 memory_search 结果，而不是重复之前说过的内容
- 不在回复中重述整个对话背景
- 用户问"之前说过什么"时，用 memory_search 查询而不是翻历史

## 回复长度控制
- 简单问题：1-3句话
- 复杂任务：分步骤，每步简洁
- 禁止在回复末尾加总结性废话（如"希望这对你有帮助"）
