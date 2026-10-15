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

- **Emergency stop**: the user turned it on to block anything that could raise spend. Say so. Cuts and pauses still work. Release it with `set_kill_switch` only when the user asks.
- **Change cap**: the user set a change cap (`set_daily_cap`) and this change would raise spend past it. Explain the numbers. Change it only if the user asks you to; never to get a refused change through. A change cap does not stop Google spending: when the user wants a real limit, that is `set_spend_guard`.
- **Free plan limit**: the message includes an upgrade link and the reset date. Pass both on. Looking at the account still works.
- **Account switched off**: `start_monitoring_account` switches it back on. Pausing still works while it is off. At the plan's client limit, `stop_monitoring_account` frees a slot by switching another client off.

## After

- Report what Google read back (the `persisted` values), not what was asked for. If a result says it was not applied, say so and give the reason.
- If a result carries `plan_notice`, mention it once.

## Undo

- `get_change_history` lists recent changes with `undoable` and `undone`. Pass the change's `id` to `undo_change`.
- Undo covers pausing and enabling (including `pause_all_campaigns`), negative keywords, bids, budgets, schedules, ad copy edits, linking and unlinking assets, and business names. It is free, even past the free plan's monthly limit, and putting something back that would raise spend still respects the account's limits.
- Confirm before undoing a change someone else in the team made.
