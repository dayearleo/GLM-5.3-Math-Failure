# MEMORY.md：GLM-5.3-Math-Failure 持久记忆

## 当前状态

基础治理骨架、题解、数学 Session 报告、两份 GLM reasoning 转录、转录来源/规则审计报告和 Flash 首次审计备注的可见原件副本，已由 `3904d16761c5ee914a7638b61582aa46cbef7723` 与 `c9a4ad2980db2dad2acca5539c4504e66d3ba371` 两个提交推送到 `origin/main`。两份 transcript 副本与用户提供文件逐字节相同；所有纳入字段在各自源可读时均按 request ID 比对字符数和 SHA-256；Flash 四段中只有第 1 段来自原数学解题 turn。

## 当前执行队列

| 方向 | 状态 | 下一步 | 相关 Feature |
|---|---|---|---|
| 转录来源/规则审计 | `COMPLETE_FOR_PUBLISHED_SCOPE` | 报告和 README 已推送；RAW-001 仍部分实现，Flash 原始 JSONL 当前缺失，GLM-5.3 完整 JSONL 含未分类 Cookie，暂不可公开 | INTEGRITY-001 / RAW-001 |

## 当前开放问题与阻塞

- 两个 ZCode raw 快照曾在本机 JSONL 中审计；分别包含 31 和 11 个非空 `Set-Cookie` 响应头值，且读取时原文件 mode 为 `0644`。完整 JSONL 未复制或推送；项目 AGENTS 禁止 Secret 入 Git，Cookie 值安全性未获确认。Flash 文件后来从 canonical catalog 消失，在可访问搜索范围内未找到，原因未知；RAW-001 仍部分实现，路径、大小、哈希与查找边界见新审计报告。
- 新审计判断：GLM-5.3 首次就从 raw JSONL 脚本抽取；Flash 首次只按当前上下文写“不可导出”备注，没读 raw，后续按明确脚本提示成功提取。六个 transcript 字段与源完全匹配；证据支持有限的证据范围失误，不证明故意欺骗。
- Flash `sess_ef61...` JSONL 在读取并完成字段比对后从 canonical catalog 消失；全盘文件名搜索受系统目录权限/ignore 限制，没有找到可恢复副本。最后已核快照 SHA-256 和时间见审计报告，消失原因 `UNKNOWN`。
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
- Flash 首次审计备注副本与 source `Write` tool-call 内容字节一致（SHA-256 `78b280771c41592d002219cee9426247a6edf22564e0fae9352a3f73b609e8d0`）；备注关于模型上下文不可见有依据，但未检查 raw source 就推断不可导出。

## 研究与工作日志

### E001 · 2026-10-01 · 建立完整治理出生骨架

- 所有 topic 入口已创建；本项目当前是 Markdown 数学/Session 案例，没有业务代码、数据库或生产服务。
