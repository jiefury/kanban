# 指标与复盘

## 核心指标

| 指标 | 定义 | 计算方式 | 使用方式 |
| --- | --- | --- | --- |
| Lead Time | 任务从创建到完成的自然周期 | `PR merged at - Issue created at`；没有 PR 时使用 Issue closed at | 按仓库、任务类型和月份比较 |
| Human Time | 人工投入区间 | Issue/复盘人工填写 | 与 Lead Time 一起看，不能互相替代 |
| First-pass Verification | 首次验证是否通过 | 首次验证结果为完整通过的任务数 / 有验证记录任务数 | 观察 Codex 输出是否减少返工 |
| Rework Rate | 发生返工的任务比例 | `Rework Count > 0` 的任务数 / 已完成任务数 | 质量信号 |
| Regression Rate | 出现回归的任务比例 | `Regression=有` 的任务数 / 已完成任务数 | 高于效率指标优先关注 |
| Review Change Rate | Review 后有修改的任务比例 | `Review Changes != 无` 的任务数 / 有 Review 的任务数 | 识别方案成熟度 |
| Reusable Output Rate | 产生沉淀的任务比例 | `Reusable Output != 无` 的任务数 / 已完成任务数 | 评估长期复利 |
| Outcome Score | 综合人工评分 | 1–5 平均值，同时看分布 | 只用于趋势，不用于单任务惩罚 |

## 分析规则

1. 至少积累 5–10 个已完成任务后再比较趋势。
2. 按任务类型和复杂度分组，不把简单翻译和跨服务重构直接混合比较。
3. 先看质量门槛：Regression Rate 和完整验证率，再看 Lead Time。
4. 同时记录未使用 Codex 的任务，作为个人基线；不要求每个任务都使用 Codex。
5. 如果人工投入下降但返工和回归上升，结论应判定为负收益。
6. 只在连续多个任务中出现稳定变化后，才更新个人规则或 Skill。

## 任务结束复盘

```markdown
## 结果
- Outcome Score：
- Verification：
- Review Changes：
- Regression：
- Rework Count：

## 证据
- PR：
- CI / 测试：
- 人工验收：

## Codex 贡献
- Codex Mode：
- Codex Surface：
- 最有价值的帮助：
- 需要人工纠正的地方：

## 沉淀
- Reusable Output：
- 是否更新 AGENTS.md、Skill、脚本、测试或文档：

## 下一步
- 保留：
- 改进：
- 暂不采用：
```
