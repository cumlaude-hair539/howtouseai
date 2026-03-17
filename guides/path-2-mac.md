# Path 2: I Have a Mac

If you are on macOS, the recommended path is:

1. Install Homebrew.
2. Install Node.js.
3. Install Git.
4. Install VS Code.
5. Install your coding agent.
6. Create a working folder.
7. Start your first project.

## What You Are Setting Up

By the end of this guide, you should have:

- Homebrew installed
- Node.js installed
- Git installed
- VS Code installed
- a working projects folder
- your coding agent ready to use

## Step 1: Install Homebrew

Open the Terminal app and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, verify:

```bash
brew --version
```

## Step 2: Install Node.js

The recommended beginner path is:

```bash
brew install node@22
```

Then verify:

```bash
node -v
npm -v
```

If your shell does not immediately see it, restart Terminal.

## Step 3: Install Git

Many Macs already have Git, but you can install or update it with Homebrew if needed:

```bash
brew install git
```

Verify:

```bash
git --version
```

Optional but recommended:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Step 4: Install VS Code

Install VS Code from the official website:

[VS Code](https://code.visualstudio.com/)

After that, open VS Code and make sure the `code` shell command is available.

Then you can open any current folder with:

```bash
code .
```

## Step 5: Install Your Coding Agent

Install the CLI tool globally:

```bash
npm install -g @openai/codex
```

Run it:

```bash
codex
```

Follow the login flow shown in the terminal.

You can also install the Codex app for macOS:

[Codex app for macOS](https://developers.openai.com/codex/app)

## Step 6: Create a Working Folder

Create your projects directory:

```bash
mkdir -p ~/projects
cd ~/projects
```

Create your first project:

```bash
mkdir my-first-ai-project
cd my-first-ai-project
```

Open it:

```bash
code .
```

## Step 7: Start Your First Project

Initialize Git:

```bash
git init
```

Create a README:

```bash
echo "# My First AI Project" > README.md
```

Commit it:

```bash
git add .
git commit -m "Initial commit"
```

Launch your coding agent:

```bash
codex
```

Good first prompt:

```text
Inspect this repository first.
Explain the current structure.
Then suggest a very small first project I can build here.
```

## Common Mistakes on Mac

### Installing Too Many Overlapping Tools at Once

Keep it simple: Homebrew, Node, Git, VS Code, and your coding agent.

### Skipping Git Setup

Configure your Git identity early.

### Starting with Giant Prompts

Start with a tiny project first.

## Quick Checklist

- Homebrew installed
- Node.js installed
- Git installed
- VS Code installed
- coding agent installed
- project folder created
- Git initialized

## Next Steps

Once this path works, the next useful topics are:

- [First Project: Start Small and Finish Something](./first-project.md)
- [Git Safety: How to Avoid Losing Work](./git-safety.md)
- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)
