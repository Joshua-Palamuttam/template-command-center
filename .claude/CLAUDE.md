# Command Center

## What This Is

This is the operational hub for a principal software engineer at SeekOut. It is NOT a code repository. It is where you come to think, plan, gather context, and stay accountable.

Every session in this workspace should start by checking for today's daily plan.

## Role Context

- **Name**: Joshua Palamuttam
- **Role**: Principal Software Engineer
- **Organization**: SeekOut (Zipstorm on GitHub)
- **Slack Display Name**: `@Joshua Palamuttam` — use this when searching for DMs and @mentions
- **Core Repositories**: AI-1099, agents, backend, backend-e2e, recruit-api, integrations, integrations-databricks, analytics-api, analytics-functions, ui-1099, spot-messaging
- **Jira Project Keys**: AI-1099, RUN
- **Confluence Spaces**: "AI 1099", "Runtime"

## Accountability Loop

**At the start of EVERY session**, do the following before anything else:

1. Check if a daily plan exists for today at `context/daily/YYYY-MM-DD.md`
2. If it exists, read it and briefly summarize: how many items are planned, how many are done, and what the top priority is. Ask if priorities have shifted.
3. If it doesn't exist, suggest running the morning-triage agent to create one.

This is non-negotiable. The daily plan is the backbone of staying focused.

## Slack Channel Map

These are the channels to monitor, organized by category:

**Product** (what's happening with the product):
- `spot-product-issues` - Product bugs and customer-facing issues
- `spot-product-updates` - Product announcements and changes
- `product-issues` - Broader product issues
- `product-updates` - Broader product updates

**Engineering** (what the team is building):
- `spot-backend-devs` - Backend engineering discussion
- `spot-pr-reviews` - PR review requests and discussions

**Runtime** (infrastructure and operations):
- `internal-runtime-team` - Runtime team internal comms
- `runtime-deployment` - Deployment status and coordination
- `runtime-daily-alerts` - Daily operational alerts

**General**:
- `general` - Company-wide
- `spot-alerts` - System alerts

## Jira Context

- Project **AI-1099**: The main AI product Jira board. Tickets follow the pattern `AI-NNNN`.
- Project **RUN**: Runtime infrastructure. Tickets follow the pattern `RUN-NNN`.
- When reviewing tickets, always check for linked Confluence docs, linked tickets, and recent comments.

## Confluence Context

- Space **AI 1099**: Design docs, architecture RFCs, feature specs for the AI product.
- Space **Runtime**: Infrastructure docs, runbooks, deployment procedures.

## Tool Usage

This workspace leverages MCP integrations:
- **Atlassian**: For Jira and Confluence (read tickets, search, read docs)
- **Slack**: For channel reading, thread reading, and sending messages
- **Figma**: For design context when reviewing UI-related work

When using these tools, always prefer structured summaries over raw dumps. Extract what matters, flag what needs attention, and skip the noise.

## Daily Plan File Format

Daily plans are stored at `context/daily/YYYY-MM-DD.md` with this structure:

```markdown
# Daily Plan - YYYY-MM-DD

## DMs and @Mentions
- [ ] @person — summary of what they need (DM / #channel mention)

## Top Priorities
1. [ ] Priority item (WHY: reason this matters, WHO is waiting)
2. [ ] Priority item (WHY: reason, DEADLINE: if applicable)

## Carried Forward
- [ ] Item from yesterday (originally planned YYYY-MM-DD)

## Slack Threads Needing Response
- #channel - thread summary (from @person)

## Meetings Today
- HH:MM - Meeting name (context: relevant ticket/doc)

## Notes
(Added throughout the day)

## End of Day
- Completed: X/Y items
- Unanswered DMs: any
- Rolled forward: list
- Blockers: any
```

## Code Review Workflow

When reviewing PRs, the full context flow is:
1. Use `pr-context` agent to gather Jira ticket + design doc + Slack discussion
2. Switch to the worktree environment: `wt-review <PR#>` in the relevant repo
3. After review, come back here to update daily plan / respond on Slack if needed

## Writing Style

Be direct. No fluff. Bullet points over paragraphs. When summarizing docs or tickets, lead with the decision or action needed, then provide supporting context.
