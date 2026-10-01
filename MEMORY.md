# MEMORY.md：GLM-5.3-Math-Failure 持久记忆

## 当前状态

治理骨架、题解、两份 GLM 报告和两份 GLM reasoning 字段转录已于 2026-10-01 在本地建立。两份副本分别与用户提供文件逐字节相同，所有转录字段也已按 request ID 与本地原始 JSONL 比对字符数和 SHA-256；Flash 文件四段中只有第 1 段来自原数学解题 turn。时间/usage 表来自三条 Session 的元数据；当前所有项目文件尚未 commit/push。

## 当前执行队列

| 方向 | 状态 | 下一步 | 相关 Feature |
|---|---|---|---|
| 案例包交付 | `ACTIVE_WORK` | 核对数学证明、文档边界与治理索引后，按授权提交并推送；完整三份 Host JSONL 仍未收录 | CASE-001 / RAW-001 |

## 当前开放问题与阻塞

- 用户后续明确授权复制两份 GLM reasoning 转录；均已纳入且与源字段哈希匹配，但不是完整 Host JSONL。三份完整 Host 原始文件（Codex rollout、GLM-5.3 JSONL、GLM-5.3-Flash JSONL）均未纳入，故 RAW-001 仍为部分实现；来源路径在交付说明中提供。
- Codex rollout 的 reasoning 项为 encrypted/summary；6:37.023 是最后一个 opaque reasoning marker，不能证明它就是首次发现错误的语义时刻。
- ZCode usage 提供总 `outputTokens`，没有单独 thinking-token 计数。

## 当前有效约束摘要

- 本节只路由当前会影响工作的 `CURRENT_REQUIREMENT`；当前只建立治理骨架，约束正文以后只维护
  指针，不在本节复制完整 Feature/设计。

## 开放事故

- 当前无已确认 `OPEN_INCIDENT`。

## 已关闭事故注册表

实际记录的 `status` 必须是 `CLOSED_INCIDENT`；空表不编造事故。

| ID | status | closed_at | closure evidence | still-valid lesson | reopen_if | current route |
|---|---|---|---|---|---|---|
| - | - | - | - | - | - | - |

## 已验证事实

- 治理骨架 validator 通过；这只验证入口布局。
- 解析推导给出 (C=\sqrt5)、原 (n^{-1/3}) 加项为假、更正 (n^{-3/2}) 版本成立。
- Codex 首题 turn duration 为 426,953ms，usage 记录 reasoning_output_tokens=21,663；两条 ZCode Session request duration 总和分别为 3,725,991ms 和 3,703,903ms。
- 两份 reasoning 转录均与用户提供文件逐字节一致，且每个字段都匹配原始 JSONL 的字符数和 SHA-256；它们不等于完整 trajectory。

## 研究与工作日志

### E001 · 2026-10-01 · 建立完整治理出生骨架

- 所有 topic 入口已创建；本项目当前是 Markdown 数学/Session 案例，没有业务代码、数据库或生产服务。
