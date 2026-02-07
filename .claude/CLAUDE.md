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
- **Jira Project Keys**: AI1099, RUN
- **Confluence Spaces**: "AI 1099", "Runtime"

## Accountability Loop

**At the start of EVERY session**, do the following before anything else:

1. Check if a daily plan exists for today at `context/daily/YYYY-MM-DD.md`
2. Check if a weekly plan exists at `context/weekly/YYYY-WNN.md`
3. If both exist: briefly summarize daily progress (items done/total), weekly capacity (hours committed/available), and the top priority. Ask if priorities have shifted.
4. If the daily plan is missing, suggest running the morning-triage agent.
5. If the weekly plan is missing, suggest running the weekly-plan agent.

This is non-negotiable. The daily plan keeps you focused. The weekly plan keeps you honest about capacity.

## Capacity Model

Assume the following unless the user provides different numbers:

```
Daily productive hours:  5-6h  (not 8 — meetings, Slack, context switching)
Weekly productive hours: 22-24h
Meeting overhead:        8-10h/week (adjust based on actual calendar)
Slack/comms overhead:    3h/week
Context switching:       2h/week
Interrupt buffer:        3h/week (non-negotiable — interrupts are guaranteed)
```

When assessing whether something fits in the schedule, always use the realistic capacity, never the theoretical 40h.

## Estimation Philosophy

**The user chronically underestimates task duration.** Every estimate must account for this:

1. Break tasks into subtasks including "hidden work" (PR review cycles, merge conflicts, Slack alignment, deploy verification)
2. Apply multipliers based on familiarity:
   - Familiar code + clear requirements: 1.5x gut estimate
   - Unfamiliar code OR unclear requirements: 2x
   - Unfamiliar code AND unclear requirements: 2.5x
3. Never give best-case as the timeline. Always communicate the realistic estimate.
4. Track actuals vs estimates in the weekly plan to calibrate over time.

When the user says "it should only take X hours" — that's the bias. Ask them to walk through the subtasks. The breakdown always reveals more work.

## Weekly Plan File Format

Weekly plans are stored at `context/weekly/YYYY-WNN.md` (e.g., `2026-W06.md`). See the weekly-plan agent for the full format. Key sections:
- Capacity calculation
- Committed work with estimates and actuals
- Stretch goals (not commitments)
- Estimation accuracy tracker
- Interrupts log

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

- Project **AI1099**: The main AI product Jira board. Tickets follow the pattern `AI1099-NNNN`.
- Project **RUN**: Runtime infrastructure. Tickets follow the pattern `RUN-NNN`.
- When reviewing tickets, always check for linked Confluence docs, linked tickets, and recent comments.

## Confluence Context

- Space **AI 1099**: Design docs, architecture RFCs, feature specs for the AI product.
- Space **Runtime**: Infrastructure docs, runbooks, deployment procedures.

## Quarterly Goals

Joshua is on two teams with goals tracked across Jira epics and Confluence:
- **AI1099 team**: Epics in AI1099 project + docs in "AI 1099" Confluence space
- **Runtime team**: Epics in RUN project + docs in "Runtime" Confluence space

Goals file: `context/goals/YYYY-QN.md` (e.g., `2026-Q1.md`)

**Mid-quarter goal additions are normal.** When new goals appear:
1. Run the quarterly-goals agent to assess capacity impact
2. Log the change in the scope change log
3. Communicate what gets displaced

Weekly plans should always reference quarterly goals. If a weekly plan has no hours mapped to an at-risk goal, flag it.

## Calendar Integration

Meeting data comes from Outlook Web via Chrome browser automation.
- Calendar file: `context/calendar/YYYY-WNN.md`
- Run the `calendar-sync` agent to refresh from Outlook
- Morning triage and weekly planning use this for real capacity numbers instead of guesses
- If the calendar file is stale (older than the current week), suggest re-syncing

## Estimation Calibration

The system learns over time. Estimation accuracy data lives in `context/calibration.md`.
- Tracks actual vs estimated hours per task
- Adjusts multipliers as data accumulates (low/medium/high confidence thresholds)
- Tracks a weekly pace factor to account for energy, focus, and mental load variations
- The estimate agent reads this file before every estimation

**Pace factor**: Some weeks are slower and that's fine. The system doesn't judge — it adjusts. A pace factor of 0.8 means "this week, things are taking 25% longer than normal" and estimates are adjusted accordingly.

## Tool Usage

This workspace leverages MCP integrations:
- **Atlassian**: For Jira and Confluence (read tickets, search, read docs)
- **Slack**: For channel reading, thread reading, and sending messages
- **Figma**: For design context when reviewing UI-related work
- **Chrome**: For reading Outlook Web calendar and other browser-based tasks

When using these tools, always prefer structured summaries over raw dumps. Extract what matters, flag what needs attention, and skip the noise.

## Daily Plan File Format

Daily plans are stored at `context/daily/YYYY-MM-DD.md` with this structure:

```markdown
# Daily Plan - YYYY-MM-DD

## Capacity Today
- Available hours: Xh (after meetings)
- Committed: Xh
- Remaining: Xh

## DMs and @Mentions
- [ ] @person — summary of what they need (DM / #channel mention) [est: Xh]

## Top Priorities
1. [ ] Priority item (WHY: reason, WHO is waiting) [est: Xh]
2. [ ] Priority item (WHY: reason, DEADLINE: date) [est: Xh]

## Carried Forward
- [ ] Item from yesterday (originally planned YYYY-MM-DD) [est: Xh]

## Slack Threads Needing Response
- #channel - thread summary (from @person)

## Meetings Today
- HH:MM - Meeting name (context: relevant ticket/doc)

## Interrupts
(Added as they happen — track what was not planned)
- [time] Interrupt from [who]: [what] [est: Xh, actual: Xh]

## Notes
(Added throughout the day)

## End of Day
- Completed: X/Y items
- Planned hours: Xh | Actual hours: Yh
- Unanswered DMs: any
- Interrupts absorbed: Xh
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
