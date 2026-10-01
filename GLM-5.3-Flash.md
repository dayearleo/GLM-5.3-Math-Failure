# GLM-5.3-Flash：矩条件极差题的 Session 分析报告

> 审计日期：2026-10-01
> 目标 Session：`sess_ef61cf38-703e-476a-b1a7-e3ce618fe016`
> 目标模型：ZCode 记录中的 `GLM-5.3-Flash`
> 范围：判断这一次运行为何没有交付数学答案；不把单次结果外推为模型总体能力。

## 1. 结论

这个 Session 实际拿到的题面要求证明 \(R_n\ge\sqrt5+C_2n^{-1/3}\)。这项数学断言是假的：有无穷多个 \(n\) 存在满足全部矩条件、且极差为 \(\sqrt5+O(1/n)\) 的有限等权数列。因此它不可能产出该不等式的正确证明；正确交付应指出题面错误并给出反例。

运行本身也没有完成交付：第一次模型响应的 output tokens 达到 `128000` 上限，`response.text` 为空；随后日志只留下 `v4 session stopped`，没有可见答案、工具结果或第二次成功响应。raw `reasoningText` 的尾段显示它正在准备数值/优化/来源核验方案，但对应请求没有发出工具调用，不能把这些计划记作已执行。

## 2. 题目的真实数学难点

### 2.1 化为固定前三个中心矩

令 \(x_i=a_i-1\)，则
\[
\sum_i x_i=0,\qquad \sum_i x_i^2=n,\qquad \sum_i x_i^3=-n.
\]
极差不变。研究的是具有指定均值、方差、三阶中心矩的有限等权经验分布，其支持区间能有多窄。

### 2.2 \(C=\sqrt5\) 的下界来自根间距

设 \(q(x)=x^2+x-1\)。矩条件给出
\[
\sum_iq(x_i)=0,\qquad \sum_ix_iq(x_i)=0.
\]
两个根为
\[
A=-\varphi=\frac{-1-\sqrt5}{2},\qquad
B=\varphi^{-1}=\frac{-1+\sqrt5}{2},
\]
间距为 \(\sqrt5\)。若样本区间长度小于 \(\sqrt5\)，至多含一个根。由 \(\sum q(x_i)=0\)，它必须含一个根；否则所有 \(q(x_i)\) 同号，或全为零而所有 \(x_i\) 相等，都与矩条件冲突。若区间只含 \(A\)，则每个非根点满足 \((x_i-A)q(x_i)<0\)；若只含 \(B\)，则每个非根点满足 \((x_i-B)q(x_i)>0\)。但两个情形下这些和都应为零，因为 \(\sum_i(x_i-A)q(x_i)=\sum_i x_iq(x_i)-A\sum_iq(x_i)=0\)，对 \(B\) 亦然，矛盾。因此范围至少为 \(\sqrt5\)。

要证明 \(C\) 正好是这个数，还要处理有限等权约束：连续极值分布在 \(A\) 点的权重为
\[
\rho=\frac{1-1/\sqrt5}{2},
\]
这是无理数，不能直接作为有限 \(n\) 个等权点的比例。尖锐性需要额外的有限点构造，而不只是写出连续两点分布。

### 2.3 原始 \(n^{-1/3}\) 加项为假

因 \(\rho\) 无理，可取无穷多个 \(n\) 使 \(\{n\rho\}\in[1/3,2/3]\)；再抽取子列使 \(\theta\) 收敛，置
\[
k=\lfloor n\rho\rfloor,\quad \theta=k-n\rho\in[-2/3,-1/3],\quad \lambda=1/n.
\]
以权重
\[
\rho+\theta\lambda=k/n,\qquad
1-\rho-(\theta+1)\lambda=(n-k-1)/n,\qquad
\lambda=1/n
\]
放置三个可调实数 \(x,y,z\)，要求
\[
px+ry+\lambda z=0,\qquad px^2+ry^2+\lambda z^2=1,\qquad px^3+ry^3+\lambda z^3=-1.
\]
在 \(\lambda=0\) 时，前两位置是 \(A,B\)。前两个矩方程对 \(x,y\) 的雅可比非零，故局部可解出 \(x,y\)；把第三个矩残差除以 \(\lambda\)，所得函数在 \(\lambda=0\) 可光滑延拓，其零阶条件为
\[
P(z)+\theta P(A)-(\theta+1)P(B)=0,
\qquad P(t)=t^3+\frac32t^2-3t.
\]
因为 \(P'(t)=3(t-A)(t-B)<0\) 于 \((A,B)\)，而 \(\theta\) 严格介于 \(-1,0\)，右侧是端点函数值的严格凸组合，故有唯一内部根，且该根处导数非零。再对第三个方程应用隐函数定理，给出充分大的这些 \(n\) 的精确矩解，满足
\[
x=A+O(n^{-1}),\qquad y=B+O(n^{-1}),\qquad z\in(A,B).
\]
取 \(k\) 个 \(x\)、\(n-k-1\) 个 \(y\) 和一个 \(z\)，再令 \(a_i=x_i+1\)，便回到原题，极差为
\[
R_n=\sqrt5+O(n^{-1}).
\]
这会否定任意正系数的 \(n^{-1/3}\) 下界，因为 \(n^{-1}=o(n^{-1/3})\)。所以第 (2) 问不能照原文字证明。

### 2.4 后来更正的指数不属于这条 Session

本 Session 的消息明确写的是 \(n^{-1/3}\)，并未包含后续对话的 \(n^{-3/2}\) 更正。更正后的命题不同：若 \(\delta=R_n-\sqrt5\) 已大于固定正数，下界直接成立；在小 \(\delta\) 情形，端点稳定性可给出
\[
|k-n\rho|\le Cn^2\delta^2,
\qquad \delta=R_n-\sqrt5,
\]
而 \(\rho\) 的代数共轭范数给出 \(|k-n\rho|\ge1/(5n)\)，于是 \(\delta\ge c n^{-3/2}\)。这是正确版本的证明骨架。不能用后来的更正来要求本 Session 当时证明不同的命题。

## 3. 身份、输入与运行设置

原始记录身份：ZCode Session `sess_ef61cf38-703e-476a-b1a7-e3ce618fe016`，本地 JSONL 两个 request 记录均使用该 sessionId。文件内容未随本公开报告复制；以下数据按 requestId 和物理记录序号定位。

| 项目 | 直接观察 |
|---|---|
| turn | `turn_ea9ef03b-fa7e-4ce2-9ecc-39fd48585a69`，一个 turn |
| 模型 / provider | `GLM-5.3-Flash` / `account:zai-individual-coding-plan`；成功响应 `modelId` 同名 |
| 生成设置 | thinking enabled，`output_config.effort=max`，每次 `max_tokens=128000` |
| 原题 | 独立 user 消息长 214 字符，指数为 `n^(-1/3)`；成功请求记录的 normalized input tokens 为 42,452 |
| 额外上下文 | 同一请求带有 10,646 字符的 user-role `<system-reminder>` 内容 |
| 工具使用 | 工具清单虽存在，但两条响应的 `toolCalls` 都为空 |
| 推理字段转录 | [`GLM-5.3-Flash-Thinking-verbatim.md`](GLM-5.3-Flash-Thinking-verbatim.md) 收录四段 `response.reasoningText`；第 1 段 318,426 字符属于本题 turn，第 2–4 段共 17,205 字符属于后续审计 turn |

## 4. 调用时间线

| 原始行 / requestId | UTC 时间与时长 | 窗口 | 响应与结果 |
|---|---|---|---|
| 1 / `c0dbb162-1b7f-48ae-ab52-fd0fa7f70332` | 14:29:42.348–15:16:58.013，47:15.665 | `full`，6 条消息 | `finishReason=length`；output=128000；可见 `response.text` 为空、工具调用 0；raw `reasoningText` 318,426 字符 |
| 2 / `e4ad4752-a591-4604-9dd6-4508a177d971` | 15:16:58.072–15:31:26.310，14:28.238 | `delta`，offset 6；一条 183 字符续写指令 | `Error: v4 session stopped`；无成功响应、usage、可见文本或工具调用 |

两条调用记录的时长合计约 61:44。续写文字保存在 `role=user` 消息中；仅凭日志无法确认它由人输入还是 Host 自动续写流程生成。

## 5. 它实际做了什么

**确定的行为结果：**第一条模型响应用完 128000 output tokens，以 `finishReason=length` 结束，但可见回答为空；第二条请求随后报 `v4 session stopped`。没有实际 Python、SLSQP、网页检索或其他工具结果。

**推理材料：**[`GLM-5.3-Flash-Thinking-verbatim.md`](GLM-5.3-Flash-Thinking-verbatim.md) 的第 1 段是该数学 turn 的原始 `reasoningText`；后 3 段来自另一审计 turn，不用于评价原题 Session。第 1 段从中心矩与端点不等式开始，尾段已拟定“原第 (2) 问可能为假”的答复框架，并计划用显式构造、连分数/数值检查和网页查证确认。它还计划运行代码并检查全局最优，但原数学 turn 的 `toolCalls` 为空，因此这些计划没有转化为数值实验或外部核验。

它遇到的关键困难不是不会算出 \(\sqrt5\)，而是没有尽早区分两项工作：先判明原命题的真假，再决定证明或反例。它在已经朝“命题为假”转向后仍继续扩展数值与来源核验方案，直至输出耗尽；随后 Host 停止 Session。虽然逐字转录已保存，报告仍不声称逐步验证了其中每一个推理断言。

## 6. 因果判定与证据边界

### 直接支持的结论

1. **不存在题面要求的证明：**原输入是 \(n^{-1/3}\) 版本；精确三点等权构造沿无穷子列给出 \(R_n=\sqrt5+O(n^{-1})\)，排除任何固定正的 \(n^{-1/3}\) 下界。
2. **本次输出未交付：**唯一成功响应达到单次 output token 上限，最终可见文本为空；之后的 Host 记录是 `v4 session stopped`。
3. **模型计划没有变成验证证据：**轨迹没有任何工具调用或工具结果。

### 五层证据边界

| 层 | 本 Session 的判定 |
|---|---|
| L1 上下文注入 | 原数学题以 214 字符 user 消息进入请求；额外 `<system-reminder>` 也在请求中。没有对当时整份外部 AGENTS 源文件作逐字比较 |
| L2 文件读取 | 无文件读取调用；解题本身不依赖 repo 文件，故未读文件不是失败证据 |
| L3 模型复述 | 未做独立复述实验 |
| L4 推理/治理执行 | 只做有限的 raw 推理区段摘要；完整 `reasoningText` 未逐字审核，工具调用为零 |
| L5 任务行为 | 失败：没有可见数学回答，末尾是 Host `v4 session stopped` |

### 不能据此断言

- 不能证明它的完整内部推理在什么时候、以什么精确步骤发现反例；报告只概括 raw 字段边界处的可见片段。
- `v4 session stopped` 本身不能区分用户停止、Host 生命周期停止或其他上游停止原因。
- 此次日志不足以比较 GLM-5.3 与 GLM-5.3-Flash 的一般能力；两者面对的是错误命题，且都未交付可评分的数学答案。

### 读取器缺口和隐私

共享 `session_trajectory.py tree` 没有展开 raw JSONL 的顶层 `response.reasoningText`，只把空的可见 `response.text` 记作 assistant message。故本报告将模型行为与原始 JSONL 的 requestId、finish reason、usage、toolCalls、reasoningText 长度及 error 直接对照；不能把规范化 tree 的事件数说成完整思维记录。该 Host 字段形状差异应另行加入共享 reader fixture 并更新能力说明，本次没有改共享工具。

原始 JSONL 在审计时 mode 为 `0644`。仓库没有复制完整 JSONL；只收录用户提供的四段 `reasoningText` 转录，并按 request ID 与来源 JSONL 核对了各段字符数和 SHA-256。第 2–4 段属于后续审计 turn，不能并入原数学 Session 的用量比较。

## 8. 与 Codex「Luna 6 做题」的时间和 Token 对照

Codex rollout 的实际模型标识为 `gpt-6-luna`，reasoning effort 为 `max`。同一原始 (n^{-1/3}) 提问的首答和本 GLM Session 可作单次运行对照：

| 运行 | 原始提问后的时长 | 输入 tokens | 输出 tokens | reasoning 输出 tokens | 可见结果 |
|---|---:|---:|---:|---:|---|
| Codex 初题 turn | 7:06.953 | 49,370 | 23,378 | 21,663 | 可见回答 2,869 字符，指出原第 (2) 问为假 |
| Codex 更正题 turn（(n^{-3/2})） | 4:00.557 | 72,770 | 13,265 | 11,878 | 可见证明 2,258 字符 |
| GLM-5.3-Flash Session | 61:43.903（两个 request 时长合计） | 42,452（成功 request 的归一化输入） | 128,000（一次成功响应） | ZCode 未提供独立 thinking-token 字段；保存的 `reasoningText` 为 318,426 字符，字符数不是 Token | 可见回答 0 字符，工具调用 0，最后 `v4 session stopped` |

Codex 的最后一个 reasoning 事件标记在首个 prompt 后 6:37.023，但其内容是加密/摘要形式；这与“6:37 时发现题面错误”的时间说法相符，不能单独证明该事件的语义。Codex 最终可见回答出现在 14:31:30.516Z，turn 完成于 14:31:31.034Z，记录时长为 7:06.953。包括后续更正题 turn 后，首问到更正证明完成的墙钟跨度为 11:31.608，两个 turn 的活动时长合计 11:07.510；不是精确的 10 分钟。

Token 字段只按各 Host 自己的 usage 记录并列；GLM 的 outputTokens 没有 reasoning/普通输出拆分，不能将 reasoning 字符数换算成思考 Token。该对照也只覆盖一个错误命题的一次运行，不构成一般模型排名。

## 9. Thinking 转录与首次审计回应

首次审计 turn 没有检查本 Session 的 raw JSONL，就生成了“当前上下文没有推理文本、因此没有可导出对象”的备注；其“上下文不可见”限定有依据，但“不可导出”的结论过早。后来按明确的 raw-source 提示词生成的四段转录，在当时可读的源快照中均逐段匹配；首段属于数学 turn，后三段属于首次审计 turn。该源快照 SHA-256 为 `a7672d31bb5a1078700b81c199ead22112a168b1f2fde77282a0d0e6636ba4b5`，目前已不在 ZCode canonical catalog，故现阶段不能重新读取复算。首次备注原件副本和范围判定见[推理转录来源与规则遵守审计](推理转录来源与规则遵守审计.md)。这证明的是一次证据路由/结论范围失误，不证明故意欺骗。

## 10. 最终判断

这次 Flash Session 没有“证明失败后留下错误答案”；它留下的是一个已耗尽输出额度、没有可见答案的运行。更早识别出原指数错误、用精确有限构造结束审计，是它应当采取的数学路径。若用户本意是 \(n^{-3/2}\)，那是另一道已更正的问题，而此 Session 并没有收到该版本。
