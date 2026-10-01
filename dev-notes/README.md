# dev-notes

本目录保存纯 `AGENTS.md + dev-notes-archive Skill` 在发送 final 前生成的项目级对话归档。一个可识别 session
一个文件，同一 session 的多个 turn 追加；文件名格式为 `0000 - YYYY-MM-DD - 标题.md`，编号不复用。旧Hook schema
若存在则保持历史，当前Skill generation另开下一编号。

归档标题从首条用户问题机械生成。正文只包含当前用户可见消息和 AI final draft，不包含system/developer指令、隐藏
推理、commentary、工具流、权限状态或Sub Agent消息。它是pre-final模型行为投影，不是Host对已交付UI的事后收据，
不是需求、设计、当前状态或验证真值；这些内容仍由项目的 `rulings.md`、`feature-list.md`、`docs/`、`MEMORY.md`
和代码/测试/运行实物分别拥有。敏感内容可能按用户要求原样保存，提交前请审阅。
