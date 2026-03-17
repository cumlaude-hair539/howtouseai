# Workflow Rules: How to Work With an AI Coding Agent Without Creating Chaos

A lot of beginner problems do not come from lack of intelligence.

They come from lack of workflow.

If your workflow is messy, even a strong AI coding agent will produce messy results.
If your workflow is controlled, the same agent becomes dramatically more useful.

These rules are here to help you work in a way that is:

- safer
- clearer
- easier to debug
- easier to scale
- easier to recover when something breaks

Codex is built to work inside your local repository by reading files, editing files, and running commands, so workflow matters as much as prompt quality. OpenAI’s docs also emphasize iterative review, verification, and explicit constraints instead of blind one-shot generation.

## Rule 1: Inspect First, Change Second

Before asking the AI agent to build, refactor, fix, or debug anything, tell it to inspect the repository first.

Good:

```text
Inspect this repository first.
Explain the current structure.
Identify the relevant files.
Do not modify anything yet.
```

Bad:

```text
Just fix everything.
```

This matters because the agent performs much better when it grounds itself in the actual repository instead of guessing.

## Rule 2: One Task at a Time

Do not stack five unrelated tasks into one prompt.

Bad:

```text
Fix auth, redesign the homepage, improve the database schema, clean the Docker config, and add Stripe.
```

Better:

```text
Inspect the repository first.

Task:
Fix the login form submission bug only.

Constraints:
- do not change unrelated files
- do not refactor the auth system yet
```

Smaller tasks produce better results because they reduce ambiguity and make review easier.

## Rule 3: Ask for the Smallest Useful Next Step

This is one of the most important rules in AI coding.

Instead of asking for the final complete system, ask for the smallest next working step.

Good:

```text
What is the smallest useful next step?
Implement only that step.
```

This matches OpenAI’s recommended iterative workflow style: break work down, review often, and verify outcomes before moving further.

## Rule 4: Define Scope Clearly

If you do not define the scope, the agent may overbuild.

Good examples:

- keep the implementation minimal
- do not overengineer
- do not add unnecessary dependencies
- do not refactor unrelated files
- implement only step 1

OpenAI’s prompt guidance and Codex best practices both reward explicit constraints and clear definitions of done.

## Rule 5: Always Review Before Trusting

Do not assume that because the AI agent wrote it, it must be correct.

Review:

- the changed files
- the diff
- the commands it ran
- the behavior of the app

Codex includes built-in review workflows like `/review`, plus diff and status tools, specifically so you can inspect work before accepting it.

Good workflow:

```text
Explain what changed.
Show the relevant files.
Tell me how to run and test this.
```

## Rule 6: Commit Before Risky Changes

Before you let the agent make a large change, commit your current working state.

Examples of risky changes:

- major refactors
- dependency upgrades
- config rewrites
- moving many files
- merge conflict resolution
- large AI-generated edits across the repo

Good habit:

```bash
git status
git add .
git commit -m "Save progress before risky change"
```

This is one of the most important workflow rules because it makes mistakes reversible.

## Rule 7: Keep Sessions Focused

Do not turn one Codex session into a giant mixed conversation about ten different topics.

If the session gets too broad, split the work.

Codex supports slash commands such as `/compact`, `/fork`, and `/resume` for managing long sessions and cleaner task separation.

Useful tools:

```text
/compact
/fork
/status
```

Use them when:

- the thread is too long
- the task changed direction
- the answers become less focused
- the repo work should be split into subtasks

## Rule 8: Diagnose Before Fixing

If something breaks, do not immediately ask the agent to fix it.

Ask it to diagnose first.

Good:

```text
Inspect the repository and current error first.

Please:
1. explain the likely cause,
2. identify the relevant files,
3. suggest the safest fix,
4. do not modify anything until the diagnosis is clear.
```

This is much safer than letting the agent start changing files blindly.

## Rule 9: Use Approvals and Sandboxing Intentionally

If the AI agent needs to run commands, inspect files, or resolve Git problems, it needs enough permissions to do so.

OpenAI documents that approvals determine when Codex pauses for permission before running commands, while sandboxing defines what directories and network access it can use.

That means your workflow should be:

- start with tighter permissions
- widen access when the task actually requires it
- avoid giving dangerous full access casually
- review the result even after granting permission

Inside Codex, useful command:

```text
/permissions
```

## Rule 10: Let the Agent Help With Git, but Do Not Abdicate Review

Your AI agent can help with:

- messy diffs
- merge conflicts
- rebase conflicts
- confusing branch state
- grouping changes into logical commits
- reviewing local changes

Codex’s built-in `/review` can review uncommitted changes, commits, or diffs against a base branch, and `/diff` plus `/status` help inspect current state.

But even if the agent resolves the problem, you still review:

```bash
git status
git diff
```

That is the correct workflow.

## Rule 11: Make the Agent Explain Itself

You should not only ask for output.
You should also ask for operational explanation.

Good examples:

- explain which files you plan to change and why
- after editing, explain exactly what changed
- explain this in beginner-friendly terms

This dramatically improves learning and reduces silent mistakes.

## Rule 12: Prefer Minimal Clean Solutions Over Smart Solutions

A lot of bad AI coding happens because the agent tries to be too clever.

For beginner and intermediate workflows, prefer:

- fewer files
- fewer abstractions
- fewer dependencies
- more clarity
- easier testing

Good constraint block:

```text
Keep the implementation simple.
Prefer the smallest clean solution.
Do not add unnecessary abstractions.
Do not add extra dependencies unless truly required.
```

## Rule 13: Verify After Every Meaningful Step

Do not build for ten steps and only then test.

Instead:

1. implement one step
2. run it
3. inspect the result
4. commit progress
5. continue

OpenAI’s best-practices guide explicitly recommends asking Codex to run the right tests, lint, type checks, and behavioral verification instead of stopping at code generation.

Good workflow prompt:

```text
Implement only step 1.
Then explain how I can verify it.
Do not continue to step 2 yet.
```

## Rule 14: Use the Built-In Session Tools

Codex has built-in slash commands specifically for workflow control.

OpenAI documents slash commands such as `/status`, `/diff`, `/review`, `/permissions`, `/compact`, and `/fork` for session visibility, review, approvals, and session management.

Practical set:

```text
/status
/diff
/review
/permissions
/compact
/fork
/resume
```

What they are useful for:

- `/status` -> inspect current session state
- `/diff` -> inspect changes
- `/review` -> review current work
- `/permissions` -> adjust approvals
- `/compact` -> clean up long threads
- `/fork` -> split work into a cleaner thread
- `/resume` -> return to a previous thread when you need that context again

## Rule 15: Trust the Repo More Than the Conversation

If there is any mismatch between what the conversation says and what the actual code says, trust the repository.

The repo is the source of truth.

That is why inspect first is such a critical rule.

## Rule 16: Use Repo-Level Guidance When the Project Grows

As your projects become more serious, it helps to define repeatable repo-local guidance.

OpenAI documents support for project-level guidance via `AGENTS.md`, which Codex reads before doing work.

That means long-term you can create repo rules such as:

- code style expectations
- review expectations
- testing requirements
- deployment rules
- do not touch these folders without approval
- standard debug workflow

This makes the agent much more consistent over time.

## Rule 17: Do Not Confuse Development Workflow With Production Workflow

A very common mistake is trying to make the first build look like a final production system.

Keep these separate:

- local development workflow
- staging or preview workflow
- production workflow

This matters for things like:

- local `npm run dev`
- mobile preview via Cloudflare Tunnel
- `nginx` reverse proxy setup
- environment variables
- deployment scripts

If you mix all of these at once, the workflow becomes harder to understand.

## Rule 18: Keep the Human in Charge

The AI agent is a collaborator, not the owner of your repo.

The human should still decide:

- what task matters
- what scope is acceptable
- when a change is safe
- whether a fix is correct
- when to commit
- when to roll back

This is the healthiest way to use agentic coding tools.

## The Ideal Daily Workflow

A strong everyday workflow looks like this:

1. Open the correct repo.

```bash
pwd
git status
```

2. Ask for inspection first.

```text
Inspect this repository first.
Explain the current structure and relevant files.
Do not change anything yet.
```

3. Ask for a tiny plan.

```text
Break this task into the smallest practical steps.
```

4. Implement one step only.

```text
Implement only step 1.
Keep it minimal.
Do not change unrelated files.
```

5. Review the result.

```text
Explain what changed and show the diff summary.
```

6. Verify.

Run the app, tests, or checks.

7. Commit.

```bash
git add .
git commit -m "Complete step 1"
```

8. Continue.

This workflow scales much better than ask for everything at once.

## Good Default Rules to Tell the Agent

You can reuse this block often:

```text
Rules for this task:
- inspect first
- explain the relevant files
- keep the implementation minimal
- do not overengineer
- do not change unrelated files
- explain your plan before editing
- explain what changed after editing
- tell me how to verify the result
```

This is a strong default contract.

## Good Workflow Prompt for New Tasks

```text
Inspect this repository first.

Task:
[describe the task]

Workflow rules:
- explain the current structure first
- identify the relevant files
- propose the smallest clean implementation
- do not modify anything until you explain the plan
- implement only the first useful step
- do not change unrelated files
- explain what changed
- explain how I can verify it
```

## Good Workflow Prompt for Risky Tasks

```text
Inspect this repository and current git state first.

This is a risky task.
Before editing:
1. explain the relevant files,
2. explain the possible risks,
3. suggest the safest approach,
4. tell me whether I should commit first,
5. do not modify anything until the plan is clear.
```

This is ideal for refactors, merges, dependency upgrades, config rewrites, and infrastructure changes.

## Compact Summary

The core workflow rules are:

- inspect first
- do one task at a time
- ask for the smallest useful next step
- define scope clearly
- review before trusting
- commit before risky changes
- keep sessions focused
- diagnose before fixing
- use approvals and sandboxing intentionally
- verify after every meaningful step
- keep the human in charge

If you follow these rules, AI coding becomes much more stable.

## Further Reading

- [Codex CLI](https://developers.openai.com/codex/cli)
- [Codex best practices](https://developers.openai.com/codex/learn/best-practices)
- [Slash commands in Codex CLI](https://developers.openai.com/codex/cli/slash-commands)
- [Agent approvals & security](https://developers.openai.com/codex/agent-approvals-security)
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md)
