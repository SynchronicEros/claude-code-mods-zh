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

在 Claude Code 裡貼上這段話（把「progress」換成想裝的名稱，或寫「全部」）：

> 請幫我安裝 https://github.com/SynchronicEros/claude-code-mods-zh 裡的 progress（照該 README「給協助安裝的 AI」一節），遇到問題幫我處理，裝好告訴我怎麼讓它生效。

要更新時說「請幫我把 progress 更新到最新版」。

<details>
<summary>給協助安裝的 AI</summary>

- 需要 Claude Code（付費方案）；只有 Codex 的使用者無法安裝。
- 安裝（user scope，在終端機或 Bash 工具執行）：`claude plugin marketplace add SynchronicEros/claude-code-mods-zh`，再 `claude plugin install <名稱>@claude-code-mods-zh`。名稱：`progress`、`retro`、`next-steps-zh`、`codex-image`、`doc-governance`。
- 更新：`claude plugin marketplace update claude-code-mods-zh`，再 `claude plugin update <名稱>@claude-code-mods-zh`；顯示 already at the latest version 即為最新。
- 一律保留總目錄那份；若同時從單一 repo 裝了同名者（例如 `doc-governance@claude-code-doc-governance-zh`），執行 `claude plugin uninstall <名稱>@<該 repo 名>`。
- 安裝或更新後須開新的 session 才生效（終端機版 `/exit` 後重打 `claude`；桌面版開新對話）。桌面版 Code 分頁不能用 `/plugin` 指令。
- 三個 Mod 需要 Claude Code v2.1.287 以上（`claude --version` 查詢，太舊執行 `claude update`）；Windows 上兩個 skill 的指令需要 Git Bash（隨 Git for Windows 安裝）。
- 裝 `next-steps-zh` 前，若已裝官方 `next-steps@claude-community`，先 `claude plugin disable next-steps@claude-community`。
- `codex-image` 須由使用者本人安裝並登入 Codex CLI，不要代為登入。`doc-governance` 0.1.3 起 skill `init` 改名為 `setup`。

</details>

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

**Install:** requires Claude Code (a paid plan). Ask Claude Code to install the mod or skill you want from this repo, or run `claude plugin marketplace add SynchronicEros/claude-code-mods-zh`, then `claude plugin install <name>@claude-code-mods-zh`; changes take effect in new sessions. Install each one from this index only (if you also added its own repo, uninstall that copy). To update: `claude plugin marketplace update claude-code-mods-zh`, then `claude plugin update <name>@claude-code-mods-zh`. Do not enable `next-steps-zh` together with the official `next-steps`.

**Quota and privacy:** the three mods call the model on your own quota (and `codex-image` uses your ChatGPT image quota) (see the notes above). Data stays local; only `progress` writes files, under `~/.claude/claude-mods-data/progress/`. Read the source before installing any mod.

**License:** MIT. `next-steps-zh` is adapted from Thariq Shihipar's `next-steps`; see its NOTICE.
