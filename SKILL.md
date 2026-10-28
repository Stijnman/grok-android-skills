# Grok Android Skills

**Description:** Android-control skills for AI agents that operate real devices and emulators through ADB, MCP, and optional vision-guided GUI reasoning.

**Purpose:** Use these skills when an agent needs to inspect or control Android UI, apps, files, shell commands, logs, or automated mobile test flows.

## Quick start

1. Enable USB debugging on the Android device or start an emulator.
2. Ensure ADB is available on the host.
3. Use **droidmind** as the default execution layer.
4. Add **qwen3-vl-android-agent** when selectors/accessibility data are incomplete or the task requires visual grounding.
5. Configure the corresponding MCP server/client as documented by that skill.
6. Re-observe and verify after every state-changing action.

## Included skills

- **droidmind** — recommended general-purpose MCP + ADB control for UI, apps, files, shell and logs.
- **qwen3-vl-android-agent** — hybrid visual planner: structured UI first, Qwen3-VL screenshots when needed, DroidMind/ADB execution, then verification.
- **android-phone-control** — observe-first Android control loop with explicit safety guidance.
- **auto-mobile** — mobile UI automation and test-authoring workflow.

## Reliability rules

- Prefer resource IDs/selectors and structured UI data over image coordinates.
- Invoke vision only when structured state is insufficient or ambiguous.
- Plan one small action at a time.
- Clamp visual coordinates to the active display bounds.
- Re-observe after each action and stop repeated no-progress loops.
- Keep unrestricted shell/device-administration commands outside the vision planner.

## Safety

Treat device actions as real user actions. Confirm destructive operations, purchases, account changes, credential entry, factory resets, app-data deletion, and other irreversible changes before execution. Do not embed device credentials or API secrets in repository files.

## Requirements

- Android device or emulator
- ADB
- An MCP-compatible client for MCP-based skills
- Optional Qwen3-VL-compatible local endpoint for visual grounding
- Skill-specific dependencies documented in each included skill

## License

MIT. See `LICENSE`.
