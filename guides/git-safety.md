# Git Safety: How to Avoid Losing Work

One of the biggest beginner mistakes is not writing bad code.

It is losing track of changes.

That is why Git matters from day one.

Git helps you:

- save progress
- go back to a working state
- understand what changed
- work safely with an AI coding agent
- recover from mistakes
- resolve conflicts in a controlled way

If you are using an AI coding workflow, Git is not optional.
It is your safety system.

## What Git Safety Really Means

Git safety means:

- commit often
- make small changes
- do not mix unrelated edits
- inspect changes before committing
- use branches when needed
- do not panic when conflicts happen
- make it easy to recover

A safe workflow is not about being perfect.
It is about making mistakes recoverable.

## The Golden Rule

If your current work matters, commit before doing risky changes.

Examples of risky changes:

- large refactors
- dependency upgrades
- merge operations
- rebase operations
- letting an AI agent edit many files at once
- trying a new framework setup
- deleting folders
- changing config files

Before risky work, do this:

```bash
git status
git add .
git commit -m "Save progress before risky change"
```

That one habit can save hours.

## The Safest Beginner Workflow

Use this pattern:

1. Make one small change.
2. Test it.
3. Inspect the diff.
4. Commit it.
5. Continue.

Example:

```bash
git status
git diff
git add .
git commit -m "Add homepage hero section"
```

Small commits are easier to understand and easier to undo.

## Always Check These Three Commands

These are your core Git safety commands:

Check current state:

```bash
git status
```

See what changed:

```bash
git diff
```

See commit history:

```bash
git log --oneline --graph --decorate -20
```

If you are confused, run these first.

## Install GitHub CLI Too, Not Just Git

If you work with GitHub repositories, install GitHub CLI (`gh`) in addition to Git.

GitHub documents `gh` as the command-line tool for GitHub workflows, and their quickstart covers commands such as:

- `gh auth login`
- `gh status`
- `gh repo view`
- `gh repo create`
- `gh pr create`

GitHub’s docs also note that when you choose HTTPS during `gh auth login`, GitHub CLI can store Git credentials for HTTPS Git operations like `git push` and `git pull`.

## Why `gh` Is Useful

With `gh`, you can:

- authenticate to GitHub
- create repositories
- view repositories
- create pull requests
- inspect GitHub status from the terminal
- work more comfortably on WSL, VPS, and remote servers

This is especially useful on:

- VPS servers
- remote development machines
- WSL
- terminal-heavy workflows
- AI agent workflows

## Install and Authenticate `gh`

After installing Git, also install GitHub CLI using the official instructions for your OS.

Then authenticate:

```bash
gh auth login
```

Useful checks after login:

```bash
gh auth status
gh repo view
gh status
```

## Recommended Setup on a Server

If you are developing on a VPS or remote server, install:

- Git
- GitHub CLI (`gh`)
- your coding agent

That way you can:

- clone repos
- push safely
- inspect pull requests
- create branches
- let the AI agent help inside a proper Git workflow

## Good First Git Safety Habits

### 1. Commit Early

Do not wait until the project is huge.

Good:

```bash
git add .
git commit -m "Initial project setup"
```

### 2. Commit After Each Meaningful Step

Good examples:

```bash
git commit -m "Add basic homepage layout"
git commit -m "Add API health route"
git commit -m "Fix mobile navbar spacing"
```

### 3. Keep Commits Focused

Do not combine everything into one giant commit.

Bad:

```text
fixed stuff
```

Better:

```text
Add initial Next.js project structure
```

### 4. Look at the Diff Before Commit

```bash
git diff
```

This helps you catch:

- accidental deletions
- secrets
- broken config edits
- unrelated file changes

### 5. Use Branches for Experiments

If you want to try something risky:

```bash
git switch -c experiment/new-layout
```

Or, on older Git:

```bash
git checkout -b experiment/new-layout
```

This keeps your main branch cleaner.

## Before Letting the AI Agent Make Bigger Changes

Before asking the AI agent to refactor, upgrade, or restructure files:

- run `git status`
- commit current work
- make sure the repo is in a known good state
- then let the agent work

Good safety prompt:

```text
Before making changes, inspect the repository and current git state.
Then explain your plan.
Make small controlled edits.
Do not change unrelated files.
After changes, summarize exactly what changed.
```

That makes the workflow much safer.

## Your AI Agent Can Help With Git Problems Too

Your coding agent is not only for writing code.

It can also help you with:

- confusing Git state
- broken branches
- merge conflicts
- rebase conflicts
- bad diffs
- accidental changes
- PR review preparation

OpenAI’s Codex docs explicitly describe Codex as a coding agent that can inspect a repository, edit files, run commands, execute tests, and help review changes before you commit or push.

## Approvals and Permissions Matter

If you want Codex to help more actively with Git operations, shell commands, or conflict resolution, you need the right approval mode and sandbox settings.

OpenAI’s current Codex docs describe approval modes and document the `/permissions` command in interactive sessions.

A safe beginner default is:

- start with the default permissions
- keep approval and sandboxing tight by default
- loosen them only for trusted repositories or clearly needed workflows

OpenAI’s best-practices guide explicitly recommends starting with default permissions and only loosening access once the need is clear.

## Practical Codex Advice

If you are using Codex and want help with Git problems:

- keep the repo open in the correct working directory
- make sure Codex can read the files it needs
- allow the right level of approvals when appropriate
- do not give dangerous full access casually

Codex also supports inline review and slash commands such as `/review`, including review of uncommitted changes, commits, and base-branch diffs.

## Good Prompt for Git Inspection

```text
Inspect this repository and its current git state first.

Please:
1. explain the current git status,
2. explain whether there are uncommitted changes,
3. identify any risky or confusing changes,
4. suggest the safest next step,
5. do not modify anything yet.
```

This is a very good first prompt when something feels wrong.

## Good Prompt for Messy Changes

```text
Inspect the repository and current git diff.

Please:
1. summarize what changed,
2. group the changes into logical categories,
3. identify anything suspicious or unrelated,
4. suggest how these changes should be split into commits,
5. do not edit files yet.
```

This is useful when the repo became messy.

## Good Prompt for Merge Conflicts

```text
Inspect the repository and current git state first.

I think I have a merge conflict.
Please:
1. explain which files are in conflict,
2. explain the conflicting changes in simple terms,
3. suggest the safest resolution,
4. if permissions allow, help resolve the conflicts carefully,
5. show me the final diff before I commit.
```

First inspect, then explain, then resolve.

## Good Prompt for Rebase Conflicts

```text
Inspect the repository and current git state first.

I think a rebase stopped because of conflicts.
Please:
1. identify which files are conflicted,
2. explain what each side is trying to do,
3. suggest the cleanest resolution,
4. if permissions allow, help resolve them,
5. tell me what command I should run next.
```

## What Merge Conflicts Actually Mean

A merge conflict does not mean Git is broken.

It means two branches changed the same area in incompatible ways and Git needs help deciding what the final result should be.

GitHub’s docs describe this as competing changes Git cannot reconcile automatically.

That means:

- conflict does not equal disaster
- conflict is a decision point

Stay calm and inspect carefully.

## Basic Merge Conflict Flow

Typical flow:

1. Try merge or pull.
2. Git reports conflict.
3. Inspect conflicted files.
4. Edit and resolve.
5. Mark resolved.
6. Continue merge.
7. Commit if needed.

Typical commands:

```bash
git status
git add .
git merge --continue
```

Git’s official documentation states that after a merge stops due to conflicts, you can conclude it with `git merge --continue`.

## Basic Rebase Conflict Flow

If a rebase stops because of conflicts:

```bash
git status
git add .
git rebase --continue
```

GitHub’s docs explicitly say that after resolving the problem, you run `git rebase --continue`. They also document `git rebase --abort` and `git rebase --skip` as the other two choices.

## When the AI Agent Is Especially Useful

The AI agent is especially helpful when:

- you do not understand the diff
- many files are involved
- conflict markers are confusing
- you need help choosing which side to keep
- you want a safer explanation before touching anything

This is one of the best uses of a coding agent:
not replacing judgment, but helping you understand the state faster.

## Very Important Limitation

Even if the AI agent helps resolve conflicts, you should still review the result yourself.

Use:

```bash
git diff
git status
```

And if possible, run the project or tests after resolution.

OpenAI’s best-practices guide explicitly recommends not stopping at code generation: ask Codex to run checks, confirm the result, and review the work before you accept it.

## Useful Commands to Remember

### Basic Safety

```bash
git status
git diff
git log --oneline --graph --decorate -20
```

### Save Progress

```bash
git add .
git commit -m "Save current progress"
```

### New Branch

```bash
git switch -c feature/my-change
```

### Check Remote

```bash
git remote -v
```

### GitHub CLI

```bash
gh auth login
gh auth status
gh repo view
gh status
gh pr create
```

## Recommended Compact Advice

If you want the short version:

- use Git from day one
- install `gh` too, not only Git
- commit before risky changes
- inspect diffs often
- use branches for experiments
- let your AI agent inspect Git problems before you panic
- give the agent enough approvals when appropriate
- still review the final diff yourself

That is the real beginner-safe workflow.

## Ready-to-Copy Prompt for AI-Assisted Git Safety

```text
Inspect this repository and current git state first.

Please:
1. explain the current status,
2. summarize any uncommitted changes,
3. identify any conflicts or risky changes,
4. suggest the safest next step,
5. if permissions allow, help me fix the issue carefully,
6. show me the final diff before any commit.
```

## If the Repo Is Already Confusing or Broken

Continue here:

- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)

## Further Reading

- [GitHub CLI quickstart](https://docs.github.com/en/github-cli/github-cli/quickstart)
- [gh auth status manual](https://cli.github.com/manual/gh_auth_status)
- [Resolving a merge conflict using the command line](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [Resolving merge conflicts after a Git rebase](https://docs.github.com/en/get-started/using-git/resolving-merge-conflicts-after-a-git-rebase)
- [git merge documentation](https://git-scm.com/docs/git-merge)
- [Codex CLI](https://developers.openai.com/codex/cli)
- [Codex best practices](https://developers.openai.com/codex/learn/best-practices)
- [Using Codex with your ChatGPT plan](https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan)
