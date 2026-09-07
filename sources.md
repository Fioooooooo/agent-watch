# Sources & Filtering Policy

> Agent Watch source policy V2

## Scan model

Agent Watch uses a two-stage discovery model:

1. **Mandatory source checklist** — deterministic recall floor. Every listed source group must be actively checked on every daily run through its official latest/release/changelog entry points. Keyword search is not a substitute for this step.
2. **Open discovery** — after the checklist is complete, use broader search to discover important Agent / Harness / Coding Agent developments outside the fixed registry.

Filtering happens only after candidates from both stages have been collected.

The system must distinguish these states:

- `checked` — the source was successfully inspected; no qualifying new item may be present.
- `failed` — the source could not be reliably inspected because of access, parsing, search, API, or other execution failure.

A failed source must never be interpreted as “no update”. If any mandatory source fails, the daily report must record `coverage incomplete` and identify the failed source(s).

## Mandatory Agent / Harness checklist

Every daily run must inspect the newest official Blog / Engineering / Changelog / Release Notes / product update / GitHub Release entries for each source below and compare publication time with the previous daily report boundary.

### OpenAI / Codex
- OpenAI product / research release feed
- OpenAI release notes / changelog
- Codex official GitHub Releases

### Anthropic / Claude Code
- Anthropic News
- Anthropic Engineering / research posts relevant to agents
- Claude Code official changelog / GitHub Releases

### Google / Gemini CLI
- Google / Gemini official product and developer announcements relevant to agents
- Gemini CLI official GitHub Releases

### Augment / Auggie
- Augment official Blog / Engineering posts
- Auggie official release / changelog sources when available

### Qwen / Qwen Code
- Qwen official Blog
- Qwen Code official GitHub Releases / changelog

### Cursor
- Cursor official Changelog
- Cursor official Blog / Engineering posts

### Cognition / Devin
- Cognition official Blog / Engineering posts
- Devin official product / changelog updates

### GitHub Copilot
- GitHub Changelog entries for Copilot
- GitHub Engineering / Blog posts exposing Copilot agent architecture or runtime changes
- Copilot CLI official release sources when applicable

### Zed / ACP
- Zed official Blog / release notes relevant to agents
- ACP official specification / protocol updates
- Zed / ACP official GitHub Releases when applicable

### Windsurf
- Windsurf official Changelog
- Windsurf official Blog / Engineering posts

### Manus
- Manus official product / engineering / changelog sources

### Kimi / Kimi Code
- Kimi official Blog
- Kimi Code “What’s New” / release notes
- Kimi Code CLI changelog / official releases

## Mandatory model-release checklist

Every daily run must also inspect the newest official model-release entries from:

- OpenAI
- Anthropic
- Google DeepMind / Gemini
- Qwen
- DeepSeek
- Kimi / Moonshot AI
- Z.ai / GLM

Other model developers such as Meta are handled through open discovery unless they become a recurring high-value source.

Only include model releases that materially affect at least one of: Coding, agentic capability, reasoning, tool use, computer use, long context, inference efficiency, or APIs / architecture that change Agent Harness design.

Generic chat models, small derivative variants, embedding models, image models, and speech models are excluded by default unless they have direct Agent architecture significance.

## Harness observation checklist

These are lower-frequency technical observation sources. They should still be checked regularly, but routine version churn is excluded:

- LangChain / LangGraph
- Vercel AI SDK
- OpenHands

Include only updates that materially change Agent loops, harness architecture, context engineering, memory, checkpointing, durable execution, long-running agents, recovery, multi-agent systems, sandboxing, MCP, or tool runtime design.

## Open discovery

After all mandatory source groups have been checked, perform an open-ended search for high-value developments not captured by the registry. This stage is intended to discover:

- new Agent / Harness projects or vendors
- important protocol work
- deep engineering posts
- major model or runtime releases outside the fixed source list
- research with direct engineering implications
- emerging techniques in context engineering, multi-agent orchestration, sandboxing, recovery, tool runtime, computer use, or long-running agents

Open discovery supplements the checklist; it never replaces it.

## Candidate and filtering workflow

For every mandatory source group:

1. Open or retrieve its official latest / release / changelog listing.
2. Inspect newly published entries since the previous daily-report boundary.
3. Record title, publication time, official URL, and source.
4. Add all plausible Agent / Harness / Coding Agent candidates to the candidate set.
5. Only after all mandatory checks are complete, run open discovery.
6. Deduplicate candidates by canonical URL / title / release identifier.
7. Apply relevance and value filtering.
8. Archive the final high-value evidence.
9. Validate source coverage before declaring the run complete.

Do not use a sliding historical recovery window as a substitute for completing the mandatory checklist correctly.

## Coverage validation

Each daily run must internally maintain a coverage checklist for all mandatory source groups.

A run is complete only when every mandatory group is either:

- `checked`, or
- explicitly `failed` and reported as `coverage incomplete`.

“Nothing important found” is a valid conclusion only for successfully checked sources.

## High-value topics

- Agent architecture
- Agent harness
- Coding agents
- Context engineering
- Memory and context provenance
- Multi-agent systems
- Sandbox and permissions
- MCP / ACP / A2A
- Skills and tool use
- Computer use / browser use
- Evaluation
- Long-running agents
- Checkpoint and recovery
- CLI / SDK / protocols
- Agent runtime

Deep engineering articles receive higher weight than ordinary feature announcements, especially material exposing actual design decisions around agent loops, tool surfaces, session management, context management, token efficiency, sandboxing, security boundaries, recovery, and multi-agent orchestration.

## Daily → Weekly responsibility

Daily reports are the primary evidence and discovery layer. They perform mandatory source enumeration, open discovery, candidate recall, filtering, coverage validation, and archival.

Weekly reports use archived daily reports as their primary evidence set and focus on cross-vendor synthesis and trend analysis. Weekly generation may revisit official sources to validate claims, fill an obvious gap, or capture a major release, but should not duplicate the entire daily scanning workload.

## Exclusions

- Marketing announcements
- Fundraising
- Customer case studies
- Partnership announcements
- SEO tutorials
- Generic AI news
- Routine UI changes
- Model news unrelated to Agent / Harness engineering

Coverage should never be expanded merely to fill a report. If a period has no meaningful updates, the report should say so.