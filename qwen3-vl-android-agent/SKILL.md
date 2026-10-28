---
name: qwen3-vl-android-agent
description: Vision-guided Android control using Qwen3-VL for screen understanding and DroidMind/ADB for execution. Use when UI hierarchy alone is insufficient or when the task requires visual grounding across arbitrary apps.
version: "1.0"
---

# Qwen3-VL Android Agent

Adds a visual planning layer on top of the existing DroidMind/ADB execution stack.

## Why this improves the stack

DroidMind is excellent at executing deterministic Android actions, but ADB/UI hierarchy does not always expose enough semantic information for custom views, canvases, images, games, remote surfaces, or visually ambiguous controls. Qwen3-VL can inspect screenshots, reason about visible UI state, and propose the next action.

Use the hybrid loop:

1. **Observe structured state first** — UI hierarchy, focused package/activity, device size.
2. **Use vision only when needed** — take a screenshot when structured state is missing, ambiguous, or inconsistent.
3. **Plan one small action** — tap, swipe, type, key event, launch app, or wait.
4. **Execute through DroidMind/ADB.**
5. **Re-observe and verify** the expected state changed.
6. Stop when the user goal is satisfied or when repeated observations show no progress.

This keeps simple tasks fast while adding visual grounding for difficult interfaces.

## Recommended model

Primary local model:

- `Qwen/Qwen3-VL-4B-Instruct-GGUF`
- Quantization: `Q4_K_M` as the practical default for local inference.
- Serve with an OpenAI-compatible endpoint using llama.cpp / llama-server.

An action-tuned Qwen3-VL checkpoint can be substituted when it is demonstrably better on the target phone/apps.

Example server:

```bash
llama serve -hf Qwen/Qwen3-VL-4B-Instruct-GGUF:Q4_K_M \
  --host 127.0.0.1 --port 8080
```

## Agent contract

Give the model:

- user goal
- current screenshot
- display width and height
- current package/activity when available
- compact UI hierarchy when available
- previous action and verification result

Require exactly one next-step action in a machine-readable shape:

```json
{
  "action": "tap",
  "x": 742,
  "y": 1812,
  "reason": "The visible Continue button is centered here.",
  "expect": "The next setup screen appears."
}
```

Supported action vocabulary should stay deliberately small:

- `tap(x,y)`
- `swipe(x1,y1,x2,y2,duration_ms)`
- `text(value)`
- `key(name)`
- `launch(package)`
- `wait(ms)`
- `done(summary)`

Do not let the vision model emit unrestricted shell commands. Shell/device administration remains a separate DroidMind tool path.

## Coordinate handling

Always provide the screenshot's exact pixel dimensions. Coordinates returned by the model must be clamped to the active display bounds before execution.

Prefer selectors/resource IDs from the UI hierarchy when a reliable element exists. Use visual coordinates only as fallback or when the UI is not represented in accessibility data.

## Verification loop

After every state-changing action:

1. capture fresh structured UI state;
2. compare activity/package and important visible text;
3. capture a new screenshot when verification is uncertain;
4. retry with a different action only after a fresh observation.

Abort the loop after repeated no-progress states instead of repeatedly tapping the same location.

## DroidMind mapping

Map planner actions to DroidMind capabilities:

| Planner | DroidMind / ADB |
| --- | --- |
| tap | UI tap |
| swipe | UI swipe |
| text | text input |
| key | key event |
| launch | start app/activity |
| observe | screenshot + UI hierarchy |
| verify | screenshot/UI state comparison |

Keep file operations, package installation, logcat, reboot, and arbitrary shell operations outside the visual action planner.

## When to use vision

Use Qwen3-VL when:

- UI hierarchy is empty or incomplete;
- controls have no useful accessibility labels;
- the target is visually identifiable but structurally ambiguous;
- an app renders a canvas/web/game/remote-desktop surface;
- the user describes a target by appearance rather than label;
- structured and visual state disagree.

Skip vision for deterministic operations such as package launch, known resource-ID taps, file transfer, logcat, or direct settings commands.

## Failure recovery

If an action fails:

1. capture a fresh screenshot and UI hierarchy;
2. include the failed action in the next model request;
3. ask for a different next action;
4. stop after three materially identical no-progress states.

This prevents runaway tap loops.

## Example task

User:

> Open Settings, find Battery, open battery usage, and tell me which app used the most battery.

Flow:

1. DroidMind launches Settings.
2. Read UI hierarchy and tap Battery by selector if available.
3. If the OEM screen uses an unlabeled/custom control, send a screenshot to Qwen3-VL.
4. Qwen3-VL returns the next grounded tap.
5. DroidMind executes it.
6. Re-observe the resulting screen.
7. Extract the visible usage result and return it to the user.

## Architecture

```text
User goal
   |
   v
Agent/orchestrator
   |---------------------> structured UI / device state
   |                              |
   |                              v
   |                         DroidMind MCP
   |                              |
   |                              v
   |                         Android / ADB
   |
   +--> screenshot --> Qwen3-VL --> one grounded action
                                  |
                                  +--> DroidMind MCP --> Android
```

The key design rule is **structured-first, vision-when-needed, verify-after-action**. This adds visual autonomy without replacing the deterministic Android-control layer that already works.
