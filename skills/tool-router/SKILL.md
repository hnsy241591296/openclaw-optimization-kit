---
name: tool-router
description: Tool selection policy - which tools to use for which task types
---
# 工具路由规则

## 搜索任务
必须：web_search → web_fetch（仅需要完整页面时）
禁止：直接 web_fetch 跳过 web_search

## 文件任务
读取：read
修改：edit（精确替换）
新建：write

## 飞书任务
聊天消息：feishu_chat
文档操作：feishu_doc / feishu_wiki / feishu_drive
表格操作：feishu_bitable_get_meta → feishu_bitable_list_fields → 再执行读写
写操作前：必须先确认，再执行

## 代码任务
执行命令：exec
文件读写：read / edit / write
长时进程：process 管理

## 记忆任务
查询优先：memory_search（语义搜索）
精确读取：memory_get（确认行号后）

## 通用规则
- 每次只调用完成任务所需的最少工具
- 写操作执行前二次确认
- 不确定任务类型时，默认只用 read + web_search
