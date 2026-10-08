# claude-code-mods-zh

繁體中文介面的 Claude Code Mods（function hooks plugins）總目錄。三個 Mod 各自一個 repo，可一次加入本目錄後挑著裝，也可單獨安裝。

| Mod | 用途 |
|---|---|
| [`progress`](https://github.com/SynchronicEros/claude-code-progress-zh) | 任務進度條：同時開多個 session 時，在輸入框上方列出每個 session 正在執行的任務做到幾成、約剩幾分鐘、是否在等你回應 |
| [`retro`](https://github.com/SynchronicEros/claude-code-retro-zh) | 復盤：偵測到你在糾正 Claude 時主動提議復盤，列出擬固定的教訓讓你逐項核准，再交給主對話寫入記憶或規則檔 |
| [`next-steps-zh`](https://github.com/SynchronicEros/claude-code-next-steps-zh) | 下一步建議繁中版：每回合結束後在輸入框上方給至多三則下一步建議；改寫自社群 plugin `next-steps` |

## 安裝

需要 Claude Code **v2.1.287 以上**（Mods 於 2026/10/01 推出，API 仍屬 early access，引擎更新可能使 Mod 失效）。

```bash
claude plugin marketplace add SynchronicEros/claude-code-mods-zh
```

```bash
claude plugin install progress@claude-code-mods-zh
```

`retro`、`next-steps-zh` 同法安裝。只想要其中一個，也可直接加入該 Mod 的 repo（安裝方式見各 repo README）。安裝或更新後，**新開的 session 才會生效**。
`next-steps-zh` 與官方 `next-steps` 不可同時啟用，否則會出現兩組建議。

## 額度與隱私

- 三個 Mod 都會使用你自己的 Claude 額度呼叫模型：`progress` 以分身估進度（短任務約 2–3 次、長任務約每分鐘 1 次）；`retro` 偵測到疑似糾正時以小模型確認一次、復盤時呼叫分身一次；`next-steps-zh` 每個夠長的回答後呼叫分身一次。
- 資料只留在本機：`progress` 把各 session 狀態寫在 `~/.claude/claude-mods-data/progress/`；`retro` 與 `next-steps-zh` 不寫任何檔案。
- 安裝任何 Mod 前請先讀原始碼：Mod 跑在 Claude Code 程序內，能讀寫檔案與呼叫模型。

## 授權

MIT（見 [LICENSE](LICENSE)）。`next-steps-zh` 改寫自 Thariq Shihipar 之 `next-steps`，原作授權與修改說明見該 repo 的 [NOTICE.md](https://github.com/SynchronicEros/claude-code-next-steps-zh/blob/main/NOTICE.md)。

---

## English

Index of Claude Code Mods (function-hook plugins) with a Traditional Chinese UI. Each mod lives in its own repo; add this marketplace once and pick, or install any mod from its own repo:

- **[progress](https://github.com/SynchronicEros/claude-code-progress-zh)** — a task progress band above the prompt: every local session's running task, percent done, minutes left, and whether it is waiting for you.
- **[retro](https://github.com/SynchronicEros/claude-code-retro-zh)** — when you correct Claude, it offers a retrospective; you approve the proposed lessons one by one, and the main thread writes them into memory or rule files. The mod itself writes nothing.
- **[next-steps-zh](https://github.com/SynchronicEros/claude-code-next-steps-zh)** — up to three next-prompt suggestions after each turn, in Traditional Chinese; adapted from the community plugin `next-steps`.

**Install** (Claude Code v2.1.287+; the mods API is early access):

```bash
claude plugin marketplace add SynchronicEros/claude-code-mods-zh
```

```bash
claude plugin install progress@claude-code-mods-zh
```

Changes take effect in new sessions. Do not enable `next-steps-zh` together with the official `next-steps`.

**Quota and privacy:** all three call the model on your own quota (see the notes above). Data stays local; only `progress` writes files, under `~/.claude/claude-mods-data/progress/`. Read the source before installing any mod.

**License:** MIT. `next-steps-zh` is adapted from Thariq Shihipar's `next-steps`; see its NOTICE.
