# 字段字典

## Project 字段

| 字段 | 类型 | 值 | 来源 | 说明 |
| --- | --- | --- | --- | --- |
| Status | 单选 | Backlog / Ready / In Progress / Review / Verify / Rework / Blocked / Done | GitHub Project | 统一进度，不表示 Codex 是否参与 |
| Repository | 单选或文本 | 业务仓库名 | 自动或创建时填写 | 便于跨仓库过滤 |
| Task Type | 单选 | 开发 / Bug 修复 / 重构 / 调研 / 文档 / 运维 | Issue Form | 任务分类 |
| Area | 文本 | 业务域或模块 | Issue Form | 避免建立过多固定选项 |
| Priority | 单选 | P0 / P1 / P2 / P3 | Issue 或 Project | 业务优先级 |
| Codex Mode | 单选 | 未使用 / 辅助 / 主导 / 自动化 | 人工填写 | Codex 的参与深度 |
| Codex Surface | 多选 | App / CLI / IDE / Cloud / API | 人工填写 | 使用入口，可为空 |
| Human Time | 单选 | <15m / 15–60m / 1–4h / >4h | 人工填写 | 只记录区间，降低记录成本 |
| Rework Count | 数字 | 0 或正整数 | 人工补齐 | Review 或 Verify 发现问题后的返工次数 |
| Blocker Reason | 单选 | 无 / 需求 / 权限 / 环境 / 外部依赖 / 数据 / 其他 | 人工补齐 | 只有阻塞时重点填写 |
| Verification | 单选 | 未验证 / 局部通过 / 完整通过 / 被阻塞 | 人工补齐 | 最终验证结果 |
| Review Changes | 单选 | 无 / 少量 / 多次 / 大幅返工 | 人工补齐 | Review 后修改量 |
| Regression | 单选 | 无 / 有 | 人工补齐 | 是否引入回归 |
| Reusable Output | 多选 | 无 / 规则 / Skill / 脚本 / 测试 / 文档 | 人工补齐 | 是否产生可复用资产 |
| Outcome Score | 数字 | 1–5 | 人工补齐 | 任务结束后的综合判断 |

## 自动事实

这些字段不要求人工在 Issue Form 中重复填写：

- Issue created at；
- Issue closed at；
- PR created at；
- PR merged at；
- PR review activity；
- CI check conclusion；
- linked PR / linked Issue。

如果 Project 不能直接显示某项自动事实，在复盘中引用 Issue、PR 和 CI 链接，不复制整段日志。

## 取值规则

- `Codex Mode` 是参与程度，不是质量评价；
- `Outcome Score` 必须基于验证和 Review 证据，不能仅因任务快速完成就打高分；
- `Rework Count` 只计算需求已稳定后的返工，不把正常迭代当作缺陷返工；
- `Regression=有` 时，`Outcome Score` 通常不应高于 3，除非复盘说明了例外原因；
- `Reusable Output=无` 不代表任务价值低，只表示没有产生可独立复用的资产。
