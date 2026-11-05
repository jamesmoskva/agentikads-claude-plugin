---
name: google-ads-audit
description: Audit or health-check a Google Ads account through AgentikAds. Use when the user asks for an audit, a health check, "what's wrong with this account", "where is the money going", or a review of a client before a meeting or a takeover.
---

# Google Ads audit

Turn the account's live data into a short, ranked plan the user can act on. Look first, explain with numbers, and change nothing until the user says which fixes to make.

## Steps

1. Find the account. Call `list_ad_accounts`. If the user named a client, match it; if there is only one account, use it without asking.
2. Run `get_account_health_checks` for that account. It runs nine checks on live data (conversion tracking, budget-capped campaigns, bidding strategy fit, ad strength and empty ad groups, extensions, quality scores, devices, hours that spend without converting, structure) plus volume: shrinking leads, budget left unspent, and keywords paused while they still converted. Findings come sorted critical first and then by the account's goal, not by spend saved. If `checks_incomplete` is not empty, say which data Google would not return. If `get_account_details` shows no goal set, ask the user what the account is for (more leads at a cost per lead, the cheapest lead, or a number of leads a month) and record it with `set_account_goal`.
3. Add context with `get_account_summary` (last 30 days) and `get_campaigns` so every finding sits next to the account's real spend and conversions.
4. For each critical or warning finding, pull the evidence that proves it before you present it. For example `get_conversion_actions` for a tracking finding, `get_search_terms` with `wasted_only` for waste, `get_keywords` for quality-score findings.

## Write it up

- If the account is shrinking ("Shrinking, not optimising"), lead with that: leads now against before, and what the eligible searches say about why. Do not propose cuts until it is understood.
- Otherwise lead with the one or two things that matter most for the account's goal, in its currency, with the evidence: "Search campaign 'Boilers' spent £412 in 30 days between 11pm and 6am with no conversions."
- Every proposed cut carries two numbers: what it saves a month and the leads a month it removes. A finding whose `fix` carries `hold` has too little evidence yet; say so rather than proposing it.
- Then the rest, grouped: fix now, worth doing, leave alone. Keep each line to what is wrong, the number, and the fix.
- Separate fixes Claude can make (negative keywords, an ad schedule, a bid or budget change) from fixes a person must make (a broken tracking tag, a landing page that is down). A day-parting finding carries a ready `fix` for `set_schedule`; quote it.
- End by asking which fixes to make. Make them one by one, confirm each result, and remind the user every change is in Operations and can be undone.

## Don't

- Don't make changes during the audit.
- Don't call a finding a problem without its number.
- Don't recommend raising spend on a campaign that converts nothing.
- Don't rank fixes by spend saved alone: a saving that costs leads is a smaller account, not a better one.
