---
name: skill-feed
description: Proactively detect failed or stuck user tasks, build targeted search queries, and find the best recovery/automation skills from ClawHub. Use when a workflow fails (API errors, retries, timeout, missing expected output) and you need ranked skill recommendations with immediate fix steps. Designed to produce provider-neutral recommendations compatible with Claude Code, ChatGPT, and Gemini workflows.
---

# SkillFeed

Automatically match the best skills to unblock a failed or stuck workflow.

## Trigger Conditions (auto)

Run this skill when any of these signals appears:

1. Command/API failure (non-zero exit, HTTP 4xx/5xx)
2. Retry threshold exceeded (default >=2 retries)
3. Expected output missing (for example no tweet id after post task)
4. Execution timeout exceeded

Do not trigger for normal delay/noise.

## Workflow

1. Capture failure context
   - task name
   - platform (X/Twitter, Telegram, GitHub, etc.)
   - error message/code
   - latest action log summary
2. Classify failure type
   - auth/permission
   - rate limit/quota
   - network/timeout
   - invalid params/payload
   - unknown
3. Build layered search queries (broad -> scenario -> failure)
   - Q1 broad capability query
   - Q2 scenario-specific query
   - Q3 failure-specific query with error tokens
4. Search ClawHub
   - Use `https://clawhub.ai/skills?focus=search`
   - Prefer sorting by stars / recently updated when comparing candidates
5. Rank candidates
   - match to goal (highest weight)
   - match to failure type
   - setup cost and risk
   - maintenance signals
6. Return recovery plan
   - Top 1 primary skill
   - 2 alternatives
   - 3-5 concrete next actions
   - fallback path if primary fails
7. Anti-noise guardrails
   - Deduplicate same error recommendations within cooldown window (default 30m)
   - Avoid auto-running high-risk external actions without user confirmation

## Query Construction Rules

Generate queries from context tokens:

- Goal tokens: `post`, `schedule`, `auto reply`, `daily report`
- Platform tokens: `x`, `twitter`, `tweet`, `telegram`, `github`
- Failure tokens: `401`, `403`, `429`, `timeout`, `invalid token`, `permission denied`

Example for failed tweet post:

- Q1: `tweet automation`
- Q2: `x twitter schedule post cron`
- Q3: `twitter post failed 401 invalid token rate limit`

## Provider Adaptation (Claude Code / ChatGPT / Gemini)

When returning recommendations, include provider-specific execution hints so the same strategy can run across major assistants.

1. Keep core logic provider-neutral
   - Use the same goal, failure classification, query generation, and ranking flow.
2. Add execution mapping by provider
   - Claude Code: emphasize terminal-first and repo workflow steps.
   - ChatGPT: emphasize concise operator checklist + copy-paste commands.
   - Gemini: emphasize structured step blocks and explicit validation checks.
3. Normalize outputs
   - Keep identical recommendation order across providers.
   - Only vary phrasing and action formatting.

## Output Format

- Goal: <what user wants>
- Failure signal: <what failed>
- Primary recommendation: `<skill>` (`/slug`) — <why>
- Alternatives:
  - `<skill>` (`/slug`) — <tradeoff>
  - `<skill>` (`/slug`) — <tradeoff>
- Immediate actions (3-5 steps)
- Success check:
  - expected output present
  - no critical error in latest run
- Fallback if still failing
- Provider runbook:
  - Claude Code: <execution notes>
  - ChatGPT: <execution notes>
  - Gemini: <execution notes>

## References

- Search and ranking recipes: `references/discovery-workflow.md`
- Scenario keyword map: `references/query-templates.md`
- Claude Code / ChatGPT / Gemini adaptation: `references/provider-adaptation.md`
