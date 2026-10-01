# feature-list.md：GLM-5.3-Math-Failure 当前需求账本

> 本文件回答系统应该怎样。实际实现和验证必须回到代码、配置、测试和运行实物。
> 新建或发生语义/交付变化的 Feature 用 `SRC/DES/IMP/VER/EVD` 路由到来源、设计、实现、
> 验证和实现证据包；证据包可以由多个 Features 共用，不强制每 Feature 单独建闭包文件。

## 状态语义

裁定：候选 / 已采纳 / 已废止。交付：未开始 / 部分实现 / 已实现待验证 / 已验证。

## 项目边界

| ID | 类型 | 当前要求 | 来源 | 裁定 | 交付 | 认知锚点 |
|---|---|---|---|---|---|---|
| CASE-001 | 数学个案 | 自包含说明矩条件题的最优常数、原始错误指数反例和更正指数证明；比较 Codex `gpt-6-luna` 与两个指定 ZCode GLM Session 的可见输出、时长和 Host usage；不得从单题外推一般排名 | 用户要求，2026-10-01 | 已采纳 | 部分实现；数学材料与报告已推送，三份完整 raw trajectory 仍未收录 | SRC:用户请求；DES:`标准答案与排错记录.md`；IMP:`README.md`、两份 Session 报告、两份转录；VER:解析推导、转录哈希及 usage metadata；EVD:README 与报告，RAW-001 仍部分交付 |
| RAW-001 | 公开数据 | 将 Codex 与两个 ZCode Session 的三份完整 raw trajectory 放入公开仓库 | 用户明确要求，2026-10-01 | 已采纳 | 部分实现；纳入 GLM-5.3 两段、GLM-5.3-Flash 四段 `reasoningText` 的逐字转录；三份完整 JSONL/rollout 未公开；Flash JSONL 当前在 canonical catalog 中缺失 | SRC:用户明确要求；DES:完整轨迹与字段摘录须区分；IMP:两份 transcript；VER:所有纳入字段在源可读时按 request ID 与 JSONL 对照字符数和 SHA-256 通过；EVD:两个 ZCode 原文件的本机路径、大小、hash、查找状态在 `推理转录来源与规则遵守审计.md` |
| INTEGRITY-001 | AI 行为审计 | 比较 GLM-5.3 与 Flash 的 reasoning 转录来源、逐字真实性、提示执行和对“缺少上下文/缺少源记录”的结论边界；如实判定是否有诚信问题 | 用户要求，2026-10-01 | 已采纳 | 已验证并推送至 `c9a4ad2`；判定为 Flash 首次证据范围失误，未证明故意欺骗 | SRC:用户澄清；DES:轨迹证据分层；IMP:`推理转录来源与规则遵守审计.md`、`GLM-5.3-Flash-Initial-Audit-Note.md`、README 与两份报告；VER:session_trajectory tree/scan、raw locators、逐字段哈希比较；EVD:报告区分内容真实性、方法差异、错误范围与未知意图 |

## 锚点合同

- `SRC`：ruling/spec/issue；`DES`：stable design/ADR；`IMP`：code/config/schema/runtime；
  `VER`：test/run/receipt；`EVD`：逐 Feature claim-to-asset-to-evidence 报告或等价 evidence bundle。
- `已验证` 必须五类可解析；缺失类别要显式降级，不能用“见相关文件”或 Feature 状态替代证据。
- 既有自由文本锚点在被触碰前可标 `LEGACY_PARTIAL`；没有直接证据时不要补猜。
