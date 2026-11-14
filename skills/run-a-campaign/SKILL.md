---
name: run-a-campaign
description: Use when someone wants to send a WhatsApp broadcast or campaign to many customers with DialogPlus AI, check how a campaign did, or pause, resume or cancel one.
---

# Run a WhatsApp campaign

A campaign sends one approved template to an audience. It reaches many people and costs real money, so it always goes draft → preview → confirm → send.

## Steps

1. **Pick the template.** Call `list_templates` and choose an approved one. Marketing templates reach only people who can receive marketing; utility templates are for updates customers expect.
2. **Draft it.** Call `create_campaign_draft` with a name, the template and language, any `{{1}}`-style values, and the audience: `all`, `active`, `inactive`, or `segment:<id>` for a saved segment. A draft sends nothing.
3. **Preview.** Call `preview_campaign_send`. Tell the person, in plain words: how many people it reaches, how many are left out and why, the estimated cost, and any warnings or blocking problems. Don't hide warnings.
4. **Send only after a clear yes** to those numbers. Call `send_campaign` with the `confirm_code` from the preview. The code works for 15 minutes, only for this person and campaign, and is refused if the audience or cost grew since the preview. Then preview again and show the new numbers.
5. **Report back** with `get_campaign`: sent, delivered, read, failed and left out.

## Changing a campaign

- `set_campaign_status` pauses a scheduled or sending campaign, or resumes a paused one.
- `cancel_campaign` stops it for good. Confirm before cancelling: it can't be undone.
- `list_campaigns` shows recent campaigns and their status.

## Good to know

- Opted-out people are always left out. People without a recorded opt-in may be warned about rather than left out, depending on the workspace's settings: mention the count the preview gives.
- Messages are charged at WhatsApp's rate from the workspace's prepaid wallet.
- Scheduling isn't available from the chat; schedule in DialogPlus AI.
