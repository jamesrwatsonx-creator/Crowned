# Crowned — App Concept

## One-line product

**Crowned is an AI-powered hip-hop intelligence network that follows the culture in real time, dissects songs bar by bar, ranks lyricists from inspectable evidence, and gives humans reputation for catching what AI misses.**

## User promise

Users should be able to answer four questions in one product:

1. What is happening in hip-hop right now?
2. What does this song/bar actually mean?
3. Who are the strongest lyricists when the work itself is analyzed?
4. What have I personally discovered, challenged, or contributed?

## Product systems

### 1. Crowned News

A live editorial/intelligence surface for hip-hop, releases, albums, industry, culture, disputes, interviews, and a clearly separated AI-news vertical.

News is not disposable content. Relevant entities, events, relationships, dates, statements, releases, interviews, and cultural context feed the Crowned corpus with provenance.

### 2. Barology

Barology analyzes songs as connected spans rather than independent lines.

It looks for:

- literal meaning;
- double/triple/multiple entendre candidates;
- homophones and near-homophones;
- pronunciation and syllable segmentation;
- internal/multisyllabic rhyme;
- assonance, consonance, alliteration;
- metaphors, similes, idioms, inversion, juxtaposition;
- setup/payoff and punchlines;
- extended schemes;
- backward and forward callbacks;
- cross-verse and cross-song relationships;
- artist catalog/self-references;
- references to other artists, songs, albums, samples, battles, labels, regions, and eras;
- sports, film, fashion, brands, politics, religion, mythology, history, geography, and current events;
- narrative perspective and storytelling structure;
- evidence that supports or falsifies a proposed interpretation.

### 3. The Crown

Rankings exist for:

- lyricists;
- albums;
- songs;
- verses;
- bars;
- technique-specific categories.

The core lyric score must not be diluted by popularity, beat quality, streaming performance, or celebrity. Those may exist as separate metrics but not as lyrical quality.

Initial score dimensions:

- lyrical density;
- wordplay;
- rhyme engineering;
- layering;
- cohesion;
- originality;
- reference depth;
- extended-scheme quality;
- storytelling/narrative quality where applicable;
- consistency.

All rankings must be inspectable back to song/bar-level evidence.

### 4. Human reputation

A human profile shows what the person understood, not merely who follows them.

Core profile records:

- catches;
- AI misses found;
- first finds;
- confirmed contributions;
- challenges;
- successful challenges;
- doubts / votes against interpretations;
- submissions later rejected;
- artists/songs analyzed;
- expertise by artist and technique;
- accuracy / validation rate;
- badges and notable discoveries.

Human and artist profiles share the same structural layout but different visual polarity:

- **Human profiles:** white / warm-white canvas, dark typography.
- **Artist profiles:** near-black canvas, light typography.

## Community adjudication

Users can support or oppose an interpretation. Opposition should be structured, not a generic dislike.

Candidate challenge reasons:

- overreach / coincidence;
- wrong reference;
- wrong lyric/transcription;
- phonetically unsupported;
- context does not support it;
- incomplete interpretation;
- stronger alternative meaning;
- evidence is inaccurate or stale.

An interpretation can become disputed or be removed from canonical display when thresholds are met, but its history is never deleted.

## Signature song interaction

Inside a song there are two primary horizontal states:

**LYRICS ↔ BAROLOGY**

Lyrics mode is clean reading with semantic span highlighting. Barology mode opens the analysis corresponding to the lyric position the user was viewing.

A lyric can contain overlapping or adjacent highlighted spans with different depth levels. Color communicates analytical depth, not decoration.

The exact palette is finalized in design, but the semantic concept is:

- normal text — no secondary meaning detected;
- increasing highlight intensity/hue — more validated layers;
- Crown/gold treatment — exceptional verified construction.

## Navigation model

Crowned uses three navigation layers:

1. **Bottom navigation** for frequent destinations.
2. **Slide-in command drawer** for the full product map.
3. **Persistent section subnavigation** once a user enters a major section.

The drawer is a matte/near-black panel that slides from the edge and leaves part of the active page visible beneath a dim layer. Selecting a major section should not force the user to reopen the drawer to move among that section's internal pages.

Example section tabs:

**Barology:** Recent · Trending · Top Scores · AI Misses · Disputed  
**Rankings:** Artists · Songs · Albums · Verses · Bars  
**News:** Today · Hip-Hop · Releases · Industry · Culture · AI  
**Activity:** All · Breakdowns · Catches · Challenges · Rank Moves · Community

## Dedicated surfaces

Crowned should have isolated pages for high-value content rather than forcing all content into Home:

- recently broken-down songs;
- top breakdowns;
- most complex songs;
- most discussed interpretations;
- most AI misses;
- disputed bars;
- live activity;
- news verticals;
- upcoming albums/releases;
- Crown rankings.

## Activity as network heartbeat

The Activity feed includes machine and human events:

- new song analyzed;
- new interpretation found;
- human catch validated;
- AI interpretation disputed;
- re-Gauntlet result;
- ranking movement;
- new release;
- new artist/album added;
- first-find achievement;
- important corpus/news update.

## Visual direction

Crowned is premium, dark, cinematic, photographic, and culturally grounded on its outer surfaces. Deeper Barology screens become progressively more analytical.

Conceptual progression:

`Home = culture → Artist = identity → Song = analysis → Bar = intelligence → Gauntlet = evidence`

Brand accent: restrained Crown gold. Semantic analysis colors are separate from brand color and only appear when they carry information.

## Splash

**CROWNED**  
*Powered by AI*

“The latest in hip-hop. Every bar decoded. Every lyricist ranked. Build your profile by catching what AI—and everybody else—missed.”

**Swipe to enter →**

Background direction: dim cinematic silhouette of an anonymous performer holding a microphone and facing a stadium-scale crowd, with subtle collage/intelligence elements integrated into darkness rather than competing with the copy.

## MVP proof

The core proof is not page count. It is whether this loop creates value:

`find artist → choose album → choose song → read lyrics → swipe to Barology → understand a defensible interpretation → catch/challenge something → receive profile credit`
