# AI-Learning: an autonomous AI team for a founder

Learn practical AI by running a company with it. This repository sets up a team of
AI agents (built on [Claude Code](https://claude.com/claude-code)) that can research,
plan, design, build, test, analyse, operate and market your product. You give the goals
and approve the important decisions.

```
                          ┌──────────────┐
                          │   Founder    │  ← you: goals & approvals
                          └──────┬───────┘
                                 │
                       ┌─────────▼─────────┐
                       │  Chief of Staff   │  plans, delegates, reviews, reports
                       └─────────┬─────────┘
   ┌──────────┬──────────┬───────┼───────┬──────────┬──────────┬──────────┐
   ▼          ▼          ▼       ▼       ▼          ▼          ▼          ▼
Product   Researcher  Designer  Programmer  QA     Analyst     Ops     Marketing
Manager
```

## The team

| Member | What they do | Their file |
|---|---|---|
| **Chief of Staff** | Turns your goal into a plan, assigns work, reviews it and reports back | [`CLAUDE.md`](CLAUDE.md) |
| **Product Manager** | Specs, user stories, acceptance criteria, roadmap | [`.claude/agents/product-manager.md`](.claude/agents/product-manager.md) |
| **Researcher** | Market, competitor and technical research with sources | [`.claude/agents/researcher.md`](.claude/agents/researcher.md) |
| **Designer** | User flows, wireframes, HTML mockups, design system | [`.claude/agents/designer.md`](.claude/agents/designer.md) |
| **Programmer** | Builds features, fixes bugs, writes tests | [`.claude/agents/programmer.md`](.claude/agents/programmer.md) |
| **QA Engineer** | Test plans, automated tests, bug reports, ship/block verdicts | [`.claude/agents/qa.md`](.claude/agents/qa.md) |
| **Analyst** | Data analysis, KPIs, financial models, charts | [`.claude/agents/analyst.md`](.claude/agents/analyst.md) |
| **Ops** | CI/CD, deployment, security, runbooks, cost control | [`.claude/agents/ops.md`](.claude/agents/ops.md) |
| **Marketing** | Positioning, copy, launch plans, content, SEO | [`.claude/agents/marketing.md`](.claude/agents/marketing.md) |

Need someone else, such as Sales, Support, Legal or Finance? Run `/hire <role>` and the
team writes the new member's definition for you.

## Quick start (about 15 minutes)

### 1. Tell the team about your company
Fill in [`company/vision.md`](company/vision.md), [`company/product.md`](company/product.md)
and [`company/brand.md`](company/brand.md). Rough notes are fine. Every agent reads these first.

### 2a. Work with the team from your computer
```bash
npm install -g @anthropic-ai/claude-code   # one-time install
git clone https://github.com/ofc-nitin/AI-Learning && cd AI-Learning
claude
```
Then, inside Claude Code:

| You type | What happens |
|---|---|
| `/kickoff Validate an AI meal-planner for busy parents` | Chief of Staff plans the work, runs the team in parallel and reports back |
| `/standup` | Status report: shipped, in progress, blocked, next priorities |
| `/hire customer support` | Adds a new team member |
| `Ask the researcher to compare Stripe vs Razorpay for India` | Hands the task to one member directly |
| `/agents` | See and edit the team |

You can also do this from [claude.ai/code](https://claude.ai/code) in the browser or the
Claude mobile app, with no install needed.

### 2b. Let the team work autonomously on GitHub
1. Install the Claude GitHub App on this repo: <https://github.com/apps/claude>
2. Add a repository secret under **Settings → Secrets and variables → Actions → New repository secret**:
   - `ANTHROPIC_API_KEY`: from <https://console.anthropic.com>, **or**
   - `CLAUDE_CODE_OAUTH_TOKEN`: run `claude setup-token` if you have a Claude Pro/Max
     plan, then switch the commented line in the workflows
3. Create a label called **`ai-team`** under **Issues → Labels**.

Now:
- **New issue → "AI team task"**: pick who it's for, describe the goal, submit. The
  team starts work, comments progress on the issue, and opens a pull request with the
  deliverable.
- **Comment `@claude as qa: review this PR`** on any issue or PR to bring in a team member.
- **Every Monday** the Chief of Staff opens a *Stand-up* issue summarising the week.
  You can also run it any time from **Actions → Weekly Stand-up → Run workflow**.

You review and merge the pull requests. Nothing goes public or costs money without your approval.

## Where things live

```
CLAUDE.md               ← team operating manual (read by every session)
.claude/agents/         ← one file per team member: their role, tools and rules
.claude/commands/       ← /kickoff, /standup, /hire
company/                ← your vision, product and brand (the team's source of truth)
deliverables/<role>/    ← everything the team produces
deliverables/decisions.md ← decision log
.github/workflows/      ← GitHub automation (issue-driven team, weekly stand-up)
.github/ISSUE_TEMPLATE/ ← "AI team task" form
```

## Learning path

Learn the AI concepts by using them. Each step teaches one idea.

| # | Do this | You'll learn |
|---|---|---|
| 1 | Read [`.claude/agents/researcher.md`](.claude/agents/researcher.md), then ask it one real question about your market | **Prompting & system prompts.** An agent is mostly a well-written job description. |
| 2 | Edit the researcher's rules (for example "always include a pricing table") and ask again | **Prompt iteration.** Small instruction changes visibly change the output. |
| 3 | Run `/kickoff` on a small goal and watch several agents run at once | **Multi-agent orchestration.** One planner, many specialists, parallel work. |
| 4 | Compare the `tools:` line in `designer.md` and `programmer.md` | **Tool use & least privilege.** Agents act through tools, so give each only what it needs. |
| 5 | Ask the programmer to build a tiny feature, then ask QA to review it | **Agent loops & verification.** Write → test → fix, with a second agent as a checker. |
| 6 | Give the analyst a CSV (sales, signups, anything) | **AI + code for data.** The agent writes and runs real analysis scripts. |
| 7 | Open an "AI team task" issue on GitHub | **Autonomous agents & CI.** The same team runs unattended, triggered by events. |
| 8 | Run `/hire` for a role you need | **Designing agents.** Write your own specialist from scratch. |
| 9 | Read [`CLAUDE.md`](CLAUDE.md) and change a team rule | **Guardrails & governance.** How you keep autonomous AI safe and on-brand. |

Further reading:
- Claude Code subagents: <https://code.claude.com/docs/en/sub-agents>
- Claude Code GitHub Actions: <https://code.claude.com/docs/en/github-actions>
- Prompt engineering guide: <https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview>

## Guardrails

The team is autonomous for *work* but not for *irreversible actions*. Every agent is told to:
- never publish, email people, spend money, delete data or touch production without your approval
- never invent data, quotes, customers or sources
- deliver through pull requests, so you review before anything is merged

Running agents costs money: API usage, or your Claude plan's limits. Start with small
tasks, watch usage in the Anthropic console, and adjust `--max-turns` in the workflows to cap long runs.
