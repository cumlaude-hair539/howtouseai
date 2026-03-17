# Path 1: I Have a Windows Laptop or PC

If you are on Windows, the recommended beginner path is:

1. Install WSL2.
2. Install Ubuntu inside WSL.
3. Install Node.js.
4. Install Git.
5. Install VS Code.
6. Install your coding agent.
7. Start your first project.

## Important

For Windows users, it is usually much better to work through `WSL2 + Ubuntu` instead of doing everything directly in PowerShell or Command Prompt.

Why?

Because most AI coding workflows, developer tools, and CLI-based guides work more naturally in a Linux environment.

## What You Are Setting Up

By the end of this guide, you should have:

- a Linux environment running on your Windows machine
- Node.js installed
- Git installed
- VS Code installed
- a working folder for projects
- your coding agent installed and ready

## Step 1: Install WSL2

Open PowerShell as Administrator and run:

```bash
wsl --install
```

This command installs:

- WSL2
- the default Linux distribution
- the basic required Windows features

After that, restart your computer if Windows asks you to.

To check WSL after reboot, run:

```bash
wsl --status
```

If needed, you can also list installed distros with:

```bash
wsl --list --verbose
```

## Step 2: Install Ubuntu in WSL

If Ubuntu was not automatically installed, open PowerShell and run:

```bash
wsl --install -d Ubuntu
```

Then launch Ubuntu from the Start menu.

The first time it opens, it will ask you to create:

- a Linux username
- a Linux password

Remember these. They are for your Ubuntu environment inside WSL.

## Step 3: Update Ubuntu Packages

Now you are inside Ubuntu. Run:

```bash
sudo apt update && sudo apt upgrade -y
```

This updates package lists and upgrades installed packages.

## Step 4: Install Node.js

The recommended path is to install Node through `nvm`.

Install `curl` first if needed:

```bash
sudo apt install -y curl
```

Install `nvm`:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Then reload your shell:

```bash
source ~/.bashrc
```

Install Node.js 22:

```bash
nvm install 22
```

Set it as default:

```bash
nvm alias default 22
```

Verify:

```bash
node -v
npm -v
```

## Step 5: Install Git

Inside Ubuntu, run:

```bash
sudo apt install -y git
```

Verify:

```bash
git --version
```

Optional but recommended: set your Git identity.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check it:

```bash
git config --list
```

## Step 6: Install VS Code

Download and install VS Code for Windows from the official website:

[VS Code](https://code.visualstudio.com/)

After installing VS Code, also install the WSL extension in VS Code.

Once that is done, from inside Ubuntu you can open your current folder in VS Code using:

```bash
code .
```

If `code` is not recognized at first, restart VS Code and WSL, then try again.

## Step 7: Install Your Coding Agent

Inside Ubuntu, install the coding agent CLI.

Example for Codex CLI:

```bash
npm install -g @openai/codex
```

Then run:

```bash
codex
```

Follow the login instructions shown in the terminal.

You can also install the Codex Windows app:

[Codex Windows app](https://developers.openai.com/codex/app/windows)

After the first launch, open the settings and make sure the app uses WSL.

Recommended settings:

- `Agent environment` -> `Windows Subsystem for Linux`
- `Integrated terminal shell` -> `WSL`

## Step 8: Create a Working Folder

For the smoothest experience, keep your projects inside your Linux home directory, not in `/mnt/c/...`.

Create a projects folder:

```bash
mkdir -p ~/projects
cd ~/projects
```

Create your first project folder:

```bash
mkdir my-first-ai-project
cd my-first-ai-project
```

Open it in VS Code:

```bash
code .
```

## Step 9: Start Your First Project

Initialize Git:

```bash
git init
```

Create a simple README file:

```bash
echo "# My First AI Project" > README.md
```

Commit it:

```bash
git add .
git commit -m "Initial commit"
```

Now launch your coding agent:

```bash
codex
```

A good first prompt:

```text
Inspect this repository first.
Explain the current structure.
Then suggest a very small first project I can build here.
```

## Common Mistakes on Windows

### Doing Everything in PowerShell Instead of Ubuntu

If the guide says `WSL2 + Ubuntu`, use Ubuntu consistently.

### Keeping Projects in `/mnt/c/...`

For many development workflows, it is better to keep project files in `~/projects/...` inside Linux.

### Skipping Git

Use Git from day one.

### Installing Random Node Versions

Use Node 22 unless your stack specifically requires something else.

## Quick Checklist

- WSL2 installed
- Ubuntu installed
- Ubuntu updated
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
