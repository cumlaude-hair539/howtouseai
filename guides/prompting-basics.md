# Prompting Basics: How to Ask Your AI Coding Agent Correctly

A lot of people think AI coding works like magic.

It does not.

The quality of the result depends heavily on how you ask.

A coding agent works much better when your prompt is:

- clear
- scoped
- structured
- realistic
- grounded in the actual repository

OpenAI’s Codex docs describe Codex as a coding agent that can read, change, and run code in the selected directory, and its best-practices docs emphasize controlled workflows, review, and verification instead of blind generation.

That means a vague prompt does not just create a vague answer.
It can create vague actions.

So prompting well is one of the biggest skills in AI coding.

## The Main Rule

Do not prompt like you are making a wish.
Prompt like you are giving a technical task.

Bad:

```text
Make me an amazing app.
```

Better:

```text
Inspect this repository first.
Then explain the current structure.
Then build the smallest possible version of a simple homepage with a title, description, and one button.
Keep the implementation minimal.
Explain what files you changed and how I can run it.
```

That second prompt is better because it defines:

- what to do first
- what to build
- how large it should be
- what constraints to follow
- what output you want back

OpenAI’s prompting guidance consistently rewards explicit instructions, concrete constraints, and clear completion criteria.

## The Best Beginner Prompt Structure

A strong beginner prompt usually has these parts.

### 1. Tell It to Inspect First

This is one of the most important habits.

Good example:

```text
Inspect this repository first.
Explain the current structure before making changes.
```

Why this matters:

Codex is designed to work inside the selected directory and adapt to the existing project structure and conventions.

### 2. Define the Exact Task

Bad:

```text
Improve the app.
```

Better:

```text
Add a simple hero section to the homepage with:
- a title
- a short paragraph
- one button
```

The more concrete the task, the better the result.

### 3. Set Scope Limits

This is critical.

If you do not define scope, the agent may overbuild.

Good examples:

- keep the implementation minimal
- do not overengineer
- do not add unnecessary dependencies
- only implement step 1

### 4. Ask for Explanation

This is especially useful for learning.

Good examples:

- explain what files you changed
- explain this in beginner-friendly terms
- explain how I can run and test it

### 5. Ask for Review Before Risky Action

For example:

```text
Before making changes, explain your plan.
```

or:

```text
Do not modify anything yet.
First inspect and propose the safest next step.
```

This is especially useful for Git problems, refactors, infra changes, and anything that touches many files.

## The Best Universal Starter Prompt

Here is a strong default prompt:

```text
Inspect this repository first.

Please:
1. explain the current structure,
2. identify the relevant files for this task,
3. propose the smallest clean implementation,
4. explain your plan before editing,
5. make only the necessary changes,
6. explain what changed,
7. explain how I can run and test it.
```

This works well because it forces the agent into a safer workflow:

`inspect -> plan -> implement -> explain`

That matches OpenAI’s Codex best-practices guidance, which emphasizes review and verification rather than one-shot generation.

## The Five Biggest Prompting Mistakes

### Mistake 1: Asking for Too Much at Once

Bad:

```text
Build the full production-ready platform.
```

This usually creates:

- too much code
- too many assumptions
- unnecessary architecture
- confusing output

Better:

```text
Build the smallest first version only.
Start with one page and one working feature.
```

### Mistake 2: Not Telling the Agent What to Inspect

Bad:

```text
Add authentication.
```

Better:

```text
Inspect the repository first.
Find the existing auth-related files and current app structure.
Then propose the smallest clean way to add authentication.
Do not change anything yet.
```

Grounding the agent in the current repository is one of the biggest quality levers.

### Mistake 3: Leaving Scope Undefined

Bad:

```text
Make it better.
```

Better:

```text
Improve only the mobile navbar spacing.
Do not change colors, typography, routing, or desktop layout.
```

### Mistake 4: Not Saying What Done Means

Bad:

```text
Fix the bug.
```

Better:

```text
Fix the bug where the button does nothing when clicked.
Done means:
- clicking the button triggers the existing submit handler,
- the page no longer throws an error,
- no unrelated files are changed.
```

### Mistake 5: Letting the Session Become Chaotic

If the conversation becomes too long or too mixed, quality drops.

Codex documents session-control commands like `/compact`, `/fork`, and `/resume` for managing long-running work.

So if the thread gets messy, use:

```text
/compact
```

or split the work into a cleaner follow-up thread.

## The Best Prompt Pattern for Coding Tasks

Use this structure:

```text
Inspect this repository first.

Task:
[clear task]

Constraints:
[scope limits]

Requirements:
[what must be true]

Before editing:
[what to analyze first]

After editing:
[what to explain or verify]
```

Example:

```text
Inspect this repository first.

Task:
Add a simple homepage hero section.

Constraints:
- keep it minimal
- do not add new dependencies
- do not refactor unrelated files

Requirements:
- title
- short paragraph
- one button

Before editing:
Explain which files you plan to change and why.

After editing:
Explain what changed and how I can run the project.
```

This is one of the safest prompt formats for beginners.

## Good Prompt Types You Should Use Often

### 1. Inspection Prompt

Use this when you do not understand the repo.

```text
Inspect this repository first.
Explain the structure in simple terms.
Which files are most important?
Which files are relevant to [task]?
Do not change anything yet.
```

### 2. Planning Prompt

Use this before implementation.

```text
Inspect the repository first.
Then break this task into tiny implementation steps.
Keep the plan minimal and practical.
Do not edit files yet.
```

### 3. Implementation Prompt

Use this after the plan is clear.

```text
Implement only step 1.
Keep the implementation minimal.
Do not change unrelated files.
Explain what changed after you finish.
```

### 4. Refactor Prompt

Use this when code works but needs cleanup.

```text
Inspect this file first.
Refactor it for clarity without changing behavior.
Do not change public API or file structure unless necessary.
Explain the refactor clearly.
```

### 5. Debugging Prompt

Use this when something is broken.

```text
Inspect the repository and current error first.

Please:
1. explain the likely cause,
2. identify the relevant files,
3. suggest the safest fix,
4. do not modify anything until the diagnosis is clear.
```

### 6. Git or Conflict Prompt

Use this when Git state is messy.

```text
Inspect the repository and current git state first.

Please:
1. explain what changed,
2. identify conflicts or risky changes,
3. suggest the safest next step,
4. if permissions allow, help resolve it carefully,
5. show me the final diff before commit.
```

Codex’s official workflow includes built-in tools like `/diff` and `/review`, which are especially useful here.

## A Very Important Habit: Ask for the Smallest Next Step

This is one of the best possible prompting habits.

Bad:

```text
Build the whole thing.
```

Better:

```text
What is the smallest useful next step?
Implement only that step.
```

This prevents the agent from jumping too far ahead.

OpenAI’s best-practices guidance for Codex stresses better results from controlled, iterative workflows rather than oversized one-shot tasks.

## Good Examples vs Bad Examples

### Example 1: Webpage

Bad:

```text
Make me a beautiful website.
```

Better:

```text
Inspect this repository first.

Build the smallest clean landing page with:
- a headline
- a short description
- one CTA button

Constraints:
- keep it minimal
- no new dependencies
- no animations yet

After editing:
Explain what changed and how I can view it locally.
```

### Example 2: Bug Fix

Bad:

```text
Fix this.
```

Better:

```text
Inspect this repository and the error first.

The problem:
The submit button does nothing.

Please:
1. identify the relevant files,
2. explain the likely cause,
3. suggest the safest fix,
4. implement only the minimal fix,
5. explain how I can verify it.
```

### Example 3: Feature Request

Bad:

```text
Add auth.
```

Better:

```text
Inspect the repository first.

I want to add the smallest possible authentication foundation.

Please:
1. explain the current auth-related structure,
2. propose the minimal clean approach,
3. break it into tiny steps,
4. implement only step 1,
5. avoid overengineering.
```

## Tell the Agent What Not to Do

This is very powerful.

You can and should say things like:

- do not overengineer
- do not add unnecessary dependencies
- do not refactor unrelated files
- do not change project structure unless necessary
- do not modify anything until you explain the plan

Explicit constraints usually improve adherence and reduce drift.

## Tell the Agent How to Explain Things

If you are a beginner, say so directly.

Examples:

- explain this in beginner-friendly language
- use simple terms and avoid jargon where possible
- after editing, explain what each changed file does

This often makes the experience dramatically better.

## Use Session Controls When Needed

If you are using Codex CLI, slash commands can make prompting much more effective.

Useful documented commands include:

- `/status`
- `/diff`
- `/review`
- `/permissions`
- `/compact`
- `/fork`
- `/resume`

Practical use:

Check the current session:

```text
/status
```

Review current changes:

```text
/diff
/review
```

Adjust permissions:

```text
/permissions
```

Clean up a long thread:

```text
/compact
```

Split work into a cleaner parallel thread:

```text
/fork
```

These commands are official productivity tools for managing longer Codex sessions.

## Reusable Prompt Templates Are a Good Idea

If you find a prompt pattern that works well, save it somewhere you actually use:

- a notes file
- a snippets document
- a repo guide
- your own prompt library

Good reusable categories:

- inspect repo
- debug issue
- split work into small steps
- review diff
- draft PR summary

The important part is consistency, not where you store the template.

## The Best Beginner Workflow for Prompting

Use this loop:

1. Inspect

```text
Inspect this repository first.
Explain the current structure.
Do not change anything yet.
```

2. Plan

```text
Break this task into tiny steps.
Keep it minimal.
```

3. Implement one step

```text
Implement only step 1.
Do not change unrelated files.
```

4. Review

```text
Explain what changed.
Show the relevant files and why.
```

5. Verify

```text
Explain how I can run and test this.
```

This loop is simple, safe, and scales well.

## Ready-to-Copy Starter Prompts

### Universal Starter

```text
Inspect this repository first.

Please:
1. explain the current structure,
2. identify the relevant files,
3. propose the smallest clean implementation,
4. explain your plan before editing,
5. implement only the necessary changes,
6. explain what changed,
7. explain how I can run and test it.
```

### Beginner Learning Mode

```text
Inspect this repository first.

I am learning, so please:
- keep the solution simple,
- avoid unnecessary abstractions,
- explain your reasoning in beginner-friendly language,
- implement only one small step at a time.
```

### Minimal Feature Request

```text
Inspect this repository first.

Task:
Add [feature].

Constraints:
- keep it minimal
- no unnecessary dependencies
- no unrelated refactors

Before editing:
Explain the relevant files and your plan.

After editing:
Explain what changed and how I can test it.
```

### Safe Debugging Prompt

```text
Inspect this repository and the current error first.

Please:
1. explain the likely cause,
2. identify the relevant files,
3. suggest the safest fix,
4. do not modify anything until the diagnosis is clear.
```

### Safe Git-Help Prompt

```text
Inspect this repository and current git state first.

Please:
1. explain the current status,
2. summarize the changes,
3. identify anything risky or conflicted,
4. suggest the safest next step,
5. if permissions allow, help carefully,
6. show the final diff before commit.
```

## Compact Summary

Good prompts usually do these things:

- tell the agent to inspect first
- define one clear task
- limit scope
- specify constraints
- define what done means
- ask for explanation
- ask for verification
- break large work into small steps

That is the difference between chaotic AI coding and controlled AI coding.

## Further Reading

- [Codex CLI](https://developers.openai.com/codex/cli)
- [Codex best practices](https://developers.openai.com/codex/learn/best-practices)
- [Slash commands in Codex CLI](https://developers.openai.com/codex/cli/slash-commands)
- [Codex app commands](https://developers.openai.com/codex/app/commands)

If you want the next layer after prompting, continue here:

- [Workflow Rules: How to Work With an AI Coding Agent Without Creating Chaos](./workflow-rules.md)
