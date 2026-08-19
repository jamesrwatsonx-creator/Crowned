# Crowned — Build Plan

## Phase 0 — freeze product truth

Before implementation changes product scope, confirm:

- `product/APP-CONTRACT.yaml`
- `product/APP-CONCEPT.md`
- `product/SCREEN-INVENTORY.md`
- `product/DATA-AND-INTEGRATIONS.md`
- `design/DESIGN-DIRECTION.md`

The next major artifact should be the final screen/design package, not random UI generation.

## Phase 1 — Base44 product skeleton

Create the Crowned Base44 app and connect/export it into this repository.

Implement:

- auth;
- UserProfile;
- Artist;
- Album;
- Song;
- Verse;
- LyricSpan;
- Interpretation;
- InterpretationRevision;
- EvidenceItem;
- Contribution;
- Vote;
- GauntletRun;
- ScoreSnapshot;
- RankingSnapshot;
- NewsArticle;
- CorpusEvent;
- activity events.

Acceptance condition: real navigation and the complete seeded core loop work with zero optional provider credentials before external AI/news integrations are introduced. Every missing provider resolves to a fixture or explicit unavailable state under `implementation/API-AND-SECRETS.md`.

## Phase 1.5 — provider registry and secret readiness

Implement the server-side adapter registry and stable configuration contract before adding live providers.

Required adapter states:

- `READY`;
- `UNCONFIGURED`;
- `DEGRADED`;
- `ERROR`.

Wire deterministic fixture adapters for video discovery, music metadata, authorized/demo lyric input, evidence/news, and the Barology model. Add an admin-only provider status response that reveals configuration state but never secret values.

Acceptance condition: adding YouTube, Firecrawl, a selected Barology model, or another approved provider requires only Base44 secret configuration plus adapter activation—not UI or canonical-entity rewrites.

## Phase 2 — signature navigation + profile system

Build:

- animated floating bottom navigation;
- center Crown destination;
- edge-drag command drawer;
- section subnavigation;
- human profile polarity;
- artist profile polarity;
- artist → album → song browsing hierarchy.

Acceptance condition: navigation gestures do not collide and both profile types share one structural component model.

## Phase 3 — Song / Barology core UX

Build the most important interaction before breadth:

- Lyrics state;
- exact span highlighting;
- full-screen Lyrics ↔ Barology swipe;
- aligned bar position between states;
- interpretation cards;
- evidence viewer;
- connected-bar jump;
- support/oppose;
- Add What Barology Missed.

Acceptance condition: a user can complete the core loop with seeded interpretations even before full AI automation exists.

## Phase 4 — Barology Gauntlet V0

Implement the service boundary from `BAROLOGY-GAUNTLET.md`.

Start smaller than the final specialist set:

1. Literal Analyst
2. Entendre/Wordplay Analyst
3. Phonetic Analyst
4. Context/Scheme Analyst
5. Catalog/History Analyst
6. General Culture/Historical Analyst
7. Missing-Meaning Analyst
8. Skeptic
9. Reference/Evidence Critic
10. Judge/Synthesizer

Run blind discovery before critics see canonical output.

Store structured conclusions, not raw hidden chain-of-thought.

Acceptance condition: the same deterministic input produces versioned, inspectable structured interpretations with evidence/status/provenance.

## Phase 5 — human challenge loop

Implement:

- missing-meaning submission;
- structured opposition reasons;
- scoped Mini-Gauntlet;
- canonical revision history;
- successful challenge/catch credit;
- expertise counters;
- activity feed events;
- vote thresholds for periodic review.

Acceptance condition: a human can overturn/improve an interpretation without deleting historical state.

## Phase 6 — rankings

Implement versioned component scores and ranking snapshots.

Do not calculate rankings from raw candidate interpretations. Only canonical/adjudicated analysis contributes.

Acceptance condition: every ranking value can drill down to score components and underlying analyzed material.

## Phase 7 — News + living corpus

Adapt the recent-culture discovery layer and web evidence layer.

Build:

- Hip-Hop Today;
- Releases;
- Industry;
- Culture;
- AI News;
- article pages;
- artist/entity linking;
- CorpusEvent extraction;
- source provenance;
- activity feed integration.

Acceptance condition: a published news item can create or update provenance-linked corpus context without automatically treating every article claim as verified fact.

## Phase 8 — Top Breakdowns / discovery loops

Add:

- Recently Analyzed;
- Most Complex;
- Highest Rated;
- Most Discussed;
- Most AI Misses;
- Disputed;
- Unresolved;
- song heat strips/maps.

Acceptance condition: users have reasons to browse Barology even when they did not arrive searching for a specific artist.

## Phase 9 — evaluation harness

Promote a meaningful set of known cases into `tests/` and wire Promptfoo or equivalent.

Release gates must track recall and overreach simultaneously.

Acceptance condition: Barology cannot be changed without a visible before/after regression report.

## Phase 10 — scale only when measured

Evaluate GraphRAG, Postgres migration, pgContext, pgGraph, and Mem0 only when current architecture fails a named acceptance test.

No speculative infrastructure migration.

## MVP release condition

The product is ready for an MVP test when a user can:

1. enter Crowned;
2. browse/search an artist;
3. select an album/song;
4. read a song;
5. swipe to Barology;
6. inspect multiple evidence-backed interpretations;
7. challenge or add a missing interpretation;
8. receive an adjudication result;
9. see the contribution reflected on their profile;
10. browse live activity/news/rankings without leaving the product model.
