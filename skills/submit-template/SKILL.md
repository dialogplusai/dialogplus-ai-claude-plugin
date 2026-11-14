---
name: submit-template
description: Use when someone wants to write a new WhatsApp message template in DialogPlus AI and submit it to WhatsApp for approval.
---

# Write and submit a WhatsApp template

1. **Agree the purpose.** Utility templates are for updates a customer expects (orders, payments, appointments); anything promotional is marketing. WhatsApp re-categorises templates that don't fit, which changes the price.
2. **Write it** with the person: a name in lowercase with underscores (like `order_ready`), the language (like `en_US`), a body with `{{1}}`, `{{2}}`… for the values that change, and a realistic sample for each value. Optionally a short header, a footer, and up to 3 quick-reply or link buttons.
3. **Preview:** call `submit_template` (it previews by default). Share the category advice it returns and fix anything it flags.
4. **Submit only after a clear yes:** call `submit_template` again with `dry_run: false`. WhatsApp reviews it, usually within minutes to a day. Check its status later with `list_templates`.

Templates can't be edited from the chat once submitted. To change wording, submit a new one with a new name.
