# Path 4: My Computer Is Weak, or I Want a Remote Setup

This is often one of the best options for people with older or weaker hardware.

## Recommended Path

1. Rent a VPS.
2. Choose Ubuntu 24.04.
3. Get your IP address and SSH credentials.
4. Connect to the server.
5. Update the server.
6. Install Node.js and Git.
7. Install your coding agent.
8. Clone or create your project.
9. Work remotely.

## Why This Path Is Useful

A remote server lets you:

- work from a weak laptop
- keep your main machine lighter
- connect from multiple devices
- run long tasks remotely
- continue from home, office, or phone

## Step 1: Rent a VPS

Choose a basic Linux VPS from a provider you trust.

For a beginner-friendly setup, look for:

- Ubuntu 24.04
- at least 4 vCPU
- at least 8 GB RAM
- SSD storage
- root access or sudo access

Examples to consider:

- [OVHcloud](https://us.ovhcloud.com/)
- [Vultr](https://www.vultr.com/)

## Step 2: Get Your Server Details

You usually receive:

- server IP address
- username, often `root`
- password or SSH key instructions

Keep these safe.

## Step 3: Connect with SSH

From macOS or Linux terminal:

```bash
ssh root@YOUR_SERVER_IP
```

From Windows PowerShell:

```bash
ssh root@YOUR_SERVER_IP
```

If you are using a password, enter it when asked.

If you are using SSH keys, your provider may give separate setup steps.

You can also use dedicated terminal apps:

- [MobaXterm](https://mobaxterm.mobatek.net/)
- [Termius](https://termius.com/index.html)

## Step 4: Update the Server

Once connected, run:

```bash
apt update && apt upgrade -y
```

If you are not `root`, use:

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 5: Install `curl`

```bash
apt install -y curl
```

Or with `sudo`:

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

Optional:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
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

Follow the login instructions shown in the terminal.

## Step 9: Create a Projects Folder

```bash
mkdir -p ~/projects
cd ~/projects
```

Create a new project:

```bash
mkdir my-first-ai-project
cd my-first-ai-project
```

Or clone an existing repository:

```bash
git clone YOUR_REPOSITORY_URL
cd YOUR_REPOSITORY_NAME
```

## Step 10: Start Working Remotely

Initialize Git if this is a new project:

```bash
git init
```

Create a README if needed:

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

## Common Mistakes With VPS

### Forgetting Basic Security Hygiene

At minimum, keep credentials safe and do not share root access casually.

### Installing Random Packages Without a Plan

Stay minimal at first.

### Not Using Git

Still use Git on the server.

### Losing Track of Where Your Project Folder Is

Keep everything organized under `~/projects`.

## Quick Checklist

- VPS rented
- Ubuntu 24.04 selected
- SSH access working
- server updated
- Node.js installed
- Git installed
- coding agent installed
- project folder created or cloned
- Git initialized if needed

## Next Steps

Once this path works, the next useful topics are:

- [First Project: Start Small and Finish Something](./first-project.md)
- [Git Safety: How to Avoid Losing Work](./git-safety.md)
- [Troubleshooting: What to Do When Something Breaks](./troubleshooting.md)
- [Deploy Basics: Real Self-Hosting From Your Own Server](./deploy-basics.md)
