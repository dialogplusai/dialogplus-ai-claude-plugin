---
name: manage-contacts
description: Use when someone wants to add or edit a contact in DialogPlus AI, tag or untag contacts, or stop marketing messages to someone who asked to stop.
---

# Manage contacts

- **Find first.** Use `search_contacts` or `get_contact` (by id or phone number with the country code) before adding someone, so you don't create a duplicate.
- **Add:** `create_contact` with a phone number (with country code, like `+919876543210`) and/or an email, and a name if known.
- **Edit:** `update_contact` changes the name, email, language, lifecycle stage or custom attributes. Say which fields you changed.
- **Tag:** `tag_contacts` adds a tag to, or removes it from, up to 50 contacts at once. A new tag name is created. For more, do it in batches and say how many were done.
- **Stop marketing:** `opt_out_contact` when a customer asked to stop. Confirm with the person first: it can't be undone from the chat, and only the customer can opt back in (for example by messaging START).

## Consent

Nothing in the chat can opt a person in to marketing. Consent only comes from the customer. If someone asks to mark contacts as opted in, explain that and point them to a sign-up form or the customer's own reply.

Don't add people the person can't vouch for, and don't copy personal details into the chat beyond what the task needs.
