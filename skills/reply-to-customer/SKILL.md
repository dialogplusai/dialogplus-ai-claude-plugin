---
name: reply-to-customer
description: Use when someone wants to answer a WhatsApp customer in their DialogPlus AI inbox, send a template in a conversation, or tidy conversations by adding a note, assigning, resolving or snoozing them.
---

# Reply to a customer and tidy the inbox

## Replying (the customer receives it)

1. Find the conversation with `list_conversations` (use `query` for a name or number) and read it with `get_conversation`, so the reply fits what the customer asked.
2. Draft the reply with the person. Don't promise refunds, prices, dates or anything else the person hasn't confirmed.
3. Preview: call `reply_to_conversation` with the text (it previews by default). Show who it goes to and the exact text.
   - If the preview says more than 24 hours have passed since the customer last wrote, WhatsApp allows only an approved template. Offer `send_template_in_conversation` instead.
   - If the conversation is resolved, reopen it first with `set_conversation_status`.
4. Send only after a clear yes to this exact message: call `reply_to_conversation` again with `dry_run: false`.

For a template: call `send_template_in_conversation` with the template name, language and its `{{1}}`, `{{2}}`… values in order. The preview shows the filled-in message and the price; send with `dry_run: false` after the person confirms. Sending the same template with the same values twice within the hour sends it once.

## Tidying (only the team sees it)

- `add_conversation_note`: a note for the team. The customer never sees notes.
- `assign_conversation`: to `me`, a teammate's email, or `nobody`.
- `set_conversation_status`: `resolve`, `reopen`, or `snooze` with an `until` time (ISO 8601, within 90 days).

These don't message the customer, so they need no preview, but say what you changed.

## Good to know

- Claude acts as the person, within the permissions they approved and their DialogPlus AI role. If a tool says a permission is missing, tell them it can be added by connecting DialogPlus AI again.
- Everything is recorded in the workspace's audit log.
