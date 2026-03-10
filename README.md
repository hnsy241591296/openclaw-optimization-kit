# OpenClaw Agent Optimization Kit
### 基于 OpenClaw 的 Agent 架构优化方案

> 将每次请求的 Token 消耗从 **~40,000** 降低至 **~5,000**，同时保持推理质量。  
> Reduce token usage per request from **~40,000** to **~5,000** while maintaining reasoning quality.

---

## 简介 / Introduction

本项目是基于 [OpenClaw](https://github.com/openclaw-ai/openclaw)（MIT License）的 Agent 配置优化方案，包含经过实战调优的 `SOUL.md` 系统提示、9 个模块化 Skill 文件，以及完整的架构设计文档。

This project is an Agent configuration optimization kit built on top of [OpenClaw](https://github.com/openclaw-ai/openclaw) (MIT License). It includes a battle-tested `SOUL.md` system prompt, 9 modular skill files, and a complete architecture design document.

---

## 优化效果 / Results

| 组件 / Component | 优化前 / Before | 优化后 / After | 节省 / Saved |
|---|---|---|---|
| 系统提示 System Prompt | ~500 tokens | ~80 tokens | **84%** |
| 工具加载 Tool Loading | ~8,000 tokens | ~600 tokens | **93%** |
| 记忆注入 Memory Injection | ~5,000 tokens | ~400 tokens | **92%** |
| 对话历史 Conversation History | ~20,000 tokens | ~1,500 tokens | **93%** |
| 插件提示 Plugin Prompts | ~3,000 tokens | ~200 tokens | **93%** |
| **总计 Total** | **~40,000 tokens** | **~3,000 tokens** | **92%** |

---

## 文件结构 / File Structure

```
workspace/
├── SOUL.md                    # 最小化系统提示 / Minimal system prompt
├── MEMORY.md                  # 核心记忆索引 / Core memory index
├── ARCHITECTURE.md            # 架构设计文档 / Architecture design doc
└── skills/
    ├── search/                # 搜索规则 / Search rules
    ├── coding-rules/          # 编码规则 / Coding rules
    ├── feishu-rules/          # 飞书操作规则 / Feishu operation rules
    ├── reasoning-rules/       # 推理规则 / Reasoning rules
    ├── tool-router/           # 工具路由策略 / Tool routing policy
    ├── memory-rules/          # 记忆管理规则 / Memory management rules
    ├── context-management/    # 上下文压缩规则 / Context compression rules
    ├── token-budget/          # Token 预算规则 / Token budget rules
    └── self-reflection/       # 回复前自检规则 / Pre-response checklist
```

---

## 核心设计 / Core Design

### 1. 最小化系统提示 / Minimal System Prompt
`SOUL.md` 仅保留角色定义、核心规则和硬性约束，去除一切冗余描述。  
`SOUL.md` retains only role definition, core rules, and hard constraints — no fluff.

### 2. 模块化 Skill 系统 / Modular Skill System
9 个 Skill 按需加载，Agent 根据任务类型自动选择对应模块，避免全量注入。  
9 skills are loaded on-demand. The agent selects the relevant module based on task type, avoiding full injection.

### 3. RAG 记忆检索 / RAG Memory Retrieval
用 `memory_search` 语义检索替代全量读取 `MEMORY.md`，只注入相关记忆片段。  
Replace full `MEMORY.md` injection with `memory_search` semantic retrieval — only relevant snippets are injected.

### 4. 工具路由策略 / Tool Routing Policy
`tool-router` skill 定义各任务类型对应的最小工具集，避免无效工具调用。  
The `tool-router` skill defines the minimal toolset per task type, eliminating unnecessary tool calls.

### 5. 上下文压缩 / Context Compression
结合 OpenClaw 内置的 `compaction` 机制，超过阈值时自动压缩历史对话。  
Leverages OpenClaw's built-in `compaction` mechanism to auto-compress history when thresholds are exceeded.

---

## 安装使用 / Installation

### 前提条件 / Prerequisites
- 已安装 [OpenClaw](https://github.com/openclaw-ai/openclaw)
- OpenClaw version 2026.3.9+

### 步骤 / Steps

**1. 克隆本仓库 / Clone this repo**
```bash
git clone https://github.com/YOUR_USERNAME/openclaw-optimization-kit.git
```

**2. 复制 workspace 文件 / Copy workspace files**
```bash
# macOS/Linux
cp -r workspace/* ~/.openclaw/workspace/

# Windows PowerShell
Copy-Item -Recurse workspace\* "$HOME\.openclaw\workspace\"
```

**3. 在 openclaw.json 中注册 Skills / Register skills in openclaw.json**

在 `~/.openclaw/openclaw.json` 的 agent 配置中添加：  
Add to your agent config in `~/.openclaw/openclaw.json`:

```json
{
  "agents": {
    "list": [
      {
        "id": "main",
        "skills": [
          "web_search",
          "search",
          "coding-rules",
          "feishu-rules",
          "reasoning-rules",
          "tool-router",
          "memory-rules",
          "context-management",
          "token-budget",
          "self-reflection"
        ]
      }
    ]
  }
}
```

**4. 重启 OpenClaw / Restart OpenClaw**

---

## 注意事项 / Notes

- 本方案在 **DeepSeek Chat** 模型下测试，切换至 Claude 等模型效果更佳。  
  Tested with **DeepSeek Chat**. Switching to Claude or similar models may yield even better instruction-following.
- `MEMORY.md` 中的个人信息请替换为你自己的内容后再上传。  
  Replace personal information in `MEMORY.md` with your own before uploading.
- Skills 的触发依赖模型对 `description` 字段的理解能力。  
  Skill triggering depends on the model's ability to understand the `description` field.

---

## 致谢 / Credits

- 基于 [OpenClaw](https://github.com/openclaw-ai/openclaw) — MIT License — Copyright (c) 2025 彼得·斯坦伯格  
- 架构优化方案由用户与 Claude (Anthropic) 协作设计完成。  
- Architecture optimization designed collaboratively by the user and Claude (Anthropic).

---

## License

MIT License — 详见 / See [LICENSE](./LICENSE)
