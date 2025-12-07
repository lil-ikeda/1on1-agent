# create-user

Creates a new team member profile.

## Language Setting

Before starting, read `./manager-profile.md` to determine the System Output Language.
All user-facing prompts and output content should be in the manager's configured System Output Language.

## Procedure

1. Ask the user the following information in a Q&A format:
   - Username (used as directory name, alphanumeric recommended)
   - Display name (localized name is fine)
   - Email address
   - Team
   - Role (e.g., QA Engineer, Backend Engineer, SRE, ML Engineer, Frontend Engineer)
   - Title/Grade
   - Join date
   - Team assignment date
   - **Language Profile**:
     - Primary Language
     - Secondary Languages (optional)
     - 1on1 Language (language to use in 1on1 with this member; leave empty to use manager's default)

2. Create the `./users/{user_name}/` directory

3. Create the `./users/{user_name}/sessions/` directory

4. Create `./users/{user_name}/profile.md` based on `./templates/user-profile.md`
   - Fill in the collected information
   - Use today's date for "Created" and "Last Updated"
   - Section headers should remain in English for system parsing
   - Content values should be in the member's 1on1 Language (or manager's default if not specified)

5. After creation, display:
   - Path of the created file
   - Next steps (guide user to manually add detailed profile information)

## Important Notes

- Username may only contain alphanumeric characters, hyphens, and underscores
- If a user with the same name already exists, show a warning and confirm whether to overwrite
- For samples, refer to `./samples/en/users/` or `./samples/ja/users/`
