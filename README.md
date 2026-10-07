# Zetteldesk plugin for Claude, ChatGPT and Codex

Write and send real letters by post from your AI assistant. Zetteldesk checks the letter, shows you the exact price and recipient,
and after your confirmation prints, envelopes and posts it. Letters are printed and posted in Germany and can be delivered to almost
any country; international delivery costs more. It does not send email.

Typical uses: a cancellation letter (Kündigung), an objection (Widerspruch), a letter to a landlord, an authority, an insurer or an
employer, a registered letter (Einschreiben).

## Install

- **Claude Code:** `claude plugin marketplace add zetteldesk/zetteldesk-plugin`, then `claude plugin install zetteldesk@zetteldesk`.
- **Codex:** `codex plugin marketplace add zetteldesk/zetteldesk-plugin`, then `codex plugin add zetteldesk@zetteldesk`.
- **Claude.ai and ChatGPT:** add `https://mcp.zetteldesk.com/mail` as a custom connector or install Zetteldesk from the plugin directory.

You sign in with your Zetteldesk account (OAuth in the browser). Create one for free on [zetteldesk.com](https://zetteldesk.com).

## What this plugin connects to

- The Zetteldesk mail MCP server at `https://mcp.zetteldesk.com/mail` (Zetteldesk API, hosted in the EU, Frankfurt).
- Through it, our print and postal partner PIN AG (eBrief), which prints and posts the letters, and Stripe for balance top-ups,
  which happen on zetteldesk.com only and never through the plugin.

It contains one skill (`send-letter`) and the MCP server definition. It has no hooks, scripts or other network access.

## Privacy

Letter content and recipient addresses are sent to Zetteldesk only to print and post the letter you confirmed. PDFs are stored
encrypted and deleted after 90 days. Full details: [Privacy Policy](https://zetteldesk.com/en/privacy),
[Terms](https://zetteldesk.com/en/terms), [Docs](https://zetteldesk.com/en/docs). Support: support@zetteldesk.com.

## About this repository

This repository is generated from our private monorepo and overwritten on every release. Please do not open pull requests here;
contact support@zetteldesk.com instead.

License: MIT.
