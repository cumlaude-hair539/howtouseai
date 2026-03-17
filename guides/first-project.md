# First Project: Start Small and Finish Something

This guide covers one of the most important rules in AI coding:

**Do not start with a giant project first.**

Your first project should be:

- small
- clear
- easy to verify
- easy to finish
- useful enough to teach the workflow

The goal of your first project is not to build your dream platform in one day.

The goal is to learn how to work with:

- your environment
- your editor
- Git
- your coding agent
- small prompt loops
- review and correction

If you can finish one small project correctly, your next projects become much easier.

## What Makes a Good First Project

A good first project is something that:

- can be explained in 1 to 3 sentences
- has a clear result
- can be built in a few steps
- can be tested quickly
- does not require huge architecture first

Good first projects:

- a simple personal webpage
- a terminal to-do app
- a notes app
- a basic calculator
- a small API that returns JSON
- a Markdown preview tool
- a habit tracker
- a simple file organizer script

Bad first projects:

- "build a startup"
- "make a full social network"
- "make a full MMORPG"
- "build an enterprise SaaS platform"
- "clone Discord, Instagram, and Stripe in one week"

Start small.
Finish small.
Then scale.

## The Right Mindset

Use this sequence:

1. Ask the agent to inspect the repository.
2. Ask it to propose a very small first version.
3. Ask it to create a step-by-step plan.
4. Ask it to implement only the first step.
5. Test that step.
6. Commit progress.
7. Continue in small loops.

This is much better than saying:

```text
Build me the final complete product.
```

That usually creates confusion, messy structure, and low-quality output.

## Very Good Default First Projects

### Option A: Simple Personal Webpage

Build a very small website with:

- a title
- a short description
- one button
- a clean layout

Why this is a good first project:

- visually easy to verify
- simple file structure
- quick to improve
- teaches HTML, CSS, JavaScript, or React basics
- good for learning how to ask the agent for controlled changes

### Option B: Terminal To-Do App

Build a command-line app that can:

- add a task
- list tasks
- mark a task as done

Why this is a good first project:

- simple logic
- no UI complexity
- fast to test
- teaches structure and iteration
- great for learning agent workflow

### Option C: Tiny JSON API

Build a tiny server with one route:

`GET /hello`

It returns:

```json
{ "message": "Hello world" }
```

Then add:

`GET /health`

It returns:

```json
{ "ok": true }
```

Why this is good:

- very small
- easy to test
- introduces backend basics
- easy to expand later

## Recommended Workflow for Your First Project

### Step 1: Create or Open Your Project Folder

If you have not done it yet:

```bash
mkdir -p ~/projects
cd ~/projects
mkdir my-first-ai-project
cd my-first-ai-project
git init
```

Create a `README`:

```bash
echo "# My First AI Project" > README.md
```

Commit it:

```bash
git add .
git commit -m "Initial commit"
```

### Step 2: Open the Project in Your Editor

If you are using VS Code:

```bash
code .
```

### Step 3: Launch Your Coding Agent

Example:

```bash
codex
```

### Step 4: Start With an Inspection Prompt

Your first prompt should usually be something like this:

```text
Inspect this repository first.
Explain the current structure.
Then suggest one very small beginner-friendly project I can build here.
Do not build everything at once.
Start with the smallest clean version.
```

This matters because it tells the agent to:

- inspect first
- think before changing files
- keep scope small
- avoid giant uncontrolled output

### Step 5: Implement Only the First Step

A very strong first prompt is:

```text
Inspect this repository first.

Then do the following:
1. Explain the current structure in simple terms.
2. Suggest one very small project that is appropriate for a beginner.
3. Break it into tiny implementation steps.
4. Start only with step 1.
5. Before writing code, explain what files you plan to create or change.
6. Keep the implementation minimal and clean.
```

This prompt usually creates much better results than vague prompts.

### Step 6: Test What Changed

Always try to run what was built.

Examples:

```bash
npm install
npm run dev
```

or:

```bash
node index.js
```

or:

```bash
python main.py
```

Do not assume it works just because the agent wrote it.

### Step 7: Commit Progress

Commit small milestones.

Examples:

```bash
git add .
git commit -m "Set up initial project structure"
git add .
git commit -m "Add first working page"
git add .
git commit -m "Add basic styling"
```

## Good Starter Prompts You Can Copy

### Prompt 1: Safe Universal Starter

```text
Inspect this repository first.
Explain the current structure in simple terms.
Then suggest one very small first project I can build here.
Break it into tiny steps and implement only step 1.
Before writing code, explain your plan.
After writing code, explain what changed and how I can test it.
```

### Prompt 2: Simple Webpage

```text
Inspect this repository first.

I want my first project to be a very small personal webpage.
Please:
1. Explain the current repository structure.
2. Propose the smallest clean version of this project.
3. Break the work into tiny steps.
4. Implement only the first step.
5. Keep the design simple and clean.
6. After implementation, explain how I can run it.
```

### Prompt 3: Terminal To-Do App

```text
Inspect this repository first.

I want to build a very small terminal to-do app.
Please:
1. Explain the current repository structure.
2. Propose the smallest clean version.
3. Break it into tiny steps.
4. Implement only step 1.
5. Keep the code beginner-friendly.
6. Explain how I can run and test it.
```

### Prompt 4: Tiny API

```text
Inspect this repository first.

I want to build a tiny API with:
- GET /hello
- GET /health

Please:
1. Explain the current structure.
2. Suggest the smallest clean implementation.
3. Break it into very small steps.
4. Implement only the first step.
5. Explain how I can run the server and test the endpoints.
```

### Prompt 5: Refuse Overengineering

```text
Do not overengineer this.
Do not add unnecessary abstractions.
Do not add extra tools unless truly needed.
Prefer the smallest clean version that works.
```

## How to Work With the Agent Correctly

A coding agent works much better when you do small, controlled loops.

Good pattern:

- inspect
- plan
- implement one step
- review
- test
- commit
- continue

Bad pattern:

- ask for everything at once
- do not review
- do not test
- do not commit
- get lost in broken output

## Always Ask the Agent to Explain Changes

Do not only ask for code.
Also ask for explanation.

Good examples:

- "Explain what each file does."
- "Explain this like I am a beginner."
- "Before changing code, tell me the plan."
- "After editing, explain exactly what changed."

This helps you actually learn instead of only copying output.

## How to Review the Result

After the agent changes files, check:

- Did it create too many files?
- Did it add unnecessary complexity?
- Can you explain what each file is for?
- Can the project actually run?
- Did it follow your scope?
- Is the code simple enough?

If something feels too big, say:

```text
This is too complex for a first project.
Please simplify it.
Remove anything unnecessary.
Keep only the minimal version.
```

That is a very good correction prompt.

## How to Avoid Common First-Project Mistakes

### Mistake 1: Starting Too Big

Bad:

```text
Build me a full SaaS platform.
```

Better:

```text
Build the smallest first version of a landing page with one button and one section.
```

### Mistake 2: Letting the Agent Create Too Much Architecture

Sometimes the agent tries to be helpful by creating:

- too many folders
- too many abstractions
- unnecessary libraries
- premature optimization

If that happens, say:

```text
Reduce the architecture.
This is only a first project.
Prefer the simplest implementation that works.
```

### Mistake 3: Not Testing After Changes

Always run what was built.

### Mistake 4: Making Too Many Edits Before Committing

Commit small milestones so recovery stays easy.

## A Very Safe First-Project Loop

Use this loop again and again:

1. Ask for inspection.
2. Ask for a tiny plan.
3. Ask for one implementation step.
4. Run or test it.
5. Commit progress.
6. Continue with the next smallest step.

This loop is extremely effective.

## What to Do After the First Project Works

Once your first project runs correctly, your next tasks can be:

- improve the layout
- add one feature
- clean up file structure
- add basic tests
- deploy it
- get your own domain
- improve your Git workflow
- connect GitHub
- ask the agent for a small refactor
- create version 2

That is how real progress happens:
not from chaos, but from small working steps.

If you want to connect a real domain next, continue here:

- [How to Get a Domain and Connect It Through Cloudflare](./how-to-get-domain.md)

If you want to work more safely before bigger changes, continue here:

- [Git Safety: How to Avoid Losing Work](./git-safety.md)

If something breaks while you are learning, continue here:

- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)

If you want to get better results from the agent itself, continue here:

- [Prompting Basics: How to Ask Your AI Coding Agent Correctly](./prompting-basics.md)

If you want a cleaner daily process for working with the agent, continue here:

- [Workflow Rules: How to Work With an AI Coding Agent Without Creating Chaos](./workflow-rules.md)

## Recommended Project Progression

A good progression looks like this:

1. Make something tiny that works.
2. Improve it slightly.
3. Refactor a little.
4. Add one more feature.
5. Deploy or publish it.
6. Start a slightly bigger project.

This is the correct way to build skill.

## Optional: Test Your Site From Your Phone

If your site is running locally and you want to open it from your phone, one beginner-friendly option is Cloudflare Tunnel with `cloudflared`.

For a fast temporary preview, you can expose your local dev server like this:

```bash
cloudflared tunnel --url http://localhost:3000
```

Replace `3000` with the actual port your app is using.

Cloudflare documents Quick Tunnels as a testing and development workflow, not a production setup:

[Cloudflare Quick Tunnels](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/do-more-with-tunnels/trycloudflare/)

If you want a more serious setup later, ask your coding agent to explain:

- what is for development
- what is for production
- how to expose your app safely
- how to keep the setup simple

Example prompt:

```text
Inspect this repository first.

I want a clean local development setup that I can open from my phone.
Please:
1. set up the project for local development,
2. explain how to expose it with cloudflared,
3. explain what is for development and what is for later production use,
4. keep everything simple and beginner-friendly.
```

## Quick Checklist

Before moving on, make sure you can do these:

- create a project folder
- initialize Git
- open the project in your editor
- start your coding agent
- ask the agent to inspect first
- ask for a tiny plan
- implement one small step
- test the result
- commit progress

If you can do that, you already have the foundation.

## Final Rule

Your first project should teach you this habit:

**small scope, clear prompt, one step, test, commit, repeat**

That habit matters more than the exact project.
