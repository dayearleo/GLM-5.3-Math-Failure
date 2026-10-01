# Security

Secret 不入 Git、Prompt 或普通日志。Session raw trajectory 可能包含 reasoning、开发者/系统提示、用户治理文本、工具输入及本地路径；公开范围应按具体文件和用户授权判断。本项目明确纳入了用户提供并授权的 GLM-5.3 reasoning 字段转录。

仓库保留数学推导、Session 标识和 usage/timing 元数据，并包含两份 `response.reasoningText` 逐字转录。它们不含原始 JSONL 的请求封套、headers 或消息列表；三份完整 Host trajectory 文件仍未收录。Flash 转录后三段来自后续审计 turn，报告必须与原题运行分开计量。
