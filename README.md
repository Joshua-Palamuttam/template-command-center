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

## Private Instance Setup

If you want to version-control your personal files (config, daily plans, goals, calibration), you can use a private repo as your daily driver with this public repo as an upstream template.

1. **Create a private repo**
   ```bash
   gh repo create <your-user>/command-center-private --private
   ```

2. **Clone the public template and re-point remotes**
   ```bash
   git clone https://github.com/Joshua-Palamuttam/command-center.git command-center
   cd command-center
   git remote rename origin template
   git remote add origin https://github.com/<your-user>/command-center-private.git
   ```

3. **Replace `.gitignore`** — the public `.gitignore` excludes personal files. For a private repo, you want a minimal one:
   ```gitignore
   # OS files
   .DS_Store
   Thumbs.db

   # Session scratch files
   context/notes/scratch-*
   ```

4. **Copy and fill in your config**
   ```bash
   cp config.example.yaml config.yaml
   # Edit config.yaml with your values
   ```

5. **Commit and push**
   ```bash
   git add .
   git commit -m "Initialize private instance"
   git push -u origin main
   ```

Now `origin` points to your private repo and `template` points to the public template. Use the `template-sync` agent to push improvements back to the template or pull updates from it.

The file `.gitignore.template` in your private repo represents what the public repo's `.gitignore` should look like. The `template-sync` agent handles this mapping automatically.

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
| `template-sync` | Syncs template files between private instance and public repo |

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
├── .gitignore.template         # Public repo's .gitignore (used by template-sync)
├── config.example.yaml        # Template — copy to config.yaml
├── config.yaml                # Your personal config (gitignored)
├── context/
│   ├── active/                # Current plans — agents always read/write here (gitignored)
│   │   ├── daily.md           # Today's daily plan
│   │   ├── weekly.md          # This week's plan
│   │   ├── calendar.md        # This week's calendar
│   │   └── goals.md           # Current quarter's goals
│   ├── archive/               # Historical files, organized year/month (gitignored)
│   │   └── YYYY/MM/daily/     # e.g., 2026/02/daily/2026-02-09.md
│   ├── calibration.example.md # Template — copy to calibration.md
│   ├── calibration.md         # Estimation calibration data (gitignored)
│   └── notes/                 # Scratch notes
└── README.md
```

## Daily Workflow

1. **Morning**: Run `morning-triage` — it scans everything and creates your daily plan
2. **Mid-day**: Run `daily-checkin` — quick progress check, reprioritize if needed
3. **As needed**: Run `estimate`, `meeting-prep`, `pr-context`, `interrupt`, or `delegate-or-own`
4. **End of day**: Run `end-of-day` — capture what happened, set up tomorrow
5. **Weekly**: Run `weekly-plan` on Monday, review on Friday (updates calibration data)
6. **Quarterly**: Run `quarterly-goals` to set up and track quarterly objectives
