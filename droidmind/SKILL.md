---
name: droidmind
description: Control Android devices (real phone or emulator) via ADB through MCP. List devices, tap/swipe/UI automation, install/start apps, files, shell, logs, screenshots. Use when user wants to control their Android phone with AI.
version: "1.0"
source: https://github.com/hyperb1iss/droidmind
---
# DroidMind – Android Phone Control

DroidMind is an MCP server that gives AI agents full control of Android devices over ADB.

## Prerequisites
- ADB installed and in PATH
- Android phone with USB debugging enabled (or emulator)
- Python 3.13+ and uv recommended

## Quick setup for MCP clients (Cursor / Claude Code etc.)
Add to mcp.json / MCP config:

```json
{
  "mcpServers": {
    "droidmind": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/hyperb1iss/droidmind", "droidmind", "--transport", "stdio"]
    }
  }
}
```

## What it can do
- List / connect / reboot devices
- Screenshots + UI automation (tap, swipe, text input, keys)
- App install / uninstall / start / stop / clear data
- File push/pull/browse
- Logcat, bugreports, shell commands (with safety)
- Device properties

## Example prompts once connected
"List my connected Android devices"
"Take a screenshot of the phone"
"Open Settings and tap on Battery"
"Install this APK and launch it"

Full docs: https://hyperb1iss.github.io/droidmind/
