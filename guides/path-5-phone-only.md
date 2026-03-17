# Path 5: I Only Have a Phone

Yes, you can still start.

## Recommended Path

1. Rent a VPS.
2. Choose Ubuntu 24.04.
3. Install an SSH app such as Termius.
4. Connect to the server from your phone.
5. Open your project folder remotely.
6. Run your coding tools on the server.
7. Make progress even without a laptop.

This is not the most comfortable path for everyone, but it is absolutely possible.

## What This Setup Gives You

With a phone-only path, your phone becomes the control device.
The actual work happens on the remote server.

That means:

- the server does the heavy lifting
- your phone is used to connect and manage it
- you can still learn and build step by step

## Step 1: Rent a VPS

Choose a Linux VPS with:

- Ubuntu 24.04
- at least 4 vCPU
- at least 8 GB RAM
- SSH access

Choose a basic Linux VPS from a provider you trust.

Examples to consider:

- [OVHcloud](https://us.ovhcloud.com/)
- [Vultr](https://www.vultr.com/)

## Step 2: Save Your Server Details

You need:

- server IP address
- username, often `root`
- password or SSH key access

Keep them safe.

## Step 3: Install an SSH App

Install an app like [Termius](https://termius.com/index.html) on your phone.

Inside the app, create a new host using:

- `Hostname or IP`: your server IP
- `Username`: usually `root`
- `Password`: your VPS password

Then connect.

## Step 4: Update the Server

Once connected, run:

```bash
apt update && apt upgrade -y
```

Or if you are not `root`:

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 5: Install `curl`

```bash
apt install -y curl
```

Or:

```bash
sudo apt install -y curl
```

## Step 6: Install Node.js Through `nvm`

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

## Step 7: Install Git

```bash
apt install -y git
```

Or:

```bash
sudo apt install -y git
```

Verify:

```bash
git --version
```

## Step 8: Install Your Coding Agent

Example:

```bash
npm install -g @openai/codex
```

Run it:

```bash
codex
```

Follow the login flow shown in the terminal.

## Step 9: Create a Projects Folder

```bash
mkdir -p ~/projects
cd ~/projects
mkdir my-first-ai-project
cd my-first-ai-project
```

If you already have a repository:

```bash
git clone YOUR_REPOSITORY_URL
cd YOUR_REPOSITORY_NAME
```

## Step 10: Work From Your Phone

Initialize Git if needed:

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

## What Is Realistic on Phone-Only?

Good use cases:

- setup
- lightweight edits
- launching and managing tools
- reading logs
- small prompts
- learning workflow basics

Harder on phone-only:

- large refactors
- big visual UI work
- long editing sessions

That is normal.
The phone path is real, but it is best treated as a practical entry path, not necessarily the most comfortable long-term setup.

## Common Mistakes on Phone-Only

### Expecting the Phone Itself to Do All Heavy Work

The remote server is doing the real work.

### Losing Track of Credentials

Keep your IP, username, and passwords safe.

### Starting With Huge Tasks

Stay small and practical at first.

## Quick Checklist

- VPS rented
- Ubuntu 24.04 selected
- phone SSH app installed
- SSH connection working
- server updated
- Node.js installed
- Git installed
- coding agent installed
- project folder created or cloned

## Next Steps

Once this path works, move to:

- [First Project: Start Small and Finish Something](./first-project.md)
- [Git Safety: How to Avoid Losing Work](./git-safety.md)
- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)
