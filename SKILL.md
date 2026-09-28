# Grok Android Skills

**Description:** Android-control skills for AI agents that operate real devices and emulators through ADB and MCP tooling.

**Purpose:** Use these skills when an agent needs to inspect or control Android UI, apps, files, shell commands, logs, or automated mobile test flows.

## Quick start

1. Enable USB debugging on the Android device or start an emulator.
2. Ensure ADB is available on the host.
3. Choose the skill that matches the task.
4. Configure the corresponding MCP server/client as documented by that skill.
5. Start with observation/read-only operations before actions that modify device state.

## Included skills

- **droidmind** — recommended general-purpose MCP + ADB control for UI, apps, files, shell and logs.
- **android-phone-control** — observe-first Android control loop with explicit safety guidance.
- **auto-mobile** — mobile UI automation and test-authoring workflow.

## Safety

Treat device actions as real user actions. Confirm destructive operations, purchases, account changes, credential entry, factory resets, app-data deletion, and other irreversible changes before execution. Do not embed device credentials or API secrets in repository files.

## Requirements

- Android device or emulator
- ADB
- An MCP-compatible client for MCP-based skills
- Skill-specific dependencies documented in each included skill

## License

MIT. See `LICENSE`.
