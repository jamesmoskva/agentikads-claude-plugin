---
name: find-wasted-spend
description: Find Google Ads search terms that spend money without converting and block the right ones with negative keywords, through AgentikAds. Use when the user asks about wasted spend, irrelevant searches, negative keywords, junk clicks, or "where is my budget leaking".
---

# Find wasted spend

Zero conversions does not always mean waste. Sort the terms first, then propose negatives only for the ones that will never buy.

Every cut also costs reach. One account lost almost half its leads to hundreds of small negatives and a paused keyword, each of which looked like a saving on its own. So judge cuts on volume as well as spend.

## Steps

1. Pick the account with `list_ad_accounts`. For "all my clients", repeat per account and report each separately.
2. Call `get_volume_trend`. If it raises "Shrinking, not optimising", say so first: cutting more is not the fix. Look at `get_change_impact` and `get_paused_converters` before anything else.
3. Call `get_search_terms` with `wasted_only` set and 30 days (90 for small accounts). Its `search_terms` are the terms with enough evidence; `watch` are too small to act on yet unless they are clearly for something the business does not sell; `converted_before` converted in the last 90 days and are never negatives.
4. Sort every candidate into one of four groups:
   - **Junk**: never buys. Manuals, PDFs, DIY, how-to questions, jobs, careers, salaries, courses, definitions, model or part numbers ("s320", "ae050"). Safe to block.
   - **Competitor**: another company's brand name. Ask the user whether they bid on competitors on purpose before blocking.
   - **Research**: price and comparison searches ("cost", "price", "how much", "best", "vs", "grant"). On high-value services these are early buyers. Hold and investigate, don't block by default.
   - **High intent**: "near me", "installer", "emergency", "quote", "hire", "company", "same day". Zero conversions here means the landing page or tracking is broken, not the term. Never block these; flag them as a problem to fix instead.
5. Check `get_negative_keywords` so you don't propose a negative that already exists.

## Propose

- A table per campaign: term, spend, clicks, group, and the proposed negative with its match type. Use PHRASE for a junk word that can appear in many searches ("jobs"), EXACT for one bad search, and BROAD rarely.
- The total monthly spend the negatives would save, and the leads at risk. Many negatives together can shrink an account that none of them would on its own.
- High-intent terms in their own section, with what to check (the landing page, conversion tracking with `get_conversion_actions`).

## Apply, after the user agrees

- One or two terms: `add_negative_keyword`. Many on one campaign: `bulk_add_negative_keywords_tool`. The same list across many campaigns: a shared list with `create_negative_keyword_list_tool`, `add_keywords_to_negative_list_tool` and `link_negative_list_to_campaign_tool`.
- Each of these checks the cut first and returns `volume`: what it saves and how many leads a month it removes. A negative that would block searches that bring cheap leads is refused until the user agrees; then pass `confirm_volume_loss`. Never pass it without asking.
- Report what was added, what Google read back, and the `volume` figures. Every negative can be removed with `undo_change`.
