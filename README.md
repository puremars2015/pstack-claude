# pstack for Claude Code

這是 pstack 的 Claude Code 版本,由 [pstack-codex](https://github.com/puremars2015/pstack-codex)(Codex 改編版)再改寫而來。核心工作流程與 23 個 playbook 已對應到 Claude Code 的工具介面。不是上游官方發行版,也不保證原版每一項機制都已移植。

## 內容

- 24 條核心工程原則。
- 23 套工作流程(playbook),由 `poteto-mode` 依任務挑選。
- 31 個實用技能,加上核心原則共 55 個技能。
- 技能選單說明為繁體中文;給代理執行的詳細規則主要保留英文。

## 安裝

從 GitHub 安裝(私人 repository,需要該機器上有可存取此 repo 的 Git 登入憑證):

```sh
claude plugin marketplace add puremars2015/pstack-claude
claude plugin install pstack@pstack-local
```

從本機資料夾安裝(在套件根目錄執行;Windows 上請用相對路徑 `./`):

```sh
claude plugin marketplace add ./
claude plugin install pstack@pstack-local
```

安裝後開新的工作階段才會載入。

## 使用

```text
/pstack:poteto-mode 重現這個 bug，找出根因，修正並驗證。
/pstack:how 說明這個模組的資料流。
/pstack:architect 比較這個 API 的兩種設計。
/pstack:interrogate 審查目前 diff，只回報有證據的問題。
/pstack:poteto-help 我想做 X,該用哪個流程?
/pstack:setup-pstack
```

除了 `setup-pstack`,所有技能都設成 `disable-model-invocation: true`,只有你明確輸入 `/pstack:...` 才會啟用,不會自動套用到一般對話。工作流程內部需要其他原則或技能時,會直接讀取同套件內的 `SKILL.md`。

預設沿用目前工作階段的模型與推理設定,不需要 API key、外部模型或 MCP server。平行工作(Agent 子代理、worktree 隔離)只有在你呼叫 `swarm`、`arena` 或明確要求平行處理時才會使用,否則逐項執行並說明限制。

## 設定

`setup-pstack` 寫入的個人設定在 `~/.claude/pstack/config.json`;專案設定 `<repo>/.claude/pstack.json` 優先,兩者不合併。這些只是技能讀取的工作流程偏好,不會改動 Claude Code 的 settings.json、CLAUDE.md 或預設模型。角色的模型覆寫只接受 Agent 工具 `model` 參數提供的值(例如 `sonnet`、`opus`、`haiku`)。

## 與 Codex 版的差異

- runtime 規範改為 [claude-runtime.md](skills/poteto-mode/references/claude-runtime.md):Agent 工具、背景代理通知、worktree 隔離、scratchpad、權限模式、提交歸屬規則。
- 呼叫語法由 `$pstack-codex:name` 改為 `/pstack:name`。
- `agents/openai.yaml` 的 `allow_implicit_invocation: false` 轉為 frontmatter 的 `disable-model-invocation: true`。
- 設定與專案技能路徑由 `.agents/`、`~/.codex/` 改為 `.claude/`、`~/.claude/`。
- 移除 `.codex-plugin/`、`.agents/plugins/marketplace.json` 與可攜式 `plugin.json`,改用 `.claude-plugin/`。

## 維護

更新時修改來源套件、提高 `.claude-plugin/plugin.json` 的版本,再重新安裝;不要修改 `~/.claude/plugins/cache` 裡的快取。

檢查套件:`python scripts/validate.py`(需要 PyYAML 與 jsonschema,版本見 `scripts/requirements-dev.txt`;技能執行時不需要)。決策記錄器是標準函式庫腳本 `skills/show-me-your-work/scripts/log.py`。其他技能不會自動執行任何安裝或排程腳本。

## 來源與授權

上游為 [cursor/plugins 的 pstack](https://github.com/cursor/plugins/tree/main/pstack),作者 Lauren Tan,MIT 授權。固定來源 commit、原始版本與移除範圍見 [UPSTREAM.json](UPSTREAM.json),原授權見 [LICENSE](LICENSE)。本改編保留來源聲明。模型多樣性、背景執行、UI 驗證與形式驗證都取決於當下實際可用的工具,不會只因安裝此套件就獲得。
