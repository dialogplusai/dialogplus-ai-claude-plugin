---
name: workspace-report
description: Use when someone asks how their DialogPlus AI workspace or WhatsApp messaging is doing, wants a daily or weekly summary, or asks about wallet balance and event usage.
---

# DialogPlus AI workspace report

1. Call `get_workspace_overview` for events used this month against the plan's allowance, messages in the last 24 hours, and the wallet balance (included only for people who can see billing).
2. Call `list_event_deliveries` for the latest messages, or the period asked about, and count them by status.
3. If anything failed, group the failures by reason as the message-delivery-check skill describes.

Write a short report:

- **Headline:** messages sent, delivered and read, and the share that failed.
- **Needs attention:** the main failure reasons with counts and the fix for each, events close to the monthly allowance, and a low wallet balance.
- **Next step:** one or two concrete actions.

Use the numbers the tools return, and don't estimate figures they don't give.
