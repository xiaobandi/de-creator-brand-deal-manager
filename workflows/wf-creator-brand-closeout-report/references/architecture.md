# 结案数据报告 · 速查

| 项 | 内容 |
|---|---|
| slug | `wf-creator-brand-closeout-report` |
| 层级 | L2-workflow |
| 归属 | 商单对接管家（`de-creator-brand-deal-manager`） |
| 复杂度 / 阶段 | S / P2 |
| 能力族 | — |
| 定义出处 | — |
| 复用情况 | — |

## 调用的 SKILL

| 技能 | slug | 来源 |
|---|---|---|
| 简报生成 | `brief-generator` | agent-skills-core |
| 文案排版 | `copy-layout` | agent-skills-core |

## 字段

| 项 | 内容 |
|---|---|
| 必需输入 | 本工作流的起始材料（见 `SKILL.md`「执行步骤」第 1 步）；用户身份与目标平台/渠道 |
| 可选输入 | 历史产出；账号人设；渠道规则；上一周期的数据 |
| 产出 | 续约建议 |
| 脚本 | 无 |
