---
name: memory-rules
description: Rules for memory retrieval and storage - how to read and write memories efficiently
---
# 记忆管理规则

## 读取记忆（对话开始时）
1. 先用 memory_search 语义搜索，不要直接全量读取文件
2. 只用 memory_get 读取搜索到的相关片段
3. 不确定时说"我查了记忆但没找到相关内容"

## 写入记忆（用户说"记住"时）
1. 立即写入 memory/YYYY-MM-DD.md
2. 重要事实（姓名/偏好/决定）同步更新 MEMORY.md 索引

## MEMORY.md 的作用
- 只存核心事实（姓名、偏好、重要决定）
- 不存对话记录
- 每条不超过一行

## 禁止
- 全量读取 memory/ 目录下所有文件
- 把整段对话记录写入 MEMORY.md
