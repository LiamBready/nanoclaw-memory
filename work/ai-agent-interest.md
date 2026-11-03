---
type: interest
title: AI/agent engineering pivot
description: Ondřej's personal 2026 shift into building AI agents — directly relevant to what I am.
tags: [nanoclaw, ai-agents]
---

# AI/agent engineering pivot

Distinct from his CKEditor client work: a personal thread, visible across
GitHub and his talks, of hands-on AI/agent engineering starting in 2026.

- [proactive-digital-twin-workshop](https://github.com/Simply007/proactive-digital-twin-workshop) - workshop kit for building an always-on AI agent "digital twin" using **NanoClaw + Claude Code + Telegram** — this is the same framework I run on
- [websummercamp-2026-workshops](https://github.com/Simply007/websummercamp-2026-workshops) - his notes from the AI Engineering track, Web Summer Camp 2026
- Forked huggingface/agents-course and LLM-framework comparison repos (LangChain vs. LlamaIndex)
- [ckeditor5-smart-callout](https://github.com/Simply007/ckeditor5-smart-callout) - a CKEditor plugin he built with Claude Code, i.e. already doing AI-assisted dev on client work
- Talk: "Beyond the Chatbot: Engineering Your Proactive Digital Twin" - Web Summer Camp 2026 workshop, Jul 2026

He said (Aug 23, 2026) he's currently exploring how to use AI for daily
work usage and validating the benefits, scope not narrowed yet — this
matches: he's not just experimenting with me, he taught a workshop on
exactly this a few weeks earlier.

Confirmed via research; not yet confirmed with him whether this makes me
the current running instance of that "digital twin," a separate second
one, or something else — worth asking rather than assuming.

Update Oct 18 2026: pulled [ai-library](ai-library.md), his production
DevRel prompt library. Its commit history shows real Slack scheduled
messages, Notion DB writes, and Monday.com updates happening autonomously —
access I don't have. So there is at least one other, more-privileged agent
instance already running his live DevRel workflow day to day; I'm a
separate, narrower-access assistant, not that instance. Still worth
confirming with him directly rather than treating this as settled from
inference alone.

## MCP OAuth capabilities (researched Nov 2, 2026)

Asked me to research OAuth for MCP, likely in connection with a Pimcore talk
(unconfirmed — no record of that talk yet, see
[speaking-writing.md](speaking-writing.md)). Current spec (2026-07-28 rev):

- Authorization is OPTIONAL in MCP, applies to HTTP transports only (STDIO
  uses env-provided credentials instead).
- Roles map directly to OAuth 2.1: MCP server = resource server, MCP client
  = OAuth client, separate authorization server issues tokens.
- MCP servers MUST implement OAuth 2.0 Protected Resource Metadata
  (RFC9728); clients MUST use it for AS discovery, then MUST support both
  OAuth Authorization Server Metadata (RFC8414) and OIDC Discovery.
- Client registration: three options, priority order is Client ID Metadata
  Documents (CIMD, now the recommended approach) > pre-registration >
  Dynamic Client Registration (RFC7591, now deprecated/back-compat only —
  this flipped in the 2026-07-28 revision).
- PKCE (S256) required; `resource` parameter (RFC8707) required on both
  auth and token requests to bind the token to the specific MCP server;
  issuer validation (RFC9207 `iss` param) required to prevent mix-up
  attacks.
- Scope handling: servers should return required scopes directly in the
  `WWW-Authenticate` challenge; clients do incremental step-up auth
  (union of previously-granted + newly-challenged scopes) rather than
  over-requesting upfront.
- Full spec: https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization
