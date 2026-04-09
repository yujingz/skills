---
name: vps-3xui
description: Deploy and validate 3x-ui on a generic Ubuntu VPS with DNS, reverse proxy, firewall, and client config delivery. Use when provisioning or rebuilding a VPS-hosted 3x-ui panel, wiring DNS records, publishing SS or Trojan endpoints, verifying browser access to the panel, or documenting a repeatable VPS 3x-ui workflow without embedding environment-specific secrets in the skill.
---

# VPS 3xUI

Set up a reusable 3x-ui host on a generic Ubuntu VPS and keep the skill process-oriented. Store all secrets, tokens, passwords, record IDs, and environment-specific values in a separate local record file, not in the skill.

## Workflow

1. Gather the inputs.
   Require SSH reachability, VPS OS, public IPs, DNS provider access, target hostnames, desired protocols, desired client formats, and whether the panel should be public or tunnel-only.
2. Inspect the current server before changing anything.
   Check open ports, installed services, firewall rules, CPU/RAM/disk, and current TCP congestion control.
3. Install the base components.
   Prefer `3x-ui` for control, `Caddy` for TLS and reverse proxy, and `ufw` for firewalling.
4. Harden the panel immediately.
   Set a non-default username, password, panel port, and base path.
   Bind the panel to `127.0.0.1` when a reverse proxy fronts it.
5. Publish DNS and HTTPS.
   Create explicit panel and proxy hostnames.
   If an edge service causes redirect loops or breaks WebSocket upgrades, prefer `DNS only` over forcing a broken proxied path.
6. Add proxy inbounds through 3x-ui.
   Use the 3x-ui API or UI instead of editing database files directly.
   Start with the simplest protocol that satisfies the user's compatibility needs.
7. Deliver client configs.
   Generate the exact client format requested by the user, such as Surge, Clash, or sing-box snippets.
8. Verify from two angles.
   Check the panel in a real browser.
   Check the proxy chain with an isolated CLI client before relying on a GUI proxy app profile.

## Protocol Heuristic

- Choose `Shadowsocks` first when broad compatibility matters more than stealth or transport sophistication.
- Choose `Trojan + WS + TLS` only when the target client syntax is known to work and a reverse proxy is already in place.
- If a complex protocol fails in a specific client but works in an isolated CLI test, ship the simpler compatible protocol first and debug the complex one later.

## Verification

- Verify listeners and firewall:
  `ss -tulpn`
  `ufw status verbose`
- Verify panel settings:
  `/usr/local/x-ui/x-ui setting -show true`
- Verify browser login:
  open the final panel URL, pass any front-door auth, log in to 3x-ui, and confirm the dashboard renders.
- Verify the proxy chain without disturbing the user's active local setup:
  start a temporary CLI client such as `xray`, expose a local SOCKS port, and fetch `https://cp.cloudflare.com/generate_204` through that SOCKS proxy.
- Only after isolated verification succeeds, edit the user's live GUI proxy profile if they explicitly asked for it.

## Secret Handling

- Never embed live tokens, passwords, panel credentials, or record IDs into the skill.
- Create a local plaintext record inside the current project when the user explicitly wants an operational record.
- Put `DO NOT COMMIT` at the top of that local record.
- Keep the skill generic and reusable across VPS providers.

## Troubleshooting Rules

- If a GUI client fails but an isolated CLI client succeeds, treat the issue as client-side syntax or compatibility first.
- If Cloudflare or another edge returns self-redirects or breaks protocol upgrades, compare edge behavior with direct-origin behavior before changing the server.
- If the direct-origin path works and the proxied path fails, prefer `DNS only` for the affected hostname unless there is a hard requirement to keep the edge in-path.
- If the user needs a working fallback quickly, add a compatible `Shadowsocks` inbound first and debug `Trojan` or other advanced transports in a separate pass.

## Local Record Pattern

When the user wants a persistent local record, write a plaintext file in the active project with sections like:

- Server
- DNS
- Panel access
- Protocol credentials
- Firewall
- Service status
- Validation notes

Mark it `DO NOT COMMIT`.
