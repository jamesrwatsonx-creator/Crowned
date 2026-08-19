# Crowned — Data and Integrations

## Canonical entities

The Base44 MVP should model the product explicitly rather than storing AI blobs in generic JSON whenever a durable entity exists.

### Identity / community

**UserProfile**
- user_id
- display_name
- avatar
- bio
- barologist_rating
- validation_rate
- catches_count
- ai_misses_count
- successful_challenges_count
- first_finds_count
- specialties
- created_at / updated_at

**Contribution**
- contributor_id
- song_id
- lyric_span_id
- interpretation_id (optional when proposing a new interpretation)
- contribution_type: ADD / CHALLENGE / SUPPORT / OPPOSE / EVIDENCE / CORRECTION
- explanation
- evidence_refs
- status
- gauntlet_run_id
- created_at / resolved_at

**Vote**
- user_id
- interpretation_id
- direction: SUPPORT / OPPOSE
- reason_code
- explanation_optional
- weight_snapshot
- created_at

**ExpertiseScore**
- user_id
- domain_type: ARTIST / TECHNIQUE / ERA / REGION / TOPIC
- domain_id_or_key
- score
- evidence_count
- updated_at

### Music corpus

**Artist**
- canonical_name
- aliases
- image_refs
- biography_summary
- active_years
- regions
- crown_score
- crown_rank
- external_ids

**Album**
- artist_id
- title
- release_date
- artwork_ref
- album_type
- crown_score
- external_ids

**Song**
- primary_artist_id
- album_id_optional
- title
- release_date
- duration
- credits
- external_ids
- analysis_status
- crown_score
- density_score

**SongArtistCredit**
- song_id
- artist_id
- role

**Verse**
- song_id
- ordinal
- performer_ids
- start_time_optional
- end_time_optional

**LyricSpan**
- song_id
- verse_id_optional
- start_token
- end_token
- start_char
- end_char
- start_time_optional
- end_time_optional
- surface_text_or_authorized_reference
- normalized_text
- phonetic_representation_optional
- density_score
- canonical_layer_count

Lyrics are rights-bearing content. The implementation should support authorized/licensed text, user-provided text, permitted transcripts, and source references. Do not architect Crowned around unauthorized bulk lyric copying.

### Interpretation / evidence

**Interpretation**
- lyric_span_id
- interpretation_type
- title
- explanation
- layer_index
- status: CONFIRMED / STRONG / PLAUSIBLE / DISPUTED / REJECTED / UNRESOLVED
- confidence
- coincidence_risk
- origin: AI / HUMAN
- originator_id_optional
- current_revision_id
- created_at / updated_at

**InterpretationRevision**
- interpretation_id
- revision_number
- explanation
- confidence
- status
- evidence_snapshot
- changed_by_type
- changed_by_id
- gauntlet_run_id_optional
- created_at

**EvidenceItem**
- interpretation_id
- evidence_type
- source_url_or_source_id
- source_title
- publisher
- published_at_optional
- retrieved_at
- claim_summary
- supporting_or_opposing
- reliability_notes

**InterpretationConnection**
- from_interpretation_id
- to_entity_type
- to_entity_id
- relation_type
- provenance: EXTRACTED / EVIDENCED / INFERRED / HUMAN
- confidence

### Barology execution

**GauntletRun**
- song_id
- trigger_type: INITIAL / HUMAN_CHALLENGE / VOTE_THRESHOLD / NEW_EVIDENCE / MODEL_UPGRADE / MANUAL
- scope_type: SONG / VERSE / SPAN / INTERPRETATION
- scope_id
- model_config_snapshot
- retrieval_snapshot
- status
- started_at / completed_at
- final_decision

**AgentResult**
- gauntlet_run_id
- agent_role
- blind_pass_boolean
- proposed_interpretations
- evidence_refs
- confidence
- critique_targets
- created_at

**FailureCase**
- interpretation_id_optional
- lyric_span_id
- failure_class
- expected_behavior
- prior_output
- corrected_output
- human_source_id_optional
- promoted_to_eval_boolean

### Rankings

**ScoreSnapshot**
- entity_type: ARTIST / ALBUM / SONG / VERSE / BAR
- entity_id
- score_version
- component_scores
- total_score
- corpus_coverage
- confidence
- created_at

**RankingSnapshot**
- ranking_type
- category
- period
- rows
- methodology_version
- created_at

### News / living corpus

**NewsArticle**
- title
- summary
- category
- source
- canonical_url
- hero_image_ref_optional
- published_at
- ingested_at
- status

**CorpusEvent**
- event_type
- title
- description
- occurred_at
- source_refs
- confidence

**KnowledgeEntity**
- entity_type
- canonical_name
- aliases
- metadata

**KnowledgeRelation**
- from_entity
- to_entity
- relation_type
- start_date_optional
- end_date_optional
- source_refs
- provenance
- confidence

## Integration boundaries

### Base44 — MVP product runtime

Use for:
- auth;
- user profiles;
- product entities;
- CRUD;
- voting/contributions;
- activity feed;
- rankings views;
- news views;
- backend functions;
- file uploads where appropriate;
- AI invocation where suitable.

Keep Barology behind a clear `analyze / challenge / retrieve / adjudicate` boundary even if the first implementation lives in Base44 functions.

### James Watson Gauntlet Loop — reasoning pattern

Adapt the recursive logic into Barology. Do not copy the product-builder vocabulary literally. The engine should perform independent construction, adversarial critique, belief updates, evidence checks, and re-analysis until the interpretation state is defensible.

### last30days-skill — current culture/news intelligence

Use as a source architecture for discovering recent artist/news/culture signals across social, video, web, and community sources. In production, expose only the required source adapters or a dedicated ingestion service; do not require the mobile app to execute a local CLI skill.

Primary Crowned use:
- hip-hop news discovery;
- artist activity monitoring;
- interview/video transcript discovery;
- social reaction signals;
- AI-news vertical;
- corpus events with dates and provenance.

### Firecrawl — web evidence retrieval

Use for:
- web search;
- page extraction;
- structured extraction;
- source discovery;
- evidence collection for Barology;
- news/article ingestion where permitted.

Never treat retrieved page text as permission to republish copyrighted material wholesale.

### GraphRAG — later corpus graph construction

Candidate for converting large volumes of unstructured articles, interviews, notes, and historical source material into entities, communities, and relationships for retrieval.

Do not deploy until the corpus size/complexity justifies indexing cost and operational overhead.

### Promptfoo — evaluation only

Use outside the user-facing runtime for:
- model/prompt comparisons;
- known-bar regression tests;
- hallucination/overreach tests;
- scoring consistency tests;
- adversarial red-team cases;
- release gates.

### pgContext — future retrieval layer

Candidate when Crowned moves to Postgres and needs large-scale hybrid semantic + keyword retrieval with filters.

### pgGraph — future relationship traversal

Candidate for multi-hop questions over the Crowned relationship graph while keeping Postgres authoritative.

### Mem0 — optional personalization/memory

Potential later use for personalized research/assistant experiences and adaptive retrieval. Do not use as the source of truth for canonical product entities or public contribution history.

### Open Notebook — internal research patterns

Use as reference for a future Corpus Studio capable of ingesting and organizing webpages, podcasts, video, audio, PDFs, interviews, and notes with citations and model flexibility.

### Graphify — provenance pattern

Borrow the distinction between extracted and inferred relationships. Crowned should additionally support EVIDENCED and HUMAN provenance.

### Base44-to-Supabase SDK — migration option

Keep as an escape-path reference, not an MVP dependency. If Base44 becomes a material limit, evaluate migration to Supabase/Postgres with compatibility tests before adopting pgContext/pgGraph.

## External music data

Crowned will eventually need authoritative metadata for artists, albums, tracks, credits, release dates, identifiers, and possibly samples/relationships.

Keep providers behind adapters so any one source can be replaced. Do not make a single third-party website the system of record for Crowned.

## Provenance rule

Every important factual edge in Crowned must answer:

- Where did this come from?
- When was it retrieved?
- Was it directly extracted, externally evidenced, inferred by AI, or proposed by a human?
- What would falsify it?
- Has it been superseded?

That provenance layer is required for credible lyric interpretation and for safe re-Gauntlet behavior.
