# OpenClaw Agent 优化架构 v2

## 优化目标
token 使用从 ~40k 降低到 ~5k，保持推理质量。

## 文件结构
workspace/
├── SOUL.md              # 最小化系统提示（角色+核心规则）
├── MEMORY.md            # 核心记忆索引（轻量）
├── memory/              # 按日期的详细记忆
│   └── YYYY-MM-DD.md
└── skills/              # 按需加载的行为模块
    ├── search/          # 搜索规则
    ├── coding-rules/    # 编码规则
    ├── feishu-rules/    # 飞书操作规则
    ├── reasoning-rules/ # 推理规则
    ├── tool-router/     # 工具选择策略
    ├── memory-rules/    # 记忆管理规则
    ├── context-management/ # 上下文压缩规则
    ├── token-budget/    # Token 预算规则
    └── self-reflection/ # 回复前自检规则

## 各组件作用
| 组件 | 作用 | 节省 |
|------|------|------|
| SOUL.md | 极简系统提示 | 减少固定开销 |
| skills/ | 按需注入行为规则 | 按任务只加载相关 skill |
| MEMORY.md | 轻量索引 | 替代全量记忆注入 |
| memory_search | RAG 检索记忆 | 只读相关片段 |
| tool-router | 工具选择策略 | 避免无效工具调用 |
| self-reflection | 回复前自检 | 减少幻觉和冗余 |
