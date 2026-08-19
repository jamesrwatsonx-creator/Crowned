# Crowned — Initial Architecture

## Architectural verdict

Build Crowned as a **Base44-first consumer product with Barology treated as a logical service boundary from day one**.

The MVP should not depend on a giant external graph/search stack. Base44 can own product state while external services supply evidence/research. GraphRAG, pgContext, pgGraph, and deeper memory infrastructure are introduced only when measured corpus/retrieval limitations justify them.

## System map

```text
                          CROWNED CLIENT
                              │
                    Base44 UI / Auth / State
                              │
      ┌───────────────────────┼────────────────────────┐
      │                       │                        │
 COMMUNITY / SOCIAL        CONTENT                  CROWN
 profiles                  artists                  rankings
 contributions             albums                   scores
 votes                     songs                    methodology
 activity                  news                     snapshots
      │                       │                        │
      └───────────────────────┼────────────────────────┘
                              │
                     BASE44 BACKEND FUNCTIONS
                              │
                 ┌────────────┴────────────┐
                 │                         │
            BAROLOGY API              CORPUS INGEST
                 │                         │
      ┌──────────┼──────────┐      ┌───────┼────────┐
      │          │          │      │       │        │
   LLM(s)   Retrieval   Gauntlet  News   Web     Metadata
      │          │          │      │       │        │
      └──────────┴──────────┘      └───────┴────────┘
                 │                         │
                 └────────────┬────────────┘
                              ↓
                     CANONICAL CROWNED DATA
```

## Base44 responsibilities

Use Base44 for the first product runtime:

- authentication;
- UserProfile / Artist / Album / Song entities;
- LyricSpan references/authorized text;
- Interpretation / Revision / Evidence entities;
- Contribution / Vote / ExpertiseScore;
- NewsArticle / CorpusEvent;
- GauntletRun / AgentResult metadata;
- ScoreSnapshot / RankingSnapshot;
- activity events;
- backend functions that call Barology/retrieval integrations;
- realtime UI updates where appropriate.

## Logical Barology service

Even if implemented initially with Base44 functions, expose a narrow internal contract.

Suggested operations:

```text
analyzeSong(songId, options)
analyzeSpan(spanId, options)
challengeInterpretation(interpretationId, contributionId)
addHumanInterpretation(spanId, contributionId)
reGauntlet(scopeType, scopeId, trigger)
getCanonicalBreakdown(songId)
getEvidence(interpretationId)
scoreSong(songId, methodologyVersion)
```

The client never directly coordinates specialist agents.

## Initial function boundaries

### `ingest_music_metadata`
Creates/updates Artist, Album, Song, credits, identifiers, release dates.

### `ingest_news_item`
Normalizes news article metadata; extracts entity/event candidates; stores provenance.

### `research_evidence`
Given a claim/reference, queries permitted search/retrieval providers and returns normalized EvidenceItems.

### `run_barology_analysis`
Creates GauntletRun; executes discovery specialists; performs retrieval; runs critics; synthesizes canonical candidates.

### `submit_contribution`
Stores human submission and triggers scoped review when required.

### `adjudicate_interpretation`
Blind independent analysis → canonical comparison → critics → evidence judge → revision/status update.

### `update_scores`
Recomputes affected span/song/album/artist score snapshots after a canonical interpretation changes.

### `publish_activity_event`
Emits user-visible activity from significant state changes.


## Provider configuration and zero-key mode

The executable Base44 build must work before optional third-party APIs are configured.

All external providers sit behind a server-side registry. Each adapter reports `READY / UNCONFIGURED / DEGRADED / ERROR`. When credentials are absent, Base44 selects a deterministic fixture adapter or returns an explicit unavailable state; it never exposes a secret-entry flow to end users and never lets an optional provider failure break navigation.

The stable secret names, adapter contracts, activation steps, and provider-free acceptance tests are canonical in `implementation/API-AND-SECRETS.md`.

```text
Base44 client
    ↓
backend function
    ↓
provider registry
    ├── configured live adapter
    └── deterministic fixture adapter
    ↓
normalized Crowned result
```

Provider selection must not alter the canonical `Artist / Album / Song / LyricSpan / Interpretation / EvidenceItem` contracts. No privileged provider call is made directly from client code.

## Background processing

Song analysis and re-Gauntlet operations must not block a normal page request.

Use states such as:

`QUEUED → DISCOVERY → RETRIEVAL → CRITIQUE → JUDGING → COMPLETE / FAILED`

The UI can show analysis progress without exposing private chain-of-thought. Store structured agent conclusions/evidence, not hidden reasoning transcripts.

## Retrieval strategy — MVP

MVP retrieval should be source-scoped and explicit:

1. song/artist catalog records already in Crowned;
2. Crowned news/corpus events;
3. approved external music metadata;
4. web evidence via Firecrawl or equivalent;
5. recent culture intelligence from adapted `last30days` ingestion;
6. human-submitted sources.

Do not add GraphRAG or a vector database until simple indexed retrieval fails measured acceptance tests.

## Future retrieval strategy

When the corpus becomes large:

```text
Postgres source of truth
    ├── pgContext: semantic + keyword + filtered retrieval
    └── pgGraph: multi-hop graph traversal
             ↓
        Barology retrieval pack
             ↓
        Gauntlet analysis
```

GraphRAG may be used as an offline/async graph-building pipeline for unstructured research material.

## News architecture

News is both a user-facing media product and a corpus-ingestion path.

```text
SOURCE DISCOVERY
   ↓
normalize article metadata
   ↓
extract artist / album / song / event / person / company / place / date
   ↓
verify / de-duplicate
   ↓
PUBLISH NEWS ARTICLE
   +
WRITE PROVENANCE-LINKED CORPUS EVENT / RELATIONS
```

Do not automatically treat article claims as facts. Preserve claim/source status and confidence.

## Scoring architecture

Never compute one permanent opaque score.

Every score record is versioned:

```text
methodology_version
coverage
component_scores
confidence
final_score
created_at
```

A ranking row points to a ScoreSnapshot. Methodology upgrades create new snapshots rather than silently mutating history.

## Activity architecture

Activity is event-driven from meaningful domain changes, not manual social posting alone.

Candidate event types:

- SONG_ANALYZED
- INTERPRETATION_ADDED
- HUMAN_CATCH_VALIDATED
- INTERPRETATION_DISPUTED
- INTERPRETATION_REJECTED
- RE_GAUNTLET_COMPLETE
- RANK_CHANGED
- RELEASE_ADDED
- NEWS_PUBLISHED
- FIRST_FIND
- EXPERTISE_LEVEL_CHANGED

## Security / privacy

- all provider/API secrets server-side only;
- private Gauntlet system instructions/constitution server-side only;
- client receives structured conclusions, scores, evidence, and statuses — never privileged prompts or hidden reasoning;
- rate-limit analysis/contribution endpoints;
- protect admin/moderator actions with explicit roles;
- public user profile data should be separated from auth/security metadata;
- source provenance must not leak credentials, cookies, private sessions, or restricted source text.

## Rights boundary

Crowned should be able to analyze:

- licensed/authorized lyrics;
- user-supplied lyrics/text where appropriate;
- permitted captions/transcripts;
- short referenced spans where legally permitted;
- metadata and source links.

Do not design the database or UX around unauthorized permanent storage of complete third-party lyric catalogs.

## Migration boundary

The Base44 MVP must preserve domain semantics so later infrastructure can move without rewriting product behavior.

If/when migration is warranted:

```text
Base44 product semantics
        ↓
compatibility/export layer
        ↓
Supabase/Postgres
        ↓
pgContext + pgGraph where justified
```

Migration trigger examples:

- retrieval latency/scale is measurably unacceptable;
- data export/control requirement becomes material;
- graph traversals are core and difficult in current storage;
- analysis workloads exceed practical Base44 backend limits;
- cost/unit economics materially improve with a dedicated backend.

Do not migrate because a future stack looks more sophisticated.
