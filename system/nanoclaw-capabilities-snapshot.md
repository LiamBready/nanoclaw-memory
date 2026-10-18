---
type: system
title: NanoClaw capabilities snapshot
description: Baseline of known NanoClaw skills/capabilities, diffed weekly by the SessionStart check hook.
---

# NanoClaw capabilities snapshot

Last checked: 2026-08-25

## Known local skills (this container)
- agent-browser, frontend-engineer, onecli-gateway, self-customize, welcome

## Known bundled/remote skills
- schedule, update-config, loop, dataviz, keybindings-help, code-review,
  simplify, fewer-permission-prompts, claude-api, run, init, security-review

## Known but not installed
- `codex` skill (nanoclaw.dev/skills/codex/) — lets an agent group run on
  OpenAI's Codex CLI instead of Claude. Installation is host-terminal-only,
  not invocable from inside a chat session. Discovered 2026-08-24.

## Known limitations
- `schedule`/RemoteTrigger fails with "Unable to get organization UUID" for
  containers using API-key auth (this one, via OneCLI) — confirmed root
  cause via public issue nanocoai/nanoclaw#1806 (open, no maintainer
  response as of 2026-08-25). Structural: OAuth-based login is required to
  resolve an org UUID; API-key mode can't. Not fixable from this side, and
  not needed — see below.
- Real fix, found 2026-08-28: `ncl tasks` (local CLI) is a separate,
  container-native scheduler that doesn't touch claude.ai Routines/org UUID
  at all. Use it for anything recurring — see
  `memory/system/standing-checks.md`. A SessionStart-hook workaround was
  built and used for 3 days (2026-08-25 to 2026-08-28) before this was
  found; it never actually fired (settings.json watcher didn't reload) and
  has been removed.
