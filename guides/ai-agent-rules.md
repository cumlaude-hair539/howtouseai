# AI Agent Rules: How Your Coding Agent Should Behave Inside Your Repository

A coding agent is not supposed to behave like chaos with autocomplete.

It should behave like a careful technical operator inside your repository.

That means:

- inspect first
- respect the existing project
- change only what is necessary
- explain what it is doing
- avoid unrelated edits
- work within permissions
- help with Git and debugging when needed
- stop and ask when the task becomes risky

Codex is designed to work inside the selected directory by reading files, editing files, and running commands, and its official guidance emphasizes approvals, sandboxing, review, and explicit workflow rules rather than blind autonomy.

## The Main Rule

The agent should behave like a disciplined repo operator, not like a random code generator.

That means the agent should:

- understand the repo before editing
- follow repo rules
- keep changes minimal and relevant
- avoid touching unrelated files
- make its actions reviewable
- stay inside the allowed permission boundary

Codex supports this kind of controlled workflow directly through approvals, sandboxing, review tools, and repo-level instruction files like `AGENTS.md`.

## Rule 1: Inspect First, Edit Second

Before the agent writes code, it should inspect the repository first.

Good behavior:

- identify the relevant files
- understand the existing structure
- understand how the project currently works
- explain the plan before making changes

Bad behavior:

- immediately generating new structure without inspection
- inventing architecture that does not match the repo
- editing many files before understanding context

Codex guidance reinforces that it works best when grounded in the repository first, rather than guessing from the prompt alone.

## Rule 2: Follow Repository Instructions

If the repository has instructions, the agent should obey them.

For Codex, this includes `AGENTS.md`.

OpenAI documents that Codex reads `AGENTS.md` files before doing work, using layered scopes such as global and project-level instructions, so teams can define how the agent should behave in that codebase.

That means your repo can define rules like:

- code style expectations
- testing expectations
- branch workflow
- deployment boundaries
- files or folders that need extra caution
- mandatory review steps
- "do not edit these paths automatically"

## Rule 3: Do Not Overengineer

The agent should prefer the smallest clean solution that fits the task.

That means:

- do not add unnecessary dependencies
- do not create extra abstractions without reason
- do not generate complex architecture for a simple task
- do not rewrite the project when a small change is enough

OpenAI’s Codex best-practices guidance recommends keeping workflows controlled, scoped, and reviewable rather than letting the agent sprawl into oversized changes.

## Rule 4: Change Only What Is Relevant

The agent should not touch unrelated files.

Good behavior:

- edit only the files relevant to the current task
- explain why each changed file matters
- leave unrelated code alone

Bad behavior:

- formatting many unrelated files
- restructuring folders for no reason
- renaming files unrelated to the task
- mixing feature work with cleanup work

This is one of the most important practical rules for keeping diffs readable and safe to review.

## Rule 5: Explain Before and After

A good agent should explain:

Before editing:

- what it found
- which files are relevant
- what it plans to do

After editing:

- what changed
- why it changed
- how to run or verify the result
- what risks remain

Codex’s documented workflows emphasize review, diff inspection, and explicit command and status visibility through tools like `/status`, `/diff`, and `/review`.

## Rule 6: Respect Approvals and Sandboxing

The agent should work within the permission model you set.

OpenAI documents two main control layers:

- approval mode: when Codex must pause and ask permission before running commands
- sandbox mode: what files, directories, and network access the agent can use

That means the agent should not be treated like it can or should do everything automatically all the time.

A healthy rule is:

- use tighter permissions by default
- loosen permissions only when the repo and task justify it
- still review the result afterward

## Rule 7: The Agent May Help With Git Problems

Your AI coding agent is not only for writing code.

It can also help with:

- inspecting Git state
- understanding diffs
- grouping changes into cleaner commits
- merge conflicts
- rebase conflicts
- local review before commit

Codex officially documents `/review` for reviewing uncommitted changes, commits, or diffs, along with `/diff` and `/status` for state inspection.

So the rule is:

the agent may help with Git problems, but the human still reviews the final diff.

## Rule 8: If You Want Deeper Help, Give the Agent the Right Approvals

If the agent is supposed to inspect, run commands, or help resolve repo problems, it needs enough access to do so.

OpenAI’s current Codex docs say `/permissions` is the built-in slash command for changing what Codex can do in a session, and they note that `/approvals` still works as an alias.

So for Codex specifically:

- the agent may need `/permissions`
- `/approvals` may still work as an alias
- full access should not be handed out casually

This is important for tasks like:

- resolving Git conflicts
- running build or test commands
- inspecting multi-file breakage
- updating configs
- handling more complex repo operations

## Rule 9: The Agent Should Review Before Big Actions

For risky tasks, the agent should not jump straight into edits.

Risky tasks include:

- refactors
- deployment config changes
- build pipeline changes
- large dependency changes
- auth changes
- Git conflict resolution
- `nginx` or server config changes

For those tasks, the agent should:

1. inspect
2. explain risks
3. propose the safest path
4. only then edit

This matches Codex’s documented review-first and approval-aware workflow model.

## Rule 10: The Agent Should Help Verify, Not Just Generate

The agent should not stop at "I wrote code."

It should also help with:

- how to run it
- how to test it
- what command to use next
- what to verify in the UI or terminal
- whether the diff matches the task

OpenAI’s best-practices guidance explicitly recommends using Codex for checks, review, and validation, not just raw generation.

## Rule 11: The Agent Should Stay Repo-Grounded

If the conversation says one thing but the code says another, the agent should trust the repository.

That means:

- inspect actual files
- inspect actual scripts
- inspect actual config
- avoid inventing features that are not present
- avoid assuming architecture that does not exist

Codex is built around the selected local directory and uses the actual repo as its working ground truth.

## Rule 12: The Agent Should Respect Trust Boundaries

Good agent behavior respects the repo’s actual trust model.

That means:

- default to bounded behavior
- widen privileges deliberately
- treat dangerous full access as an exception, not the default

This follows OpenAI’s documented approvals and sandboxing model.

## Rule 13: The Agent Should Use Built-In Session Tools Properly

Codex documents built-in slash commands for session control, review, permissions, and workflow management. These include:

- `/status`
- `/diff`
- `/review`
- `/permissions`
- `/compact`
- `/fork`

A good agent workflow uses those tools when appropriate:

- `/status` -> inspect current session state
- `/diff` -> inspect current changes
- `/review` -> review work before commit
- `/permissions` -> adjust approvals
- `/compact` -> clean up long sessions
- `/fork` -> split work into a cleaner thread

## Rule 14: Reusable Agent Behavior Should Live in the Repo

If you have repeating workflows, put them into repo-level instructions instead of rewriting them every time.

OpenAI documents `AGENTS.md` as the right place for durable project-specific guidance.

That means over time you can define repeatable agent behaviors such as:

- how to inspect the repo
- how to handle Git conflicts
- how to prepare deployment configs
- how to review changes before commit
- how to avoid dangerous file paths

## Rule 15: The Human Stays in Charge

Even with strong agent support, the human should still decide:

- what task matters
- what permissions are appropriate
- whether the proposed plan is acceptable
- whether the final diff is safe
- whether to commit
- whether to deploy

Codex is a coding agent, not ownership transfer.

## Good Default Behavior Rules for the Agent

You can paste this block as a reusable instruction set:

```text
Agent rules:
- inspect the repository first
- explain the relevant files before editing
- keep changes minimal and task-focused
- do not overengineer
- do not add unnecessary dependencies
- do not change unrelated files
- explain the plan before making risky edits
- explain exactly what changed after editing
- help verify the result
- respect approvals, sandboxing, and repo instructions
- use git-aware caution
- do not commit or deploy unless explicitly asked
```

This aligns well with OpenAI’s documented guidance around approvals, review, repo instructions, and scoped agent workflows.

## Good Prompt to Establish Agent Behavior

```text
Before doing any work in this repository, follow these rules:

1. Inspect the repository first.
2. Explain the current structure and relevant files.
3. Keep changes minimal and relevant to the task.
4. Do not overengineer.
5. Do not change unrelated files.
6. Explain your plan before risky edits.
7. After editing, explain exactly what changed.
8. Tell me how to verify the result.
9. Respect current permissions and approvals.
10. Do not commit, deploy, or make destructive changes unless I explicitly ask.
```

## Good Prompt for Git or Problem-Solving Mode

```text
Inspect this repository and current git state first.

Agent rules for this task:
- do not modify anything before diagnosis
- explain the current git state clearly
- identify conflicts or risky changes
- suggest the safest next step
- if permissions allow, help carefully
- show the final diff before any commit
```

This fits Codex’s built-in Git, diff, and review workflow.

## Good Prompt for Deployment or Config Mode

```text
Inspect this repository first.

Agent rules for this task:
- treat deployment as a risky task
- identify relevant files and configs first
- explain risks before editing
- keep the setup minimal and production-minded
- do not refactor unrelated application code
- explain every config change clearly
- do not deploy or restart anything unless explicitly asked
```

## If You Want These Rules to Persist Inside the Repo

The best long-term pattern is to place your durable instructions into `AGENTS.md`.

OpenAI documents that Codex reads `AGENTS.md` before work begins, making it the right place for repository-specific behavior rules.

That means this guide is the human-facing explanation, but the repo-facing version should eventually live in:

```text
AGENTS.md
```

## Compact Summary

A good AI coding agent should:

- inspect first
- follow repo rules
- stay within permissions
- keep changes small and relevant
- explain before and after
- help with Git and debugging
- use review tools
- avoid risky autonomous behavior by default
- leave final control to the human

That is what agent rules should mean in practice.

## Further Reading

- [Codex CLI](https://developers.openai.com/codex/cli)
- [Slash commands in Codex CLI](https://developers.openai.com/codex/cli/slash-commands)
- [Agent approvals & security](https://developers.openai.com/codex/agent-approvals-security)
- [Best practices](https://developers.openai.com/codex/learn/best-practices)
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md)
