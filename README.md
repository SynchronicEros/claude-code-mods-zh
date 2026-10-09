# claude-code-mods-zh

繁體中文介面的 Claude Code Mods（function hooks plugins）與 skills 總目錄。每個 Mod 或 skill 各自一個 repo，可一次加入本目錄後挑著裝，也可單獨安裝。

## 安裝

**需要 Claude Code（付費方案）；Codex 免費版不能安裝。** Mod（`progress`、`retro`、`next-steps-zh`）另需 Claude Code **v2.1.287 以上**（Mods 於 2026/10/01 推出，API 仍屬 early access，引擎更新可能使 Mod 失效）；skill 無此限制。查版本：

```bash
claude --version
```

Windows：Windows 版 Claude Code 也能安裝。三個 Mod 不呼叫外部指令，不需另裝工具（作者尚未在 Windows 實機測試）；`codex-image` 與 `doc-governance` 需要 Git Bash。

```bash
claude plugin marketplace add SynchronicEros/claude-code-mods-zh
```

```bash
claude plugin install progress@claude-code-mods-zh
```

`retro`、`next-steps-zh`、`codex-image`、`doc-governance` 同法安裝。只想要其中一個，也可直接加入該 Mod 的 repo（安裝方式見各 repo README）。安裝或更新後，**新開的 session 才會生效**。

`next-steps-zh` 與官方 `next-steps` 不可同時啟用，否則會出現兩組建議；裝過官方版的人先停用：

```bash
claude plugin disable next-steps@claude-community
```

| Mod | 用途 |
|---|---|
| [`progress`](https://github.com/SynchronicEros/claude-code-progress-zh) | 任務進度條：同時開多個 session 時，在輸入框上方列出每個 session 正在執行的任務做到幾成、約剩幾分鐘、是否在等你回應 |
| [`retro`](https://github.com/SynchronicEros/claude-code-retro-zh) | 復盤：偵測到你在糾正 Claude 時主動提議復盤，列出擬固定的教訓讓你逐項核准，再交給主對話寫入記憶或規則檔 |
| [`next-steps-zh`](https://github.com/SynchronicEros/claude-code-next-steps-zh) | 下一步建議繁中版：每回合結束後在輸入框上方給至多三則下一步建議；改寫自社群 plugin `next-steps` |

| Skill | 用途 |
|---|---|
| [`codex-image`](https://github.com/SynchronicEros/claude-code-codex-image-zh) | 經 Codex CLI 產圖：讓 Claude 呼叫 Codex 內建影像生成工具，原圖直接存進目前專案；須先自行安裝並登入 Codex CLI |
| [`doc-governance`](https://github.com/SynchronicEros/claude-code-doc-governance-zh) | 文件治理起手式：`setup` 自公開範本建立 CLAUDE.md、決策紀錄與用途目錄，`upgrade` 比對範本更新並依擴增指南擴增規範；範本內容為 CC BY 4.0 |

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

Changes take effect in new sessions. Do not enable `next-steps-zh` together with the official `next-steps` (`claude plugin disable next-steps@claude-community`).

**Quota and privacy:** all three call the model on your own quota (see the notes above). Data stays local; only `progress` writes files, under `~/.claude/claude-mods-data/progress/`. Read the source before installing any mod.

**License:** MIT. `next-steps-zh` is adapted from Thariq Shihipar's `next-steps`; see its NOTICE.
