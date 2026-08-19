# Crowned — Screen Inventory

This inventory separates primary screens from supporting overlays/states. It is intentionally broader than the first build so navigation architecture is not painted into a corner.

## MVP primary screens

### 1. Splash / Entry
- cinematic background
- CROWNED mark
- Powered by AI
- product quote
- swipe-to-enter interaction

### 2. Home
- trending artist carousel
- featured story / featured analysis
- mixed feed of news, releases, Barology analyses, Crown movement, AI misses, and notable community activity

### 3. Discover
- universal search
- Artists / Albums / Songs / Bars / News / AI Misses
- eras, regions, techniques, themes, and other discovery filters

### 4. Activity
- live network activity
- tabs: All / Breakdowns / Catches / Challenges / Rank Moves / Community

### 5. News
- lead story
- Today / Hip-Hop / Releases / Industry / Culture / AI
- separate article pages and topic pages

### 6. Crown Rankings
- Artists / Songs / Albums / Verses / Bars
- category and time-range filters
- methodology/explanation access

### 7. Artist Profile
- black/near-black visual polarity
- hero image + artist identity
- Crown score / rank / analyzed catalog
- album carousel
- overview / music / bars / news / stats
- technique fingerprint
- top songs / top bars / recent news

### 8. Album Profile
- artwork / metadata
- album Barology score
- track list with song scores
- lyric-density heat strips
- album-wide intelligence fingerprint

### 9. Song — Lyrics
- song metadata
- clean vertically scrolling lyric view
- semantic span highlighting
- Lyrics / Map / Discussion controls
- full-screen horizontal swipe to Barology

### 10. Song — Barology
- opens aligned to the lyric/bar position from Lyrics mode
- exact highlighted span
- interpretation count
- canonical breakdown
- evidence + connected bars
- confidence/status/provenance
- support / oppose
- Add What Barology Missed
- Breakdown / Debate views

### 11. Human Profile
- white/warm-white visual polarity
- same structural shell as Artist Profile
- Barologist rating / catches / AI misses / validation rate
- Activity / Catches / Doubts / Artists / Badges
- expertise by artist and technique

### 12. Top Breakdowns
- Recently Analyzed
- Most Complex
- Highest Rated
- Most Discussed
- Most AI Misses
- Trending
- song cards include score, density, interpretations, human contributions, and heat strip

## V1 incremental screens

### 13. Barology Hub
- Recent / Trending / Top Scores / AI Misses / Disputed

### 14. AI Misses
- unresolved bars
- recently validated catches
- hardest unsolved interpretations
- contributor leaderboard

### 15. Disputes
- active disputed interpretations
- evidence comparison
- qualified community voting
- re-Gauntlet status

### 16. Release Calendar
- albums/singles coming this week/month/year
- artist and album follow/watch actions

### 17. Artist Technique Detail
- wordplay, rhyme engineering, storytelling, reference depth, schemes, etc.
- evidence drilldown to songs/bars

### 18. Barology Map
- song/verse complexity heat map
- jump to dense regions
- relationship visualization for connected spans

### 19. Contributor Expertise Detail
- per-artist contribution history
- per-technique accuracy
- first finds
- successful challenges

### 20. Search Results / Intelligence Search
- semantic questions such as “Jay-Z Biggie references” or “hardest triple entendres”
- entity + graph aware results rather than title-only matching

## FUTURE surfaces

- internal Corpus Studio
- moderator/adjudicator workspace
- methodology and benchmark explorer
- artist claim/verification portal
- creator/artist self-annotation portal
- research chat over Crowned corpus
- personalized watchlists
- notification center
- advertising/sponsorship management surfaces

## Supporting overlays / states

These are not separate primary destinations:

- command drawer / hamburger navigation
- interpretation bottom sheet
- add-missed-meaning composer
- structured challenge reason sheet
- evidence/source viewer
- connected-bar jump preview
- share card composer
- filter/sort sheet
- login/register
- onboarding
- loading / analysis-in-progress
- Gauntlet re-analysis status
- moderation confirmation
- report content

## Gesture rules

To avoid gesture collisions:

- vertical swipe/scroll = move through content;
- horizontal carousel = browse collections such as artists/albums;
- full-screen horizontal swipe = reserved for Lyrics ↔ Barology inside a song;
- edge swipe / handle = open command drawer;
- bottom navigation = frequent global destinations.
