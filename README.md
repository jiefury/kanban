# Codex Delivery OS

> 用 GitHub 管理、追踪和评估 Codex 在多项目研发中的实际产出。
>
> 本仓库只保存管理规范、模板、指标和自动化配置，不保存任何真实业务代码。

## 目标

把每个真实开发任务变成一条可审计的交付链：

`业务仓库 Issue → Codex 执行 → PR → Review → Verify → Done → 复盘`

核心原则：

- 真实代码、业务 Issue、PR 和 CI 留在对应业务仓库。
- 一个跨仓库 GitHub Project 统一聚合任务。
- 本仓库是模板、字段、指标和同步规则的唯一维护源。
- 每个实际开发任务一条 Issue，不按对话次数拆分。
- 自动采集 GitHub 活动，人工只补充投入、返工和结果判断。

## 已确认的设计

### 统一状态

`Backlog → Ready → In Progress → Review → Verify → Done`

异常路径：

- `In Progress → Blocked`
- `Review / Verify → Rework → Review`

Codex 参与方式是字段，不是状态：

- 未使用
- 辅助
- 主导
- 自动化

### 评估维度

- 效率：Lead Time、人工投入、Codex 参与阶段
- 质量：首次验证结果、Review 修改次数、返工和回归
- 沉淀：规则、Skill、脚本、测试或文档
- 结果：1–5 分人工评分

## 目录

- [设计说明](docs/design.md)
- [字段字典](docs/field-dictionary.md)
- [指标与复盘](docs/metrics-and-review.md)
- [仓库清单](config/repositories.yml)
- [业务仓库 Issue Form 源模板](templates/codex-task.yml)
- [同步工作流](.github/workflows/sync-templates.yml)

## 使用方式

1. 在真实业务仓库创建 Codex Task Issue。
2. 填写目标、范围、验收标准和初始 Codex 字段。
3. 将 Issue 加入跨仓库 Project `Codex Delivery OS`。
4. 在 Codex 中引用 Issue 编号和仓库，按状态推进。
5. 创建 PR，并在 PR 中关联 Issue，例如 `Closes #123`。
6. Review、验证完成后补齐结果字段并完成复盘。
7. 当模板或指标发生变化时，由本仓库创建同步 PR 到登记的业务仓库。

## 当前边界

本仓库不会：

- 镜像或复制业务代码；
- 代替业务仓库保存 Issue、PR、CI；
- 自动记录完整对话内容；
- 用 Token、对话轮数或模型名称作为核心绩效指标；
- 在没有 GitHub App 凭据时直接修改业务仓库。

## 第一阶段

先在少量业务仓库试运行，观察 5–10 个已完成任务，再调整字段。优先关注：

- 记录成本是否足够低；
- Lead Time 与人工投入是否可获得；
- 质量评分是否能解释返工；
- 哪些 Codex 规则值得沉淀为可复用资产。
