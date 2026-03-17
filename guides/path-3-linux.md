# Path 3: I Have Linux

If you already use Linux, the recommended path is:

1. Update system packages.
2. Install Node.js.
3. Install Git.
4. Install VS Code or use terminal.
5. Install your coding agent.
6. Create a working folder.
7. Start your first project.

## What You Are Setting Up

By the end of this guide, you should have:

- an updated Linux environment
- Node.js installed
- Git installed
- a VS Code or terminal workflow ready
- a project folder
- a coding agent ready to use

## Step 1: Update Packages

For Ubuntu or Debian-based systems, run:

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 2: Install Node.js

The recommended path is to install Node through `nvm`.

Install `curl` if needed:

```bash
sudo apt install -y curl
```

Install `nvm`:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Reload your shell:

```bash
source ~/.bashrc
```

Install Node 22:

```bash
nvm install 22
nvm alias default 22
```

Verify:

```bash
node -v
npm -v
```

## Step 3: Install Git

```bash
sudo apt install -y git
```

Verify:

```bash
git --version
```

Optional:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Step 4: Install VS Code or Stay in Terminal

If you want VS Code, install it from the official website or from the repository instructions for your Linux distribution:

[VS Code](https://code.visualstudio.com/)

If you prefer terminal-only, that is also completely fine.

## Step 5: Install Your Coding Agent

Example:

```bash
npm install -g @openai/codex
```

Run it:

```bash
codex
```

Follow the login flow.

## Step 6: Create a Working Folder

```bash
mkdir -p ~/projects
cd ~/projects
mkdir my-first-ai-project
cd my-first-ai-project
```

If you are using VS Code:

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

## Common Mistakes on Linux

### Installing Node from Outdated Distro Repositories

Use `nvm` for cleaner version control.

### Forgetting to Reload Shell After `nvm` Installation

Use:

```bash
source ~/.bashrc
```

### Skipping Git

Still use Git even for tiny projects.

## Quick Checklist

- system updated
- Node.js installed
- Git installed
- VS Code or terminal workflow ready
- coding agent installed
- project folder created
- Git initialized

## Next Steps

Once this path works, the next useful topics are:

- [First Project: Start Small and Finish Something](./first-project.md)
- [Git Safety: How to Avoid Losing Work](./git-safety.md)
- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)
