---
description: Add a new member to the AI team by creating a new subagent definition.
argument-hint: <role, e.g. "sales", "customer support", "legal", "finance">
---

The Founder wants to add this role to the AI team: **$ARGUMENTS**

1. Read the existing agents in `.claude/agents/` and copy their structure and tone.
2. Create `.claude/agents/<kebab-case-role>.md` with:
   - frontmatter: `name`, a `description` that says exactly when to use this member
     (the Chief of Staff routes work based on it), `tools` limited to what the role
     needs, and `model: inherit`
   - a system prompt with these sections: **Your job**, **How you work**, a
     **Deliverables** or **Report format** section that saves to
     `deliverables/<role>/`, and **Rules** (including what the role must never do
     without Founder approval)
3. Add the new member to the team table in `CLAUDE.md` and in `README.md`.
4. Add the role to the "Assign to" dropdown in `.github/ISSUE_TEMPLATE/task.yml`.
5. Summarise the new hire in 3 lines.
