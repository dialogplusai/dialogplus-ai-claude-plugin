---
name: inbox-catch-up
description: Use when someone asks what's waiting in their DialogPlus AI inbox, which WhatsApp customers need a reply, or wants a summary of recent conversations.
---

# Catch up on the DialogPlus AI inbox

1. Call `list_conversations` for open conversations. Use `assigned: "me"` when the person asks about their own, `"unassigned"` for ones nobody has picked up, or a `query` to find a customer.
2. Read the few that matter most with `get_conversation`: the longest waiting first, then the most recent.
3. For each, give one or two lines: who it is, what they want, how long they've waited, and the next step. Put the ones that need a reply soonest at the top.
4. Offer to act on them: reply, add a note for the team, assign, resolve or snooze. Follow the reply-to-customer skill for anything the customer will receive.

If a customer's last message is more than 24 hours old, WhatsApp allows only an approved template message in reply; mention it so the person knows a free-text reply won't go through.

Keep summaries short and include only what's needed. Don't copy whole conversations, phone numbers or other personal details into the summary unless the person asks for them.
