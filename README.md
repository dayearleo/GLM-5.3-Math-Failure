# GLM-5.3-Math-Failure

> 项目类型：单题、多 Session 的数学问题处理个案审计
> 建立日期：2026-10-01
> 上游：<https://github.com/dayearleo/GLM-5.3-Math-Failure>

## 项目目的

本仓库记录同一道矩条件极差题在 Codex `gpt-6-luna` 与 ZCode `GLM-5.3`、`GLM-5.3-Flash` 指定 Session 中的回答差异，作为一个可供智谱 AI 关注的具体案例。项目重点是对照模型是否检查题目真假、是否给出可见的完成答案、耗时和 Host 报告的 token 用量。

这道题的原始第 (2) 问要求
\[
\max_i a_i-\min_i a_i\ge \sqrt5+C_2n^{-1/3}.
\]
这个断言本身为假；可行数列能达到 \(\sqrt5+O(n^{-1})\)。因此本案例比较的是**发现并处理错误命题、完成回复的行为**，不能表述成“Codex 证明了一个真定理而 GLM 证明失败”，也不足以单独证明两类模型的一般数学能力排序。指数更正为 \(n^{-3/2}\) 后，命题才成立。

## 本案例的时间与 Token 数据

下表来自 Codex rollout 和两个 ZCode `model-io` Session 的 usage/turn 记录。时间均为 UTC；ZCode 时长为各 request 记录时长之和。Codex 的 `reasoning_output_tokens` 是 Host 单独给出的字段；ZCode 只给出总 `outputTokens`，没有 thinking-only Token 拆分。

| 模型与阶段 | 时长 | 输入 Tokens | 输出 Tokens | reasoning Tokens | 可见最终结果 |
|---|---:|---:|---:|---:|---|
| Codex `gpt-6-luna`, 原始 \(n^{-1/3}\) 提问 | 7:06.953 | 49,370 | 23,378 | 21,663 | 2,869 字符；判定原第 (2) 问为假并给出构造 |
| Codex `gpt-6-luna`, 更正为 \(n^{-3/2}\) 后 | 4:00.557 | 72,770 | 13,265 | 11,878 | 2,258 字符；给出更正命题的下界证明 |
| GLM-5.3 Session | 62:05.991 | 85,144¹ | 256,000² | 未单独报告 | 可见答案 0 字符；两次 output 上限结束后 Host 停止 Session |
| GLM-5.3-Flash Session | 61:43.903 | 42,452¹ | 128,000² | 未单独报告 | 可见答案 0 字符；成功输出达上限，后续 Host 停止 Session |

¹ ZCode 的 `response.usage.inputTokens` 汇总值，按 Host 归一化口径统计，和 Codex 的输入统计口径不保证完全等价。

² ZCode 成功响应的 `outputTokens`。GLM-5.3 两次成功响应各 128,000；Flash 一次成功响应 128,000。错误/停止请求没有 usage。Raw `reasoningText` 字符数不是 Token 数，不用于代替 reasoning Token。

原始数学解题 Session 中，GLM-5.3 的两段 `reasoningText` 共 **596,686 字符**，GLM-5.3-Flash 的一段为 **318,426 字符**；Codex 原始 reasoning 记录为加密/摘要形式，不能作同类字符统计。这些字符数与 Host Token usage 分栏展示，不互相换算。Flash 转录文件还收录同一 ZCode Session 后续审计 turn 的三段 reasoningText，共 17,205 字符；它们不是原数学解题 turn 的耗时/Token 统计对象。

Codex 首题 turn 的最后一个 reasoning 事件标记在 14:31:01.134Z，即首个 prompt 后 6:37.023；该事件内容是加密/摘要状态，不能据此证明那就是“首次发现第 (2) 问为假”的时刻。Codex 最终可见答复出现在 14:31:30.516Z，turn 完成于 14:31:31.034Z，记录时长为 7:06.953。原始问题加上后续更正答案的墙钟跨度为 11:31.608，两个 turn 活动时长之和为 11:07.510。因此“总计 10 分钟”是近似口述，原始记录更接近 11 分半。

从单个案例可以得出的有界观察是：Codex 在首答中识别了假命题并交付反例；两个指定 GLM Session 长时间运行且没有可见最终答案。由于原命题为假、上下文/toolset 和 Provider usage 口径不完全相同、每种 GLM 只有一个 Session，本数据不构成统计评测或一般模型排名。

## 阅读顺序

1. [标准答案与排错记录](标准答案与排错记录.md)：证明 \(C=\sqrt5\)，证明原 \(n^{-1/3}\) 版本为假，并证明更正的 \(n^{-3/2}\) 版本。
2. [GLM-5.3 Session 分析](GLM-5.3.md)：原始请求/响应元数据、模型停止状态、数学任务难点和 Codex 时间/Token 对照。
3. [GLM-5.3-Flash Session 分析](GLM-5.3-Flash.md)：对应 Session 的同类分析与对照。
4. [GLM-5.3 推理转录](GLM-5.3-Thinking.md)与 [GLM-5.3-Flash 推理转录](GLM-5.3-Flash-Thinking-verbatim.md)：按 request ID、字符数和段落 SHA-256 标注的原字段逐字文本。
5. 项目治理入口：[`feature-list.md`](feature-list.md)、[`MEMORY.md`](MEMORY.md)、[`rulings.md`](rulings.md)、[`docs/README.md`](docs/README.md)。

## 转录与原始 Session 文件的边界

目标 Session ID：

- ZCode GLM-5.3：`sess_ce01b37f-1dd1-429f-9ab5-53450ffbb35c`
- ZCode GLM-5.3-Flash：`sess_ef61cf38-703e-476a-b1a7-e3ce618fe016`
- Codex：`Luna 6 做题`，rollout session `01a0f7da-2228-7d21-9ad2-581ae6524740`

仓库收录两份用户提供的 reasoning 转录：[GLM-5.3](GLM-5.3-Thinking.md) 的两段（共 596,686 字符），以及 [GLM-5.3-Flash](GLM-5.3-Flash-Thinking-verbatim.md) 的四段（共 335,631 字符）。两份副本都与用户提供的文件逐字节一致；整文件 SHA-256 分别为 `218aba0d86a195709a0fd4ec5c4cee30eb33a8ab7b93b560db34d01ec713707a` 和 `b19da8461969b16290153f0fad5096f853c8f88ac8065e43d42cdf9c2ce5a425`。两份转录的所有 reasoning 字段又按 request ID 与各自本地源 JSONL 比对，字符数和 SHA-256 均匹配。

Flash 转录第 1 段属于原数学解题 turn（318,426 字符）；第 2–4 段属于之后另一个审计 turn（合计 17,205 字符），不计入数学 Session 的原始解题用量。两份转录都不含原 JSONL 的请求封套、消息列表、headers 或完整 Host 事件，因此是 **reasoning 字段摘录**，不是完整 raw trajectory。

Codex 原始 rollout、GLM-5.3 原始 JSONL、GLM-5.3-Flash 原始 JSONL 均未纳入本仓库。报告按各来源可见的 Session/request 元数据记录时长、usage 和可见答复状态；两份字段转录仍不是三份完整 trajectory 的替代品。GLM reasoning 字符数也不等于 Token 数。

## 快速检查

本项目没有运行代码或依赖安装。数学结论以文内解析推导为准；时间/usage 数值来自对应 Host Session 元数据。两份 GLM 转录的每段字段都已按 request ID 与本地源 JSONL 对照字符数和 SHA-256；仓库副本也分别与用户提供文件逐字节一致。不要把摘录称为完整 raw trajectory、把 reasoning 字符数伪称为 Token，或把一个案例推广成整体能力结论。

## 认知入口

| 问题 | 入口 |
|---|---|
| 项目硬约束 | `AGENTS.md` |
| 当前需求 | `feature-list.md` |
| 当前状态/下一步 | `MEMORY.md` |
| 用户裁定 | `rulings.md` |
| 稳定 topic 文档 | `docs/README.md` |
| 未定调查/方案 | `dev-docs/README.md` |
| Codex 可见问答历史 | `dev-notes/README.md` |

## 组件地图

| 组件 | 职责 | 需求 | 设计 | 实现 | 验证 |
|---|---|---|---|---|---|
| 数学案例与标准解 | 处理矩条件极差题、核验指数真假 | `CASE-001` | `标准答案与排错记录.md` | Markdown 文档 | 解析推导；未建立代码测试 |
| Session 案例报告 | 比较三个指定 Session 的可见完成状态和 usage | `CASE-001` | `GLM-5.3.md`、`GLM-5.3-Flash.md` | Host 元数据与报告 | 单案例观察，不是统计评测 |
| GLM reasoning 文本摘录 | 保存 GLM-5.3 与 Flash 的 `response.reasoningText` 逐字转录 | `CASE-001` | `GLM-5.3-Thinking.md`、`GLM-5.3-Flash-Thinking-verbatim.md` | 用户提供副本；段哈希与源 JSONL 均核对 | 不包含完整 JSONL 封套或完整 Session |
