# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

1on1 Management System - A system that proposes topics to discuss in 1on1 meetings based on past session history, designed for Engineering Managers.

## Commands

### `/setup-manager`
Create your own manager profile. Collects information interactively and generates `./manager-profile.md`.

### `/create-user`
Create a new team member profile. Collects basic information interactively and generates profile under `./users/{user_name}/`.

### `/create-session {user_name}`
Create a session file for the specified member's next 1on1. Proposes 3-5 topics after multi-agent review.

### `/complete-session {user_name}`
Post-session processing. Performs member assessment and manager review based on transcript.

## Directory Structure

```
1on1-agent/
├── .claude/commands/     # Slash command definitions
├── agents/               # Agent profiles
├── templates/            # Template files
├── samples/              # Sample files (for reference)
│   ├── en/               # English samples
│   └── ja/               # Japanese samples
├── users/                # User data (.gitignore target)
└── manager-profile.md    # Manager profile (.gitignore target)
```

## Language Settings

- Agent instructions and templates use English section headers for consistent parsing
- Content language is determined by manager's Language Settings in `manager-profile.md`
- Each user can override the 1on1 language in their profile

## Notes

- Session history loads up to 10 most recent files
- `users/` directory and `manager-profile.md` are excluded via `.gitignore` as they contain personal information
