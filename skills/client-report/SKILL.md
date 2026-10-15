---
name: client-report
description: Write a Google Ads performance report for a client (weekly or monthly, this period against the last) through AgentikAds. Use when the user asks for a client report, a weekly or monthly update, a performance summary, or "how did my clients do".
---

# Client report

A report a client can read in two minutes: what happened, why, and what is next. Plain English, real numbers, no jargon.

## A report to send the client

When the user wants something to send or forward (an email, a PDF, a monthly update), use `create_client_report`: it writes the owner-friendly report from Google's own figures, with the agency's name and logo, and returns the text, a preview link and a PDF. Show the user the text or the preview link. Send it with `send_client_report` only when they say to, to the addresses they give; nothing is sent automatically. `get_client_reports` lists past ones.

For a quick summary in the chat instead, gather and write it as below.

## Gather

1. Pick the account or accounts with `list_ad_accounts`. For "all my clients", do each one in turn and finish with a one-line roundup per client.
2. This period and the last one of the same length. `get_account_summary` with `days` covers one window; for an exact comparison use `run_gaql_query` with two named queries on `customer` or `campaign` metrics for each date range (cost, clicks, impressions, conversions, conversions value).
3. `get_campaigns` for the campaign split and `get_conversions_by_action` to say what the conversions were (calls, forms, purchases).
4. `get_change_history` for the changes made this period, so the report can say what was done and why.

## Write

Use this structure:

- **Headline**: one sentence on the result. "26 enquiries this week, up from 19, at £31 each."
- **The numbers**: spend, conversions, cost per conversion (or return on ad spend for online sales), clicks, with the change against last period. A small table is fine.
- **What drove it**: the two or three campaigns or searches behind the change.
- **What we did**: the changes from the history, in plain words.
- **Next**: one to three actions for the coming period.

Use the account's currency. Say "enquiries" or "sales", not "conversions", when you know which. Don't blame or praise the algorithm; say what the data shows. If tracking looks broken (clicks but zero conversions on a normally converting account), say so first, because every other number depends on it.
