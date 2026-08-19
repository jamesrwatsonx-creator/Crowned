# Crowned — API and Secrets Contract

## Decision

Crowned must remain buildable and testable before any optional third-party API keys are obtained.

The Base44 application uses seeded fixtures and provider adapters until a provider is configured. Missing credentials are a normal `UNCONFIGURED` state, not an application error.

## Non-negotiable rules

1. Never commit real credentials, tokens, cookies, OAuth client secrets, or service-account files.
2. Store credentials in **Base44 Dashboard → Secrets** or the approved server-side secret store.
3. The client never calls privileged providers directly. Base44 backend functions call provider adapters.
4. Every adapter must support `READY / UNCONFIGURED / DEGRADED / ERROR`.
5. Every API-dependent screen must have a seeded, empty, or unavailable state and must not crash when a key is absent.
6. Provider responses are normalized into Crowned entities; provider-specific payloads never become the canonical product model.
7. Lyrics, transcripts, artwork, audio, video, and articles remain rights-bearing content. A key does not grant republication rights.
8. Adding or changing a provider requires provenance, rate-limit, caching, failure, and replacement behavior.

## Stable server-side secret names

These names are reserved now so APIs can be added later without changing product semantics.

| Secret | Required for first UI build | Purpose | Missing-key behavior |
|---|---:|---|---|
| `YOUTUBE_API_KEY` | No | YouTube Data API v3: public video, channel, playlist, search, and metadata discovery | Use seeded video/source cards; disable live YouTube search |
| `FIRECRAWL_API_KEY` | No | Web search, extraction, news ingestion, and Barology evidence retrieval | Use stored evidence fixtures and source links |
| `BAROLOGY_LLM_PROVIDER` | No | Selects the configured model adapter | Run deterministic seeded Barology examples |
| `OPENAI_API_KEY` | No | Optional Barology model provider | Adapter remains `UNCONFIGURED` |
| `GEMINI_API_KEY` | No | Optional Barology model provider | Adapter remains `UNCONFIGURED` |
| `ANTHROPIC_API_KEY` | No | Optional Barology model provider | Adapter remains `UNCONFIGURED` |
| `MUSIC_METADATA_PROVIDER` | No | Selects music metadata adapter | Use seeded Artist/Album/Song records |
| `MUSIC_METADATA_API_KEY` | No | Generic key for a future keyed metadata provider | Keyless/seeded adapter remains active |
| `NEWS_PROVIDER_API_KEY` | No | Optional future news aggregation provider | RSS, stored sources, or fixtures only |
| `LYRICS_PROVIDER` | No | Names a future authorized/licensed lyrics source | Accept authorized/user-provided text or source references only |
| `LYRICS_PROVIDER_API_KEY` | No | Credential for the selected authorized lyrics provider | Full catalog ingestion remains disabled |
| `APP_BASE_URL` | No | Published Base44 URL, later replaced or supplemented by custom domain | Use runtime request origin where safe |

Only configure the key for the selected Barology model provider. Do not require all three model keys.

## Providers that do not necessarily need keys

Crowned may use approved keyless sources behind the same adapter boundary:

- MusicBrainz-compatible metadata, subject to its identification, rate-limit, and attribution requirements;
- Cover Art Archive-compatible artwork references, subject to source and rights rules;
- permitted RSS/Atom feeds;
- user-supplied text and source URLs;
- manually seeded canonical records.

Keyless does not mean unrestricted. Preserve provenance, comply with provider policies, cache responsibly, and never make a public third-party service Crowned's system of record.

## Adapter contracts

### Video discovery

```text
VideoDiscovery.search(query, pageToken)
VideoDiscovery.getVideo(videoId)
VideoDiscovery.getChannel(channelId)
VideoDiscovery.getPlaylist(playlistId)
```

The initial live adapter may use YouTube Data API v3. Do not treat YouTube captions, transcripts, audio, or video as automatically licensed for storage or analysis.

### Music metadata

```text
MusicMetadata.searchArtist(query)
MusicMetadata.getArtist(externalId)
MusicMetadata.getRelease(externalId)
MusicMetadata.getRecording(externalId)
```

Normalize into `Artist / Album / Song / SongArtistCredit` and retain external identifiers and provenance.

### Authorized lyric input

```text
LyricSource.getAuthorizedReference(songId)
LyricSource.acceptUserSuppliedText(songId, text, rightsAttestation)
LyricSource.getPermittedTranscript(sourceId)
```

Do not build an adapter that scrapes and permanently stores complete unauthorized lyric catalogs.

### Evidence and news

```text
EvidenceSearch.search(query, filters)
EvidenceSearch.extract(url, schema)
RecentCulture.search(topic, window, sourcePolicy)
RecentCulture.discover(category, window)
```

Every normalized item stores source URL/ID, publisher, retrieval time, publication time where available, and provenance status.

### Barology model

```text
BarologyModel.propose(scope, retrievalPack, version)
BarologyModel.criticize(candidates, evidence, version)
BarologyModel.judge(candidates, critiques, evidence, version)
```

The provider is replaceable. Canonical status, evidence, revisions, scores, and contribution history stay in Crowned.

## Provider-free development mode

Before APIs are configured, seed one complete demonstrator:

```text
artist
→ album
→ song
→ authorized/demo lyric spans
→ interpretations
→ evidence fixtures
→ challenge
→ adjudication fixture
→ profile credit
→ score/ranking update
```

Seed data must be clearly marked `DEMO` and must not be mixed with live canonical claims.

Required behavior:

- onboarding and navigation work;
- artist → album → song works;
- Lyrics ↔ Barology works;
- Talk to This Song shows a deterministic demo exchange;
- challenge/adjudication/profile-credit loop works;
- News and video surfaces show fixtures or an explicit unavailable state;
- an admin/provider status surface identifies what is configured without revealing secret values.

## Base44 implementation pattern

Backend functions read secrets at runtime and instantiate adapters:

```text
Base44 client
    ↓
Base44 backend function
    ↓
provider registry
    ├── live adapter when configured
    └── fixture adapter when unconfigured
    ↓
normalized Crowned entity/result
```

Never send provider keys to the browser, embed them in generated UI code, paste them into public prompts, or commit them to GitHub.

## Activation checklist

For each provider:

1. obtain the credential from the provider;
2. add it to Base44 Dashboard → Secrets using the stable name above;
3. restrict the key to the required API and application/server context where supported;
4. enable the matching provider flag/selection;
5. run the adapter contract test;
6. verify `READY` on the provider status surface;
7. verify no secret appears in client bundles, logs, source provenance, or error messages;
8. verify rate limits, caching, retry/backoff, and degraded behavior;
9. verify rights/attribution requirements before publishing retrieved content.

## Acceptance tests

- Crowned's complete seeded core loop works with zero optional provider credentials.
- Missing keys never produce a blank screen, uncaught exception, or secret-entry prompt for end users.
- Live provider activation requires secrets/configuration only, not a rewrite of UI or canonical entities.
- Every provider can be replaced behind its adapter contract.
- No API secret is present in Git history or the client bundle.
- Provider status reveals configuration state but never credential values.
