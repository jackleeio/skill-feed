# SkillFeed

SkillFeed 是一个场景驱动的 Skill 推荐器：当任务失败、超时或重试过多时，它会自动构建搜索词并在 ClawHub 中推荐最合适的技能与修复路径。

## 核心能力

- 失败检测：识别 API 报错、超时、缺失输出、重试过多
- 智能检索：自动生成 Q1/Q2/Q3 分层查询词
- 推荐输出：主推荐 + 备选 + 立即执行步骤 + fallback
- 多模型适配：Claude Code / ChatGPT / Gemini 输出风格映射

## 目录结构

- `SKILL.md`：主流程与触发规则
- `references/discovery-workflow.md`：检索与排序策略
- `references/query-templates.md`：场景查询模板
- `references/provider-adaptation.md`：跨模型适配指南

## 打包文件

- `../dist/skill-feed.skill`

## 快速使用

1. 安装 skill
2. 输入场景或失败信号
3. 获取推荐技能与执行步骤
4. 按步骤验证并回传结果进行下一轮推荐
