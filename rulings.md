# rulings.md：GLM-5.3-Math-Failure 用户裁定

## R-001 · 2026-10-01 · 项目目的与范围

用户要求建立 `dayearleo/GLM-5.3-Math-Failure` 个案仓库，比较 Codex「Luna 6 做题」与两个指定 ZCode GLM Session 对矩条件极差题的处理，写中文 README、标准题解和两份报告，提交者 email 使用 `dayearleo@proton.me`，完成后推送到指定 upstream。项目希望引起智谱 AI 对该运行差异的注意。

**数学语境**：两个 GLM Session 实际收到的是 (n^{-1/3}) 原始题面，该增强下界为假。Codex 首答指出其为假；随后题面被更正为 (n^{-3/2})，Codex 再答更正问题。报告按各 Session 实际收到的命题分别评价。

**原始轨迹要求与交付状态**：用户明确要求公开三个完整 raw trajectory。后续用户先后提供并授权复制 GLM-5.3 与 GLM-5.3-Flash reasoning 转录；这些摘录已按字节加入仓库，也逐段与源 JSONL 字段校验，但不包含完整 JSONL。Codex rollout 仍未纳入，故“三份完整 trajectory”要求仍是部分交付。用户补充说明，拿不到其它 reasoning 可以接受，主要目标是汇报本次数学能力差异案例；不得把两份 reasoning 转录称为完整 raw evidence。

## R-002 · 2026-10-01 · 完整治理骨架

正式 Git 仓库的治理入口已初始化；入口只描述实际范围，不表示软件实现或公开发布已经完成。

## R-003 · 2026-10-01 · 纳入 GLM-5.3 可读推理转录

用户提供 `/Volumes/D/math/GLM-5.3-Thinking.md`，说明它逐字收录 GLM-5.3 Session 的两段 `response.reasoningText`，并明确授权将该文件复制到目标 repo。副本按字节与提供文件相同；两段转录又按 request ID 与本地源 JSONL 的字符数、SHA-256 对照通过。它是两个推理字段的转录摘录，不是完整 ZCode JSONL 或三份 trajectory 的替代品；README 与报告必须保持这一证据边界。

## R-004 · 2026-10-01 · 纳入 GLM-5.3-Flash 可读推理转录

用户提供 `/Volumes/D/math/GLM-5.3-Flash-Thinking-verbatim.md`，并在当前任务上下文中要求将 Flash thinking trajectory 纳入目标 repo。该文件已逐字节复制；四个 reasoning 字段均按 request ID 与本地源 JSONL 比对，字符数和 SHA-256 全部匹配。第 1 段属于原数学解题 turn；第 2–4 段来自后续审计 turn，不得计入原题 Session 的耗时/Token 或作为其作答内容。
