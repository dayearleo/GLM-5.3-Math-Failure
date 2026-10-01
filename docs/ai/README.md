# AI

本仓库审计三个既有模型运行，不部署模型服务。记录的准确模型标识为 Codex `gpt-6-luna`（`reasoning_effort=max`）、ZCode `GLM-5.3`、ZCode `GLM-5.3-Flash`；Session ID、turn/request usage 和错误见 README 与 GLM 报告。

ZCode 的 outputTokens 不拆分 thinking 与普通文本；Codex rollout 单独记录 `reasoning_output_tokens`。仓库纳入了用户提供的 GLM-5.3 两段和 GLM-5.3-Flash 四段 `response.reasoningText` 逐字转录。GLM-5.3 的 transcript 是从 raw JSONL 用脚本提取；Flash 首次拒绝时把模型上下文不可见过度推广成不可导出，收到明确步骤后再从 raw 提取。转录正文均匹配源字段，意图性欺骗未获证明。Flash 的后三段属于后续审计 turn，不计入原数学运行。完整 ZCode JSONL 和 Codex rollout 未收录；reasoning 字符数不能替代 Token 统计。三个目标 Session 只支持案例级结论，不能支撑总体能力排名。
