---
name: find-wasted-spend
description: Find Google Ads search terms that spend money without converting and block the right ones with negative keywords, through AgentikAds. Use when the user asks about wasted spend, irrelevant searches, negative keywords, junk clicks, or "where is my budget leaking".
---

# Find wasted spend

Zero conversions does not always mean waste. Sort the terms first, then propose negatives only for the ones that will never buy.

## Steps

1. Pick the account with `list_ad_accounts`. For "all my clients", repeat per account and report each separately.
2. Call `get_search_terms` with `wasted_only` set and 30 days (90 for small accounts). Use `min_spend` to skip pennies.
3. Sort every term into one of four groups:
   - **Junk**: never buys. Manuals, PDFs, DIY, how-to questions, jobs, careers, salaries, courses, definitions, model or part numbers ("s320", "ae050"). Safe to block.
   - **Competitor**: another company's brand name. Ask the user whether they bid on competitors on purpose before blocking.
   - **Research**: price and comparison searches ("cost", "price", "how much", "best", "vs", "grant"). On high-value services these are early buyers. Hold and investigate, don't block by default.
   - **High intent**: "near me", "installer", "emergency", "quote", "hire", "company", "same day". Zero conversions here means the landing page or tracking is broken, not the term. Never block these; flag them as a problem to fix instead.
4. Check `get_negative_keywords` so you don't propose a negative that already exists.

## Propose

- A table per campaign: term, spend, clicks, group, and the proposed negative with its match type. Use PHRASE for a junk word that can appear in many searches ("jobs"), EXACT for one bad search, and BROAD rarely.
- The total monthly spend the negatives would save.
- High-intent terms in their own section, with what to check (the landing page, conversion tracking with `get_conversion_actions`).

## Apply, after the user agrees

- One or two terms: `add_negative_keyword`. Many on one campaign: `bulk_add_negative_keywords_tool`. The same list across many campaigns: a shared list with `create_negative_keyword_list_tool`, `add_keywords_to_negative_list_tool` and `link_negative_list_to_campaign_tool`.
- Report what was added and what Google read back. Every negative can be removed with `undo_change`.
