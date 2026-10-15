# AgentikAds for Google Ads

Manage your clients' Google Ads in Claude. This plugin connects Claude to the AgentikAds connector and adds five skills that agencies use every day: an account health check, finding wasted spend, client reports, a daily check across every client, and making changes safely.

## Set up

1. Install the plugin. On claude.ai and in Cowork, open the plugin's **Connectors** tab and connect **AgentikAds**. In Claude Code the connector loads with the plugin; run `/mcp` to sign in.
2. Sign in with the Google login that has access to your Google Ads accounts, and tick the client accounts Claude should work on.
3. Ask away. For example: "Run a health check on Smith Plumbing", "Find wasted spend across all my clients", or "Write this week's report for every client".

Full guide with more examples: https://agentikads.com/docs/claude

## Skills

- **google-ads-audit**: runs nine checks on live data and turns the findings into a ranked plan with money figures.
- **find-wasted-spend**: finds search terms that spend without converting, separates junk from terms worth keeping, and adds negative keywords once you agree.
- **client-report**: writes a period-on-period report for one client or all of them, in plain English a client can read.
- **morning-check**: a report-only daily check across every client: spend spikes, conversion drops, campaigns that stopped serving. Makes no changes, so it suits a scheduled task.
- **safe-changes**: how Claude makes changes here: confirming anything that raises spend, respecting each account's emergency stop and any change cap the user sets, and undoing a change. Real spending limits are a spend guard (`set_spend_guard`), which alerts or pauses a client when spend reaches a daily or monthly limit.

## What data it sends

The skills are instructions for Claude and send nothing themselves. The connector sends your requests to AgentikAds at agentikads.com, which reads and changes your own Google Ads accounts through the Google Ads API on your behalf. AgentikAds stores account names and IDs, your limits and a log of the changes made through it. It never sees payment details, doesn't sell your data and doesn't use it to train AI models. Privacy policy: https://agentikads.com/privacy

## Plans

Free for 5 client accounts and 300 changes a month, no card; looking, pausing and undoing are always free. Paid plans are priced by client accounts with unlimited changes. See https://agentikads.com/#pricing

## Support

support@agentikads.com
