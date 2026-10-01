# Grok Android Skills

Skills for controlling real Android phones and emulators with AI agents.

## Skills

- **droidmind** – Primary execution layer. Full MCP + ADB control (UI, apps, files, shell, logs).
- **qwen3-vl-android-agent** – Vision-guided planner for arbitrary Android GUIs; uses Qwen3-VL for screenshots and DroidMind/ADB for actions.
- **android-phone-control** – General observe-first control loop + safety notes.
- **auto-mobile** – UI automation & test authoring MCP (Zillow origin).

## Recommended architecture

Use **DroidMind first** for deterministic UI hierarchy/selectors and device actions. Add
**Qwen3-VL Android Agent** only when the screen is visually ambiguous or accessibility
data is incomplete.

```text
goal -> observe UI -> selector available? -> DroidMind action -> verify
                  \
                   -> screenshot -> Qwen3-VL -> grounded action -> DroidMind -> verify
```

This hybrid approach is faster and more reliable than sending every screen through a
vision model.

## Requirements for real phone control

1. USB debugging ON
2. ADB in PATH
3. MCP client config pointing at the server (uvx / npx)
4. Optional local Qwen3-VL endpoint for vision-guided operation

See individual `SKILL.md` files for exact setup and operating guidance.
