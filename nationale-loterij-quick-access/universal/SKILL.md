---
name: nationale-loterij-quick-access-universal
description: Accessible Android navigation using authorized ADB.
---

# Nationale Loterij Quick Access

Purpose: Accessible, voice-first control of the user's Samsung Galaxy A54 through an authorized Linux Mint host and wireless ADB.

## Workflow
1. Check `adb devices -l` and reconnect only with user authorization.
2. Launch `be.loterienationaleloterij` using `adb shell monkey -p be.loterienationaleloterij -c android.intent.category.LAUNCHER 1`.
3. Inspect each screen with `adb shell uiautomator dump /sdcard/window.xml` and `adb exec-out cat /sdcard/window.xml`. Locate UI targets by labels and fresh bounds; use `adb shell input tap X Y`, then verify the result.
4. When requested, prefer normal email/password login and user-approved saved-password autofill. Never read, export, store or log secrets. User must personally complete PIN, biometrics, itsme, security warnings and identity checks.
5. Navigate results, ticket scanner, Club, and retailers. Obtain explicit approval before any purchase, deposit, wager or financial action.
6. Retry a harmless read once on transient errors. If disconnected or screen differs, stop and report rather than blindly tapping.
7. Keep voice responses short and accessible; never claim success without verification.

Official site: https://www.nationale-loterij.be/

## Platform instructions
For any LLM with authorized run_command and optional view_image tools. Without tools, guide rather than pretend to operate the phone. Validate all tool inputs.
