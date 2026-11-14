---
name: send-whatsapp-update
description: Use when someone wants to send a customer a WhatsApp message through DialogPlus AI, such as an order, delivery, payment, booking or appointment update, or asks which messages their workspace can send.
---

# Send a WhatsApp update through DialogPlus AI

DialogPlus AI sends WhatsApp messages through **events**. Each event, such as `order.shipped` or `invoice.issued`, is set up once in DialogPlus AI with an approved WhatsApp template and the data fields it needs. Messages go out only through events the workspace has set up, to one person at a time.

## Steps

1. **Find the event.** Call `list_events` and pick the event that matches what the person wants to send. If none fits, say so and explain that a workspace admin creates events on the Events page in DialogPlus AI. Don't substitute a different event.
2. **Gather what it needs.** The event lists its required data fields. Ask the person for any value you don't have. Don't invent values, guess phone numbers, or reuse another customer's details. Phone numbers include the country code, like `+919876543210`.
3. **Preview first.** Call `send_event` with `dry_run: true`. Show the person the exact message the customer will receive, the template, its category (utility or marketing) and the price.
4. **Send only after a clear yes.** When the person confirms this specific message, call `send_event` again with the same values and `dry_run: false`. Include a `reference`, such as the order or invoice number: if the call is repeated, DialogPlus AI won't send a second message with the same reference.
5. **Report back.** Share the delivery id and that the message is on its way. Offer to check delivery later with `get_event_delivery`.

## Good to know

- Each message is charged at WhatsApp's rate from the workspace's prepaid wallet and counts toward the workspace's monthly events. If the wallet is low, the preview says so.
- DialogPlus AI skips people who opted out and applies the workspace's consent rules. If a send is skipped, explain the reason it gives instead of retrying.
- Marketing templates need the customer's marketing consent. Utility templates are for updates the customer expects, such as orders, payments and appointments.
- To message many people at once, suggest a broadcast in DialogPlus AI instead of sending events one by one.
