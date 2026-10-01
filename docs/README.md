# docs/：GLM-5.3-Math-Failure 稳定知识索引

> 需求真值在根 `feature-list.md`，当前状态在根 `MEMORY.md`。本目录 topic 入口从项目出生时
> 建立；“当前无稳定合同”是诚实状态，不表示该 topic 永久不适用。

| Topic | 入口 | 当前状态 |
|---|---|---|
| 产品/范围 | `product/README.md` | 单题模型 Session 个案；不作总体排名 |
| 领域/术语 | `domain/README.md` | 矩、中心矩、极差、等权经验分布 |
| 系统设计 | `design/system/README.md` | 当前无稳定系统设计 |
| 详细设计 | `design/detailed/README.md` | 当前无稳定详细合同 |
| 决策 | `decisions/README.md` | 暂无 ADR |
| 接口 | `interfaces/README.md` | 当前无稳定接口 |
| 数据 | `data/README.md` | 当前无数据合同 |
| 质量 | `quality/README.md` | 解析证明与单次 usage 观察；非统计评测 |
| 安全 | `security/README.md` | 只有通用 secret/授权边界 |
| 运维 | `operations/README.md` | 当前无生产 runbook |
| 开发 | `development/README.md` | Markdown-only，无代码构建 |
| 发布 | `releases/README.md` | 尚未采用发布版本 |
| AI 合同 | `ai/README.md` | 指定模型、Session、usage 与隐私边界 |
| 历史 | `history/README.md` | 2026-10-01 个案时序与文件状态 |
| 参考 | `reference/README.md` | 本地题解参考与 Session source IDs |

## 当前案例材料

| 材料 | 作用 | 证据边界 |
|---|---|---|
| `../标准答案与排错记录.md` | 矩条件变换、(C=\sqrt5)、原 (n^{-1/3}) 反例、修正 (n^{-3/2}) 下界 | 解析证明 |
| `../GLM-5.3.md` | GLM-5.3 指定 Session 分析 | metadata、可见答复状态及单独 reasoning 转录链接；完整 raw trajectory 未收录 |
| `../GLM-5.3-Flash.md` | GLM-5.3-Flash 指定 Session 分析 | metadata、可见答复状态及 reasoning 转录边界；完整 raw trajectory 未收录 |
| `../GLM-5.3-Thinking.md` | 两段 GLM-5.3 `response.reasoningText` 的逐字转录 | request ID、字符数与 SHA-256 均对照源 JSONL；不是完整 JSONL |
| `../GLM-5.3-Flash-Thinking-verbatim.md` | 四段 GLM-5.3-Flash `response.reasoningText` 的逐字转录 | request ID、字符数与 SHA-256 均对照源 JSONL；首段属数学 turn，后三段属审计 turn；不是完整 JSONL |
| `../README.md` | Codex/ZCode 时间和 token 多维对照 | 单案例观察，不是统计评测 |
