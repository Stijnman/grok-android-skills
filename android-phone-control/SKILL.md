---
name: android-phone-control
description: General skill for controlling a real Android phone via ADB. Covers device discovery, screenshots, UI gestures (tap/swipe), text input, app management, shell. Safe observe-first loop. Use when the user wants AI to operate their physical Android phone.
version: "1.0"
---
# Android Phone Control Skill

For real-device control you need:
1. USB debugging enabled on the phone
2. ADB on the host
3. An MCP server or command-layer that exposes ADB (DroidMind, PhoneMcp, openclaw-adb-mcp, scrcpy-mcp, etc.)

Recommended primary: **DroidMind** (see sibling skill).

Basic flow the agent should follow:
1. adb devices (or equivalent tool) → confirm device is "device"
2. Capture screenshot or UI dump
3. Decide action (tap by text/coord, swipe, type, launch app)
4. Execute
5. Re-observe

Never run destructive shell (rm -rf, factory reset, etc.) without explicit confirmation.
