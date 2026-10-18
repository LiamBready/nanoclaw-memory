---
type: project
title: ai-library
description: Ondřej's production library of AI prompt modules running his day-to-day DevRel work at CKEditor — actively used by a separate, more-privileged agent instance, not by me.
tags: [devrel, ckeditor, ai-agents, github]
---

# ai-library

A git repo of reusable prompt/workflow "modules" that drive Ondřej's actual
DevRel operations. Learned by pulling the repo directly, Oct 18 2026 (see
[GitHub rules](../index.md) in persona for repo roles).

- Upstream: `Simply007/ai-library` (his repo, read-and-propose-only for me)
- My fork: `LiamBready/ai-library` (where I'd stage any contribution) — as
  of Oct 18 2026 has no branches beyond `main` and one closed test PR (#7).
  No live work from me there.

## What it is

A collection of ~15 modules, each a self-contained prompt + reference
materials (voice guides, templates, past examples) for one recurring DevRel
task. Every module inherits `_general/module-base.md`: shared defaults
(typography rules, never-guess-facts, approval gates before anything
leaves the repo, outputs to `_outputs/` with YAML front matter) plus a
**DevRel Board** (Notion Kanban) tracking policy keyed per-module as
`ask`/`always`/`never`.

### Modules and how they connect

- **Content creation**: `article-writer`, `talk-outline-writer` (+ workshop
  mode, can scaffold a workshop repo), `video-script-helper`, `cfp-architect`
- **Metadata**: `youtube-video-metadata`, `youtube-short-metadata`
- **Distribution**: `devrel-news-post` (internal Slack #devrel ~3PM posts),
  `social-poster` (LinkedIn/X/Bluesky/Reddit), `reddit-mention-responder`
  (CKEditor mention monitoring + replies)
- **Orchestration**: `conference-research` (scores/shortlists conferences,
  syncs to a Notion Events DB, feeds `cfp-architect`), `devrel-schedule`
  (reads the Notion "#devrel schedule" DB, generates posts via
  `devrel-news-post`, schedules them as actual Slack scheduled messages),
  `webinar-workflow` (full CKEditor webinar lifecycle via Zuddl API +
  Notion, supersedes old `webinar-helper`), `ondrej-askin-workflow`
  (interview video production via Google Drive + Monday.com)
- **Internal/admin**: `meeting-prep`, `expense-report` (post-trip notes +
  receipts → the Slack DM he sends Marta in finance, per-diem-ready split,
  confidential/never published)
- **Publishing**: `personal-website-sync` — crawls `_outputs/` and other
  sources, batches a reviewable log, then publishes to
  `ondrej.chrastina.dev` (Kontent.ai + Gatsby) via Management API + triggers
  a GitHub Actions rebuild

Pipeline shape: content/metadata/distribution modules all feed `_outputs/`,
which `personal-website-sync` later publishes. `devrel-schedule` and
`webinar-workflow` are the two modules that actually touch external systems
on a schedule (Slack scheduled messages, Zuddl, Notion).

## This runs on different access than me

Commit history (Oct 12–16 2026) shows real, autonomous execution: Slack
scheduled messages at specific times, Notion row updates, a Monday.com-
linked expense card, a Slack tool permission that was refused and had to be
worked around manually. That requires Slack, Notion, and Monday.com access
I don't have in my current early phase (no calendar/files, no email).

This answers the open question in
[ai-agent-interest.md](ai-agent-interest.md): there is at least one other,
more-privileged agent instance already running his live DevRel workflow
day to day. I am a separate, narrower-access assistant — not that instance.
Worth confirming with him directly rather than treating this as settled.

## State as of Oct 18 2026

- Upstream `main` only has one open PR: **#5**, "n8n + CKEditor AI showcase:
  Branded Report Generator" — his own draft, not mine, still open.
- Everything else (modules #2, #3, #4, #6, #8, #9, #10, #11) is merged/closed.
- Recent real usage: Rotterdam trip expense report (sent, then corrected),
  PCDD 2026 speaking announcements across LinkedIn/X/Bluesky/Reddit,
  devrel-schedule swaps (fintech_devcon moved twice, Cybercamp.ai, Pimcore
  speaking slot), a Reddit reply on r/buildinpublic.
