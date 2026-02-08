# Command Center

An operational hub for senior/principal software engineers, powered by Claude Code. It helps you stay on top of daily priorities, track capacity, manage quarterly goals, and make informed decisions — all through conversational agents.

## Quick Start

1. **Clone the repo**
   ```bash
   git clone <repo-url> command-center
   cd command-center
   ```

2. **Copy the config template**
   ```bash
   cp config.example.yaml config.yaml
   ```

3. **Fill in your values** — open `config.yaml` and add your name, Slack channels, Jira projects, GitHub repos, etc. Every field is commented with explanations.

4. **Set up calibration** (optional)
   ```bash
   cp context/calibration.example.md context/calibration.md
   ```

5. **Open in Claude Code** — start a session and Claude will read your config automatically.

## What It Does

Command Center is a set of Claude Code agents and a structured workflow for managing your engineering work. It integrates with Slack, Jira, Confluence, and your calendar to:

- **Triage your morning** — scan DMs, channels, Jira tickets, and yesterday's plan to create a prioritized daily plan
- **Track capacity** — realistic weekly plans with estimation calibration that learns from your actuals
- **Manage quarterly goals** — track progress across teams, handle mid-quarter additions, and make tradeoffs visible
- **Prepare for meetings** — gather Jira, Confluence, and Slack context into a brief
- **Review PRs with context** — pull the Jira ticket, design doc, and Slack discussion before looking at code
- **Handle interrupts** — show the cost of taking on new work so you can make informed tradeoffs

## Agents

| Agent | What it does |
|-------|-------------|
| `morning-triage` | Scans DMs, channels, Jira, calendar; creates today's prioritized plan |
| `slack-catch-up` | Reads channels and DMs, surfaces what needs attention |
| `weekly-plan` | Creates/maintains weekly capacity plan, tracks actuals vs estimates |
| `quarterly-goals` | Tracks progress against quarterly objectives, handles mid-quarter changes |
| `daily-checkin` | Mid-day progress check against today's plan |
| `end-of-day` | Captures what happened, rolls forward incomplete items |
| `estimate` | Produces realistic time estimates with calibrated multipliers |
| `meeting-prep` | Gathers Jira/Confluence/Slack context for an upcoming meeting |
| `pr-context` | Gathers full context (ticket, design doc, discussion) for a PR review |
| `confluence-review` | Reads and critically summarizes a Confluence document |
| `jira-review` | Pulls a Jira ticket with linked items and presents an actionable summary |
| `interrupt` | Sizes an incoming interrupt and shows impact on current commitments |
| `delegate-or-own` | Helps decide whether to do a task yourself or hand it off |
| `calendar-sync` | Reads Outlook/Google calendar via browser automation |

## MCP Integrations

This workspace expects the following MCP servers configured in Claude Code:

- **Atlassian** — Jira and Confluence access
- **Slack** — Channel reading, search, and messaging
- **Figma** — Design context (optional)
- **Chrome** — Browser automation for calendar sync

## File Structure

```
command-center/
├── .claude/
│   ├── CLAUDE.md              # Main instructions (reads config.yaml at session start)
│   ├── agents/                # All agent definitions
│   └── settings.local.json    # MCP tool permissions
├── config.example.yaml        # Template — copy to config.yaml
├── config.yaml                # Your personal config (gitignored)
├── context/
│   ├── calibration.example.md # Template — copy to calibration.md
│   ├── calibration.md         # Estimation calibration data (gitignored)
│   ├── daily/                 # Daily plan files (gitignored)
│   ├── weekly/                # Weekly plan files (gitignored)
│   ├── goals/                 # Quarterly goal files (gitignored)
│   └── calendar/              # Calendar data files (gitignored)
└── README.md
```

## Daily Workflow

1. **Morning**: Run `morning-triage` — it scans everything and creates your daily plan
2. **Mid-day**: Run `daily-checkin` — quick progress check, reprioritize if needed
3. **As needed**: Run `estimate`, `meeting-prep`, `pr-context`, `interrupt`, or `delegate-or-own`
4. **End of day**: Run `end-of-day` — capture what happened, set up tomorrow
5. **Weekly**: Run `weekly-plan` on Monday, review on Friday (updates calibration data)
6. **Quarterly**: Run `quarterly-goals` to set up and track quarterly objectives
