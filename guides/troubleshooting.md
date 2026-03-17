# Troubleshooting: What to Do When Something Breaks

When you start coding with AI tools, things will break sometimes.

That is normal.

Most beginner problems are not caused by being bad at coding.
They are usually caused by one of these:

- wrong folder
- wrong terminal
- missing dependency
- wrong Node version
- auth or login issue
- permissions issue
- port already in use
- the app did not actually start
- messy Git state
- the AI agent does not have enough permissions to inspect or fix the issue

The goal of troubleshooting is not panic.
The goal is to identify:

- what layer is broken
- what command confirms it
- what the safest next action is

For Codex CLI specifically, OpenAI documents slash commands such as `/status`, `/diff`, `/review`, `/permissions`, `/new`, and `/compact`, which are useful for diagnostics, review, and session control.

## The First Troubleshooting Rule

When something breaks, do not start randomly reinstalling everything.

Start with a fast check of the current state.

Use these first:

```bash
pwd
ls
git status
node -v
npm -v
```

If you are using GitHub CLI too:

```bash
gh auth status
```

npm’s docs explicitly recommend `node -v` and `npm -v` to check your installed versions.

## Always Troubleshoot by Layers

The easiest way to debug is to think in layers.

### Layer 1: Environment

Questions:

- are you on the correct machine?
- are you in WSL, Ubuntu, macOS terminal, Linux shell, or a VPS?
- are Node and npm installed?
- is Git installed?
- is `gh` installed and authenticated?
- is Codex installed?

### Layer 2: Project Folder

Questions:

- are you in the correct project directory?
- does the repo actually exist here?
- is `package.json` present?
- did you run the install step?

### Layer 3: App Runtime

Questions:

- did the app actually start?
- is the correct port running?
- are there missing environment variables?
- is there a build error?

### Layer 4: Git State

Questions:

- are there uncommitted changes?
- are you on the wrong branch?
- is there a conflict?
- did a merge or rebase stop halfway?

### Layer 5: Agent Permissions

Questions:

- can the AI agent see the repo?
- can it read the right directories?
- can it run the command it needs?
- is it waiting for approval?

This layered approach fits Codex well because OpenAI’s docs expose model, approval policy, writable roots, token usage, diffs, and review state through commands like `/status`, `/diff`, `/review`, and `/permissions`.

## The Universal Quick-Check Sequence

If you are unsure what is broken, run this:

```bash
pwd
ls
git status
node -v
npm -v
```

Then if it is a Node project:

```bash
ls
cat package.json
npm install
npm run dev
```

Then if it is a GitHub repo:

```bash
git remote -v
gh auth status
```

npm’s docs describe `npm install` as the standard command that installs a package and the packages it depends on, with lockfiles respected when present.

## Problem 1: `command not found`

This usually means one of these:

- the tool is not installed
- the shell was not restarted
- your `PATH` is wrong
- you installed it in a different environment than the one you are using now

Examples:

- `node: command not found`
- `npm: command not found`
- `gh: command not found`
- `codex: command not found`

What to check:

```bash
which node
which npm
which git
which gh
which codex
```

If nothing is returned, the shell cannot find the command.

## Problem 2: Node or npm Is Broken or Missing

What to check first:

```bash
node -v
npm -v
```

If those fail, your Node setup is not ready.

npm officially recommends using a Node version manager where possible.

Safe fix mindset:

- do not install random versions from random tutorials
- use a version manager where possible
- keep one clean active version first

Good AI prompt:

```text
Inspect my environment first.
I think Node.js or npm is missing or broken.
Please tell me:
1. what commands I should run to confirm the issue,
2. what the likely cause is,
3. what the safest fix is for my OS,
4. what I should avoid doing.
Do not make assumptions before checking.
```

## Problem 3: Global npm Install Gives `EACCES` or Permission Errors

This is very common when someone tries to install a global package incorrectly.

Example:

```bash
npm install -g @openai/codex
```

and gets an `EACCES` error.

npm’s official guidance says the recommended fix is to reinstall npm using a Node version manager. Their fallback option on non-Windows systems is to change npm’s default global directory to a user-owned path.

Safe interpretation:

If you see `EACCES`, do not immediately start using:

```bash
sudo npm install -g ...
```

everywhere.

That often creates a mess.

Good prompt for the agent:

```text
Inspect my environment first.
I get an EACCES permission error when installing a global npm package.
Please:
1. explain why this happens,
2. check whether my Node/npm setup is likely using the wrong install method,
3. suggest the safest fix,
4. keep the solution beginner-friendly.
```

## Problem 4: Codex Does Not Start or Behaves Strangely

Codex CLI is installed via npm and is meant to run locally in the selected directory.

First checks:

```bash
codex --version
codex
```

If Codex starts but seems wrong, in Codex CLI use:

```text
/status
```

OpenAI’s slash-command docs say `/status` shows the active model, approval policy, writable roots, and current token usage.

If Codex seems stuck, OpenAI’s troubleshooting docs recommend:

- check whether Codex is waiting for an approval
- run a basic command like `git status`
- start a new thread with a smaller, more focused prompt

Good first recovery steps:

- check `/status`
- check whether it is waiting for approval
- run `git status`
- restart with a smaller prompt
- make sure you are in the correct project folder

## Problem 5: The Agent Cannot Read or Fix Enough of the Repo

Often the tool is not bad.
It just does not have enough permission or directory access.

In Codex CLI, check:

```text
/status
/permissions
```

On Windows native CLI, if extra read access is needed:

```text
/sandbox-add-read-dir C:\absolute\path
```

Important idea:

If you want the AI agent to help with:

- Git conflicts
- broken scripts
- multi-file refactors
- config repair
- dependency debugging

then it usually needs enough approvals and permissions to inspect files and run safe commands.

## Problem 6: It Works in Codex CLI but Not in the Codex App

OpenAI’s troubleshooting docs say the Codex app and Codex CLI use the same underlying Codex agent and configuration, but they might rely on different versions at a given time, and some experimental features may land in the CLI first.

Useful checks:

```bash
codex --version
```

and on macOS for the app-bundled version:

```bash
/Applications/Codex.app/Contents/Resources/codex --version
```

If the CLI works and the app does not, do not assume your whole setup is broken.
It may simply be a version or feature gap.

## Problem 7: Wrong Directory, Wrong Repo, Wrong Branch

This is one of the most common real problems.

You think the agent is editing your project, but you are actually in:

- the wrong folder
- the wrong clone
- the wrong subdirectory
- the wrong branch

First checks:

```bash
pwd
ls
git status
git branch
git remote -v
```

If anything looks wrong, fix that before doing anything else.

OpenAI’s troubleshooting guidance explicitly says that if commands behave differently than expected, validate the current directory and branch first.

## Problem 8: `gh` Is Installed but GitHub Access Still Fails

GitHub’s CLI docs say `gh auth login` is the standard authentication flow.

What to check:

```bash
gh auth status
gh auth login
gh repo view
```

Common reasons it fails:

- you are logged into the wrong GitHub account
- the repo remote points somewhere else
- you authenticated on one machine but are working on another
- your VPS is not authenticated yet

Good prompt:

```text
Inspect my GitHub CLI and git setup first.
I think gh is installed, but GitHub access is not working correctly.
Please:
1. tell me what commands to run,
2. explain whether this is an auth issue, repo issue, or remote issue,
3. suggest the safest fix.
```

## Problem 9: `npm install` Works, but `npm run dev` Fails

This usually means environment or app-level issues, not installer issues.

Common causes:

- missing `.env` values
- wrong script name
- unsupported Node version
- package installed but app config is incomplete
- port conflict
- syntax or build errors

First checks:

```bash
cat package.json
npm run
npm run dev
```

If the error mentions a port or server bind issue, inspect what is already running.
If it mentions missing environment values, check `.env.example` or project docs.

## Problem 10: Port Already in Use

This is extremely common with web projects.

Typical symptom:

- the app says port `3000` or another port is already in use
- the server does not start
- a previous dev server is still running in another terminal

What to do:

First identify whether another copy of your app is still running.

Then either:

- stop the old process
- use a different port temporarily
- close the old terminal if that is where the server is still running

Good prompt:

```text
Inspect the project and current environment first.
My dev server says the port is already in use.
Please:
1. explain what that means,
2. tell me how to confirm what is using the port,
3. suggest the safest fix,
4. keep the commands appropriate for my OS.
```

## Problem 11: Git Is Messy and You Do Not Know What Changed

This is exactly where the AI agent can help.

First checks:

```bash
git status
git diff
git log --oneline --graph --decorate -20
```

Inside Codex CLI, also use:

```text
/diff
/review
/status
```

Strong prompt:

```text
Inspect this repository and current git state first.

Please:
1. explain what changed,
2. group the changes into logical pieces,
3. identify anything suspicious,
4. suggest the safest next step,
5. do not edit anything yet.
```

## Problem 12: Merge Conflict or Rebase Conflict

This feels scary, but it is very normal.

Usually it means Git could not automatically reconcile overlapping changes.

First checks:

```bash
git status
git diff
```

Then ask the AI agent to inspect before editing.

Strong prompt:

```text
Inspect the repository and current git state first.

I think I have a merge or rebase conflict.
Please:
1. identify which files are conflicted,
2. explain the conflict in simple terms,
3. suggest the safest resolution,
4. if permissions allow, help resolve it carefully,
5. show me the final diff before I commit.
```

GitHub’s docs describe merge conflicts as competing changes Git cannot reconcile automatically, and their rebase docs explicitly say to resolve the conflict and then run `git rebase --continue`.

## Problem 13: The Agent Seems Stuck

OpenAI’s troubleshooting guidance says that if a thread appears stuck, you should:

- check whether Codex is waiting for an approval
- run a basic command like `git status`
- start a new thread with a smaller, more focused prompt

Practical recovery steps:

- check for a pending approval
- run `/status`
- run `git status`
- retry with a smaller, clearer prompt
- start a fresh thread if necessary

## Problem 14: The Terminal Itself Looks Broken

OpenAI’s troubleshooting page for the app says that if the terminal appears stuck, you can:

1. close the terminal panel
2. reopen it
3. rerun a basic command such as `pwd` or `git status`

Good first commands:

```bash
pwd
git status
ls
```

If these do not behave as expected, your issue may be the terminal or session, not the repo.

## Problem 15: Long Session, Too Much Context, Confusing Answers

Codex CLI documents:

- `/compact` to summarize the visible conversation and free context
- `/new` to start a fresh conversation in the same session

Good recovery tools inside Codex CLI:

```text
/compact
/new
/status
```

Use this when:

- the session got too long
- the agent starts mixing tasks
- replies become less focused
- you want a clean reset without losing the repo itself

## The Best Troubleshooting Mindset

When something breaks:

Do not do this:

- reinstall random tools immediately
- run dangerous commands blindly
- delete folders in panic
- assume the AI agent just sucks
- assume the repo is ruined

Do this instead:

- identify the broken layer
- run 3 to 5 confirming commands
- inspect the actual error text
- ask the AI agent to inspect before modifying
- give it enough permissions if appropriate
- review the result before continuing

That is the professional workflow.

## The Best Universal Troubleshooting Prompt

```text
Inspect my current environment and repository first.

I need troubleshooting help.
Please do the following:
1. identify what layer is likely broken (environment, project setup, app runtime, git state, or permissions),
2. tell me what commands I should run to confirm the issue,
3. explain the likely cause in simple terms,
4. suggest the safest fix,
5. avoid making changes until the diagnosis is clear.
```

## The Best Troubleshooting Prompt for Codex Specifically

```text
Inspect this repository and current session state first.

Please:
1. explain the current repo state,
2. explain the current git state,
3. tell me whether there may be a permissions or approvals issue,
4. suggest the smallest diagnostic steps first,
5. only propose fixes after the diagnosis is clear.
```

Inside Codex CLI, combine that with:

```text
/status
/diff
/review
/permissions
```

because those commands are explicitly documented for session diagnostics, diff inspection, review, and approval control.

## Practical Command Block

```bash
pwd
ls
git status
git diff
git log --oneline --graph --decorate -20
node -v
npm -v
npm install
npm run dev
gh auth status
codex --version
```

And inside Codex CLI:

```text
/status
/diff
/review
/permissions
/new
/compact
```

## If You Need Logs or Want to Report a Codex Issue

OpenAI’s troubleshooting docs say you can submit feedback from the composer, and they list log and session locations including:

- app logs on macOS under `~/Library/Logs/com.openai.codex/...`
- session transcripts under `$CODEX_HOME/sessions`
- default session storage under `~/.codex/sessions`

They also explicitly advise reviewing logs before sharing them to ensure they do not contain sensitive information.

That means if something looks like a real Codex bug:

- gather the version
- gather the exact error
- review the logs first
- avoid pasting secrets
- then report it properly

## Compact Summary for Beginners

If something breaks:

- check the folder
- check Git state
- check Node and npm
- check `gh` auth
- check whether the app really started
- check whether Codex is waiting for approval
- use `/status`, `/diff`, `/review`, and `/permissions`
- ask the AI agent to diagnose before editing
- fix one layer at a time

That is the clean way to troubleshoot.

## Further Reading

- [npm: Downloading and installing Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm/)
- [npm: Resolving EACCES permissions errors when installing packages globally](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally/)
- [npm install](https://docs.npmjs.com/cli/v11/commands/npm-install/)
- [GitHub CLI quickstart](https://docs.github.com/en/github-cli/github-cli/quickstart)
- [gh auth status manual](https://cli.github.com/manual/gh_auth_status)
- [Resolving a merge conflict using the command line](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [Resolving merge conflicts after a Git rebase](https://docs.github.com/en/get-started/using-git/resolving-merge-conflicts-after-a-git-rebase)
- [git merge documentation](https://git-scm.com/docs/git-merge)
- [Codex CLI](https://developers.openai.com/codex/cli)
- [Slash commands in Codex CLI](https://developers.openai.com/codex/cli/slash-commands)
- [Codex app commands](https://developers.openai.com/codex/app/commands)
- [Codex app troubleshooting](https://developers.openai.com/codex/app/troubleshooting)
- [Codex best practices](https://developers.openai.com/codex/learn/best-practices)
- [Agent approvals and security](https://developers.openai.com/codex/agent-approvals-security)
