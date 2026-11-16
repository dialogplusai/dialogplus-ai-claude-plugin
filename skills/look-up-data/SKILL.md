---
name: look-up-data
description: Use when someone asks to look something up in their DialogPlus AI data tables (branches, price lists, product codes, order statuses), asks what a table holds, or wants to know what a journey's Data table step will find for a customer.
---

# Look things up in DialogPlus AI data tables

Data tables are the workspace's own reference lists that chatbot journeys read: branches and their hours, price lists, order statuses. Claude can read them; rows are changed in the app.

1. Call `list_data_tables` to find the table. Match the person's words to a table's name, and ask which one they mean if two could fit. Note its searchable columns, its key column and which columns are sensitive.
2. Call `find_data_rows` with the table's name or slug:
   - `where` for exact values in searchable columns, such as `{"code": "QA1"}` or a branch's city. Use the column keys from `list_data_tables`, not their labels.
   - `search` for text that may appear in any searchable column.
   - Only searchable columns can be matched. If the person asks about another column, say so and offer a search on a searchable one.
3. Show what you found in a short table or list with the column labels. Keep to what was asked, and say how many rows matched if there are more than you show.

- **Sensitive values** (phone numbers, ID numbers and the like) come back masked, for example `•••• 0001`. Say they're hidden. Only people allowed to see sensitive values can reveal them in DialogPlus AI, and each reveal is recorded. Don't try to work them out.
- **Nothing found:** say so plainly and suggest a broader `search` or checking the spelling. Don't guess values.
- **Changes:** Claude can't add, edit or delete rows. Point to **Data tables** in DialogPlus AI, where rows can be edited or imported from a spreadsheet.
- **What a journey will find:** a journey's Data table step makes the same exact-match lookup. To check what a customer would get, run `find_data_rows` with the values that customer would give.
