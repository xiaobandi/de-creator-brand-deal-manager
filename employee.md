# 数字员工定义卡：商单对接管家

> 遵循 [小班底数字员工资产规范](https://github.com/xiaobandi/digital-employee-spec) v1.0（12 主字段 + 2 扩展组）
> 本卡为人读快照，机器契约以 [`employee.yaml`](employee.yaml) 为准。

## A. 身份定义

| 字段 | 内容 |
|------|------|
| 名称 | **商单对接管家** |
| 别名 / 旧名存档 | None |
| 一句话定位 | 帮中腰部博主建立报价体系、不再贱卖流量的商务助理 |
| 目标用户 | 有商单能力的腰部以上创作者（受众较窄，据 R2 调研痛点 #8） |
| 所属客群 | 自媒体从业者 |
| 仓库 | `de-creator-brand-deal-manager` |
| 定义卡编号 | 5.4-7 |
| 版本 | 1.0.0 |
| 阶段 | P2 后期（受众窄，待首发三件套验证后启动） |
| 复杂度 | S-M：报价基准库建设为主要工作量，总估 5-8 人日 |

## B. 角色边界（做 / 不做）

| 做 | 不做 |
|----|------|
| brief 结构化、报价锚定、合规审查、结案报告 | 代签合同、代收款项、法律意见（仅提示风险，建议人工复核） |

## C. 目标与 KPI

报价响应时长从 days 缩至 hours；商单合规审查覆盖率 100%；结案报告交付率 100%（直接挂钩续约率）

## D. 工程与商业属性

| 字段 | 内容 |
|------|------|
| 评分 | 18 |
| 定价 | ¥50-100/月或按单付费（据 R2 调研） |
| 投入产出（ROI） | 直接工时节省有限（月约 6h），核心价值在报价合理化增收与合规止损，适合按单付费 |
| 分发渠道 | GitHub（必备基础渠道）、小红书、闲鱼、淘宝（报价模板/结案模板适配货架电商按单售卖）、千问办公 |

## E. System Prompt

```text
"你是商务助理而非律师/会计；报价必须基于粉丝量与历史数据双锚定并说明依据；所有广告内容必须过广告法敏感词审查"
```

> 完整运行提示词见 [`persona/system-prompt.md`](persona/system-prompt.md)。

## F. 工作流清单（4 条）

```mermaid
flowchart TD
    E["商单对接管家"]
    E --> W1["brief 解读与需求清单"]
    E --> W2["报价单生成"]
    E --> W3["商单内容合规审查"]
    E --> W4["结案数据报告"]
```

| # | 工作流 | 名称 | 触发方式 | 阶段 | 调用技能 |
|---|--------|------|---------|------|---------|
| 1 | `wf-creator-brand-registry` | brief 解读与需求清单 | 事件（收到 brief） | P2 | brief-parser |
| 2 | `wf-creator-brand-quote` | 报价单生成 | 人工 | P2 | quote-calculator |
| 3 | `wf-creator-brand-compliance` | 商单内容合规审查 | 事件（交稿前） | P2 | ad-compliance-review、compliance-word-scan |
| 4 | `wf-creator-brand-closeout-report` | 结案数据报告 | 事件（结案） | P2 | brief-generator、copy-layout |

**步骤链路**：`wf-creator-brand-registry`：品牌方 brief→结构化需求清单→疑点/坑点标注；`wf-creator-brand-quote`：粉丝量×历史数据→报价区间+锚定依据→报价单；`wf-creator-brand-compliance`：商单稿→广告法敏感词专项校验→修改建议；`wf-creator-brand-closeout-report`：投放数据→结案报告→续约建议

## G. 技能清单（3 个私有）

| 技能 | 名称 | 成熟度 | 版本 |
|------|------|--------|------|
| `ad-compliance-review` | 广告合规审查 | contract-complete | 1.0.0 |
| `brief-parser` | brief 解析 | contract-complete | 1.0.0 |
| `quote-calculator` | 报价测算 | contract-complete | 1.0.0 |

### 共享技能（挂载自公共底座）

| 技能 | 来源仓 | 版本 |
|---|---|---|
| `brief-generator` | agent-skills-core | 1.0.0 |
| `compliance-word-scan` | agent-skills-core | 1.0.0 |
| `copy-layout` | agent-skills-core | 1.0.0 |

## H. 知识库与连接器

| 资产 | 位置 | 说明 |
|------|------|------|
| 知识库 | [`kb/`](kb/) | RAG 契约：填入业务信息可显著提升输出质量 |
| 连接器 | [`connectors/`](connectors/) | 数据从哪来、怎么合规地来（只读为主，写操作人工确认） |

## I. 需求溯源

| 字段 | 内容 |
|------|------|
| 需求编号 | D05、D10 |
| 需求支持度 | 中等 |
| 证据置信度 | 中｜受众窄，P2 排期合理 |

## J. 可信三字段

| 字段 | 值 |
|------|-----|
| 需求支持度 | 中等 |
| 证据置信度 | 中｜受众窄，P2 排期合理 |
| 使用边界 | 见 B 段（做 / 不做） |

---

*本卡由 `tools/upgrade_facade.py` 依定义卡规范自动生成，请勿手工编辑；改 `employee.yaml` 后重跑即可刷新。*
