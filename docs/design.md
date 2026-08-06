# Codex Delivery OS 设计说明

## 1. 目标与边界

`jiefury/kanban` 是跨项目 Codex 使用管理台，不是业务代码仓库。

它只保存 Issue Form 源模板、Project 字段和视图规范、Codex 使用与交付指标、任务复盘模板、目标业务仓库清单，以及通过 GitHub App 创建同步 PR 的工作流。

它不保存真实业务代码，也不复制业务仓库的 Issue、PR、CI 或发布物。

## 2. 任务模型

一个真实开发任务对应一个业务仓库 Issue。一条任务可以包含多轮 Codex 对话、多个提交和一个或多个 PR，但不因为对话次数拆分记录。

交付链：

```text
业务仓库 Issue
  → Ready
  → In Progress
  → Review
  → Verify
  → Done
```

异常路径：

- `In Progress → Blocked`：等待需求、权限、环境或外部依赖；
- `Review / Verify → Rework → Review`：发现问题后返工；
- 未合并、未验证的任务不能标记 `Done`。

## 3. GitHub 结构

| 层级 | 所在位置 | 职责 |
| --- | --- | --- |
| 真实任务 | 业务仓库 Issue | 目标、范围、验收、复盘 |
| 代码交付 | 业务仓库 PR | 代码、Review、CI、合并 |
| 统一追踪 | 跨仓库 Project `Codex Delivery OS` | 状态、字段、视图、指标 |
| 规范源 | 本仓库 | 模板、字段、指标、自动化 |

推荐 Project 视图：总览、当前执行、待验证、Codex 评估、沉淀。

## 4. 数据采集策略

自动采集 GitHub 能可靠提供的事实：Issue/PR 时间、PR 是否合并、Review 和 CI 活动、关联仓库。

人工只填写无法从 GitHub 推断的内容：Codex Mode、Codex Surface、Human Time、Rework Count、Blocker Reason、Verification、Regression、Reusable Output、Outcome Score 和复盘文字。

不把 Token、对话轮数或模型名称作为核心绩效指标，因为它们不能直接证明交付价值。

## 5. 同步机制

本仓库的 `templates/codex-task.yml` 是唯一源模板。

当源模板或仓库清单变化时，GitHub Actions 校验源文件和清单，读取 `enabled: true` 的目标，使用 GitHub App Token 创建同步分支、更新目标仓库的 Issue Form，并创建 Draft PR。未配置 App ID 或私钥时，不执行跨仓库同步。

## 6. 分阶段启用

第一阶段只登记少量真实业务仓库，完成 5–10 个任务后再调整字段。

第二阶段启用同步 App，并观察同步 PR 是否稳定。

第三阶段才基于 Project 数据生成月度趋势；在样本不足前，不用单个任务评分评价 Codex 总体质量。
