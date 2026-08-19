# Barology — Evaluation Plan

## Goal

Barology must improve without becoming more willing to invent meanings.

The evaluation system therefore tracks both:

1. **recall** — did Barology catch defensible constructions humans/evidence support?
2. **precision / overreach control** — did Barology avoid unsupported interpretations?

A model that finds more meanings but hallucinates more aggressively is not an improvement.

## Evaluation datasets

### A. Gold confirmed set
Bars/interpretations with direct artist/source confirmation or exceptionally strong evidence.

Measures:
- detection recall;
- span accuracy;
- reference accuracy;
- explanation fidelity.

### B. Human AI-miss set
Validated human discoveries that prior Barology versions missed.

Every entry includes:
- song/span identity;
- expected interpretation;
- failure class;
- evidence;
- version first missed;
- version first solved.

### C. Overreach set
Bars deliberately selected because attractive but unsupported interpretations are easy to invent.

Measures:
- false-positive rate;
- coincidence-risk calibration;
- willingness to remain PLAUSIBLE/UNRESOLVED rather than overclaim.

### D. Phonetic set
Audio/text cases involving:
- homophones;
- near-homophones;
- syllable boundary shifts;
- pronunciation-dependent ambiguity;
- cases where written lyrics alone are misleading.

### E. Long-context set
Interpretations requiring:
- backward callbacks;
- forward payoff;
- extended schemes;
- cross-verse relationships;
- cross-song/catalog context.

### F. Historical/reference set
Cases requiring accurate identification of:
- albums/songs;
- hip-hop history;
- sports/culture;
- film/brands;
- religion/mythology;
- historical/current events.

Include adversarial chronology cases where the proposed reference did not yet exist.

### G. Disputed set
Real cases with two or more defensible interpretations.

Measures:
- preservation of alternatives;
- confidence calibration;
- avoidance of false certainty.

## Core metrics

### Span recall
Did Barology identify the relevant text range?

### Interpretation recall
Did it recover the expected defensible meaning?

### Precision
What proportion of surfaced non-literal interpretations are supported by the gold/adjudicated record?

### Overreach rate
How often does Barology elevate coincidence to STRONG/CONFIRMED?

### Reference factuality
Are titles, dates, people, events, album/song facts, and relationships correct?

### Chronology accuracy
Does the interpretation respect what existed/happened at the relevant date?

### Calibration
Do confidence/status labels correspond to actual adjudication outcomes?

### Alternative preservation
Does the system preserve credible competing readings rather than collapsing them prematurely?

### Evidence quality
Are supporting citations actually relevant to the claimed interpretation?

### Long-context resolution
Can Barology correctly connect distant bars/songs when required?

### Cost / latency
Track analysis cost and time separately from quality so optimization does not silently degrade reasoning.

## Failure classes

Use the same production taxonomy:

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

## Release gate

A new Barology version cannot be promoted solely because its aggregate score rises.

Minimum comparison:

```text
CURRENT VERSION vs CANDIDATE VERSION

Gold recall
Human-miss recall
Overreach false positives
Reference factuality
Chronology accuracy
Calibration
Long-context performance
Latency
Cost
```

If recall improves but overreach materially worsens, the release requires explicit review.

## Gauntlet-style evaluation

For significant changes:

1. freeze a baseline output set;
2. run candidate version blind on the same cases;
3. compare structured outputs without model/version labels;
4. independent judge selects better output per case based on evidence and correctness;
5. inspect regressions by failure class;
6. keep or revert the change;
7. add every newly discovered failure to the permanent suite.

Do not let the same agent that authored a prompt/model change be the sole evaluator of that change.

## Human contribution → eval promotion

When a human contribution overturns or materially improves Barology:

```text
validated contribution
    ↓
classify failure
    ↓
create minimized reproducible case
    ↓
add expected interpretation/evidence
    ↓
promote to regression suite
    ↓
future Barology versions must solve it without creating unacceptable new false positives
```

This is the compounding moat: the community is continuously generating difficult semantic reasoning cases.

## Promptfoo role

When implementation begins, Promptfoo is the preferred first evaluation harness candidate for:

- model matrix runs;
- prompt/version comparison;
- structured assertions;
- custom graders;
- red-team/overreach cases;
- CI release gates.

The exact harness is implementation-derived. This document defines what must be measured regardless of tool.
