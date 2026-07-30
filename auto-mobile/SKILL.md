---
name: auto-mobile
description: Mobile UI automation and test authoring for Android (MCP). Tap, swipe, observe hierarchy, launch apps, screenshots. Good for testing flows and development assistance.
version: "0.9"
source: https://github.com/zillow/auto-mobile (archived; community fork kaeawc/auto-mobile)
---
# AutoMobile

MCP server focused on Android UI automation and automated test authoring.

Install / run:
npx -y auto-mobile@latest   (or community fork)

Config example:
{
  "mcpServers": {
    "AutoMobile": {
      "command": "npx",
      "args": ["-y", "auto-mobile@latest"]
    }
  }
}

Capabilities: observe UI, intelligent tap by text/id, swipe, scroll, app lifecycle, screenshots, test generation.
