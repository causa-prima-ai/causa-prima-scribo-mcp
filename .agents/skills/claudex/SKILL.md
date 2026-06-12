---
name: claudex
description: Hybrid Claude+Codex execution flow. Claude (Fable 5) keeps planning, architecture, frontend/visual/UX work, and the genuinely hardest parts; backend and heavier mechanical implementation gets a written spec and is dispatched to Codex (gpt-5.5, xhigh effort) whose quota is otherwise unused. Use when the user says /claudex <task>.
argument-hint: "<task description>"
---

# Claudex — split work between this session and Codex

Goal: save Fable 5 tokens. This session's value is planning quality and visual/frontend output — spend tokens there. Codex (ChatGPT quota, effectively free) executes well-specified backend and bulk implementation work.

## 1. Triage the task

Read the user's request and split it into work items. Route each item:

**Keep in this session (Claude):**
- Planning, architecture decisions, API/contract design
- Frontend: UI components, layout, styling, animations, copy, anything where visual taste matters
- The genuinely hardest/riskiest parts: subtle concurrency, tricky migrations, security-sensitive code, anything where a wrong move is expensive
- Small edits where writing a spec would cost more than just doing it
- Final integration, review of Codex's output, and verification (build/tests)

**Dispatch to Codex:**
- Backend implementation: API routes, lambdas, services, DB queries/migrations (non-risky ones), webhooks
- Heavy mechanical work: refactors across many files, test writing, boilerplate, data plumbing, script writing
- Anything well-specifiable where execution is labor, not judgment

If the task is purely one side, don't force a split — route the whole thing. Briefly tell the user the split before executing (one or two sentences, no ceremony).

## 2. Write the spec for Codex parts

Before dispatching, do enough repo reconnaissance to write a precise spec (exact file paths, existing patterns to follow, function signatures). A vague spec wastes the round-trip. The spec must include:

- **Objective** — one sentence.
- **Files** — exact paths to create/modify, and reference files whose patterns to copy.
- **Requirements** — concrete behavior, signatures, edge cases. Decide the design yourself; don't leave architecture choices to Codex.
- **Constraints** — what NOT to touch, project conventions (check CLAUDE.md), no new deps unless listed.
- **Done criteria** — how Codex should verify (build command, tests to run).

## 3. Dispatch

Use the Agent tool with `subagent_type: "codex:codex-rescue"`. The prompt must start with these flags, then `/goal` (a built-in Codex skill that drives goal-led execution — it must ALWAYS lead the prompt body), then the spec:

```
--fresh --model gpt-5.5-codex --effort xhigh

/goal <one-line objective>

<the spec>
```

- Codex runs write-capable by default — that's intended.
- If Claude-side work exists in parallel, run the agent with `run_in_background: true` and do the frontend/hard parts in this session while Codex works. Otherwise run it in the foreground.
- For follow-up fixes to a prior Codex run in the same session, use `--resume` instead of `--fresh` — still lead the prompt body with `/goal`.
- If dispatch fails because Codex is missing/unauthenticated, tell the user to run `/codex:setup`.

## 4. Integrate and verify

When Codex returns:

1. Read its diff (`git diff`/`git status`) — review like a PR. Check it matched the spec and project conventions.
2. Fix small issues yourself; for substantial misses, send one corrective follow-up with `--resume` rather than redoing the work here.
3. Wire Codex's backend output to your frontend work if the task was split.
4. Verify end-to-end: build, run tests, whatever the done criteria said. Report results honestly.

## 5. Deep-review gate (mandatory)

The goal is NOT finished until `/deep-review` approves. After integration and verification pass:

1. Run the `/deep-review` skill (Skill tool) over the full change set — Claude's work and Codex's work together. It is a repo-level skill that lives inside each repo; if it's not in the available-skills list for the current repo, tell the user instead of skipping the gate.
2. If it raises findings, fix them: small issues in this session; substantial backend misses go back to Codex via `--resume` with a corrective spec.
3. Re-run `/deep-review` after every fix round. Iterate until it approves with no blocking findings.
4. Do not report the task as done, and do not stop, while deep review is still rejecting. Approval is the exit condition.

Final report to user: what Claude did, what Codex did, verification status, and deep-review verdict (must be approved).
