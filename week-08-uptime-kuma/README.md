# Session 8 — Monitoring with Uptime Kuma

> 💡 **Note for students:** This README is a real example from the instructor's own lab, kept exactly at the level of detail you should aim for — not more, not less. Where something is worth noticing, you'll see a callout like this one. Everything else is just... the actual README.

## What I built

This week I added Uptime Kuma to the stack — a self-hosted monitoring dashboard that keeps an eye on whether my other services are actually up. It watches Pi-hole, File Browser, and Immich right now, and I'll add more as I deploy them. It's the first service in this lab that isn't really *for* me to use directly — it's for keeping tabs on everything else.

> 💡 **Why this matters as an example:** Notice the README doesn't just say "installed Uptime Kuma." It says what it's actually monitoring, right now, specific to this build. That specificity is the whole difference between a good README and a checkbox one.

## Why this one matters

Not:
> "Installed a monitoring tool."

Actually:
- service availability — knowing something is down before a user tells you
- outage detection — the difference between "it's down" and "it's been down for 20 minutes"
- operational monitoring mindset — this is what ops and platform teams actually do all day

## Deployment

Deployed via Docker Compose alongside the rest of the stack. Config lives in `docker-compose-files/uptime-kuma/`.

```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    restart: unless-stopped
    ports:
      - "3001:3001"
    volumes:
      - ./kuma-data:/app/data
```

## What I tested

- Opened `http://server-ip:3001` and completed the first-run setup (admin account, test credentials only)
- Added three monitors:
  - Pi-hole — HTTP check on port 80
  - File Browser — HTTP check on its port
  - Immich — HTTP check on its port
- Set check interval to 60 seconds for all three
- Manually stopped the Pi-hole container to confirm Uptime Kuma actually caught it — it flagged the outage within about a minute and logged the downtime

> 💡 **Why this matters as an example:** That last bullet is the important one. Anyone can screenshot a green dashboard. Deliberately breaking something to prove the monitoring *works* is what shows you understand what the tool is actually for.

## One problem I hit and how I fixed it

First attempt, Pi-hole kept showing as down even though it was clearly running — I could open it fine in the browser. Turned out I'd pointed the monitor at the wrong port (I used 53, which is DNS, not the web interface). Changed the monitor to check the correct HTTP port and it went green immediately.

> 💡 **Why this matters as an example:** This is the section students skip writing, and it's the one that matters most. A perfect setup with no notes shows nothing. A mistake explained clearly shows you can actually troubleshoot — which is the entire point of the programme.

## Screenshots

- Uptime Kuma dashboard with all three services showing green
- The dashboard mid-outage, showing Pi-hole flagged as down
- Monitor configuration screen for one of the services

## Next up

Session 9 — Reverse Proxy and HTTPS with Nginx Proxy Manager.
