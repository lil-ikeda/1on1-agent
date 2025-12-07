# init

Performs initial setup for the 1on1 management system.
Creates a profile for the manager (yourself).

## Pre-check

1. Check if `./manager-profile.md` already exists
2. If it exists, ask "A manager profile already exists. Do you want to overwrite it? (y/n)"

## Procedure

Ask the user the following information in a Q&A format.
For each question, briefly explain why that information is needed.

### 0. Language Settings

First, collect language preferences:

- **Primary Language**: "What is your primary language? (e.g., English, Japanese)"
- **Secondary Languages**: "What other languages do you speak? (optional)"
- **System Output Language**: "What language should system outputs (documentation, session files, agent feedback) be in?"
- **1on1 Default Language**: "What language do you typically use in your 1on1 sessions?"

### 1. Basic Information

- **Name**: "What is your name? (The agent will use this to embody your personality)"
- **Title**: "What is your current title? (e.g., Engineering Manager, VPoE)"
- **Management Experience**: "How long have you been in a management role? (e.g., ~2 years)"
- **Engineering Experience**: "How many years of engineering experience do you have?"
- **Background**: "Please share a brief career background (e.g., SIer → Startup → Current)"

### 2. 1on1 Style

- **Core Values in 1on1s**: "What are 3 things you value most in 1on1s? (e.g., drawing out true feelings, providing growth opportunities)"
- **Communication Style**: "What is your communication style in 1on1s? (e.g., listening-focused, question-driven)"
- **1on1 Purpose**: "What do you think is the purpose of 1on1s?"
- **Stance Towards Team Members**: "What is your fundamental stance towards team members?"

### 3. Self-Understanding

- **MBTI**: "What is your MBTI type? (Can skip if unknown)"
  - Ask not just the type, but also "What characteristics might affect your 1on1s"
- **StrengthsFinder TOP5**: "What are your top 5 StrengthsFinder strengths? (Can skip if unknown)"
  - For each strength, ask "How does this show up in your work"
- **Weaknesses**: "What weaknesses or challenges are you aware of?"

## Output

Based on the collected information, create `./manager-profile.md`.

Use `./templates/manager-profile.md` as the base template.

The output content (values, descriptions) should be in the user's specified System Output Language, but section headers should remain in English for system parsing.

### File Structure

```markdown
# Manager Profile - {name}

**Created**: {date}
**Last Updated**: {date}

---

## Language Settings

### Personal Languages
| Item | Value |
|------|-------|
| Primary Language | {primary_language} |
| Secondary Languages | {secondary_languages} |

### System Output Language
| Item | Language |
|------|----------|
| Documentation | {doc_language} |
| Session Files | {session_language} |
| Agent Feedback | {feedback_language} |

### 1on1 Default Language
- Default: {1on1_language}

---

## Basic Information

| Item | Value |
|------|-------|
| Name | {name} |
| Title | {title} |
| Management Experience | {management_exp} |
| Engineering Experience | {engineering_exp} |
| Background | {background} |

---

## 1on1 Philosophy

### Core Values in 1on1s
- {value1}
- {value2}
- {value3}

### Communication Style
- {style}

### Fundamental Stance
- **Purpose**: {purpose}
- **Approach**: {approach}
- **Work-Life Balance**: {wlb_stance}

### Stance Towards Team Members
- {stance}

---

## Personality Profile

### MBTI
- **Type**: {mbti_type}
- **Characteristics**:
  - {characteristic_affecting_1on1}

### StrengthsFinder TOP5
| Rank | Strength | How It Shows in Work |
|------|----------|---------------------|
| 1 | {strength1} | {manifestation1} |
| 2 | {strength2} | {manifestation2} |
| 3 | {strength3} | {manifestation3} |
| 4 | {strength4} | {manifestation4} |
| 5 | {strength5} | {manifestation5} |

### Weaknesses / Areas for Growth
- {weakness}

---

## Update History

| Date | Changes |
|------|---------|
| {date} | Initial creation |
```

## After Completion

1. Display the path of the created file
2. Guide: "For samples, refer to `./samples/en/manager-profile.md` or `./samples/ja/manager-profile.md`"
3. Guide: "Next, register team members with `/create-user`"
