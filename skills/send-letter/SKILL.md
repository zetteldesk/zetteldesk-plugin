---
name: send-letter
description: Write, print and post a physical paper letter by mail with Zetteldesk. Use when the user wants a real letter sent by post (Brief verschicken, Brief schicken, Einschreiben, registered mail, certified letter), for example a cancellation letter (Kündigung), an objection (Widerspruch), a formal notice, or a letter to a landlord, authority, insurer, employer or relative, in German or any other language. Letters are printed and posted in Germany and can be delivered to almost any country. Not for email.
---

# Send a physical letter with Zetteldesk

Zetteldesk prints and posts paper letters. Letters are printed and posted in Germany and can be delivered to almost any country; international delivery costs more. It does not send email. Tools: `compose_letter`, `validate_letter`, `get_quote`, `send_letter`, `get_letter`, `list_letters`, `cancel_letter`, `get_balance`, `create_upload_url`.

## Workflow

1. **Collect** the sender address, the recipient address and what the letter should say. If the user has a finished PDF, skip composing and use that PDF.
2. **Compose.** `compose_letter(sender, recipient, subject, body_markdown)` renders a DIN 5008 letter and returns an `upload_id` and a preview URL. Pass that `upload_id` to `validate_letter` and `send_letter`. `compose_letter` takes no PDF: for a PDF the user provides, pass `pdf_base64` or `pdf_url` to `validate_letter` and `send_letter`, or for a large file call `create_upload_url`, upload it and pass the returned `upload_id` to those tools.
3. **Validate.** `validate_letter` checks the PDF (give it the `upload_id`, `pdf_base64` or `pdf_url`) and returns the detected recipient and the price. Pass the same options (`color`, `duplex`, `registered`, `international`) that will be used for sending.
4. **Confirm.** Show the user the recipient, the page count, the options and the exact price, and wait for an explicit yes. Sending charges the prepaid balance and cannot be undone once the letter has been handed to the printer.
5. **Send.** `send_letter` with the same `upload_id` (or PDF input) and options. Use an `idempotency_key` when retrying so a letter is never sent twice.
6. **Report.** `get_letter` shows the status and the event timeline. `cancel_letter` only works within moments of sending, before the letter is handed to the printer; after that the letter is posted and cannot be recalled.

## Addresses

- **Domestic (Germany):** name, street and number, `12345 City`. No country line and no `D-` prefix.
- **International:** set `international=True` and write the country on the last address line, spelled out in full in German or English (for example `Italien` or `Italy`, not `IT`). Abbreviations such as `UK`, `US` or `D` are not recognised. The full list of recognised names is in [countries.md](countries.md).
- If validation reports an address problem, show the message to the user and fix the address; nothing has been charged.

## Money

- The price is shown by `validate_letter` and `get_quote` (gross EUR cents). International letters and registered mail (`registered=True`) cost more.
- Letters are paid from a prepaid balance. `get_balance` returns the balance and the top-up link. Top-ups happen on zetteldesk.com only; there is no tool that takes payment.

## Boundaries

- Only physical letters. For email or messaging this skill does not apply.
- The letter text is the user's; the skill only formats and posts it.
