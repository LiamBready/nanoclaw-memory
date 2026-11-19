---
type: system
title: NanoClaw capabilities snapshot
description: Baseline of known NanoClaw skills/capabilities, diffed weekly by the SessionStart check hook.
---

# NanoClaw capabilities snapshot

Last checked: 2026-11-16

## Known local skills (this container)
- agent-browser, frontend-engineer, onecli-gateway, self-customize, welcome

## Known bundled/remote skills
- schedule, update-config, loop, dataviz, keybindings-help, code-review,
  simplify, fewer-permission-prompts, claude-api, run, init, security-review

## Known MCP tools (new capabilities, not skills)
- `create_agent` — confirmed live and callable in this container as of
  2026-10-26 (verified via ToolSearch, not just docs). Ships with
  v2026.10.1-rc.1 (2026-10-20) / rc.2 (2026-10-22): "agents creating other
  agents from templates." Lets this agent spawn a long-lived companion
  sub-agent (own instructions, own isolated workspace/container, own
  message-destination name) directly from chat — no host-level setup
  required to use it. First call likely triggers an approval card to
  Ondřej as admin, since this container probably isn't `cli_scope: global`;
  he can promote it host-side via
  `ncl groups config update --id <agent-id> --cli-scope global` to skip
  that gate. New sub-agents aren't wired to their own chat channel by
  default — that needs `ncl wirings create` on the host, only if a direct
  line to the sub-agent (not routed through this agent) is wanted.
  Flagged to Ondřej 2026-10-26; offered to test the approval flow, awaiting
  his go-ahead.

## Known but not installed
- PDF reading for Claude agents — ships in v2026.11.0-beta.1 (2026-10-31),
  still present in beta.2/beta.3 (2026-11-12/14). Lets Claude-based agents
  (this one) read long PDFs sent directly in chat — no host-terminal setup
  beyond running `/update-nanoclaw` and being on the `beta` channel (not yet
  on `stable`; v2026.10.1 never shipped stable, superseded by 2026.11.0).
  Installs with a custom/rebuilt agent image need `ncl groups restart --id
  <group-id> --rebuild` too. Flagged to Ondřej 2026-11-16, offered to flag
  when it reaches stable or to try the beta now; awaiting his call.
- `send_card` KPI fields/tables/charts — same beta release. Lets this agent
  send richer cards (Slack renders natively, Teams shows charts as tables;
  WhatsApp Cloud/Mattermost/linked-WhatsApp have no or partial support).
  Same prerequisite as above (beta channel + update). Flagged 2026-11-16.
- `codex` skill (nanoclaw.dev/skills/codex/) — lets an agent group run on
  OpenAI's Codex CLI instead of Claude. Installation is host-terminal-only,
  not invocable from inside a chat session. Discovered 2026-08-24.
- Cursor (provider) — new alternate model-provider option, same pattern as
  Codex/OpenCode. Introduced in v2026.10.1-rc.1/rc.2 (2026-10-20/22).
  Host-terminal install, not chat-invocable. Low priority unless Ondřej
  wants to try it as a backend. Flagged 2026-10-26.
- `Iron Proxy` (docs.nanoclaw.dev/operate/gateways.md) — alternative
  credential gateway to OneCLI, shipped v2.4.0 (2026-09-23). Own web console
  (Iron Control) for secrets/OAuth/approvals; auto-approves model-provider
  domains and keyless local models over plain HTTP (relevant if Ondřej ever
  wants this agent talking to a home-lab local model). Needs Docker on the
  host; installed via `/add-iron-proxy`. OneCLI remains the default — this
  is additive, not a replacement. Host-level setup. Flagged to Ondřej
  2026-10-19.

## Known limitations
- Interactive/chat side went unresponsive to Ondřej from 2026-11-09 to
  2026-11-18 (per him; no error log on this side). Fixed by a full restart
  of the host machine — not a container/group restart, the whole box.
  Notably, `ncl tasks` kept running the whole time with 0 failed runs
  (daily EUR/CZK check, weekly capability check both fired on schedule) —
  the scheduler/task infra is decoupled from whatever hangs the interactive
  session, so scheduled output landing on time is not a reliable signal that
  the chat session itself is responsive. No root cause identified; flag to
  Ondřej if it recurs and ask what he observed (unresponsive vs. erroring vs.
  something else) to narrow it down next time.
- `schedule`/RemoteTrigger fails with "Unable to get organization UUID" for
  containers using API-key auth (this one, via OneCLI) — root cause was
  public issue nanocoai/nanoclaw#1806. **Closed 2026-10-02** (confirmed via
  issue thread 2026-10-26): maintainer shipped a native `ncl tasks`
  scheduler (cron schedules, one session per task) that doesn't depend on
  Claude Code RemoteTrigger — exactly the workaround already adopted below.
  No action needed. Re-checked 2026-10-26, still closed, no change.
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
- v2026.10.1-rc.1 (2026-10-20) / rc.2 (2026-10-22): agent-to-agent creation
  (`create_agent`, see above — already live in this container), Cursor
  added as a provider, OneCLI gateway updated to 1.45, webhook server
  changes, Google Chat verification improvements, better setup handling for
  slow model responses. Pre-release (rc), not yet on the stable channel,
  but the `create_agent` tool is already exposed here regardless.
- v2026.11.0-beta.1 (2026-10-31) / beta.2 (2026-11-12) / beta.3 (2026-11-14):
  2026.11.0 replaces 2026.10.1, which never reached stable — everything from
  both rc builds carries forward into this release. New since rc.2: PDF
  reading for Claude agents, `send_card` KPI/table/chart support (both
  flagged above), agents no longer cut off mid-turn on slow local models,
  stuck-channel sends no longer silence a whole conversation, Discord/Google
  Chat/Mattermost/Resend channel fixes, locally-built agent images move to
  Claude Code 2.1.321 + Haiku 5.5. Several breaking changes ship alongside
  (OneCLI gateway must be on 1.45, webhook server now binds 127.0.0.1 only,
  Google Chat needs two new env vars, Codex+ChatGPT logins need
  re-auth) — all handled by `/update-nanoclaw`, not manual host work, but
  worth knowing before Ondřej runs it. `stable` channel remains on 2026.10.0
  until 2026.11.0 itself ships.
