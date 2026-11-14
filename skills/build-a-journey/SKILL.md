---
name: build-a-journey
description: Use when someone wants to build, change or publish a WhatsApp chatbot journey (an automated conversation or flow) in DialogPlus AI, for example "make a bot that answers order questions", "add a menu to our welcome journey" or "put the new bot live".
---

# Build a chatbot journey

A journey is an automated WhatsApp conversation: something starts it (a keyword, or any message no other journey picks up), then it sends messages, asks questions, branches on answers and can hand the chat to the team. You design it here; DialogPlus AI saves it as a draft that reaches no one until it's published.

## Build a new one

1. **Understand the bot.** Ask only what you need: what starts it (the words customers send), what it should ask or tell them, where each answer leads, when a person should take over, and which WhatsApp number it's for if the workspace has several.
2. **Read the guide.** Call `get_journey_guide`. It lists the step types this workspace can use with their exact payloads, the rules, an example, the numbers and the starter templates. If a starter template fits, offer it: `create_journey` with `template` builds it, and you can adjust it after.
3. **Agree the outline.** Describe the steps in plain words (not JSON): the trigger, each message and question, each button or menu option and where it goes, and how it ends. Change it until the person is happy.
4. **Create it.** Call `create_journey` with a name and the `nodes` you designed, shaped exactly as the guide shows. Pass `number` when the workspace has more than one.
5. **Fix what it reports.** If `ready_to_publish` is false, fix every blocking issue with `edit_journey` (`changes` in order: `add_node`, `update_node`, `delete_node`, `set_next`, `rename`), then check again. Mention warnings in plain words.
6. **Share the link.** Give the person `open_in_builder` so they can see it on the canvas and try it in the builder's test mode.

## Publish it

Only when the person asks to put it live:

1. Call `preview_journey_publish`. Tell the person, plainly: the number it will answer on, what starts it, the templates it sends (each is charged), who it hands chats to, what it replaces, and any warnings or blocking problems.
2. If it **answers every message** (no keyword), say so clearly: it will reply to anything no other journey picks up on that number.
3. After a clear yes, call `publish_journey` with the `confirm_code` from the preview. The code works for 15 minutes, only for this person and this exact draft. If the journey changed since, preview again and show the new result.

## Change an existing one

1. `list_journeys`, then `get_journey` to read its steps and what starts it.
2. Agree the change, then `edit_journey`. Only the draft changes: a live journey keeps answering customers with its published version until it's published again.
3. To make the change live, publish it as above. `set_journey_status` pauses a live journey, or resumes a paused one exactly as it was.

## Good to know

- WhatsApp's limits: up to 3 reply buttons of 20 characters, up to 10 menu rows (titles 24 characters, descriptions 72), messages up to 4,096 characters.
- Keywords: `equals` matches the whole message. Avoid `contains` with short words (“hi” is inside “this”); use a regex for greetings, as the guide shows.
- Keep `waitForUser` false on messages, unless the customer must write something before the next step.
- API call, Code and Payment steps are added in the builder only. You can route around them, not add, change or remove them, and their settings aren't shown to you.
- Don't put customers' personal details into journey texts; use saved answers like `{{contact_name}}` instead.
