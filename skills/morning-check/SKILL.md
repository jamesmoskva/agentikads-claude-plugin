---
name: morning-check
description: A report-only daily check across every Google Ads client through AgentikAds, flagging anything that needs a person today. Use when the user asks for a morning check, a daily check, "anything I need to know", "check all my accounts", or sets up a scheduled daily task.
---

# Morning check

Look at yesterday for every client, compare it with the last 30 days, and report only what needs attention. This skill never changes anything: it is safe to run as a scheduled task while nobody is watching.

## For each account in `list_ad_accounts` (skip any marked `switched_off`)

1. `get_daily_metrics` for 30 days. Yesterday is the last complete day; compare it with the 30-day daily average.
2. `get_campaign_daily_metrics` for 7 days to see which campaign moved.
3. `get_todays_spend` when something looks like it is still running away.

## Flag, most urgent first

- **Spend spike**: yesterday's spend more than twice the daily average.
- **Conversions stopped**: zero conversions yesterday on an account that normally converts daily, while clicks were normal. Usually tracking or the landing page.
- **Cost per conversion jumped**: more than 30% above the 30-day average, with enough conversions to mean it.
- **Campaign stopped serving**: an enabled campaign with zero impressions all day.
- **Budget-limited**: a converting campaign spending its whole budget early.

## Report

- One line per account that is fine ("Smith Plumbing: normal, £84 spent, 3 enquiries").
- A short section per account that needs attention: what happened, the numbers, and the likely cause, with the tool that would confirm it.
- Suggest fixes, but make none. If the user wants one made, they can ask, and the change goes through the usual confirmations.

Quiet days should produce a short report. Don't invent concerns to fill space.
