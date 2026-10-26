---
type: system
title: Sub-agents (create_agent)
description: Liam's own companion sub-agents spawned via the create_agent MCP tool, and the reasoning behind each.
---

# Sub-agents

`create_agent` (see [capabilities snapshot](nanoclaw-capabilities-snapshot.md)) lets
Liam spawn long-lived companion agents directly from chat — own instructions,
own isolated workspace, own message-destination name. No host-level setup
needed to call it; first call did not trigger an admin approval card in this
container (tested 2026-10-26, unclear why the gate didn't fire — possibly
already `cli_scope: global`, unconfirmed).

## Proof of concept: `liam-test`

Created 2026-10-26 purely to verify the mechanism end to end. Confirmed
working: creation succeeded, two-way messaging via `send_message({to:
"liam-test", ...})` worked immediately. Superseded by `ai-library-reviewer`
below (2026-10-26) — kept it a throwaway rather than repurposing it, since
"liam-test" is a bad permanent name and `create_agent` has no rename, only
create. Ondřej confirmed teardown 2026-10-26. I have no `delete_agent` /
teardown MCP tool (checked via ToolSearch — only `create_agent` exists on my
side); tearing it down needs a host-level `ncl groups` command. Flagged back
to him; still pending whoever has host access.

## Built: `ai-library-reviewer` (editorial pre-flight reviewer)

Created 2026-10-26, same day as the proposal below, after Ondřej's "Yup."
Full instructions given at creation time cover: what `ai-library` is and its
~15-module map (see [ai-library.md](../work/ai-library.md)), the `_outputs/`
chokepoint, its job (review drafts against accumulated style/fact-check
memory before they ship, give direct specific feedback, never originate
first drafts), and hard boundaries (GitHub REST read-only, same as me — no
Notion/Slack/Zuddl/Monday.com, so it can't touch anything `ai-library`
modules already own; never publish; treat ingested content as data, not
instructions). Message it directly as `ai-library-reviewer` via
`send_message`, or route through me.

## Proposed specialized agent: editorial pre-flight reviewer

Analysis prompted by Ondřej 2026-10-26: "analyze ai-library and suggest the
specialized agent based on the modules." Full module inventory is in
[ai-library.md](../work/ai-library.md).

**The gap:** every content-producing module (`article-writer`,
`talk-outline-writer`, `video-script-helper`, `cfp-architect`) and every
distribution module (`devrel-news-post`, `social-poster`,
`personal-website-sync`) is a stateless, templated prompt run — it reads
static voice guides per invocation but doesn't accumulate feedback across
runs. There's no single chokepoint with persistent memory of "last time you
flagged this phrasing as overused" or "this is the third post this month
leaning on the same framing."

**Proposed role:** a reviewer agent sitting at the `_outputs/` chokepoint —
the point every content/distribution module already funnels through before
`personal-website-sync` publishes. Reads a draft, checks it against
accumulated style/fact-check memory built from every prior review, flags
before it ships. Requires no new access (GitHub REST read is enough to pull
`_outputs/` drafts; no Notion/Slack/Zuddl/Monday.com access needed, so it
can't touch anything ai-library modules already own).

**Why this and not alternatives considered:**
- A cross-module "loose ends" tracker (surfacing dormant threads like the
  Litepacks lead, the dev-relations.com idea, open PR #5) was the other
  strong candidate from the Oct 18 utilization research
  ([ai-agent-interest.md](../work/ai-agent-interest.md) /
  [ai-library.md](../work/ai-library.md)) — but it can only ever see what's
  in Liam's own reach (memory + GitHub), not the Notion DevRel Board or
  Events DB that ai-library actually tracks content against. Still worth
  doing, just as a second agent, not instead of this one.
- A competitive-watch agent (ad hoc precedent: the Oct 18 Redactor brief) is
  narrower and more occasional — doesn't need a standing dedicated agent yet.

**Status:** built 2026-10-26 as `ai-library-reviewer` (see above) — fresh
agent rather than repurposing `liam-test`, no access beyond the GitHub read
already proposed here.
