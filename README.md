# 1on1 Agent

A 1on1 support agent powered by Claude Code. Proposes discussion topics based on past session history and continuously improves 1on1 quality.

---

## ⚠️ Important: Handling Personal Information

**The information handled by this tool includes personal and confidential member data.**

### Precautions

1. **Local Execution Recommended**
   - Claude Code runs locally, but input information is sent to Anthropic's servers via API
   - Please verify compliance with your company policies and privacy regulations before use

2. **Repository Visibility Settings**
   - If forking this repository, **always operate as a private repository**
   - `users/` and `manager-profile.md` are excluded via `.gitignore`, but be careful not to commit them accidentally

3. **Handling Information from 1on1s**
   - Content discussed in 1on1s is confidential information based on trust between manager and member
   - Do not share with third parties without consent

---

## Design Philosophy

### Multi-Agent Review from Multiple Perspectives

Rather than relying on a single AI, multiple specialized agents review from different perspectives.

```
Manager Agent → EM Best Practice → Tech Specialist Agent
(Initial Draft)   (General Perspective)  (Specialized Perspective)
                                              ↓
                                      Career Agent
                                      (Conditional Activation)
```

| Agent | Role |
|-------|------|
| Manager Agent | Topic proposals reflecting the EM's personality and values |
| EM Best Practice | Alignment with general 1on1 best practices |
| Tech Specialist Agent | Technical perspective specific to member's role |
| Career Agent | Turnover risk and career growth perspective (conditional) |

### Articulating EM's Personality and Style

By defining the EM's values and style in `manager-profile.md`, the AI functions as a **tool that extends the EM's own thinking** rather than a generic assistant.

---

## Setup

### Prerequisites

- [Claude Code](https://claude.ai/code) installed

### Steps

1. **Fork the repository** (as a private repository)

2. **Initial setup**
   ```
   /init
   ```
   Creates your own profile through interactive dialogue.

3. **Register team members**
   ```
   /create-user
   ```

---

## Usage

### Before Session

```
/create-session {user_name}
```

- Loads profile and past sessions
- Runs multi-agent review
- Proposes 3-5 focused topics

### After Session

```
/complete-session {user_name}
```

- Paste the transcript
- Calculates member assessment scores (Turnover Risk / Burnout Risk / Motivation)
- Conducts manager review
- Updates profile and session files

---

## Directory Structure

```
1on1-agent/
├── .claude/
│   └── commands/           # Slash command definitions
│       ├── init.md
│       ├── create-user.md
│       ├── create-session.md
│       └── complete-session.md
│
├── agents/                 # Agent profiles
│   ├── em-best-practice.md
│   ├── career-agent.md
│   ├── member-assessment.md
│   ├── manager-review.md
│   └── tech-specialist-*.md
│
├── templates/              # Template files
│   ├── manager-profile.md
│   ├── user-profile.md
│   └── session.md
│
├── samples/                # Sample files (for reference)
│   ├── en/                 # English samples
│   └── ja/                 # Japanese samples
│
├── users/                  # User data (.gitignore target)
│   └── {user_name}/
│       ├── profile.md
│       └── sessions/
│           └── YYYY-MM-DD.md
│
├── manager-profile.md      # Manager profile (.gitignore target)
├── CLAUDE.md
└── README.md
```

---

## Customization

### Adding Tech Specialist Agents

You can add new tech specialist agents to the `agents/` directory:

```
agents/tech-specialist-mobile.md
agents/tech-specialist-data.md
```

After adding, update the tech agent selection table in `create-session.md`.

### Editing Manager Profile

The `manager-profile.md` created by `/init` can be manually edited anytime. Refer to samples in `samples/en/manager-profile.md` or `samples/ja/manager-profile.md`.

### Language Settings

The system supports multilingual output:
- Configure your preferred language in `manager-profile.md` during `/init`
- Each team member can have a different 1on1 language in their profile
- Session files and feedback will be generated in the configured language

---

## Notes

- Score evaluations are reference values; final judgment should be made by the manager
- This tool supports 1on1 "preparation" and "reflection" but does not replace the 1on1 itself
- **Use raw transcripts, not summaries**
  - Fillers like "um", "well" and hedging expressions ("not super... but") contain important nuances
  - Summaries strip these out, reducing scoring accuracy for turnover risk etc.
  - We recommend pasting raw data from Google Meet transcription or similar tools

---

## License

MIT
