# AGY Pulse

**简体中文** | [English](./README_EN.md)

轻量极简的 **Google Antigravity (IDE / 2.0)** Windows 原生右上角悬浮状态胶囊与配额/速率监控插件（单文件自包含安装与卸载，支持**中 / 英实时互切**）。

---

## 一键安装 / 更新（Windows PowerShell）

打开 PowerShell 执行以下一行命令即可完成 `agy` CLI 配额桥接检测、插件释放与热重载启动：

```powershell
irm https://raw.githubusercontent.com/Yuuki113/agy-pulse/main/agy-pulse.ps1 | iex
```

也可以直接下载仓库中的单文件 [`agy-pulse.ps1`](./agy-pulse.ps1) 到本地执行：

```powershell
powershell -ExecutionPolicy Bypass -File .\agy-pulse.ps1
```

---

## 一键彻底卸载

### 方式一：PowerShell 一行彻底卸载（推荐）

自动关闭悬浮窗与后台进程，并删除插件目录及本地运行缓存：

```powershell
& ([scriptblock]::Create((irm https://raw.githubusercontent.com/Yuuki113/agy-pulse/main/agy-pulse.ps1))) -Uninstall
```

本地脚本卸载：

```powershell
powershell -ExecutionPolicy Bypass -File .\agy-pulse.ps1 -Uninstall
```

> 若希望保留悬浮窗拖拽坐标与语言设置以便日后重装复用，可在命令末尾追加 `-KeepData`。

### 方式二：在 Antigravity 界面内禁用 / 卸载

在 Antigravity 左侧栏进入 `Skills & Customizations -> Plugins`，找到 **AGY Pulse** 即可随时切换开关或卸载。

---

## 核心特性

1. **极简三段式常驻磁吸胶囊**
   - **剩余额度**：智能短板优先（自动匹配当前对话所属模型组，取 `周额度` 与 `5h 额度` 中剩余更少的一项实时预警）。
   - **真实上下文容量**：对齐 Antigravity 客户端真实自动压缩上限（Gemini 4 系列 `512k`、Flash `256k`、Claude `200k`），三色预警（`<35%` 绿 / `35%–75%` 黄 / `≥75%` 红）。
   - **实时全局总速（`tok/s`）**：同时展示当前对话实时 `tok/s` 与全局运行总速 `Σ`（实时汇总所有正在生成中的对话速率）。

2. **单击展开极简详情面板（防悬停误触）**
   - **当前实际路由模型与缓存命中率**：顶部实时展示当前步骤实际路由的模型名称（如编排模式下区分规划期的 `Gemini 4 Neon` 与执行期的 `Gemini 4 Hydrogen`）及 Prompt 缓存命中率。
   - **双模型组配额表**：并列展示 `Gemini` 与 `Claude / GPT` 的 **周额度** 与 **5h 额度** 进度及精简重置倒计时。
   - **运行中对话速率榜（支持单击直达切换）**：自动读取真实会话标题，仅统计并展示当前正在运行的对话，并在每行显示**实际路由模型标签**（如 `G4 Neon` / `G4 Hydrogen` / `G4 Carbon`）、上下文用量与 `tok/s`；**点击任意运行中对话即可一键切换至该会话**（自动优选官方 `sidecar.ui` 通道或 `Ctrl+K` 快速跳转）。

3. **中 / 英双语实时无缝互切**
   - 首次运行自动识别系统语言（中文系统默认简体中文，英文系统默认 English）；
   - 可随时通过展开面板右上角 **`EN` / `中`** 按钮、胶囊右键菜单或侧边栏按钮一键实时切换，设置自动持久化同步。

4. **原生无感体验**
   - **左键单击**展开/收起详情面板（自动归还编辑器输入焦点，不打断打字）；
   - **左键按住拖拽**调整吸附坐标（自动持久化记忆）；
   - **右键菜单**支持展开/收起、语言切换、一键复位、强制刷新云端配额或隐藏胶囊；
   - 切出 Antigravity 窗口自动隐藏，随软件自启、随软件退出。

---

## 常见问题

### 提示「未检测到 agy CLI」或更新 Antigravity 后额度消失？

插件的云端剩余额度依赖官方 `agy` CLI（`%LOCALAPPDATA%\agy\bin\agy.exe`）。由于 Antigravity 桌面端升级安装程序在覆盖更新时会清理 `%LOCALAPPDATA%\agy` 目录，AGY Pulse 已内置双重自愈机制：
1. **跨版本镜像保护**：自动在插件受保护数据目录维护 `agy.exe` 镜像，Antigravity 客户端更新重启后会自动无感恢复，不再丢失额度；
2. **后台自动补装**：若首次安装时未开启代理导致缺失 `agy` CLI，只需**开启系统代理 / TUN 模式后点击悬浮详情面板右上角 `↻`**，后台即会自动拉取补装并立即同步官方额度。

---

## License

[MIT License](./LICENSE) — Copyright (c) 2026 Yuuki113
