---
type: system
title: NanoClaw capabilities snapshot
description: Baseline of known NanoClaw skills/capabilities, diffed weekly by the SessionStart check hook.
---

# NanoClaw capabilities snapshot

Last checked: 2026-10-19

## Known local skills (this container)
- agent-browser, frontend-engineer, onecli-gateway, self-customize, welcome

## Known bundled/remote skills
- schedule, update-config, loop, dataviz, keybindings-help, code-review,
  simplify, fewer-permission-prompts, claude-api, run, init, security-review

## Known but not installed
- `codex` skill (nanoclaw.dev/skills/codex/) — lets an agent group run on
  OpenAI's Codex CLI instead of Claude. Installation is host-terminal-only,
  not invocable from inside a chat session. Discovered 2026-08-24.
- `Iron Proxy` (docs.nanoclaw.dev/operate/gateways.md) — alternative
  credential gateway to OneCLI, shipped v2.4.0 (2026-09-23). Own web console
  (Iron Control) for secrets/OAuth/approvals; auto-approves model-provider
  domains and keyless local models over plain HTTP (relevant if Ondřej ever
  wants this agent talking to a home-lab local model). Needs Docker on the
  host; installed via `/add-iron-proxy`. OneCLI remains the default — this
  is additive, not a replacement. Host-level setup. Flagged to Ondřej
  2026-10-19.

## Known limitations
- `schedule`/RemoteTrigger fails with "Unable to get organization UUID" for
  containers using API-key auth (this one, via OneCLI) — root cause was
  public issue nanocoai/nanoclaw#1806. **Closed upstream 2026-10** (date not
  given in issue metadata, confirmed closed as of this check): maintainer
  shipped a native `ncl tasks` scheduler (cron schedules, one session per
  task) that doesn't depend on Claude Code RemoteTrigger — exactly the
  workaround already adopted below. No action needed.
- Real fix, found 2026-08-28: `ncl tasks` (local CLI) is a separate,
  container-native scheduler that doesn't touch claude.ai Routines/org UUID
  at all. Use it for anything recurring — see
  `memory/system/standing-checks.md`. A SessionStart-hook workaround was
  built and used for 3 days (2026-08-25 to 2026-08-28) before this was
  found; it never actually fired (settings.json watcher didn't reload) and
  has been removed.
- This weekly check itself failed 7 straight times (2026-08-31 through
  2026-10-12) with a generic "OneCLI gateway failed to resolve rules for
  this request" 502 — no further detail available, and no matching GitHub
  issue found when searched 2026-10-19. Resolved itself by 2026-10-19
  without a diagnosed cause. NanoClaw v2026.10.0 (2026-10-09) added
  descriptive error messages for failed runs — once the host is on that
  release, a repeat of this failure should actually explain itself. Updating
  the host is outside this agent's access (no host-level control).

## Release history (for next diff)
- v2.3.0 (2026-08-24): per-agent provisioned Slack apps, `/add-codex` pinned
  to @openai/codex 0.146.0.
- v2.4.0 (2026-09-23): Iron Proxy introduced (see above); install-wide and
  per-group model/speed controls; agents on Claude Code 2.1.280; OpenCode
  provider reworked with host-managed auth.
- v2026.10.0-rc.1/rc.2 (2026-10-04/05): Iron Proxy refinements (keyless
  local models over plain HTTP), OneCLI gateway pinned to 1.42.0, descriptive
  failed-run error messages introduced.
- v2026.10.0 (2026-10-09): first calendar-versioned release; updates now
  follow release channels (stable/beta/edge) instead of tracking `main`;
  OneCLI gateway pinned to exactly 1.42.0 (closes a credential-injection
  bypass — security fix).
