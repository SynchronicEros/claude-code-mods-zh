# claude-code-mods-zh

繁體中文介面的 Claude Code Mods（function hooks plugins）與 skills 總目錄。每個 Mod 或 skill 各自一個 repo，可一次加入本目錄後挑著裝，也可單獨安裝。

| Mod | 用途 |
|---|---|
| [`progress`](https://github.com/SynchronicEros/claude-code-progress-zh) | 任務進度條：同時開多個 session 時，在輸入框上方列出每個 session 正在執行的任務做到幾成、約剩幾分鐘、是否在等你回應 |
| [`retro`](https://github.com/SynchronicEros/claude-code-retro-zh) | 復盤：偵測到你在糾正 Claude 時主動提議復盤，列出擬固定的教訓讓你逐項核准，再交給主對話寫入記憶或規則檔 |
| [`next-steps-zh`](https://github.com/SynchronicEros/claude-code-next-steps-zh) | 下一步建議繁中版：每回合結束後在輸入框上方給至多三則下一步建議；改寫自社群 plugin `next-steps` |

| Skill | 用途 |
|---|---|
| [`codex-image`](https://github.com/SynchronicEros/claude-code-codex-image-zh) | 經 Codex CLI 產圖：讓 Claude 呼叫 Codex 內建影像生成工具，原圖直接存進目前專案；須先自行安裝並登入 Codex CLI |
| [`doc-governance`](https://github.com/SynchronicEros/claude-code-doc-governance-zh) | 文件治理起手式：`setup` 自公開範本建立 CLAUDE.md、決策紀錄與用途目錄，`upgrade` 比對範本更新並依擴增指南擴增規範；範本內容為 CC BY 4.0 |

## 安裝

- 需要 **Claude Code（付費方案）**；Codex 免費版不能安裝（只有 Codex 的人，改照[範本 repo 的「只用 Codex 的人」](https://github.com/SynchronicEros/eros-kmu-learning-example#只用-codex不用-claude-code的人)）。
- 還沒裝 Claude Code：見[官方安裝說明](https://code.claude.com/docs/zh-TW/setup)。
- Mod（`progress`、`retro`、`next-steps-zh`）需要 Claude Code **v2.1.287 以上**（Mods 於 2026/10/01 推出，API 仍屬 early access，也就是搶先體驗版，引擎更新可能使 Mod 失效）；skill 無此限制。
- Mac 第一次安裝可能跳出安裝「命令列開發者工具」的視窗：按「安裝」，裝完再重跑一次指令。
- Windows：三個 Mod 不需另裝工具（作者尚未在 Windows 實機測試）；`codex-image` 與 `doc-governance` 需要 Git Bash：安裝 [Git for Windows](https://git-scm.com/downloads/win) 就有（選項都用預設即可），裝完重開 Claude Code。

**指令貼在哪裡**：貼在**終端機**，貼上後按 Enter（Mac：按 ⌘＋空白鍵開 Spotlight，搜尋「終端機」；Windows：在開始選單搜尋「PowerShell」）。不是貼在 Claude Code 的對話框。若終端機回應 `command not found`（找不到指令），表示終端機裡還沒有 Claude Code：照上面的官方安裝說明安裝；只用桌面版的人，改用下方「對話框裡」的寫法。

先查版本，會顯示像 `2.1.292 (Claude Code)` 的一行；版本太舊就執行 `claude update`：

```bash
claude --version
```

```bash
claude plugin marketplace add SynchronicEros/claude-code-mods-zh
```

```bash
claude plugin install progress@claude-code-mods-zh
```

`retro`、`next-steps-zh`、`codex-image`、`doc-governance` 同法安裝（把 `progress` 換成名稱）。

**對話框裡**（已經在 Claude Code 裡，或只用桌面版）：改打 `/plugin marketplace add SynchronicEros/claude-code-mods-zh`，再打 `/plugin install progress@claude-code-mods-zh`；會跳出英文選單，選第一個 **Install for you (user scope)**。

安裝時若出現英文訊息「SSH not configured, cloning via HTTPS」或「userConfig options not yet set」，可以忽略（沒設定就用預設值）。

裝好後要**開新的 session（一次新對話）**才會生效：終端機版先打 `/exit` 離開，再打 `claude`；桌面版開一個新對話。

**本目錄與單一 repo 二擇一**：每個 Mod 或 skill 也可直接從它自己的 repo 安裝，但同一個只從一處裝（skill 兩處都裝會出現兩份）。用 `claude plugin list` 檢查；若同一名稱出現兩次（例如 `doc-governance@claude-code-mods-zh` 與 `doc-governance@claude-code-doc-governance-zh`），**保留本目錄那份**，移除單一 repo 那份（只執行一次）：

```bash
claude plugin uninstall doc-governance@claude-code-doc-governance-zh
```

再用 `claude plugin list` 確認只剩一份。對話框裡：打 `/plugin`、按 Tab 切到 Installed 分頁檢查，打 `/plugin uninstall` 開啟面板移除。桌面版：按輸入框旁的「＋」→ Plugins → Manage plugins，可停用或移除。

`next-steps-zh` 與官方 `next-steps` 不可同時啟用，否則會出現兩組建議。先用 `claude plugin list` 看有沒有 `next-steps@claude-community`；**沒有就不用做**，有的話停用（對話框裡打 `/plugin disable` 開啟面板操作）：

```bash
claude plugin disable next-steps@claude-community
```

重複執行，或對沒裝的東西執行時，出現 ✘ 與「not installed」或「already disabled」都無害。

## 更新

有新版時，在終端機執行兩行（把 `progress` 換成要更新的名稱），再開新的 session：

```bash
claude plugin marketplace update claude-code-mods-zh
```

```bash
claude plugin update progress@claude-code-mods-zh
```

看到「already at the latest version」就代表已是最新版。對話框裡：先打 `/plugin marketplace update claude-code-mods-zh`，再打 `/plugin`、按 Tab 切到 Installed 分頁，選要更新的 plugin → Update now。桌面版的更新方式官方文件沒有說明，找不到的話請改用終端機。`doc-governance` 0.1.3 起 skill `init` 改名為 `setup`：更新後改打 `/doc-governance:setup`，或照舊說「建立治理架構」。

## 額度與隱私

- `codex-image` 每張圖用掉你自己的 ChatGPT 產圖額度；請用自己的 ChatGPT 帳號，不要多人共用。
- 三個 Mod 都會使用你自己的 Claude 額度呼叫模型：`progress` 以分身估進度（短任務約 2–3 次、長任務約每分鐘 1 次）；`retro` 偵測到疑似糾正時以小模型確認一次、復盤時呼叫分身一次；`next-steps-zh` 每個夠長的回答後呼叫分身一次。
- 資料只留在本機：`progress` 把各 session 狀態寫在 `~/.claude/claude-mods-data/progress/`（有設 `CLAUDE_CONFIG_DIR` 時在該目錄下）；`retro` 與 `next-steps-zh` 不寫任何檔案。
- 安裝任何 Mod 前請先讀原始碼：Mod 跑在 Claude Code 程序內，能讀寫檔案與呼叫模型。

## 授權

MIT（見 [LICENSE](LICENSE)）；`doc-governance` 下載的範本內容依範本 repo 的 CC BY 4.0。`next-steps-zh` 改寫自 Thariq Shihipar 之 `next-steps`，原作授權與修改說明見該 repo 的 [NOTICE.md](https://github.com/SynchronicEros/claude-code-next-steps-zh/blob/main/NOTICE.md)。

---

## English

Index of Claude Code Mods (function-hook plugins) and skills with a Traditional Chinese UI. Each one lives in its own repo; add this marketplace once and pick, or install any mod from its own repo:

- **[progress](https://github.com/SynchronicEros/claude-code-progress-zh)** — a task progress band above the prompt: every local session's running task, percent done, minutes left, and whether it is waiting for you.
- **[retro](https://github.com/SynchronicEros/claude-code-retro-zh)** — when you correct Claude, it offers a retrospective; you approve the proposed lessons one by one, and the main thread writes them into memory or rule files. The mod itself writes nothing.
- **[next-steps-zh](https://github.com/SynchronicEros/claude-code-next-steps-zh)** — up to three next-prompt suggestions after each turn, in Traditional Chinese; adapted from the community plugin `next-steps`.
- **[codex-image](https://github.com/SynchronicEros/claude-code-codex-image-zh)** (skill) — Claude generates images through the Codex CLI's built-in image tool and saves the original file into your project. Install and log in to the Codex CLI yourself first; each image uses your own ChatGPT quota.
- **[doc-governance](https://github.com/SynchronicEros/claude-code-doc-governance-zh)** (skills) — a minimal document-governance starter kit: `setup` sets up CLAUDE.md, a decision log and folders from the public template; `upgrade` compares with the latest template and drafts new rules when you need them. Template content is CC BY 4.0.

**Install** (requires Claude Code on a paid plan — the free Codex tier cannot install these; mods need v2.1.287+, check with `claude --version`; the mods API is early access; on Windows the mods need no extra tools (not yet tested there), the two skills need Git Bash):

```bash
claude plugin marketplace add SynchronicEros/claude-code-mods-zh
```

```bash
claude plugin install progress@claude-code-mods-zh
```

Install `retro`, `next-steps-zh`, `codex-image` and `doc-governance` the same way. Install each one from either this index or its own repo, not both — keep the index copy and remove the other with `claude plugin uninstall <name>@<its repo>` (skills installed twice show up twice; check with `claude plugin list`). To update: `claude plugin marketplace update claude-code-mods-zh`, then `claude plugin update <name>@claude-code-mods-zh`, then start a new session.

Changes take effect in new sessions. Do not enable `next-steps-zh` together with the official `next-steps` (`claude plugin disable next-steps@claude-community`).

**Quota and privacy:** the three mods call the model on your own quota (and `codex-image` uses your ChatGPT image quota) (see the notes above). Data stays local; only `progress` writes files, under `~/.claude/claude-mods-data/progress/`. Read the source before installing any mod.

**License:** MIT. `next-steps-zh` is adapted from Thariq Shihipar's `next-steps`; see its NOTICE.
