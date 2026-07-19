# Week 7 — Password Management with Vaultwarden

## What I Built

Deployed [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (a lightweight self-hosted Bitwarden-compatible server) as a Docker container on my Ubuntu Server VM. Created a test vault account and confirmed I could log in, save an entry, and retrieve it.

- Server IP: `192.168.100.x`
- Access URL: `vault.lab`
- Container name: `vaultwarden`

## Why Vaultwarden

Vaultwarden was chosen as a full password manager service because it's lightweight, easy to run in Docker, and compatible with the standard Bitwarden apps/browser extensions.

## Concepts Covered

- Password managers and why self-hosting one matters
- Local-only vs. public exposure — this service stays local for now, no internet exposure yet
- Backup considerations for data that matters (vault database)
- Basic security thinking: least exposure, test credentials only

> **Note:** Used test credentials only during this session — no real passwords stored.

## Commands I Ran

```bash
# Pull and run the Vaultwarden container
docker compose up -d

# Check it's running
docker ps

# Check logs if something looks off
docker logs vaultwarden
```

## Expected Result

- `docker ps` shows the `vaultwarden` container as `Up`
- Visiting `https://vault.lab` in the browser loads the Vaultwarden login/registration page
- A test account can be created, logged into, and a test entry saved and retrieved

## Problem I Hit and How I Fixed It

*(Fill in with your actual issue — example below)*

**Problem:** Couldn't reach the Vaultwarden page from the browser after starting the container
**Fix:** Checked `docker ps` and saw the container wasn't running — `docker logs vaultwarden` showed a port conflict on 8081. Changed the host port to `8082` and it came up fine.

## Screenshots

- [x] `docker ps` output showing Vaultwarden container running
- [ ] Vaultwarden login/registration page in browser
- [ ] Test vault entry saved and visible

## Notes for Next Session

- Vaultwarden is local-only for now — no HTTPS or remote access yet (comes later with Nginx Proxy Manager and Cloudflare Tunnel)
- Should think about a backup plan for the `vw-data` volume before exposing this publicly
