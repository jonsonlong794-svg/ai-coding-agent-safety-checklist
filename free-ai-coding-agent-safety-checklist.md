
# AI Coding Agent Safety Checklist

> Before you let Claude Code, Codex, Cursor, or any AI coding agent edit your repo, check these 30 things.

---

# Part I. English Version

## Why this checklist exists

AI coding agents are powerful, but they are not automatically safe.

They can write code, edit files, refactor modules, add dependencies, change configuration, and sometimes modify more than you expected.

The problem is not that coding agents are useless.

The problem is that most people use them without a workflow.

This checklist helps you manage coding agents like junior developers:

- give them clear tasks,
- limit their scope,
- review their work,
- test their output,
- and keep a rollback path.

Use this checklist before every non-trivial agent coding session.

---

## 1. Before you run the agent

### A. Repository safety

- [ ] I am working on a separate Git branch, not directly on `main` or `master`.
- [ ] I have committed or saved the current working state.
- [ ] I checked `git status` before starting.
- [ ] I know which files are allowed to be changed.
- [ ] I know which files must not be touched.
- [ ] I have a simple rollback plan.

### B. Task clarity

- [ ] The task has one clear goal.
- [ ] I wrote the expected outcome.
- [ ] I wrote what is out of scope.
- [ ] I listed relevant files, folders, commands, or docs.
- [ ] I defined acceptance criteria.
- [ ] I know how I will verify the result.

### C. Risk control

- [ ] The task does not involve secrets, credentials, tokens, or private keys.
- [ ] The task does not require production database changes.
- [ ] The task does not modify authentication, billing, or permissions unless explicitly reviewed.
- [ ] The task does not modify deployment configuration unless necessary.
- [ ] The agent is not allowed to delete files without asking.
- [ ] The agent is not allowed to add dependencies without explaining why.

---

## 2. Copy-paste prompt before execution

Use this prompt before letting the agent edit files:

```text
You are working as a careful coding agent.

Before making changes:
1. Restate the task in your own words.
2. Identify the relevant files.
3. List the likely risks.
4. Propose a short implementation plan.
5. Wait for my approval before editing files.

Constraints:
- Do not touch files outside the agreed scope.
- Do not delete files unless I explicitly approve.
- Do not add dependencies unless necessary.
- Do not modify authentication, billing, database, deployment, or permission logic unless I explicitly approve.
- Explain every important change.
- Provide tests or manual verification steps.
- At the end, summarize changed files, tests run, remaining risks, and rollback instructions.
```

---

## 3. During the agent run

Stop the agent if any of these happen:

- [ ] The agent starts editing before explaining the plan.
- [ ] The agent touches unrelated files.
- [ ] The agent makes a very large diff without warning.
- [ ] The agent deletes files unexpectedly.
- [ ] The agent adds dependencies without explanation.
- [ ] The agent changes authentication, permissions, billing, database, or deployment logic.
- [ ] The agent says “this should work” without tests or evidence.
- [ ] The agent cannot explain why a change is necessary.

---

## 4. After the agent finishes

### A. Review the diff

- [ ] I reviewed every changed file.
- [ ] The diff matches the original task.
- [ ] There are no unrelated refactors.
- [ ] There are no unexpected file deletions.
- [ ] There are no unnecessary dependency changes.
- [ ] No secrets, tokens, or credentials were exposed.

### B. Test the output

- [ ] Existing tests pass.
- [ ] New tests were added if needed.
- [ ] Manual verification steps are written.
- [ ] I tested the main user flow.
- [ ] I checked at least one edge case.
- [ ] I checked whether the change could break existing behavior.

### C. Prepare rollback

- [ ] I know how to revert the change.
- [ ] I know the previous stable commit.
- [ ] I recorded what changed.
- [ ] I recorded known limitations or remaining risks.

---

## 5. Final merge question

Before merging, ask yourself:

> Would I be comfortable explaining this agent-generated change to another developer tomorrow?

If the answer is no, do not merge yet.

---

## 6. Quick risk levels

### Low risk

Examples:

- small UI text changes,
- documentation updates,
- small bug fixes,
- isolated utility functions.

You still need review and tests.

### Medium risk

Examples:

- modifying business logic,
- changing API behavior,
- adding dependencies,
- refactoring multiple files,
- touching shared components.

You need clear acceptance criteria and rollback.

### High risk

Examples:

- authentication,
- authorization,
- billing,
- database migrations,
- deployment config,
- permissions,
- file deletion,
- security-sensitive code.

Do not let the agent make these changes without a strict plan and human review.

---

## 7. One-page version

Use this short version when you are in a hurry:

```text
Before:
- Create a branch.
- Commit current work.
- Define goal, scope, non-goals, and acceptance criteria.
- List allowed files and forbidden files.
- Ask the agent to explain the plan before editing.

During:
- Stop if it edits unrelated files.
- Stop if it changes auth, database, billing, deployment, permissions, or secrets.
- Stop if it adds dependencies without explanation.

After:
- Review every changed file.
- Run tests.
- Do manual verification.
- Check rollback path.
- Do not merge if you cannot explain the diff.
```

---

# Part II. 中文版

# AI 编程 Agent 安全使用清单

> 在让 Claude Code / Codex / Cursor 或任何 AI 编程 Agent 修改你的代码库之前，先检查这 30 件事。

---

## 为什么需要这份清单？

AI 编程 Agent 很强，但它并不天然安全。

它可以写代码、改文件、重构模块、添加依赖、修改配置，有时候还会改到你没预期的地方。

问题不是 AI 编程 Agent 没用。

真正的问题是：

> 大多数人不是在“管理”AI 编程 Agent，而是在“放任”AI 编程 Agent 随机改代码。

这份清单的核心思想是：

> 不要把 AI 编程 Agent 当魔法工具，要把它当初级程序员管理。

你需要给它：

- 清晰任务，
- 明确边界，
- 可用上下文，
- 审查标准，
- 测试要求，
- 回滚路径。

---

## 1. 在运行 Agent 之前

### A. 代码库安全

- [ ] 我正在一个单独的 Git 分支上工作，而不是直接在 `main` 或 `master` 上改。
- [ ] 我已经提交或保存了当前工作状态。
- [ ] 我已经运行过 `git status`。
- [ ] 我知道哪些文件允许 Agent 修改。
- [ ] 我知道哪些文件禁止 Agent 修改。
- [ ] 我知道如果出问题怎么回滚。

### B. 任务是否清楚

- [ ] 这个任务只有一个明确目标。
- [ ] 我写清楚了预期结果。
- [ ] 我写清楚了哪些内容不属于本次任务。
- [ ] 我列出了相关文件、文件夹、命令或文档。
- [ ] 我定义了验收标准。
- [ ] 我知道如何验证结果是否正确。

### C. 风险控制

- [ ] 这个任务不涉及 secrets、credentials、tokens 或 private keys。
- [ ] 这个任务不需要修改生产数据库。
- [ ] 这个任务不修改认证、权限、支付或计费逻辑，除非我会专门审查。
- [ ] 这个任务不修改部署配置，除非确实必要。
- [ ] Agent 不允许在未经确认的情况下删除文件。
- [ ] Agent 不允许在没有解释原因的情况下添加新依赖。

---

## 2. 运行前可复制的 Prompt

在让 Agent 修改文件前，先复制这段：

```text
你是一个谨慎的 AI 编程 Agent。

在修改任何文件之前，请先完成以下步骤：

1. 用你自己的话复述任务。
2. 找出可能相关的文件。
3. 列出潜在风险。
4. 提出一个简短的实现计划。
5. 等我确认后，再开始修改文件。

约束条件：
- 不要修改约定范围之外的文件。
- 不要删除文件，除非我明确同意。
- 不要添加新依赖，除非确实必要并解释原因。
- 不要修改认证、支付、数据库、部署或权限逻辑，除非我明确同意。
- 解释每个重要改动。
- 给出测试方法或手动验证步骤。
- 最后总结：修改了哪些文件、运行了哪些测试、还有哪些风险、如何回滚。
```

---

## 3. Agent 运行过程中

如果出现以下情况，立刻停下来检查：

- [ ] Agent 还没解释计划就开始修改文件。
- [ ] Agent 修改了无关文件。
- [ ] Agent 生成了非常大的 diff，但没有提前说明。
- [ ] Agent 意外删除了文件。
- [ ] Agent 添加了新依赖，但没有解释原因。
- [ ] Agent 修改了认证、权限、支付、数据库或部署逻辑。
- [ ] Agent 只说 “this should work”，但没有测试或证据。
- [ ] Agent 不能解释为什么某个改动是必要的。

---

## 4. Agent 完成之后

### A. 审查 diff

- [ ] 我检查了每一个被修改的文件。
- [ ] diff 和原始任务一致。
- [ ] 没有无关重构。
- [ ] 没有意外删除文件。
- [ ] 没有不必要的依赖变化。
- [ ] 没有暴露 secrets、tokens 或 credentials。

### B. 测试结果

- [ ] 现有测试通过。
- [ ] 如果需要，已经添加了新测试。
- [ ] 已经写出手动验证步骤。
- [ ] 我测试了主要用户流程。
- [ ] 我至少检查了一个边界情况。
- [ ] 我检查了是否可能破坏已有行为。

### C. 回滚准备

- [ ] 我知道如何撤回这次修改。
- [ ] 我知道上一个稳定 commit 是哪个。
- [ ] 我记录了这次改了什么。
- [ ] 我记录了已知限制或剩余风险。

---

## 5. 合并前最后一个问题

在 merge 之前，问自己：

> 如果明天让我向另一个开发者解释这次 AI Agent 生成的改动，我能解释清楚吗？

如果答案是否定的，不要合并。

---

## 6. 风险等级

### 低风险

例子：

- 文案修改，
- 文档更新，
- 小 bug 修复，
- 独立工具函数。

仍然需要审查和测试。

### 中风险

例子：

- 修改业务逻辑，
- 改变 API 行为，
- 添加依赖，
- 重构多个文件，
- 修改共享组件。

需要明确验收标准和回滚方案。

### 高风险

例子：

- 认证，
- 权限，
- 支付，
- 数据库迁移，
- 部署配置，
- 文件删除，
- 安全敏感代码。

不要让 Agent 在没有严格计划和人工审查的情况下修改这些内容。

---

## 7. 一页极简版

赶时间时，至少做这几件事：

```text
运行前：
- 新建分支。
- 提交当前状态。
- 写清楚目标、范围、非目标和验收标准。
- 列出允许修改和禁止修改的文件。
- 要求 Agent 先解释计划，再修改文件。

运行中：
- 如果它修改无关文件，停止。
- 如果它修改认证、数据库、支付、部署、权限或 secrets，停止。
- 如果它添加依赖但不解释原因，停止。

运行后：
- 检查每个被修改文件。
- 运行测试。
- 做手动验证。
- 确认回滚路径。
- 如果你解释不清 diff，不要 merge。
```

---

# Suggested CTA / 推荐结尾

If this checklist was useful, the full **AI Coding Agent Operating System** includes:

- AGENTS.md template
- task brief template
- context pack template
- agent run log
- code review checklist
- test and acceptance checklist
- rollback checklist
- handoff summary
- example workflow

中文：

如果这份清单对你有帮助，完整的 **AI Coding Agent Operating System** 还包括：

- AGENTS.md 模板
- 任务说明模板
- 项目上下文模板
- Agent 运行日志
- 代码审查清单
- 测试验收清单
- 回滚清单
- 交接总结模板
- 示例工作流
