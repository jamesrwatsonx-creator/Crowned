# CROWNED

**AI-powered hip-hop intelligence: the latest in hip-hop, every bar decoded, every lyricist ranked, and a reputation system for the humans who catch what AI misses.**

> **Splash copy**
>
> **CROWNED**  
> *Powered by AI*  
> “The latest in hip-hop. Every bar decoded. Every lyricist ranked. Build your profile by catching what AI—and everybody else—missed.”

## Product thesis

Crowned combines four products that reinforce one another:

1. **Crowned News** — a live hip-hop and AI news product that keeps users returning and continuously expands the cultural corpus.
2. **Barology** — an AI system that analyzes songs span-by-span, not merely line-by-line, across literal meaning, phonetics, rhyme, entendres, schemes, artist catalogs, hip-hop history, culture, historical events, current events, and long-range callbacks.
3. **The Crown** — inspectable rankings for lyricists, albums, songs, verses, and bars.
4. **Human reputation** — profiles built around catches, successful challenges, AI misses, expertise, and contribution history rather than follower count alone.

The core loop is:

```text
CULTURE HAPPENS
    ↓
CROWNED OBSERVES IT
    ↓
NEWS + CORPUS
    ↓
BAROLOGY ANALYZES
    ↓
GAUNTLET CHALLENGES
    ↓
HUMANS CATCH MISSES / DISPUTE CLAIMS
    ↓
EVIDENCE + RE-GAUNTLET
    ↓
CANONICAL INTERPRETATION GRAPH IMPROVES
    ↓
RANKINGS + REPUTATION UPDATE
```

## Current build target

**MVP platform:** Base44-first consumer application with modular external intelligence services.

Do not copy whole source repositories into Crowned. Adapt only the capabilities Crowned needs behind explicit interfaces. The consumer app remains the product; research, retrieval, graph, evaluation, and memory systems remain replaceable modules.

## Repository contract

```text
Crowned/
├── product/          canonical product truth
├── design/           current design direction + later final design package
├── implementation/   architecture, Barology engine, integrations, build plan
├── app/              executable product implementation when Base44/code export lands
├── tests/            Barology evals, regression sets, product acceptance tests
├── .github/          CI/review automation when implementation begins
├── AGENTS.md          instructions for coding/research agents
└── README.md
```

## Core technical systems

**Build now**

- Base44 — app shell, auth, profiles, entities, voting, activity, rankings, news surfaces, backend functions.
- James Watson Gauntlet Loop — adapted into the Barology adversarial reasoning loop.
- `last30days-skill` — live culture/news discovery pattern and source intelligence.
- Firecrawl — web research, evidence retrieval, structured extraction.

**Add as the corpus matures**

- GraphRAG — unstructured sources → structured knowledge graph.
- Promptfoo — Barology regression tests, prompt/model comparisons, red-team/evaluation harness.
- pgContext — hybrid semantic + full-text retrieval over a future Postgres corpus.
- pgGraph — multi-hop relationship traversal over the future Crowned graph.

**Optional / later**

- Mem0 — user/agent memory when contributor histories become rich enough to justify adaptive retrieval.
- Open Notebook — patterns for an internal Crowned Corpus Studio for ingesting interviews, podcasts, PDFs, web pages, video, and audio.
- Graphify — provenance ideas for EXTRACTED vs INFERRED graph edges.
- Base44-to-Supabase SDK — possible migration path if Base44 becomes a scaling constraint.

## Non-negotiable reasoning rule

Barology must not optimize for finding the maximum number of meanings. It must optimize for **defensible interpretations**.

Every interpretation preserves:

- exact lyric span;
- interpretation type;
- evidence;
- connected bars/entities;
- source/provenance;
- AI/human origin;
- confidence;
- coincidence/overreach risk;
- community support/opposition;
- current status;
- complete revision history.

Rejected interpretations are hidden from canonical display, never erased from history.

## Start here

1. `product/APP-CONCEPT.md`
2. `product/SCREEN-INVENTORY.md`
3. `product/DATA-AND-INTEGRATIONS.md`
4. `product/APP-CONTRACT.yaml`
5. `design/DESIGN-DIRECTION.md`
6. `implementation/ARCHITECTURE.md`
7. `implementation/BAROLOGY-GAUNTLET.md`
8. `implementation/INTEGRATION-REGISTRY.md`
9. `tests/BAROLOGY-EVAL-PLAN.md`
10. `AGENTS.md`

## Success condition

The MVP succeeds when this sequence feels exceptional and works end-to-end:

```text
HOME / ACTIVITY
→ ARTIST
→ ALBUM
→ SONG
→ LYRICS
→ SWIPE TO BAROLOGY
→ INSPECT EVIDENCE
→ CHALLENGE / ADD WHAT AI MISSED
→ GAUNTLET ADJUDICATION
→ HUMAN PROFILE CREDIT
→ RANKING / CORPUS UPDATE
```
