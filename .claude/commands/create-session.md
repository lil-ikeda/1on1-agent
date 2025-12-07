# create-session

Creates a session file for the specified member's next 1on1 and proposes topics to discuss.

## Arguments

- `$ARGUMENTS`: Username (required)

## Language Setting

1. Read `./manager-profile.md` to get the manager's System Output Language settings
2. Read `./users/$ARGUMENTS/profile.md` to get the member's 1on1 Language setting
3. Determine output language:
   - Use member's "1on1 Language" if specified
   - Otherwise, use manager's "Session Files" language setting
   - Fall back to manager's Primary Language

All session content should be generated in the determined output language.

## Procedure

### 1. Input Validation

- If `$ARGUMENTS` is empty, display the list of users under `./users/` and prompt for selection
- If the specified user's directory doesn't exist, display an error

### 2. Information Gathering

Read the following files:

- `./manager-profile.md` - Manager profile
- `./users/$ARGUMENTS/profile.md` - User profile
- Up to 10 most recent session files under `./users/$ARGUMENTS/sessions/` (in descending date order)

### 3. Confirm Requests from Member

Ask the user: "Does the member have any specific topics they want to discuss? (Enter topics or 'n' for none)"

- If the answer is "n", "-", or "none", treat it as no specific topics

### 4. Topic Proposal Generation (3-4 Stage Review)

#### Step 1: Initial Draft by Manager Agent

Based on the instructions in `./manager-profile.md`, propose 3-5 topics

#### Step 2: Review by EM Best Practice Agent

Review Step 1 output following instructions in `./agents/em-best-practice.md`

#### Step 3: Review by Tech Specialist Agent

Select the appropriate tech agent based on member's **Role** and review:

| Role | Agent File |
|------|------------|
| QA Engineer | `./agents/tech-specialist-qa.md` |
| SRE / Infrastructure Engineer | `./agents/tech-specialist-sre.md` |
| ML Engineer | `./agents/tech-specialist-ml.md` |
| Backend Engineer | `./agents/tech-specialist-backend.md` |
| Frontend Engineer | `./agents/tech-specialist-frontend.md` |

※ If role doesn't match any above, select the closest one or skip

#### Step 4: Review by Career Agent (Optional)

Follow instructions in `./agents/career-agent.md` and only conduct review if the following conditions apply:

- Performance not being recognized
- High turnover potential (tenure 2-3+ years, dissatisfaction with growth opportunities, etc.)
- Seeking promotion or role change (leadership/management aspirations, etc.)
- Considering skill change (career transition: QA→Dev, Dev→SRE, etc.)
- Career direction uncertainty (unable to articulate clearly)
- Increased external activities (side work, conference talks, OSS, etc.)
- Upcoming life events (marriage, childbirth, caregiving - events that may impact career perspective)

Skip if none apply

### 5. Create Final Version

Integrate review results from all stages to create the final topic list:

- Remove duplicates
- Sort by priority
- Narrow down to 3-5 topics

### 6. Create Session File

Create `./users/$ARGUMENTS/sessions/YYYY-MM-DD.md` based on `./templates/session.md`:

- Use today's date
- Include requests from member if any
- Fill the Preparation section with 3-5 topics, each containing:
  - **Topic title** as the heading
  - **Suggested Questions**: 2-3 specific questions to ask during the 1on1
  - **Background**: Context and intent for why this topic is important now
- All content should be in the determined output language

### 7. Completion Report

Display the following (in the output language):
- Path of the created file
- Summary of proposed topics
- Reminder: "After the session, run `/complete-session`"

## Output Example

```
Session file created: ./users/tanaka/sessions/2025-11-28.md

## Topics for This Session (3 items)

1. Follow up on career direction discussed last time
2. Recent test automation progress
3. Team communication

After the session, run `/complete-session tanaka`!
```
