# Quality

本仓库没有业务代码，故无程序测试套件。核心数学结论由 `标准答案与排错记录.md` 的解析证明支持；Session 结果与 token/time 使用来自三个 Host 的 usage/turn 元数据。两份 GLM 转录中的每段 reasoning 字段都按 request ID 对照来源 JSONL，字符数与 SHA-256 均匹配；Flash 的后三段属于后续审计 turn。

比较样本为 Codex 一个原题 turn、一个更正题 turn，以及 GLM-5.3 和 GLM-5.3-Flash 各一个 ZCode Session。原题增强命题为假，且每个 GLM 仅一次运行；这不是统计评测、受控多次实验或总体能力结论。单段 reasoning 字段转录不是 full raw evidence，三份完整 Host trajectory 均未收录。
