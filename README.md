# DialogPlus AI for Claude

[DialogPlus AI](https://dialogplus.ai) is a WhatsApp Business platform. This plugin connects Claude to your DialogPlus AI workspace so you can run it from the chat: catch up on and reply to the inbox, manage contacts, run campaigns, submit templates, send updates through your events, pause anything that's sending, and check what reached your customers and why some messages failed. Anything a customer receives is shown with its price before it's sent.

## What's included

- **The DialogPlus AI connector** at `https://api.dialogplus.ai/mcp`, with these tools:
  - `get_workspace_overview`: events used this month, messages in the last 24 hours, wallet balance (if you can see billing)
  - `list_events`, `send_event`: your events, and sending a WhatsApp message through one (previewed first)
  - `get_event_delivery`, `list_event_deliveries`: whether messages were sent, delivered, read or failed, and why
  - `list_templates`: your WhatsApp templates and their wording
  - `search_contacts`, `get_contact`: find contacts and see their details
  - `list_conversations`, `get_conversation`: inbox conversations and their recent messages
  - `reply_to_conversation`, `send_template_in_conversation`: answer a customer (previewed first)
  - `add_conversation_note`, `assign_conversation`, `set_conversation_status`: notes for the team, assigning, resolving and snoozing
  - `create_contact`, `update_contact`, `tag_contacts`, `opt_out_contact`: add, edit and tag contacts, and stop marketing to someone who asked
  - `list_campaigns`, `get_campaign`, `create_campaign_draft`, `preview_campaign_send`, `send_campaign`, `set_campaign_status`, `cancel_campaign`: broadcast campaigns, from draft to results
  - `submit_template`: write a WhatsApp template and submit it for approval (previewed first)
  - `list_journeys`, `set_journey_status`: chatbot journeys, and pausing or resuming one
  - `list_event_triggers`, `set_event_status`, `set_trigger_status`, `retry_event_delivery`: pause events and their sources, and resend failed messages
- **Skills** that help Claude use them well: sending an update, replying to customers, running a campaign, managing contacts, submitting a template, stopping messages quickly, checking delivery and failures, catching up on the inbox, and a workspace report.
- **Commands** in Claude Code and Cowork: `/dialogplus-ai:status` and `/dialogplus-ai:failed-messages`.

## Before you start

- A DialogPlus AI account and a workspace with a WhatsApp number connected.
- To send messages: an event set up with an approved WhatsApp template, and wallet balance.

## Install in Claude Code

```
/plugin install dialogplus-ai --marketplace dialogplusai/dialogplus-ai-claude-plugin
```

On Claude Code before 2.1.275, add the marketplace first:

```
/plugin marketplace add dialogplusai/dialogplus-ai-claude-plugin
/plugin install dialogplus-ai@dialogplus-ai
```

Then run `/mcp` and sign in to **dialogplus-ai**.

## Connect

1. Install the plugin, open its **Connectors** tab and connect **DialogPlus AI**.
2. Sign in with your DialogPlus AI account, choose the workspace, check what Claude may do, and select **Allow**.
3. Ask things like “Which messages failed today, and why?”, “Did order A-1042's update reach the customer?” or “What's waiting in my inbox?”.

## What Claude can and can't do

- Claude acts as you, with the permissions you tick on the sign-in screen and never more than your DialogPlus AI role allows. Each area (inbox, contacts, campaigns, events, templates, journeys) has separate permissions for reading, changing and sending, so you can allow reading only.
- Anything a customer receives is previewed first: the exact message, who it goes to and the price. Claude asks before every send. A campaign needs a confirmation code from its preview, valid for 15 minutes, and is refused if the audience or cost grew since.
- Nothing deletes contacts, conversations, templates or journeys, and nothing opts a customer in to marketing: consent only comes from the customer.
- Each tool has its own rate limit, and bulk tagging is capped at 50 contacts at a time.
- Every tool Claude uses is recorded in your workspace's audit log.
- Take permissions away, or disconnect, any time in DialogPlus AI under **Settings → Security → Connected AI assistants**.

## Data and privacy

- This plugin is made of instructions (skills and commands) and the connector's address. It runs no code on your computer, and has no hooks, scripts or other services.
- Claude reaches your workspace only through the connector at `api.dialogplus.ai`, which returns the data each tool asks for, within your permissions.
- For each call, DialogPlus AI's audit log records which tool was used, by whom, when and whether it worked, plus ids and choices such as the conversation, campaign or event. Message and note text is kept only as its length, and phone numbers only as their last four digits. What Claude changes is also recorded the same way as the change would be if you made it in the app. DialogPlus AI doesn't see or keep your conversations with Claude.
- Privacy policy: <https://app.dialogplus.ai/#/legal/privacy> · Privacy questions: privacy@dialogplus.ai

## Support

- Documentation: <https://app.dialogplus.ai/#/docs/mcp>
- Email: support@dialogplus.ai

## License

MIT. See [LICENSE](LICENSE).
