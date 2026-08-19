# Barology Gauntlet

## Purpose

Barology should not be a single prompt that “explains lyrics.” It is an adversarial interpretation system that proposes, retrieves, challenges, revises, and verifies candidate meanings.

The operating loop is adapted from the Gauntlet philosophy:

```text
UNDERSTAND
→ MODEL
→ DISCOVER
→ RETRIEVE
→ CHALLENGE
→ FALSIFY
→ FIND MISSES
→ UPDATE BELIEFS
→ SYNTHESIZE
→ VERIFY
→ SCORE
```

The system optimizes for **defensible interpretation**, not maximum cleverness.

## Analysis object

The unit of analysis is an exact lyric span, not a line.

A span may overlap another span and may participate in:

- one local interpretation;
- several simultaneous interpretations;
- a multi-bar scheme;
- a callback/setup-payoff relationship;
- a catalog/history/culture reference;
- a phonetic construction that differs from written segmentation.

Each candidate interpretation must point to the exact tokens/chars/time range that support it.

## Stage 0 — Normalize

Input pack:

- song identity;
- artist/featured artists;
- album/release date;
- credits where available;
- authorized/user-provided lyric representation;
- optional aligned audio/transcript timestamps;
- artist catalog context;
- Crowned corpus/news context available as-of relevant dates.

Produce:

- verses;
- tokens;
- sentence/bar boundaries;
- phonetic forms where available;
- candidate spans;
- entity candidates;
- retrieval queries.

## Stage 1 — Blind independent discovery

Specialists work independently. They do not see one another's candidate interpretations.

### Literal Analyst
Explains explicit surface meaning and grammatical structure.

### Entendre Hunter
Searches for double/triple/multiple meanings, idiom collisions, puns, inversion, and semantic ambiguity.

### Phonetic Analyst
Tests homophones, near-homophones, alternate syllable boundaries, pronunciation changes, sound-alike names/titles, and audio-specific ambiguity.

### Rhyme Engineer
Maps internal rhyme, multisyllabic rhyme, slant rhyme, assonance, consonance, alliteration, and sound-pattern constraints that may support meaning.

### Scheme Hunter
Searches for concepts sustained across multiple lines/bars and identifies setup/payoff boundaries.

### Backward Context Analyst
Tests whether the current span completes, reframes, or echoes earlier material.

### Forward Context Analyst
Tests whether the current span is setup, foreshadowing, or later reframed.

### Catalog Analyst
Searches the artist's own songs, albums, aliases, recurring phrases, collaborators, public history, and known motifs.

### Hip-Hop Historian
Searches other artists, albums, battles, labels, scenes, samples, eras, regional slang, lineage, and genre history.

### Culture Analyst
Searches film, TV, sports, fashion, brands, internet culture, celebrities, business, and broader pop culture.

### Historical Analyst
Searches historical events, figures, religion, politics, mythology, geography, wars, social movements, institutions, and dated facts.

### Current-Events Analyst
Searches relevant events around the writing/release period and later events when analyzing callbacks retrospectively. Time provenance is mandatory.

### Narrative Analyst
Tests speaker perspective, character, scene, chronology, imagery, storytelling, juxtaposition, and thematic structure.

### Missing-Meaning Agent
Assumes the other discovery agents missed the strongest non-obvious interpretation and searches specifically for it.

## Stage 2 — Candidate normalization

Merge semantically equivalent candidates without deleting provenance.

For each candidate, normalize:

- exact span;
- interpretation title;
- explanation;
- mechanism/type;
- required facts;
- related bars;
- related entities;
- proposed layer relationships;
- agent support count;
- initial confidence;
- retrieval tasks required to verify it.

Do not convert agent agreement into truth. Multiple agents can share the same hallucinated association.

## Stage 3 — Retrieval

Build an evidence pack for each meaningful candidate.

Search order:

1. local song/album/artist corpus;
2. artist catalog;
3. Crowned knowledge/events/news;
4. approved music metadata/reference sources;
5. web research/evidence;
6. human-submitted evidence.

Evidence is classified as:

- SUPPORTING;
- OPPOSING;
- CONTEXT_ONLY;
- UNVERIFIED.

Evidence quality and relevance are separate values.

## Stage 4 — Adversarial critique

Critics are given candidates and evidence but did not participate in discovery.

### Skeptic
Attempts to prove the candidate is coincidence/overreading.

Questions:
- Does a simpler literal reading explain everything?
- Would this association occur easily by chance?
- Is the alleged second meaning independently signaled?

### Phonetic Critic
Attempts to reject sound-based claims that do not actually match pronunciation/audio.

### Context Critic
Tests whether surrounding bars support or contradict the interpretation.

### Reference Critic
Checks whether referenced titles, people, events, dates, facts, brands, songs, albums, or historical details are actually correct.

### Scheme Critic
Tests whether a proposed multi-bar scheme is continuous rather than a collection of unrelated coincidences.

### Intent-Signal Critic
Searches for signs of deliberate construction: repeated wording, rhyme constraints, artist statements, video imagery, later callbacks, catalog patterns, or converging evidence.

Absence of direct artist confirmation is not automatic rejection; it lowers certainty where intent is central.

### Stronger-Alternative Critic
Attempts to construct a competing interpretation that explains more of the evidence with fewer assumptions.

### Missing-Link Critic
Asks what additional relationships should exist if the candidate is true, then sends those relationships back to retrieval.

## Stage 5 — Belief update

Candidates may be:

- strengthened;
- narrowed to a smaller span;
- expanded into a multi-bar span;
- split into separate interpretations;
- merged;
- downgraded;
- marked disputed;
- rejected;
- left unresolved.

If critique produces materially new hypotheses, return to retrieval rather than immediately synthesizing.

## Stage 6 — Independent judge

The final judge receives:

- normalized candidates;
- discovery provenance;
- evidence pack;
- adversarial critiques;
- competing hypotheses;
- prior canonical interpretation only when this is a re-Gauntlet.

The judge returns structured conclusions, not hidden reasoning transcripts.

Required output per interpretation:

```json
{
  "span_id": "...",
  "type": "CATALOG_REFERENCE",
  "status": "STRONG",
  "layer_count_contribution": 1,
  "confidence": 0.87,
  "coincidence_risk": 0.16,
  "supporting_evidence_ids": [],
  "opposing_evidence_ids": [],
  "connected_span_ids": [],
  "connected_entity_ids": [],
  "origin": "AI",
  "failure_risk": ["INTENT_NOT_CONFIRMED"],
  "summary": "..."
}
```

## Acceptance tests for an interpretation

An interpretation does not need to pass every test, but the judge must record which are applicable and their outcomes.

### `LITERAL_COHERENCE`
Does the reading preserve or deliberately subvert the sentence's ordinary meaning?

### `PHONETIC_MATCH`
If sound-based, is the alternate reading audibly plausible?

### `CONTEXT_SUPPORT`
Do nearby bars support the reading?

### `LONG_RANGE_SUPPORT`
Do later/earlier bars materially strengthen it?

### `CATALOG_SUPPORT`
Does the artist's catalog/history create a specific relevant connection?

### `REFERENCE_VALIDITY`
Does the external referenced object/event/person/title actually exist and match the claim?

### `CHRONOLOGY_VALIDITY`
Was the reference available/possible at the relevant time?

### `SCHEME_CONTINUITY`
Does the proposed scheme continue across the claimed range?

### `INTENT_SIGNAL`
Is there evidence consistent with deliberate construction?

### `COINCIDENCE_RISK`
How easy is it to generate the connection accidentally?

### `ALTERNATIVE_EXPLANATION`
Does a stronger/simpler rival explain more evidence?

### `HUMAN_CONSENSUS`
What do qualified contributors independently see?

## Status policy

### CONFIRMED
Direct artist/source confirmation or overwhelming evidence with negligible credible opposition.

### STRONG
Multiple independent support signals, low-to-moderate coincidence risk, and no stronger rival.

### PLAUSIBLE
Defensible interpretation with meaningful but incomplete support.

### DISPUTED
Material qualified disagreement or competing interpretations remain unresolved.

### REJECTED
Fails evidence/context/phonetic/reference tests or is dominated by a substantially better explanation.

### UNRESOLVED
The system detects a likely construction or anomaly but cannot responsibly explain it yet.

## Human contribution flow

```text
HUMAN HIGHLIGHTS SPAN
    ↓
adds interpretation / challenge / evidence
    ↓
store contribution immediately
    ↓
scoped blind independent analysis
    ↓
retrieve evidence
    ↓
compare human hypothesis vs current canonical state
    ↓
critics attack both
    ↓
judge
    ↓
canonical revision + profile reputation + eval case when applicable
```

Human submissions are hypotheses, not truth by popularity.

## Vote-triggered re-Gauntlet

Voting affects review priority and dispute state; it does not directly rewrite truth.

Trigger re-Gauntlet when configurable thresholds are met, especially when:

- enough qualified opposition accumulates;
- a high-reputation domain expert challenges;
- new evidence is added;
- an artist/source later confirms or contradicts an interpretation;
- a new song creates a possible callback;
- Barology model/methodology is upgraded;
- moderators request a review.

## Failure taxonomy

Every validated miss should receive one or more classes:

- PHONETIC_SEGMENTATION
- HOMOPHONE
- MULTI_BAR_SCHEME
- LONG_RANGE_CALLBACK
- CATALOG_REFERENCE
- HIP_HOP_HISTORY
- CULTURAL_REFERENCE
- HISTORICAL_REFERENCE
- CURRENT_EVENT_CONTEXT
- REGIONAL_SLANG
- NARRATIVE_PERSPECTIVE
- RHYME_CONSTRAINED_MEANING
- ENTITY_DISAMBIGUATION
- CHRONOLOGY
- EVIDENCE_RETRIEVAL
- OVERREACH_FALSE_POSITIVE
- OTHER

The failure taxonomy drives the Barology evaluation suite.

## Scoring boundary

Barology analysis creates evidence. The scoring layer consumes canonical analysis.

Do not make the discovery agents aware that finding more devices can improve an artist's score. That would create an incentive to hallucinate complexity.

Analysis first. Score second.
