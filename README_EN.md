# AGY Pulse

[简体中文](./README.md) | **English**

Minimalist Windows native magnetic HUD capsule and side-pane monitor for **Google Antigravity (IDE / 2.0)** — tracking live quota limits, real auto-compaction context capacity, and concurrent token speed (`tok/s`) with instant **EN / 中文** switching.

---

## One-Line Install / Update (Windows PowerShell)

Run the following command in PowerShell to install the official `agy` CLI (for quota sync), extract the plugin, and hot-reload the HUD:

```powershell
irm https://raw.githubusercontent.com/Yuuki113/agy-pulse/main/agy-pulse.ps1 | iex
```

Or download [`agy-pulse.ps1`](./agy-pulse.ps1) and run it locally:

```powershell
powershell -ExecutionPolicy Bypass -File .\agy-pulse.ps1
```

---

## Clean Uninstall

### Option 1: One-Line PowerShell Uninstall (Recommended)

Stops the floating HUD and sidecar processes, then removes the plugin directory and cached runtime data:

```powershell
& ([scriptblock]::Create((irm https://raw.githubusercontent.com/Yuuki113/agy-pulse/main/agy-pulse.ps1))) -Uninstall
```

From a local script:

```powershell
powershell -ExecutionPolicy Bypass -File .\agy-pulse.ps1 -Uninstall
```

> Append `-KeepData` to preserve your saved HUD position and language preference.

### Option 2: Disable / Uninstall in Antigravity UI

Open `Skills & Customizations -> Plugins` in the left sidebar of Antigravity, find **AGY Pulse**, and toggle or uninstall it.

---

## Features

1. **Minimalist 3-Segment Magnetic Capsule**
   - **Remaining Quota**: Automatically tracks your active model group and surfaces whichever bucket (`Weekly` or `5h`) is tighter.
   - **Real Active Context Window**: Calibrated to Antigravity's actual auto-compaction caps (`512k` for Gemini 4 series, `256k` for Flash, `200k` for Claude), with 3-tier health colors (`<35%` green / `35–75%` amber / `≥75%` red).
   - **Live Global Total `tok/s`**: Shows the current chat's speed alongside the live aggregate throughput `Σ` across all currently running conversations.

2. **Click-to-Expand Detail Card (Zero Accidental Hover Popups)**
   - **Actual Routed Model & Prompt Cache Hit Rate**: Top header displays the live routed model for the active step (distinguishing `Gemini 4 Neon` vs `Gemini 4 Hydrogen` in Orchestrator mode) alongside prompt cache hit rate.
   - **Dual-Group Quota Breakdown**: Shows `Weekly` (left) and `5h Limit` (right) bars and compact reset countdowns for both `Gemini` and `Claude / GPT`.
   - **Active Chats Speed List**: Shows only currently generating conversations with each chat's **actual routed model badge** (e.g. `G4 Neon` / `G4 Hydrogen` / `G4 Carbon`), context usage, and live `tok/s` (idle chats are hidden).

3. **Instant EN / 中文 Language Toggle**
   - Automatically detects your system locale on first launch (`zh` for Chinese locales, `en` otherwise).
   - Switch anytime via the **`EN` / `中`** button in the expanded HUD header, the capsule right-click menu, or the side-pane dashboard — persisted and synced immediately without restarting.

4. **Native, Non-Intrusive UX**
   - **Left-click** to expand/collapse (automatically restores editor focus so typing is never interrupted);
   - **Left-drag** anywhere on the titlebar (position persists across restarts);
   - **Right-click** menu for toggle, language switch, reset position, force refresh, or hide;
   - Automatically hides when switching away from Antigravity and starts/exits with the app.

---

## Troubleshooting

### Seeing `"agy CLI not found"` or quota missing after updating Antigravity?

Live account quota uses the official `agy` CLI (`%LOCALAPPDATA%\agy\bin\agy.exe`). Because the Antigravity Desktop NSIS updater wipes `%LOCALAPPDATA%\agy` during app upgrades, AGY Pulse includes built-in self-healing:
1. **Update-Proof Mirror**: Automatically keeps a protected mirror of `agy.exe` inside the plugin's data directory and restores it transparently after Antigravity updates;
2. **One-Click Background Auto-Install**: If `antigravity.google` was unreachable during initial setup, simply **enable your proxy / TUN mode and click `↻`** in the expanded HUD card — AGY Pulse will automatically install `agy` CLI in the background and sync your quota immediately.

---

## License

[MIT License](./LICENSE) — Copyright (c) 2026 Yuuki113
