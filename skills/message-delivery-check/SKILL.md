---
name: message-delivery-check
description: Use when someone asks whether a WhatsApp message from DialogPlus AI reached a customer, why messages failed or were skipped, or how today's event messages are doing.
---

# Check WhatsApp message delivery

## One message

Call `get_event_delivery` with the delivery id, or with the event key and the reference used when sending (such as the order number). Report the status in plain words:

| Status | Meaning |
|---|---|
| queued, sending, retrying | DialogPlus AI is still sending it |
| sent | WhatsApp accepted it; it hasn't reached the phone yet |
| delivered | It reached the customer's phone |
| read | The customer opened it (shown only when they share read receipts) |
| failed | It couldn't be delivered; the delivery says why |
| skipped | It wasn't sent on purpose, for example because the person opted out |

## Several messages

Call `list_event_deliveries` filtered by `status: "failed"` (or `"skipped"`), and by the event if the person named one. Group the results by reason, count them, and lead with the most common.

## Common reasons and what to do

- **Not on WhatsApp or can't receive messages** (WhatsApp error 131026): check the number, or reach the customer another way.
- **More than 24 hours since the customer last wrote** (131047): only an approved template can be sent outside that window; make sure the event uses one.
- **WhatsApp limited marketing messages to this person** (131049): WhatsApp caps how many marketing messages each person receives. Try again later, and use utility templates for transactional updates.
- **The person stopped marketing messages** (131050): don't send them marketing again.
- **Template problems** (132000 wrong number of values, 132001 template missing in that language, 132015 paused, 132016 disabled): look the template up with `list_templates` and fix it in DialogPlus AI.
- **Too many messages to one number** (131056): wait before sending to that number again.
- **Skipped for wallet balance or consent:** top up the wallet, or check the customer's consent in DialogPlus AI.

Don't guess a cause the delivery doesn't state. If the reason is unclear, say so and suggest the Activity tab on the Events page in DialogPlus AI.
