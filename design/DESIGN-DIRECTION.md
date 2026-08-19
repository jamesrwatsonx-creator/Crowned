# Crowned — Design Direction

This file captures approved visual/interaction direction only. It is not a replacement for a final design package.

## Brand character

Crowned should feel like a premium hip-hop intelligence network, not a generic news app, generic social clone, or a dashboard covered in AI gradients.

Reference fusion:

- cinematic social feed behavior;
- editorial/news information architecture;
- premium dark technical surfaces;
- evidence-oriented Barology interactions;
- restrained luxury rather than glossy excess.

## Core palette

- near-black / black primary app canvas;
- charcoal raised surfaces;
- white typography;
- muted gray metadata;
- restrained Crown gold as permanent brand accent;
- separate semantic analysis colors reserved for validated meaning depth.

Do not make purple/magenta the primary brand accent merely because it appears in social references.

## Profile polarity

Human and artist profiles share the same underlying component/layout system.

**Human**
- white or warm-white background;
- black/dark typography;
- gray structural surfaces;
- gold used sparingly.

**Artist**
- near-black background;
- white typography;
- charcoal structural surfaces;
- gold used sparingly.

The geometry remains familiar while the polarity makes it immediately obvious which type of profile is being viewed.

## Signature navigation

### Bottom navigation

Five primary positions:

`Home · Discover · Crown · News · Profile`

Crown is the center landmark and may be slightly larger/elevated. The bar should feel sculpted/floating rather than like a default tab strip.

Motion behavior:
- active indicator glides/springs between destinations;
- active icon lifts/enlarges subtly;
- inactive icons dim;
- active label appears only when useful;
- selected destination may receive a restrained gold light response;
- haptics differentiate tab switch vs Crown activation;
- scroll can compress the bar to reclaim space;
- deep Barology mode may use a more minimal nav state.

Avoid constant shimmer or decorative motion that competes with content.

### Command drawer

The hamburger/edge control opens a near-black panel over roughly half the viewport, tuned during design for label readability. Part of the current screen remains visible and dimmed.

Behavior:
- opens by tap or edge drag;
- follows the finger during drag;
- release threshold determines snap-open vs snap-closed;
- selected section receives gold type or a thin gold rail;
- section switch does not erase navigation context.

Once inside a major section, persistent section tabs give access to sibling views without reopening the drawer.

## Home

Home is culturally alive rather than analytical-first.

Top area:
- CROWNED mark;
- search / notifications;
- horizontally scrollable artist carousel similar in familiarity to story navigation, but representing trending/followed artists rather than literal stories.

Feed object types may include:
- lead news;
- new Barology analysis;
- AI Missed It;
- Crown movement;
- new release;
- Bar of the Day;
- top breakdown;
- notable community catch.

Large imagery should be used selectively; not every card needs to be a hero card.

## Artist hierarchy

The app should make this descent effortless:

`Artist → Album → Song → Bar → Meaning`

Artist carousel → album carousel → song list is the primary discovery grammar.

## Song experience

### Lyrics state

- near-black canvas;
- large readable text;
- minimal chrome;
- vertically scrollable;
- exact spans can be highlighted;
- semantic highlighting should remain readable and accessible;
- the interface should never feel like a spreadsheet of annotations.

### Barology state

Full-screen horizontal swipe from Lyrics.

Opens aligned to the same bar/span the user was viewing.

Displays:
- exact selected span;
- number of canonical layers;
- interpretations;
- reference type;
- evidence;
- connected bars;
- confidence/status;
- AI vs human origin;
- support/oppose;
- Add What Barology Missed.

Barology is increasingly analytical, but should still feel editorial and premium rather than like developer tooling.

## Semantic color

Color represents analytical depth and status, not decoration.

Final hue values are a design decision, but the conceptual progression is:

- normal text: no validated secondary layer;
- low highlight: 2-layer construction;
- stronger highlight: 3 layers;
- deeper highlight: 4 layers;
- highest non-Crown highlight: 5+ layers;
- Crown/gold treatment: exceptional verified construction, not simply “many meanings.”

A color can begin/end mid-line because the underlying object is a token/span range.

Do not let the heatmap reward hallucinated complexity. Visual depth must be downstream of evidence status.

## Barology heat maps

At song/album level, use compact strips/maps to make density visible before opening the full breakdown.

Examples:
- verse complexity strips;
- per-song density strips in an album track list;
- album technique fingerprint;
- artist career trend visualization.

The goal is to create a visual language users can recognize and share.

## Splash

Background:
- anonymous performer silhouette with microphone;
- performer around 40% of screen height/visual mass;
- facing a huge stadium/crowd;
- image intentionally dimmed for copy readability;
- subtle collage of cultural/intelligence objects may be embedded into darkness: lyric notes, graph lines, album shapes, news fragments, waveform, crown motif;
- do not turn the splash into a feature poster.

Copy:

**CROWNED**  
*Powered by AI*

“The latest in hip-hop. Every bar decoded. Every lyricist ranked. Build your profile by catching what AI—and everybody else—missed.”

**Swipe to enter →**

## Motion principles

- most UI responses: ~180–350 ms;
- major transitions: ~450–700 ms when justified;
- spring physics for direct-manipulation navigation;
- no motion without information, hierarchy, feedback, or brand purpose;
- preserve 60fps target on supported mobile hardware;
- haptics are part of interaction design, not an afterthought.

Signature motions:
- nav active indicator follows tab/page movement;
- command drawer physically tracks edge drag;
- Lyrics ↔ Barology behaves like two connected surfaces;
- connected-bar jump scrolls to target and gives a brief controlled pulse;
- validated AI miss gets a restrained Crown confirmation moment rather than confetti;
- score changes can roll/transition rather than snap.

## Anti-patterns

Avoid:
- generic AI purple gradients;
- excessive glassmorphism;
- every card glowing;
- giant rounded rectangles everywhere;
- dashboard density on cultural/news screens;
- Instagram cloning without Crowned-specific information value;
- over-animated lyric text;
- semantic colors being used for unrelated buttons or decoration.
