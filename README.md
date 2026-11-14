# DialogPlus AI for Claude

[DialogPlus AI](https://dialogplus.ai) is a WhatsApp Business platform. This plugin connects Claude to your DialogPlus AI workspace so you can check whether messages reached your customers, find out why some failed, catch up on the inbox, look up contacts and templates, and send WhatsApp updates through your events, with each message and its price shown before anything is sent.

## What's included

- **The DialogPlus AI connector** at `https://api.dialogplus.ai/mcp`, with these tools:
  - `get_workspace_overview`: events used this month, messages in the last 24 hours, wallet balance (if you can see billing)
  - `list_events`, `send_event`: your events, and sending a WhatsApp message through one (previewed first)
  - `get_event_delivery`, `list_event_deliveries`: whether messages were sent, delivered, read or failed, and why
  - `list_templates`: your WhatsApp templates and their wording
  - `search_contacts`, `get_contact`: find contacts and see their details
  - `list_conversations`, `get_conversation`: inbox conversations and their recent messages
- **Skills** that help Claude use them well: sending an update safely, checking delivery and failures, catching up on the inbox, and a workspace report.
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

- Claude acts as you, with the permissions you approved on the sign-in screen and never more than your DialogPlus AI role allows.
- Only `send_event` changes anything. Claude shows the exact message and its price first, and asks before every send. Each message is charged at WhatsApp's rate from your workspace wallet.
- Contacts, conversations and templates are read, never edited or deleted. The connector can't send inbox replies or broadcasts.
- Every tool Claude uses is recorded in your workspace's audit log.
- Disconnect any time in DialogPlus AI under **Settings → Security → Connected AI assistants**.

## Data and privacy

- This plugin is made of instructions (skills and commands) and the connector's address. It runs no code on your computer, and has no hooks, scripts or other services.
- Claude reaches your workspace only through the connector at `api.dialogplus.ai`, which returns the data each tool asks for, within your permissions.
- For each call, DialogPlus AI's audit log records which tool was used, by whom, when and whether it worked; for a send, also the event, the last four digits of the number and your reference. DialogPlus AI doesn't see or keep your conversations with Claude.
- Privacy policy: <https://app.dialogplus.ai/#/legal/privacy> · Privacy questions: privacy@dialogplus.ai

## Support

- Documentation: <https://app.dialogplus.ai/#/docs/mcp>
- Email: support@dialogplus.ai

## License

MIT. See [LICENSE](LICENSE).
