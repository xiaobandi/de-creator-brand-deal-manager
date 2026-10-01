# 商单内容合规审查

> 商单稿→广告法敏感词专项校验→修改建议

工作流 `wf-creator-brand-compliance`　·　归属 商单对接管家　·　触发 事件（交稿前）　·　
复杂度 M　·　阶段 P2

## 调用链

- `广告合规审查`（ad-compliance-review）
- `平台合规词扫描`（compliance-word-scan）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 商单对接管家 的「商单内容合规审查」：<你的输入>
```
