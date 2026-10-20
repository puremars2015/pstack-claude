---
name: setup-pstack
description: 設定 pstack 的工作流程偏好與角色選項，保留目前工作階段的預設模型。
---

Read [the runtime contract](../poteto-mode/references/claude-runtime.md) before executing this skill.

# Setup pstack

Read the runtime contract for configuration precedence. Detect the session's actual model choices (the values the Agent tool's `model` parameter exposes) and tool capabilities; do not infer entitlement from model marketing names. If no preferences were requested, write the defaults below. Do not ask for a budget just to complete initial setup. An optional user-selected role override must match an exposed model and effort and comply with the host's override rules.

Use `~/.claude/pstack/config.json` for a personal setup, or `<repository>/.claude/pstack.json` when the user asks for project scope. Preserve existing recognized preferences and report invalid entries before replacing them. Validate the result with the bundled schema, e.g. `python <plugin-root>/scripts/validate.py --config <path>`. Never modify the session's default model, settings.json, or CLAUDE.md.

```json
{"version": 1, "model": "inherit-parent", "candidate_count": 2, "roles": {}}
```

Report the actual path and settings. This file guides these skills; it does not alter the host or make new models available. Verification scaffolding and formal verification remain separate optional tasks.
