---
name: stop-sending
description: Use when someone wants to stop or pause WhatsApp messages in DialogPlus AI right away, for example wrong messages are going out, a store or system is sending bad data, or a chatbot journey is misbehaving; also to turn them back on.
---

# Stop messages quickly

Find what is sending, pause it, and confirm it stopped. Pausing is safe and can be undone.

1. **Find the source.** Ask what customers received, or check `list_event_deliveries` for recent messages and the event behind them.
2. **Pause the right thing:**
   - An event (messages from a system, store or sheet): `set_event_status` with the event's key and `paused`. Messages sent to it are refused until it's back on.
   - One source behind an event (a store, sheet, database or webhook): `list_event_triggers`, then `set_trigger_status` with `paused`.
   - A campaign: `list_campaigns`, then `set_campaign_status` with `pause`.
   - A chatbot journey: `list_journeys`, then `set_journey_status` with `pause`. Customers stop getting that journey.
3. **Check it stopped:** `list_event_deliveries` again, or `get_campaign`.
4. **Turn it back on** only when the person says the problem is fixed: the same tool with `active` or `resume`. Resuming a journey publishes it again after its checks.

Failed messages can be sent again with `retry_event_delivery` (it previews first, and each retry is charged like a new message).
