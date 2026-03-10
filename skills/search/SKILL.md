---
name: search
description: Rules for web search operations
---
# 网络搜索规则

## 触发条件
查实时信息（天气/价格/新闻）时触发

## 核心规则
1. 必须先用 web_search，禁止直接用 web_fetch
2. 搜索词控制在 3-6 词
3. 不重复搜索同一关键词
4. 需要完整页面时才用 web_fetch

## 输出规则
- 天气：只说天气状况+温度+一句建议，不超过3行
- 新闻：只说核心结论，不超过5行
- 价格：直接给数字+来源
- 禁止输出完整生活指数列表
