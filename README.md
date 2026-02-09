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
   git clone https://github.com/Joshua-Palamuttam/template-command-center.git command-center
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

Agents are lightweight executors that preload skills via the `skills:` field. Methodology lives in skills; agents provide context and delegation targets.

| Agent | Skills | What it does |
|-------|--------|-------------|
| `researcher` | `research` | Deep multi-source research — Confluence, Jira, Slack, web. Builds structured evidence bases |
| `sounding-board` | `sounding-board` | Adversarial thinking partner — stress-tests ideas with research-backed critical analysis |
| `morning-triage` | `morning-triage` | Scans DMs, channels, Jira, calendar; creates today's prioritized plan |
| `slack-catch-up` | `slack-catch-up` | Reads channels and DMs, surfaces what needs attention |
| `weekly-plan` | `weekly-plan` | Creates/maintains weekly capacity plan, tracks actuals vs estimates |
| `quarterly-goals` | `quarterly-goals` | Tracks progress against quarterly objectives, handles mid-quarter changes |
| `daily-checkin` | `daily-checkin` | Mid-day progress check against today's plan |
| `end-of-day` | `end-of-day` | Captures what happened, rolls forward incomplete items |
| `estimate` | `estimate` | Produces realistic time estimates with calibrated multipliers |
| `meeting-prep` | `meeting-prep` | Gathers Jira/Confluence/Slack context for an upcoming meeting |
| `pr-context` | `pr-context` | Gathers full context (ticket, design doc, discussion) for a PR review |
| `confluence-review` | `confluence-review` | Reads and critically summarizes a Confluence document |
| `jira-review` | `jira-review` | Pulls a Jira ticket with linked items and presents an actionable summary |
| `interrupt` | `interrupt` | Sizes an incoming interrupt and shows impact on current commitments |
| `delegate-or-own` | `delegate-or-own` | Helps decide whether to do a task yourself or hand it off |
| `calendar-sync` | `calendar-sync` | Reads Outlook/Google calendar via browser automation |
| `template-sync` | — | Syncs agents, skills, and hooks between private instance and public repo |
| `weekly-retro` | `weekly-retro` | Reviews planned vs actual, updates calibration data, surfaces patterns |
| `status-report` | `status-report` | Generates stakeholder-ready status update grouped by quarterly goals |
| `ticket-breakdown` | `ticket-breakdown` | Decomposes epics/stories into estimated subtasks including hidden work |

## Skills

Skills hold reusable methodology — the HOW. They can be invoked directly as slash commands or preloaded by agents.

| Skill | What it does |
|-------|-------------|
| `/morning-triage` | Scan DMs, @mentions, Slack channels, and Jira to create a prioritized daily plan |
| `/daily-checkin` | Mid-day progress check against today's plan, scan for new DMs |
| `/end-of-day` | Capture what happened, update daily plan, roll forward incomplete items |
| `/weekly-plan` | Create/maintain weekly capacity plan, track actuals vs estimates |
| `/weekly-retro` | Friday retrospective — compare planned vs actual, update calibration data |
| `/estimate` | Realistic time estimates with calibrated multipliers and three-point ranges |
| `/interrupt` | Size an incoming interrupt and show tradeoffs against current plan |
| `/meeting-prep` | Gather Jira/Confluence/Slack context for an upcoming meeting |
| `/status-report` | Generate stakeholder-ready status update grouped by quarterly goals |
| `/slack-catch-up` | Scan Slack channels and DMs, surface what needs attention |
| `/calendar-sync` | Read Outlook calendar via Chrome and extract meeting data |
| `/quarterly-goals` | Track quarterly goals across teams, handle mid-quarter additions |
| `/jira-review` | Pull a Jira ticket with linked docs, comments, and PRs |
| `/confluence-review` | Read and critically summarize a Confluence document |
| `/pr-context` | Gather full context for a PR — Jira ticket, design doc, Slack discussion |
| `/ticket-breakdown` | Decompose epics/stories into estimated subtasks including hidden work |
| `/delegate-or-own` | Decide whether to own a task or delegate, generate handoff briefs |
| `/research` | Multi-source research with confidence ratings — Confluence, Jira, Slack, web |
| `/sounding-board` | Stress-test ideas with structured adversarial analysis and thinking frameworks |
| `/plan-create` | Create strategic feature plan + handoff prompt for the target repo |
| `/plan-feature` | **Orchestrator** — manage the feature planning pipeline (research → refine → plan) |
| `/plan-resume` | Generate a continuation prompt for resuming feature plan implementation |
| `/standup` | 3-line standup summary: yesterday, today, blockers |
| `/capacity` | Show remaining hours today and this week, flag overcommitment |
| `/log-interrupt` | Append an interrupt to today's daily plan with timestamp |
| `/draft-reply` | Search a Slack channel, read a thread, draft a response with backing context |
| `/wrap-up` | Update daily plan with progress — lighter than `end-of-day` |
| `/what-next` | Recommend the next highest-impact task based on remaining capacity |

## Hooks

Deterministic automation on Claude Code lifecycle events. Configured in `.claude/settings.local.json`, scripts in `.claude/hooks/`.

| Hook | Event | What it does |
|------|-------|-------------|
| `session-start-check.py` | `SessionStart` | Verifies daily/weekly plans exist and are current |
| `pre-compact-context.py` | `PreCompact` | Preserves priorities and capacity across context compression |
| `log-slack-send.py` | `PostToolUse` | Logs outbound Slack messages to daily plan Notes section |
| `inject-daily-context.py` | `UserPromptSubmit` | Injects top 3 priorities as ambient context each turn |
| *(inline prompt)* | `Stop` | Nudges to update daily plan after significant work |

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
│   ├── agents/                # Lightweight executors (preload skills via skills: field)
│   ├── skills/                # Reusable methodology (the HOW)
│   │   └── <name>/SKILL.md   # Each skill in its own directory
│   ├── hooks/                 # Lifecycle hook scripts (.py)
│   └── settings.local.json    # MCP tool permissions + hooks config
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
│   ├── notes/                 # Scratch notes and standalone research
│   └── plans/                 # Feature planning pipeline
│       ├── active/            # Plans in progress
│       │   └── <plan-name>/   # state.md, research.md, analysis.md, plan.md, handoff.md
│       └── archive/           # Completed/abandoned plans
└── README.md
```

## Architecture: Skills = Knowledge, Agents = Executors

- **Skills** hold all detailed methodology — process steps, output formats, decision frameworks. They're reusable by any agent or directly by the user via slash commands.
- **Agents** are lightweight wrappers: frontmatter (with `skills:` field) + brief system prompt. They preload skills and run in their own context window.
- **The orchestrator** (`/plan-feature`) checks state files and routes to the right agent or skill next.

This pattern keeps methodology in one place (skills), agents slim and composable, and the pipeline stateful via `state.md` files.

## Feature Planning Pipeline

For strategic features that need research → refinement → planning before implementation:

1. **Start**: `/plan-feature search-reranking` — creates plan directory, routes to research
2. **Research**: `/research search-reranking` — gathers evidence from Confluence, Jira, Slack, web
3. **Refine**: `/sounding-board search-reranking` — stress-tests the research findings
4. **Plan**: `/plan-create search-reranking` — interviews for ambiguities, produces strategic plan + handoff prompt
5. **Handoff**: Copy `handoff.md` to the target repo and start implementation
6. **Resume**: `/plan-resume search-reranking` — generates a continuation prompt with current progress

Check status anytime: `/plan-feature` (shows all active plans)

## Daily Workflow

1. **Morning**: `/morning-triage` — scans everything and creates your daily plan
2. **Mid-day**: `/daily-checkin` or `/what-next` — progress check, pick next task
3. **As needed**: `/estimate`, `/meeting-prep`, `/pr-context`, `/interrupt`, `/delegate-or-own`
4. **Quick actions**: `/standup`, `/capacity`, `/log-interrupt`, `/draft-reply`
5. **End of day**: `/wrap-up` for a quick update or `/end-of-day` for the full close-out
6. **Weekly**: `/weekly-plan` on Monday, `/weekly-retro` on Friday (feeds calibration data)
7. **Quarterly**: `/quarterly-goals` to set up and track quarterly objectives
