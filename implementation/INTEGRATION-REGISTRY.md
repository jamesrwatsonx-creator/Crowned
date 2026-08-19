# Crowned — Integration Registry

This registry records useful source repositories and the exact role each is allowed to play. Inclusion here does **not** mean its code should be copied wholesale into Crowned.

## Tier 1 — use in the initial build

### `jamesrwatsonx-creator/james-watson-gauntlet-loop`
**Role:** reasoning architecture for Barology.

Adapt:
- recursive critique / belief updates;
- independent construction and criticism;
- evidence-driven verification;
- explicit stopping/acceptance logic.

Do not import:
- unrelated app-builder surfaces;
- private/hidden constitution material;
- product-specific UI.

Crowned adapter concept:

```text
BarologyGauntlet.run(scope, retrievalPack, trigger)
```

### `jamesrwatsonx-creator/last30days-skill`
**Role:** current-culture/news discovery architecture.

Use for:
- recent hip-hop signals;
- artist/news discovery;
- YouTube/social transcript discovery;
- cross-source engagement signals;
- AI-news discovery;
- watchlist-style deltas.

Production note: it is a skill/CLI-oriented project. Crowned should adapt the needed source logic behind an ingestion service or backend adapter rather than requiring the app runtime to execute an interactive local skill.

Crowned adapter concept:

```text
RecentCulture.search(topic, window, sourcePolicy)
RecentCulture.discover(category, window)
```

### `jamesrwatsonx-creator/firecrawl`
**Role:** web search/extraction/evidence retrieval.

Use for:
- finding supporting/opposing sources;
- structured extraction;
- research across JS-heavy pages;
- article/source ingestion where permitted;
- evidence packets for Gauntlet critics.

Crowned adapter concept:

```text
EvidenceSearch.search(query, filters)
EvidenceSearch.extract(url, schema)
```

## Tier 2 — introduce when corpus/eval maturity requires it

### `jamesrwatsonx-creator/graphrag`
**Role:** offline/async transformation of unstructured research into graph-oriented corpus intelligence.

Candidate trigger:
- simple entity extraction + indexed queries fail on cross-document discovery;
- corpus size makes manual relationship maintenance unreasonable;
- multi-document thematic/community retrieval becomes a core Barology need.

Do not make every new article wait on expensive graph indexing before publication.

### `jamesrwatsonx-creator/promptfoo`
**Role:** Barology evaluation and red-team harness.

Use for:
- regression suites;
- prompt/model A/B tests;
- known human-catch benchmarks;
- overreading/hallucination tests;
- scoring consistency;
- release gates.

This belongs in development/CI, not in the consumer request path.

Crowned adapter concept:

```text
npm run eval:barology
npm run eval:barology:regression
npm run eval:barology:overreach
```

## Tier 3 — future Postgres intelligence layer

### `jamesrwatsonx-creator/pgContext`
**Role:** hybrid semantic/full-text retrieval with metadata filtering when Crowned moves to Postgres-scale corpus storage.

Best use:
- “find bars semantically similar to this concept”;
- artist/time/album filtered retrieval;
- hybrid keyword + semantic evidence search;
- candidate retrieval before graph expansion.

Adopt only after a migration decision has independently been justified.

### `jamesrwatsonx-creator/pgGraph`
**Role:** multi-hop relationship traversal over Postgres-authoritative Crowned data.

Best use:
- artist → mentor → artist → song relationships;
- bar → entity → historical event → another bar;
- shortest/limited paths between references;
- relationship-aware Barology retrieval.

Use bounded traversal and explicit path limits.

## Tier 4 — optional / pattern sources

### `jamesrwatsonx-creator/mem0`
**Role:** adaptive user/agent memory for future personalized Crowned assistants.

Potential value:
- contributor expertise-aware retrieval;
- personal research history;
- “show me bars like things I previously caught.”

Do not use it as canonical public contribution history.

### `jamesrwatsonx-creator/open-notebook`
**Role:** reference architecture for future internal Corpus Studio.

Useful patterns:
- web/video/audio/PDF ingestion;
- source organization;
- model choice;
- citations;
- transformations;
- contextual chat/research.

Do not ship its full UI or notebook product inside the consumer MVP.

### `jamesrwatsonx-creator/graphify`
**Role:** graph/provenance design inspiration.

Borrow:
- explicit edge provenance;
- distinction between directly extracted and inferred relationships;
- path/explain mental model.

Crowned extends provenance to:

`EXTRACTED / EVIDENCED / INFERRED / HUMAN`

### `jamesrwatsonx-creator/base44-to-supabase-sdk`
**Role:** migration research / possible compatibility path.

Do not include as an MVP runtime dependency.

Use only if Base44 migration is approved after measuring scale, control, cost, or graph/retrieval constraints.

### `jamesrwatsonx-creator/vibe-coding-with-base44`
**Role:** build/reference material for Base44 planning, permissions, testing, security, and integration workflows.

Do not import into runtime.

## Repos intentionally not selected for Crowned core

Examples include broad agent frameworks, UI shells, automation platforms, image/video generation stacks, and unrelated application repos.

Examples:
- AIOS;
- agency-agents;
- uAgents;
- Flowise;
- n8n;
- open-webui;
- lobehub;
- LocalAI;
- image/video generation repositories;
- TradingAgents.

They may contain useful ideas, but adding a framework without a specific measured Crowned requirement increases coupling and operational surface without improving the core product.

## Integration acceptance rule

A new dependency/service is allowed only if this sentence can be completed precisely:

> Crowned cannot currently satisfy **[named user/system acceptance test]** because **[measured limitation]**; this integration fixes that by **[specific capability]**, and we can verify success using **[observable test]**.

If that sentence cannot be completed, the integration is premature.
