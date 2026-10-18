---
type: system
title: Scheduling — how to actually do it
description: The correct mechanism for recurring/one-shot agent-initiated tasks in this container. Read this before ever building a workaround.
---

# Scheduling

Use `ncl tasks` (local CLI, `/usr/local/bin/ncl`) for anything recurring or
scheduled ("check X daily", "remind me tomorrow at 6pm"). It is separate
from claude.ai's Routines/RemoteTrigger API and does not depend on OAuth or
an organization UUID — it works from this API-key-auth container. The
`/schedule` skill (claude.ai Routines) fails here with "Unable to get
organization UUID" (see `nanoclaw-capabilities-snapshot.md`, issue
nanocoai/nanoclaw#1806) — don't use it for this container; use `ncl tasks`
instead.

```
ncl tasks create --name "<short>" --prompt "<what to do when woken>" --recurrence "<cron, instance TZ>"
ncl tasks create --name "<short>" --prompt "<...>" --process-after "<time>"   # one-shot
ncl tasks list / get <id> / pause <id> / resume <id> / cancel <id> / delete <id>
```

Full syntax: `ncl tasks create --help`.

## Lesson learned (2026-08-25 to 2026-08-28)

Spent 3 days on a SessionStart-hook + timestamp-file workaround before
finding this. It never actually fired (settings.json watcher didn't pick up
the edit — a real limitation of that mechanism, worth remembering
separately), and was the wrong tool regardless. Check for `ncl` / `ncl tasks
--help` FIRST next time something needs to run on a schedule, before
reaching for hooks or claude.ai Routines.

## Active recurring tasks

- `eur-czk-check` — daily 09:00, reports EUR→CZK rate + trend to Ondrej
  (he's watching for a good moment to convert EUR to CZK).
- `nanoclaw-capability-check` — weekly Monday 09:00, diffs NanoClaw
  skills/capabilities against `nanoclaw-capabilities-snapshot.md`, only
  messages Ondrej if something new/usable is found.
