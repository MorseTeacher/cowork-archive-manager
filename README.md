# Cowork Archive Manager

A browser-based GUI tool for managing archived sessions in Claude Desktop (Cowork).

**[日本語版はこちら](#日本語)**

## Why?

Claude Desktop has an "Archived" section for viewing archived tasks, but a known bug prevents it from appearing ([#22931](https://github.com/anthropics/claude-code/issues/22931), [#24534](https://github.com/anthropics/claude-code/issues/24534)). Session deletion is also not yet implemented ([#25304](https://github.com/anthropics/claude-code/issues/25304)).

This tool provides a workaround — **restore** and **delete** archived sessions through a browser-based GUI until the bugs are fixed.

## Features

- View all sessions (Archived / Active / All)
- Restore sessions individually or in bulk (`isArchived` → `false`)
- Permanently delete sessions individually or in bulk
- Open the session folder in your file manager
- Auto-shutdown when the browser tab is closed
- Bilingual UI (Japanese / English, auto-detected from browser language)

## Requirements

- **macOS** / **Windows** / **Linux**
- Python 3.8+ (no external packages required)
- Claude Desktop installed

## Installation

### Option 1: Run directly with Python

```bash
git clone https://github.com/SugaCrypto/cowork-archive-manager.git
cd cowork-archive-manager
python3 cowork_archive_manager.py
```

### Option 2: Install as macOS app

```bash
git clone https://github.com/SugaCrypto/cowork-archive-manager.git
cd cowork-archive-manager
chmod +x install.sh
./install.sh
```

This creates `~/Applications/Cowork Archive Manager.app`. Double-click to launch.

> **Note:** Requires Xcode Command Line Tools. Run `xcode-select --install` if not installed.

## Usage

1. Launch the tool — a management UI opens automatically in your browser
2. Use the filter to select "Archived" to see archived sessions
3. Click "Restore" to restore a session, or "Delete" to permanently remove it
4. After restoring, **fully quit Claude Desktop (Cmd+Q on macOS) and relaunch** to apply changes

## Uninstall

### macOS app

```bash
rm -rf ~/Applications/Cowork\ Archive\ Manager.app
```

### Lock file

```bash
rm -f ~/.cowork_archive_manager.lock
```

## How It Works

- Uses only Python standard library (`http.server`)
- Runs a local server on `127.0.0.1:52849` (no external network access)
- Modifies the `isArchived` flag in session JSON files to restore sessions
- Auto-shuts down when the browser heartbeat stops

### Session File Locations

| OS | Path |
|---|---|
| macOS | `~/Library/Application Support/Claude/local-agent-mode-sessions/` |
| Windows | `%APPDATA%/Claude/local-agent-mode-sessions/` |
| Linux | `~/.config/Claude/local-agent-mode-sessions/` |

## License

MIT License - See [LICENSE](LICENSE) for details.

---

<a id="日本語"></a>

## 日本語

Claude Desktop (Cowork) のアーカイブ済みセッションを管理するブラウザベースのGUIツールです。

### なぜ必要？

Claude Desktop にはアーカイブしたタスクを表示する「Archived」セクションがありますが、既知のバグにより表示されない問題が報告されています（[#22931](https://github.com/anthropics/claude-code/issues/22931)、[#24534](https://github.com/anthropics/claude-code/issues/24534)）。また、セッションの削除機能も未実装です（[#25304](https://github.com/anthropics/claude-code/issues/25304)）。

このツールはバグが修正されるまでの回避策として、アーカイブ済みセッションの**復元**と**削除**をブラウザベースのGUIで行えるようにします。UIはブラウザの言語設定に応じて日本語/英語が自動で切り替わります。

### インストール

```bash
git clone https://github.com/SugaCrypto/cowork-archive-manager.git
cd cowork-archive-manager
python3 cowork_archive_manager.py
```

macOS アプリとして使う場合:

```bash
chmod +x install.sh
./install.sh
```

### 使い方

1. ツールを起動すると、ブラウザに管理画面が自動で開きます
2. フィルターで「アーカイブ済み」を選択すると、アーカイブされたセッションが一覧表示されます
3. 「復元」ボタンでセッションを復元、「削除」ボタンで完全削除できます
4. 復元後は **Claude Desktop を完全終了（Cmd+Q）→ 再起動** で反映されます
