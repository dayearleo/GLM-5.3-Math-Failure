# AGENTS.md：GLM-5.3-Math-Failure

> 本文件是项目宪法和认知路由，不是知识容器。

## 最高目的与第一动作

项目治理的目的不是文档齐全，而是让 AI 软件工程成功。任何工作的第一语义动作都是判断并
建立本任务认知闭包；非平凡 repo 工作必须先完整执行 `repo-cognitive-closure`，利用
README、MEMORY、Feature、docs 和底层实物获得正确认知后，才能回答或行动。

不得为了节省上下文而把项目认知路由、证据纪律、异常边界或完成判据压缩到 AI 无法正确工作；
先保证指导完整，再去除真正重复。

本文件不得设置 150 行等任意行数或文件大小硬上限。真实边界只来自 host 实际 byte/context
预算；当前常规项目规模远非会触及。若未来接近真实预算，先提升配置、改善路由或去真正重复，
不得删除会改变 AI 判断的 always-on 认知。

持续增长、频繁追加或妨碍定位的治理文档可以按自然语义边界分片；约 200 行只是软目标，绝不是
压缩、删减或发布 Gate。分片后先读原 canonical index，确认完整 shard table、`last_shard` 和
顺序追加型 `append_target`，再读 owner shard；新 shard 与索引必须同一 commit 更新。

Feature、current design 和 topical owner 是可修订的当前真值；状态变化时原位修改 owner，旧状态
由 Git、MEMORY/history、rulings 或 sequential 日志保留。禁止因为表格行太长就在后面追加
“状态修正/最新版/以此为准”覆盖块。长行难维护时按职责路由历史证据或在自然语义边界分片，不为数字
压缩内容，也不留下两个相互冲突的当前结论。

## 广度优先执行

BREADTH_FIRST_EXECUTION_V1。

完整系统研发默认先建立主要职责与关键连接的全景，再尽早形成可运行、可验证的最小完整链路，逐轮扩大覆盖。广度按用户结果和真实集成衡量，不按文件、组件或文档数量衡量；不能用空壳、mock或假数据冒充要求中的真实能力。

开工闭包须同时确认父级结果、当前已贯通的链路和下一项最小可验结果，只对当前安全/正确行动所需的认知深入；未来不确定性保留复审条件，不默认变成当前阻塞。

局部深化、新通用层或额外基础设施必须说明它服务的当前结果、直接必要性、较小替代和返回主链的条件；已有投入、结构漂亮或可能的远期复用不是独立理由。必要的安全、正确性、迁移、根因和技术风险调查允许先深入，不得为了快而跳过。

每个自然工作单元结束后回看父目标，区分新增可用行为、关键未知减少和纯准备工作；满足当前需要后停止可选深化，优先补未贯通的真实连接。父任务只有在已接受范围的集成验收满足时才能完成。

研究、审计和方案任务以其授权交付为结果，广度优先不授权转入代码、模型或发布。上述判断复用现有plan/Topic/MEMORY和Skills，不新建默认账本、评分平台、审批Gate或语义Hook。

## 规范化治理资产与受控脚本

治理资产可以是human-edited文档，也可以是machine-managed canonical CSV/JSON/SQLite/matrix。README与
schema必须给出owner和canonical manager；manager存在时，AI先用`query/list/get`建立认知，并用
`upsert/delete-or-retire/validate/migrate/export/diff`操作，不默认全文加载或逐行手改raw载体。只有manager
诊断、schema migration、损坏恢复或明确合同允许时才直接检查底层文件。

脚本只承担机械CRUD、完整性、原子写、确定性序列化和receipt，不替代用户/Feature/设计的语义裁决，也不
扩大删除权限。新规范化要素必须同时提供schema/version、stable IDs、dry-run、锁/并发、引用完整性、
round-trip、migration/rollback、正负/故障测试和human-readable export；没有稳定结构和可证明收益时继续用
Markdown，不为形式化而形式化。

## 文件变更前

修改、移动、重命名、删除或覆盖现有文件前，先确认所属 Git repo、tracked/dirty 状态、最近
commit 和当前 tag。移动/删除前必须有可恢复 commit；保留其他 Session 的未提交变化。

## 认知加载

- AGENTS 是启动内存和强制路由，不是完整知识库。新 Session、上下文压缩恢复、跨 repo/cwd
  接手，或用户询问当前状态、下一步、是否记录、能否继续等 repo 依赖问题时，必须先恢复
  README/MEMORY 外部工作记忆，再回答或行动。
- 非平凡工作先把用户请求转成成功标准、关键问题、范围和高代价误判，再读 `README.md` 和
  `MEMORY.md` 建立项目全景与当前态。
- 修改组件前读 `feature-list.md` 对应节、用户来源/rulings、`docs/README.md`、稳定 system/
  detailed/interface/data/operations 合同，并沿 README 回到代码、config、schema、tests、data、
  logs、进程和运行产物等决定性证据。
- README/MEMORY/Feature/map/摘要只负责路由；不能证明实现、验证和当前运行。
- 用户意图、当前需求、系统设计、详细合同、实现、验证、运行、当前态和历史必须分开。
- 冲突按事实类型、版本和时间消解；无法消解就披露并降低结论。
- “不存在/没有遗漏/全部覆盖”等负结论要说明搜索范围和盲区，不能把没搜到写成不存在。
- 新 Session、压缩、范围/cwd/repo/关键资产或动态事实变化后，审计并按需重建闭包。
- 遇到 `governance-shard-index:v1` 时，先读索引再按任务读 owner/append shard；不能把某一片冒充
  logical document 全文，也不能把约 200 行软目标当作读取截断或压缩理由。
- 恢复后区分 `ACTIVE_WORK`、`CURRENT_REQUIREMENT`、`OPEN_INCIDENT`、`CLOSED_INCIDENT`、
  `HISTORICAL_EVIDENCE`、`SUPERSEDED_FACT`、`DRAFT_PROPOSAL`；用户本轮目标和 MEMORY 当前
  执行队列优先。已关闭事项不得因近期、高频或压缩摘要重新成为当前任务；只有用户明确要求、
  出现满足 `reopen_if` 的当前直接证据、相关 requirement/design/runtime 变化，或本轮就是复盘/
  历史分析时才进入调查。复盘不自动授权重新实施。
- 完成前执行 T01-T26 影响检查，只更新真实变化的唯一真值源；文档化、实现和验证分状态。
- 若本 repo 已长期存在且 current/history 只能从完整 Git 历史恢复，先加载
  `repo-legacy-reconstruction`，不要用 bootstrap 模板覆盖冲突；历史重建阶段不得移动/删除路径。
- 全 repo 结构重塑只有在 reconstruction PASS、用户授权、全路径 manifest、consumer scan、rollback
  和 pre-migration tag 完成后才加载 `repo-structure-migration`，普通目录整理不获得该权限。

## Codex 对话原文归档

若当前`CODEX_HOME/skills/dev-notes-archive/SKILL.md`已安装，每个main Agent在当前Git项目的用户turn都必须在发送final前执行它；
不能依赖普通业务问题隐式命中该 Skill。Skill 先把当前用户消息和完整 final draft 写入私有 staging，再由 helper 在
短项目锁内创建/追加 `dev-notes/0000 - YYYY-MM-DD - 标题.md` 并核验，最后 AI 输出与 staged answer 相同的 final。
`prompt.md`必须逐字包含用户消息的全部可见字符，包括前后行动指令、约束和上下文；不得摘要、改写或只摘核心问题。

只保存用户可见提问和 final draft，不保存隐藏推理、commentary、工具流、权限状态或 Sub Agent 消息。该模式不使用
对话归档 Hook，且归档发生在 final 发送前，所以文件不是 Host 对最终 UI 文本的事后收据。失败时必须披露，不能凭
AGENTS/Skill 存在声称已记录。`dev-notes` 是可能含敏感内容的历史投影，不是需求、设计、状态或验证真值；提交或分享前审阅。

## 项目不变量

- 当前暂无项目特有不变量；首次用户裁定时在此登记摘要，并把原意写入 `rulings.md`。
- Secret 不进入 Git、Prompt、普通日志或公开文档。
- Push、发布和破坏性外部状态变更需要用户明确授权。
