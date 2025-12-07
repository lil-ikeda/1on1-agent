# complete-session

After a 1on1 session ends, organizes session content based on transcript, performs member assessment and manager review, and updates related files.

## Arguments

- `$ARGUMENTS`: Username (required)

## Language Setting

1. Read `./manager-profile.md` to get the manager's System Output Language settings
2. Read `./users/$ARGUMENTS/profile.md` to get the member's 1on1 Language setting
3. Determine output language:
   - Use member's "1on1 Language" if specified
   - Otherwise, use manager's "Session Files" language setting
   - Fall back to manager's Primary Language

All session content and updates should be in the determined output language.

## Procedure

### 1. Input Validation

- If `$ARGUMENTS` is empty, display the list of users under `./users/` and prompt for selection
- If the specified user's directory doesn't exist, display an error

### 2. Information Gathering

Read the following files:

- `./users/$ARGUMENTS/profile.md` - User profile
- Today's or most recent session file under `./users/$ARGUMENTS/sessions/`
- Past sessions under `./users/$ARGUMENTS/sessions/` (up to 5 most recent for context)

### 3. Collect Transcript

Ask the user:

"Please paste the session transcript (e.g., from Google Meet's transcription feature)"

※ Wait until the transcript is pasted

**Important**: Use raw transcript, not a summary of meeting notes. Summaries lose nuances (tone, hedging expressions, etc.) which reduces scoring accuracy.

### 4. Analyze and Organize Transcript

Extract the following from the pasted transcript:

- **Topics Discussed**: Organize main topics as bullet points
- **Member's Comments & Insights**: **Quote the member's words verbatim** (preserve tone and nuance)
- **Action Items for Next Time**: Clearly state who does what
- **Items to Follow Up**: Items requiring continued attention

### 5. Member Assessment (Calculate 3 Scores)

Follow instructions in `./agents/member-assessment.md` to calculate the following scores:

#### Turnover Risk (1-5)
| Score | Level | Description |
|-------|-------|-------------|
| 1 | Very Low | No signs of turnover, high engagement |
| 2 | Low | Stable with minor complaints |
| 3 | Medium | Warning signs present, needs attention |
| 4 | High | Clear warning signs, possible job hunting |
| 5 | Very High | Resignation imminent or already expressed |

#### Burnout Risk (1-5)
| Score | Level | Description |
|-------|-------|-------------|
| 1 | Very Low | Good health, managing stress well |
| 2 | Low | Light stress, manageable |
| 3 | Medium | Signs of accumulated stress, monitor |
| 4 | High | Burnout symptoms, intervention needed |
| 5 | Very High | Serious condition, immediate action needed |

#### Motivation Score (1-5)
| Score | Level | Description |
|-------|-------|-------------|
| 1 | Very Low | Lost motivation, disengaged |
| 2 | Low | Passive, doing bare minimum |
| 3 | Medium | Normal, neither good nor bad |
| 4 | High | Motivated, proactively engaged |
| 5 | Very High | Highly motivated, self-driven challenges |

Each score must include **rationale** (with **specific quotes from transcript**).

**Scoring Precautions**:
- Don't miss tone or hedging expressions ("a bit", "not super... but", etc.)
- Quote the person's actual words, not summarized versions
- Be extra careful when assigning extreme scores (1 or 5) and verify rationale

### 6. Manager (1on1 Quality) Review

Follow instructions in `./agents/manager-review.md` to review session quality:

- **Listening Quality**: How well was the member's voice drawn out?
- **Quality of Questions**: Were questions effective at drawing out true feelings?
- **Follow-up**: Were carryover items from previous sessions confirmed?
- **Support Provided**: Were actions taken to resolve blockers?
- **Topic Selection**: Were topics set up for the next session?

Output evaluation in the following format:

```
## Manager Review

### Overall Rating: ★★★☆☆ (3/5)

### What Went Well
- ...

### Areas for Improvement
- ...

### Focus Points for Next Session
- ...
```

### 7. Update profile.md

Based on transcript and score evaluation, update the following sections:

- **Current Status** > Current Projects/Tasks
- **Current Status** > Recent Challenges/Concerns
- **Current Status** > Motivation Level
- **Current Status** > Health/Work-Life Balance
- **Requests from Member** (if there are topics for next time)
- **1on1 History Summary** > Topics from Last Session
- **1on1 History Summary** > Items Requiring Follow-up
- **1on1 History Summary** > Past Insights/Desires Expressed
- **Update History** (add today's update)
- **Last Updated** (update date)

### 8. Update Session File

Update today's session file `./users/$ARGUMENTS/sessions/YYYY-MM-DD.md`:

- **Session Info** > Duration
- **Session Notes** > Topics Discussed
- **Session Notes** > Member's Comments & Insights
- **Session Notes** > Action Items for Next Time
- **Session Notes** > Items to Follow Up
- **Reflection** > Session Impressions (include manager review results)

※ Add new "Member Assessment Score" section:

```markdown
---

## Member Assessment Score (AI Generated)

| Metric | Score | Rationale |
|--------|-------|-----------|
| Turnover Risk | X/5 | ... |
| Burnout Risk | X/5 | ... |
| Motivation | X/5 | ... |

### Score Trends (Last 5 Sessions)
<!-- Include score trends if past scores exist -->
```

### 9. Create Next Session File

Ask the user: "Do you want to create the next session file? (y/n)"

If "y", execute `/create-session $ARGUMENTS`

### 10. Completion Report

Display the following (in the output language):

```
## Complete

### Updated Files
- ./users/$ARGUMENTS/profile.md
- ./users/$ARGUMENTS/sessions/YYYY-MM-DD.md

### Member Assessment Scores
| Metric | Score |
|--------|-------|
| Turnover Risk | X/5 |
| Burnout Risk | X/5 |
| Motivation | X/5 |

### Manager Review
Overall Rating: ★★★☆☆ (X/5)
- [Improvement summary]

### Follow-up Items for Next Session
- ...
```

---

## Important Notes

- Transcripts may contain confidential information; do not send to external services
- Score evaluations are reference values; final judgment is made by the manager
- If extreme scores (1 or 5) appear, verify the reasons in detail
- Manager review is for self-improvement, not for performance evaluation
