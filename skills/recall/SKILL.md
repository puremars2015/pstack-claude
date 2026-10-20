---
name: recall
description: 根據可存取的相關聊天與專案紀錄，重建任務背景、既定決策與尚未完成的工作。
disable-model-invocation: true
---

Read [the runtime contract](../poteto-mode/references/claude-runtime.md) before executing this skill.

# Recall

Use the conversation already available, the project's memory directory, and read-only history for the specific relevant session when accessible (session tools, or that session's transcript under `~/.claude/projects/`). Inspect current repository state to distinguish an old plan from implemented work. Do not scrape private application databases or claim access to unavailable conversations.

Return the current objective, accepted decisions, exact revisions/artifacts, completed work, unfinished work, and blockers with sources. Exclude unrelated private history. Mark stale or contradictory records and say which current observation resolves them. Reading another session does not authorize sending it a message.
