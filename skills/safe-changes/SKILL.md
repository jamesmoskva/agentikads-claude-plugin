---
name: safe-changes
description: How to make changes to Google Ads accounts through AgentikAds safely, including budgets, bids, pausing and enabling, and undoing a change. Use whenever the user asks Claude to change, raise, lower, pause, enable, add, remove or undo something in Google Ads.
---

# Making changes safely

Every change made through AgentikAds is logged in the workspace's Operations history with who made it, checked against the account's limits, read back from Google, and most can be undone. Work with that, not around it.

## Before

- Name the account and the campaign you are about to change, and the exact new value.
- Anything that can raise spend (a budget or bid increase, enabling a campaign, removing a negative keyword) needs the user's clear yes first. Say the before and after: "Raise 'Boilers' from £20 to £35 a day?"
- For a budget or bid, check the current value first (`get_budget_snapshot`, `get_keywords`) so the change is relative to what is really there.

## When a change is refused

- **Daily cap or emergency stop**: the account's limits blocked it. Explain the limit and that the user can change it in AgentikAds Settings. Don't look for a way around it.
- **Free plan limit**: the message includes an upgrade link and the reset date. Pass both on. Looking at the account still works.
- **Account switched off**: it can be switched back on in Settings, or with `start_monitoring_account`.

## After

- Report what Google read back (the `persisted` values), not what was asked for. If a result says it was not applied, say so and give the reason.
- If a result carries `plan_notice`, mention it once.

## Undo

- `get_change_history` lists recent changes with `undoable` and `undone`. Pass the change's `id` to `undo_change`.
- Undo covers pausing and enabling, negative keywords, bids, budgets, schedules and ad copy edits. It is free, even past the free plan's monthly limit, and putting something back that would raise spend still respects the account's limits.
- Confirm before undoing a change someone else in the team made.
