---
type: portfolio
title: Speaking and writing
description: Ondřej's talks, webinars, podcasts, and articles, researched Aug 23, 2026.
---

# Speaking and writing

Full lists on his own site: talks at https://ondrej.chrastina.dev/talks/,
writing at https://ondrej.chrastina.dev/journal/. This file holds the
notable/recent ones plus links; ask him or re-fetch the site for anything
older or more obscure.

## Cadence

Very active speaker in 2025-2026 — roughly one talk, webinar, or podcast
appearance every 2-4 weeks. Writing is sparser, a handful of posts a year,
often cross-posted to dev.to (CKEditor's or Kontent.ai's publication) or,
earlier, Medium (freeCodeCamp pub, PWA series).

## Notable 2026 talks/webinars

- "Content Editing Unlocked" - TYPO3 Developer Days, Karlsruhe, Aug 2026
- "Beyond the Chatbot: Engineering Your Proactive Digital Twin" (workshop) - Web Summer Camp, Opatija, Jul 2026
- "The Real Story Behind AI in Content Editing" - CMS Summit Frankfurt, May 2026 (~80 attendees; also competed in CMS Idol)
- "Sleep Better on Release Day" (JS SDK testing strategy) - DEVWorld Amsterdam, May 2026 (~5,000 attendees)
- "Drupal in the Age of AI" - Acquia Engage Denver, Apr 2026 (co-presented w/ Seth Gregory, EPAM)
- "Extreme TypeScript: Mastering Recursion and Inference" - Brno meetup, Apr 2026 (webinar version Jan 2026)
- DrupalCon Chicago, Mar 2026 - two sessions on CKEditor in Drupal + AI content creation gaps
- Podcasts: Bas.fm ("Why Most GitHub Repos Fail"), Hackmamba, Tech Talks Daily, AI Master Podcast

## Own recurring format

"Ondrej askin'" - his own interview series, short on-the-floor conversations
with speakers/CEOs at conferences (DevWorld, DrupalCon, Acquia Engage, CMS
Summit, T3CON, WebExpo Prague, etc.). YouTube playlist:
https://youtube.com/playlist?list=PLZ9F0R17Zg3NafacHVuYqghN3ikNMgoMs

## Notable writing

- "CKEditor 5 Pitfall: Don't Forget the Paragraph Plugin" (Jun 2025)
- "DrupalCon Chicago 2026: How I vibe-coded my first custom Drupal module extending CKEditor" (Apr 2026)
- "AI Conference 2025 - CKEditor in da house" (Oct 2025)
- "From Prototype to Purpose: The Journey of Our Custom Elements at Kontent.ai" (Feb 2025)
- "How I Turned Kubernetes Into a Fun, Kid-Friendly YouTube Short" (Feb 2025)
- PWA series on Medium/freeCodeCamp (2019-2020 era)

Full article list: https://dev.to/simply007

## In progress

- **NG-Poland AI Conference (pre-recorded, 20 min)** — invite via Darek,
  recording day Thu Oct 29 2026. Restructured 2026-10-26 (per Ondřej) away
  from the generic/anonymized "Teach the Agents Well" framing (still the
  PCDD 2026 / React Summit 2027 material, see
  [ai-library.md](ai-library.md)) into two named case studies: CKEditor's
  own readable-docs/MCP-server/skill ladder from the Sep 17 2026 webinar
  "Less time, fewer tokens, better effects" with PM **Marcin Burek** (first
  pass wrongly used a different, unrelated on-premises webinar — corrected
  after Ondřej flagged the content didn't match), and the Drupal
  `ai_best_practices` skill he contributed (MR !105, 83% vs 39% eval).
  Outline, script, and slide-design prompt at
  `drafts/ng-poland-ai-conf-2026-talk.md`. Scheduled a ping for Thu 9:00am.
  Avatar-video thread: no avatar/video tool connected (checked OpenAI API
  too — not connected in this environment); tried a DIY angle (headless
  Chromium + ffmpeg screen-capture of a slide deck, since he'll narrate
  separately — "I can do the voiceover with my head later") — Chromium is
  present but ffmpeg and any browser-automation lib aren't, and no slide
  deck is actually built yet, only the design prompt. 2026-10-26: he added
  a standing todo to **explore HeyGen (paid subscription) vs. a real
  recording — authenticity question** — meant for the Notion DevRel Board,
  but I have no Notion access (that board belongs to the other,
  more-privileged agent instance running `ai-library`, see
  [ai-library.md](ai-library.md)); logging it here instead until he adds it
  himself or routes it over there.

- **"Preparing AI Best Practices for Your Product: Lessons from CKEditor,
  Drupal, and TYPO3"** — Pimcore Community Dev Days 2026, Frankfurt,
  2026-11-10, 45 min incl. Q&A (confirmed 2026-10-19). Lives in the
  `ai-library` repo (`Simply007/ai-library`, upstream — not my fork), not
  as local drafts here. Status: draft. Found on upstream branch
  `pcdd26-pimcore-research` (3 commits ahead of `main`, last commit
  2026-10-19) — confirmed pushed, per his hope Nov 2. That branch is now
  **29 commits behind `main`**, so it's stale and needs rebasing before
  more work lands on it.
  - Key files: `_outputs/talk-pcdd-2026-ai-best-practices-product.md`
    (outline), `_outputs/talk-pcdd-2026-ai-best-practices-product-research.md`
    (event/Pimcore/Copilot/Agent Bundle/observability research),
    `_outputs/cfp-pimcore-community-dev-days-2026-ai-best-practices.md` (CFP).
  - Audience note from the outline: Pimcore/Symfony/PHP devs, intermediate
    to senior, AI-curious but skeptical — some saw a Pimcore RAG+MCP talk
    and an Agentic PXM masterclass at the 2025 edition already.
  - He asked (Nov 2) for an OAuth-for-MCP research pass, probably feeding
    this talk's Copilot/Agent Bundle material — see
    [ai-agent-interest.md](ai-agent-interest.md) for that research.
  - He said he has a new story for the talk "once I start working on it" —
    noted here to resurface when he picks this up.
  - He asked for a prep branch, suspecting one exists — it does
    (`pcdd26-pimcore-research` above, PR #13 on upstream). Per the GitHub
    rules in CLAUDE.md, `Simply007/ai-library` is upstream: I can
    read/propose but never push or commit there directly, so instead of
    touching that branch I rebased it. 2026-11-02: created
    `liam/pcdd26-pimcore-prep` on my fork (`LiamBready/ai-library`) with
    the same 3 commits replayed on top of current upstream `main`, opened
    as **PR #18** against `Simply007/ai-library` `main`. Conflict both
    times on `personal-website-sync/mapping.md` line 31 ("Skipped" list) —
    other work keeps landing on `main` adding its own clause to that same
    line (first the pre-existing `launch-*`/`interview-*`/etc. wording,
    then PR #17's `decision-*` clause); each time, merged this PR's
    `talk-*-research` addition in alongside rather than reverting the
    other changes. Closed #13 (with Ondřej's explicit one-off override of
    the "never close his PRs" rule — rule itself stays as-is, he wants to
    keep approving this case by case) with a comment pointing to #18.
    #18 is `mergeable: clean` as of 2026-11-03 13:40 — but given how often
    `main` is moving (another, more-privileged agent instance is actively
    merging PRs here), it may need yet another rebase before he merges it.

## Recurring topics

CKEditor/rich-text editing + AI; headless CMS ecosystem (Kontent.ai,
bridging into Drupal/TYPO3); DevRel craft itself (repo health, SDK testing
strategy); AI applied to content/dev tooling broadly; TypeScript deep dives
and other web fundamentals as a secondary thread.
