# Deploy Basics: Real Self-Hosting From Your Own Server

In this guide, deployment means real self-hosting.

Not click deploy on a platform.
Not a temporary preview link.
Not managed magic.

Here, deployment means:

- you have your own server or VPS
- your app runs there
- your domain points there
- your reverse proxy serves traffic
- your process stays alive after reboot
- you control updates, restarts, logs, and configuration

For Next.js, self-hosting is officially supported, and the docs explicitly recommend putting a reverse proxy like `nginx` in front of the Next.js server instead of exposing it directly to the internet. They also note that self-hosting can run as a Node.js server or in Docker.

## What a Real Self-Hosted Deployment Usually Looks Like

A practical self-hosted web deployment usually looks like this:

```text
Domain
  -> DNS
  -> Server IP
  -> nginx
  -> app process on localhost
```

For example:

```text
example.com
  -> Cloudflare DNS
  -> VPS public IP
  -> nginx on ports 80/443
  -> Next.js app on 127.0.0.1:3000
```

This is the normal production mindset for a self-hosted Node or Next.js app.

## The Core Deployment Stack

For a clean beginner-to-intermediate self-hosted deployment, the base stack is usually:

- Ubuntu server
- Node.js
- Git
- GitHub CLI (`gh`)
- your app code
- a long-running service manager
- `nginx`
- domain plus DNS
- optional Cloudflare proxy layer

This is the practical baseline for "my app lives on my own server."

## What Each Part Does

### 1. Your Server

This is the machine that runs the app.

Usually:

- Ubuntu VPS
- public IP
- SSH access
- enough RAM and CPU for your app

### 2. Your App Process

Your app usually should not listen directly on the public internet.

Instead, it runs locally on the server, for example:

```text
127.0.0.1:3000
```

That means the app is reachable by `nginx` on the same machine, but is not directly exposed as the public entry point.

This matches Next.js self-hosting guidance, which recommends a reverse proxy in front of the Next.js process.

### 3. nginx

`nginx` becomes the public front door.

It usually:

- listens on port 80 and 443
- receives incoming requests
- forwards them to your local app
- helps with request handling before traffic reaches the app

Next.js explicitly recommends using a reverse proxy like `nginx` for self-hosting because it can handle malformed requests, slow connection attacks, payload limits, rate limiting, and related concerns before traffic reaches the Next.js server. nginx’s own beginner guide also documents the proxy-server pattern directly.

### 4. A Service Manager

You need the app to stay alive after:

- disconnecting SSH
- server reboot
- crashes
- restarts

That means you need a service or process manager.

A common Linux-native choice is `systemd`.

For this guide, the cleanest baseline is:

- `systemd` for the app service
- `nginx` for reverse proxy
- Git and GitHub CLI for code updates

## The Deployment Flow in Plain English

A real self-hosted deployment usually goes like this:

1. prepare the server
2. install Node.js, Git, and `gh`
3. clone the repository
4. install dependencies
5. build the app if needed
6. make the app run locally on the server
7. create a `systemd` service
8. configure `nginx` to proxy to the app
9. point DNS to the server
10. test the domain
11. update safely over time

That is the real deployment lifecycle.

## Recommended Baseline for a Next.js Self-Deploy

If your project is a Next.js app, the clean self-hosted baseline is:

- Next.js app runs on `127.0.0.1:3000`
- `systemd` keeps it running
- `nginx` proxies public traffic to it
- your domain points to the server
- Cloudflare DNS can optionally sit in front

Next.js officially supports self-hosting and explicitly recommends a reverse proxy like `nginx` instead of exposing the Next.js server directly.

## Recommended Server Software to Install

On a self-hosted deployment server, you should usually install:

- `git`
- `gh`
- Node.js
- `nginx`

And depending on your stack:

- `build-essential`
- `curl`
- your service layer

GitHub CLI is useful because it gives you GitHub terminal workflows like auth, repo inspection, PR handling, and repo operations, not just raw Git.

## Why Install `gh` on the Server Too

A lot of people install only Git.
That is incomplete for a serious GitHub-based workflow.

Installing `gh` on the server helps with:

- GitHub authentication
- checking repo state
- working with GitHub repos more comfortably
- terminal-based GitHub workflows during deploy and update operations

So the practical recommendation is:

- install `git`
- install `gh`
- authenticate GitHub properly on the server

not just Git.

## The Clean Deployment Architecture

Basic self-hosted architecture:

```text
User Browser
  -> Domain
  -> DNS
  -> Server IP
  -> nginx
  -> Next.js / Node app on localhost
```

With Cloudflare in front:

```text
User Browser
  -> Cloudflare DNS / proxy
  -> Server IP
  -> nginx
  -> app on localhost
```

Cloudflare recommends proxied `A`, `AAAA`, and `CNAME` records for web traffic, and their DNS docs make clear that those are the main proxy-eligible record types for HTTP and HTTPS traffic.

## DNS for Self-Hosting

If the site lives on your own server, the usual DNS setup is:

Root domain to server IP:

```text
Type: A
Name: @
Content: YOUR_SERVER_IP
```

Optional `www` alias:

```text
Type: CNAME
Name: www
Content: example.com
```

Cloudflare’s DNS docs state that `A` and `AAAA` map hostnames to IP addresses, and `A`, `AAAA`, and `CNAME` are the common proxy-eligible record types for web traffic.

## Reverse Proxy Matters

A lot of beginners want to run the app directly on a public port and call it done.

That is not the clean production pattern.

For self-hosting, Next.js explicitly recommends `nginx` or another reverse proxy in front of the app.

So the recommendation here is:

Do not expose the Next.js process directly if you are doing a real self-hosted deployment.

Use:

- app bound locally
- `nginx` publicly exposed

## How Your App Should Run on the Server

For a Node or Next.js app, the app process should usually:

- run under a controlled service context
- bind to localhost
- restart automatically if it crashes
- start automatically on boot

That is exactly the kind of role `systemd` is commonly used for on Linux servers.

## Development vs Production on Your Own Server

Do not mix these:

Development:

```bash
npm run dev
```

This is for local development.
Not your real production deployment.

Production-like app run usually means:

- install dependencies
- build the app
- run the production server
- keep it alive with `systemd`
- route traffic through `nginx`

Next.js distinguishes development flow from self-hosted production flow, and self-hosting guidance is specifically about the latter.

## Good First Self-Hosting Mindset

Your deployment should answer these questions clearly:

- where is the code?
- how is the app started?
- what keeps it running?
- what domain points to it?
- what port does `nginx` proxy to?
- how do you restart it?
- how do you update it?
- how do you inspect logs?

If you cannot answer those, the deployment is not yet operationally solid.

## A Practical First Self-Hosted Deployment Plan

### Step 1: Prepare the Server

Make sure you have:

- Ubuntu server
- SSH access
- public IP
- domain ready

### Step 2: Install Core Tools

Install:

- Node.js
- Git
- GitHub CLI
- `nginx`

This is your foundation.

### Step 3: Clone the Repo

Put the project on the server in a clean directory.

Example ideas:

- `/var/www/myapp`
- a dedicated deploy user home directory

The exact path is up to your structure, but keep it consistent.

### Step 4: Install Dependencies and Build

For a typical Node or Next.js app:

- install dependencies
- run the build
- verify the app can start locally on the server

This proves the server can actually run the project before you add `nginx` and DNS on top.

### Step 5: Run the App Locally First

Before touching the domain, make sure the app can run on the server itself.

Example concept:

```text
app listens on 127.0.0.1:3000
```

If the app cannot run locally on the server, `nginx` and DNS will not save you.

### Step 6: Create a systemd Service

This is what makes the app behave like a real deployed service.

The service should:

- start the app
- restart on failure
- start on boot
- run in the correct working directory

### Step 7: Configure nginx

`nginx` should:

- listen publicly
- receive requests for your domain
- proxy them to the local app port

nginx’s beginner guide explicitly documents the proxy server pattern, and Next.js recommends using such a reverse proxy in front of the Next.js process.

### Step 8: Point DNS to the Server

Create the `A` record for the root domain and optional `CNAME` for `www`, then wait for DNS to propagate.

Cloudflare recommends proxied `A`, `AAAA`, and `CNAME` records for hostnames serving web traffic.

### Step 9: Test Through the Domain

Now test the real external path:

```text
browser -> domain -> server -> nginx -> app
```

Only after this works should you call it deployed.

## What a Good Deployment Update Flow Looks Like

A clean update flow usually looks like this:

1. SSH into the server
2. go to the repo directory
3. inspect Git state
4. pull latest code
5. install dependencies if needed
6. build app if needed
7. restart service
8. verify app
9. inspect logs if broken

That is the operational side of self-hosting.

## What Not to Do

Do not do this:

- run the app manually in a terminal and call it production
- expose the app directly to the internet without a reverse proxy
- skip restart strategy
- skip logs
- mix dev commands with production commands
- make DNS changes before the app works locally
- let the AI agent redesign the whole server without a plan

Do this instead:

- make the app run locally on the server first
- create a real service
- put `nginx` in front
- then connect DNS
- then test
- then document the flow

## How to Ask Your AI Agent for Deployment Help Correctly

A lot of people say:

```text
Deploy this for me.
```

That is too vague.

A better deployment prompt is:

```text
Inspect this repository first.

I want a real self-hosted deployment on my own Ubuntu server.

Please:
1. identify what kind of app this is,
2. explain the expected production run method,
3. propose a minimal self-hosted deployment architecture using:
   - Node.js
   - systemd
   - nginx
   - domain + DNS
4. clearly separate local development from production deployment,
5. explain what files or configs need to be created,
6. keep the setup minimal and production-minded,
7. do not overengineer.
```

That gives the agent a real infrastructure brief instead of a vague wish.

## Better Prompt for a Next.js Self-Deploy

```text
Inspect this repository first.

I want to deploy this Next.js project on my own Ubuntu server.

Requirements:
- real self-hosting
- nginx reverse proxy
- app running locally behind nginx
- systemd service for the app
- domain pointed to the server through DNS
- clear separation between development and production

Please:
1. explain the deployment architecture,
2. identify the relevant project files,
3. tell me what environment variables or config I should expect,
4. prepare the smallest clean self-hosting plan,
5. explain each step in beginner-friendly terms,
6. do not make unrelated refactors.
```

## Better Prompt for Server Preparation

```text
I want to prepare an Ubuntu server for self-hosting this app.

Please help me create the minimal server setup with:
- Node.js
- git
- gh
- nginx
- systemd-based app service

Please:
1. explain why each component is needed,
2. give me the setup order,
3. separate server preparation from application deployment,
4. keep the workflow practical and simple.
```

## Better Prompt for nginx Setup

```text
Inspect this project and deployment target first.

I want nginx to sit in front of the app as a reverse proxy.

Please:
1. explain what port the app should run on locally,
2. explain how nginx should route traffic to it,
3. prepare a minimal nginx reverse proxy configuration,
4. explain which parts I may need to customize for my domain,
5. keep it production-minded and minimal.
```

This aligns with both nginx’s proxy-server model and Next.js self-hosting guidance.

## Better Prompt for DNS and Domain Setup

```text
I want this self-hosted app to be reachable through my own domain.

Please:
1. explain whether I should use A, AAAA, or CNAME records,
2. explain how to point the domain to my server,
3. explain what Cloudflare proxying changes,
4. explain the simplest clean DNS structure for:
   - root domain
   - optional www
5. keep the explanation beginner-friendly.
```

Cloudflare’s DNS docs are the right reference point for this because they document proxyable record types and how `A`, `AAAA`, and `CNAME` behave for web traffic.

## Minimal Self-Hosting Doctrine

If you want the shortest version of the whole guide:

real self-hosted deployment means:

- your own server
- your app running locally on it
- `systemd` keeps it alive
- `nginx` proxies public traffic
- your domain points to the server
- you can update, restart, and inspect logs yourself

That is the baseline.

## Compact Summary

For this project, deployment should mean:

- no platform magic
- no fake preview counted as production
- no direct raw app exposure
- real self-hosting
- reverse proxy in front
- service manager behind it
- domain and DNS correctly pointed
- updates and restarts under your control

That is a real deployment mindset.

## Further Reading

- [Next.js self-hosting](https://nextjs.org/docs/app/guides/self-hosting)
- [nginx Beginner's Guide](https://nginx.org/en/docs/beginners_guide.html)
- [Cloudflare Proxy status](https://developers.cloudflare.com/dns/proxy-status/)
- [GitHub CLI quickstart](https://docs.github.com/github-cli/github-cli/quickstart)

If you want the practical server tool stack behind this deployment model, continue here:

- [Useful Tools for AI: What to Install on a Server So an AI Agent Can Work Properly](./useful-tools-for-ai.md)
