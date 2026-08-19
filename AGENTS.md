# CROWNED — Agent Instructions

This repository is the permanent source of truth for Crowned.

## Read order

Before changing implementation, read:

1. `README.md`
2. `product/APP-CONTRACT.yaml`
3. `product/APP-CONCEPT.md`
4. `product/SCREEN-INVENTORY.md`
5. `product/DATA-AND-INTEGRATIONS.md`
6. `design/DESIGN-DIRECTION.md`
7. `implementation/ARCHITECTURE.md`
8. `implementation/BAROLOGY-GAUNTLET.md`
9. `implementation/INTEGRATION-REGISTRY.md`
10. `tests/BAROLOGY-EVAL-PLAN.md`

If these files disagree, surface the conflict. Do not silently choose a new product direction.

## Product boundary

Crowned is the consumer product. Barology is the intelligence engine underneath it. External repositories are capability sources, references, or independently deployable services — not a reason to turn Crowned into a monorepo of unrelated frameworks.

Never vendor an entire external repository merely because a useful pattern exists inside it. Extract the smallest capability behind a stable interface, preserve license/attribution requirements, and keep it replaceable.

## Build order

Build the smallest complete loop before breadth:

`artist → album → song → lyrics → Barology → challenge → adjudication → profile credit`

News, activity, rankings, navigation, and discovery should support this loop rather than displace it.

## Barology truth rules

1. Analyze exact lyric spans, including overlapping spans; do not assume one line equals one meaning unit.
2. Preserve uncertainty. `CONFIRMED`, `STRONG`, `PLAUSIBLE`, `DISPUTED`, `REJECTED`, and `UNRESOLVED` are materially different states.
3. Separate evidence from inference.
4. A critic must be independent from the agent that proposed the interpretation.
5. Run a blind independent interpretation before exposing the current canonical interpretation to the reviewing critic.
6. Preserve rejected/overturned interpretations in revision history.
7. Never inflate entendre counts to make a song look impressive.
8. A human contribution becomes canonical only after evidence review / Gauntlet adjudication.
9. Every validated AI miss should become an evaluation case and be assigned a failure class.
10. Scores must be decomposable and reproducible from stored components; never store only an opaque final number.

## Content and source rules

- Store source provenance and timestamps for factual claims.
- Treat lyrics, artwork, audio, video, photographs, articles, and transcripts as rights-bearing content. Do not build Crowned around unauthorized bulk copying or scraping.
- Prefer metadata, licensed/authorized content, user-supplied text, permitted transcripts, and source links until rights are explicitly resolved.
- Never expose service keys, privileged prompts, private Gauntlet constitutions, or admin credentials to client code.

## Change discipline

For important Barology changes:

`baseline → isolated change → regression eval → critic review → keep/revert`

Do not mix model/prompt changes, scoring changes, retrieval changes, and UI changes into one unreviewable change unless they are inseparable.

## MVP stack

Base44 is the initial product/runtime layer. Keep external intelligence behind adapters so Crowned can later migrate or split services without rewriting product semantics.

Do not introduce pgGraph, pgContext, GraphRAG, Mem0, or another orchestration framework into production simply because it exists in the integration registry. Each must earn inclusion from a measured limitation in the current architecture.
