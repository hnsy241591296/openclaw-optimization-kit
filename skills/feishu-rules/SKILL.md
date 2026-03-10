---
name: feishu-rules
description: Rules for Feishu operations and messaging
---
# 飞书操作规则
## 触发条件
发飞书消息、操作飞书文档、日历、多维表格时触发

## 核心规则
1. 发消息前必须确认收件人和内容
2. 读取操作可直接执行
3. 写入操作需二次确认
4. 不在群聊中代表用户发言
5. 批量写入前先测试单条
