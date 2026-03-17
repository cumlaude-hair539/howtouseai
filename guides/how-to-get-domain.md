# How to Get a Domain and Connect It Through Cloudflare

If you want your website to open through your own domain, the workflow is usually this:

1. Buy a domain.
2. Add that domain to Cloudflare.
3. Point the domain's nameservers to Cloudflare, if needed.
4. Create DNS records or attach the domain to a Cloudflare Tunnel.
5. Make your website available from your server or local development setup.

Cloudflare supports both patterns:

- normal DNS records such as `A`, `AAAA`, or `CNAME` for pointing traffic to a server IP
- Cloudflare Tunnel for pointing a hostname to a local or private service without exposing a public IP directly

## First Choose: Common Domain Paths

### Path A: Buy the Domain Elsewhere, Then Use Cloudflare DNS

This is a very common path for beginners.

Example:

You buy the domain at a registrar, then add the site to Cloudflare and change the domain's nameservers to the ones Cloudflare gives you.

Use this when:

- you already bought a domain somewhere else
- you want Cloudflare to handle DNS and proxying
- you may want to use Cloudflare Tunnel later

### Path B: Buy the Domain Directly on Cloudflare

Cloudflare now allows you to register a new domain directly through Cloudflare Registrar.

This is often the cleanest option if you are starting from zero, because the domain will already use Cloudflare nameservers.

Use this when:

- you have not bought a domain yet
- you want the simplest Cloudflare-first setup
- you want DNS and registrar management in one place

### Path C: Transfer an Existing Domain to Cloudflare Registrar

Cloudflare also supports transferring an existing domain registration to Cloudflare Registrar.

Use this when:

- you already own a domain
- you want the registration itself managed inside Cloudflare
- you want fewer providers in the chain

## The Easiest Beginner Recommendation

For most beginners, the cleanest practical route is one of these:

- buy the domain on Cloudflare directly, if that works for your TLD and your plan
- buy the domain at another registrar, then connect it to Cloudflare DNS

In both cases, the next step is the same:

- use Cloudflare DNS
- either point the domain to your server IP
- or connect a subdomain to a Cloudflare Tunnel

## Step 1: Buy a Domain

Buy a domain from a registrar you trust.

Examples:

- `myproject.com`
- `myapp.dev`
- `example.net`

When choosing a domain:

- keep it short
- avoid weird spelling if possible
- avoid hyphens unless necessary
- make sure you control the registrar account and email

If you buy it outside Cloudflare, you will manage it through that registrar until you point it to Cloudflare nameservers.

If you buy it directly on Cloudflare, Cloudflare will already manage the domain through Cloudflare Registrar.

## Step 2: Add the Domain to Cloudflare

If the domain was purchased somewhere else, add it to Cloudflare as a site or zone.

Cloudflare may scan your existing DNS records automatically, but you still need to review them carefully.

What to do:

- log into Cloudflare
- add your domain
- review the imported DNS records
- make sure nothing important is missing

If this is a brand new domain with no existing site yet, you may only need a minimal set of records.

If you bought the domain directly on Cloudflare, this setup is simpler because the domain is already on Cloudflare nameservers.

## Step 3: Change Nameservers at Your Registrar, If Needed

This is the key step for domains purchased outside Cloudflare.

After adding the domain, Cloudflare will assign nameservers to your zone.
You then go to your registrar and replace the current nameservers with the Cloudflare ones.

Once the nameserver change propagates, Cloudflare becomes authoritative for DNS for that domain.

If the domain is registered on Cloudflare Registrar, the domain already uses Cloudflare nameservers and they must stay there.

## Step 4: Choose How the Domain Should Point to Your Site

Now choose one of these two practical setups.

### Option A: Point the Domain to a Server IP

Use this when:

- you have a VPS or server
- your site is hosted there
- you want standard DNS-based routing

Usually you create:

- an `A` record for the root domain, such as `example.com`
- a `CNAME` or another `A` record for `www`

Example concept:

```text
Type: A
Name: @
Content: YOUR_SERVER_IP
```

and optionally:

```text
Type: CNAME
Name: www
Content: example.com
```

Then your server or `nginx` should serve the site for that domain.

### Option B: Point a Subdomain to Cloudflare Tunnel

Use this when:

- your app runs locally or on a private machine
- you do not want to expose a public IP
- you want a clean development preview link like `dev.example.com`

Example concept:

```text
dev.example.com -> Cloudflare Tunnel -> http://localhost:3000
```

This is one of the best setups for mobile testing of a local project.

## Step 5: If Using a Normal Server, Make Sure `nginx` Is Configured

If your domain points to a real VPS or server IP, `nginx` is often the front door.

Typical flow:

```text
domain -> Cloudflare DNS -> server IP -> nginx -> app
```

For self-hosted web apps, that is a standard practical pattern:

- Cloudflare handles DNS and proxying
- `nginx` handles incoming HTTP and HTTPS on the server
- `nginx` forwards traffic to the app process

For example, if your app runs on port `3000`, `nginx` can listen on ports `80` and `443` and proxy traffic to `127.0.0.1:3000`.

## Step 6: If Using Tunnel, Install and Authenticate `cloudflared`

If you want to use Cloudflare Tunnel, the real workflow is:

1. Install `cloudflared`.
2. Authenticate it with your Cloudflare account.
3. Create a tunnel.
4. Attach a hostname such as `dev.example.com`.
5. Point that hostname to your local service such as `http://localhost:3000`.

If you add the route through the Cloudflare dashboard, Cloudflare automatically creates the DNS record pointing the hostname to the tunnel subdomain.

## Beginner-Friendly Practical Examples

### Example 1: VPS Website on Your Root Domain

`example.com`

Flow:

```text
example.com -> A record -> VPS IP -> nginx -> website
```

Use this when your website is deployed on a server full-time.

### Example 2: Local Development Preview on a Subdomain

`dev.example.com`

Flow:

```text
dev.example.com -> Cloudflare Tunnel -> localhost:3000
```

Use this when the app runs on your laptop, WSL, home machine, or private VPS and you want to open it from your phone.

## Recommended Beginner Pattern

For a first project, one of the cleanest setups is:

- root domain for the real site later
- subdomain for development now

Example:

```text
example.com     -> later production site
dev.example.com -> current development preview
```

That keeps development and production separate and avoids confusion.

## Quick Checklist

- domain purchased
- domain added to Cloudflare
- nameservers updated if needed
- DNS records reviewed
- root domain or subdomain chosen
- server DNS or Tunnel route configured
- site reachable from the browser

## Final Note

If you want the simplest path, think in this order:

1. Get the domain.
2. Put DNS under Cloudflare.
3. Decide whether the site points to a server IP or a Tunnel.
4. Keep development and production separate when possible.

If you want the next step after domain and DNS, continue here:

- [Deploy Basics: Real Self-Hosting From Your Own Server](./deploy-basics.md)
