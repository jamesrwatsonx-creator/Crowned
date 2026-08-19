# Barology — Screen Inventory

This inventory separates first-run onboarding, primary app screens, and supporting overlays/states. It is intentionally broader than the first build so navigation architecture is not painted into a corner.

## First-run onboarding screens

### 0. Splash / Entry
- looping cinematic performance/stadium video
- BAROLOGY wordmark
- AI-Powered Hip-Hop Intelligence
- Hip-hop, decoded.
- short product promise
- Get Started
- optional branded swipe-to-enter interaction

### 1. Sign In
- Wispr-style minimal white/warm-white layout
- Continue with Google
- Continue with Apple
- Continue with Email
- small terms/privacy copy

### 2. Create Barology Profile
- profile photo
- username
- display name
- explains that the profile records catches, challenges, and AI misses

### 3. Pick Artists
- headline: “Who do you listen to most?”
- searchable artist portrait grid/carousel
- select at least three

### 4. Pick Eras
- headline: “Which eras of hip-hop do you appreciate most?”
- 80s / 90s / 2000s / 2010s / 2020s
- multiple selection

### 5. Lyricism Preferences
- headline: “What do you appreciate most about lyricism?”
- double entendres, wordplay, rhyme schemes, storytelling, punchlines, metaphors, historical references, catalog callbacks, battle rap, samples/callbacks, street language/slang, religious/symbolic references, pop-culture references
- preferences seed recommendations but do not define earned expertise

### 6. How Barology Works
A simple three-beat walkthrough:
- “See what Barology found.”
- “Swipe for the breakdown.”
- “Think there's more to it? Say it.”

Demonstrates lyric highlight → Lyrics/Barology swipe → song chat contribution.

### 7. First Bar Challenge
- headline: “What do you see?”
- user highlights a phrase and types what they think it means
- sandbox or real scoped Barology evaluation
- accepted contribution moment: “You caught something.”
- primary action: Enter Barology

See `product/ONBOARDING.md` for canonical onboarding copy and behavior.

## MVP primary app screens

### 8. Home
- trending artist carousel
- featured story / featured analysis
- mixed feed of news, releases, Barology analyses, Crown movement, AI misses, and notable community activity

### 9. Discover
- universal search
- Artists / Albums / Songs / Bars / News / AI Misses
- eras, regions, techniques, themes, and other discovery filters

### 10. Activity
- live network activity
- tabs: All / Breakdowns / Catches / Challenges / Rank Moves / Community

### 11. News
- lead story
- Today / Hip-Hop / Releases / Industry / Culture / AI
- separate article pages and topic pages

### 12. The Crown Rankings
- Artists / Songs / Albums / Verses / Bars
- category and time-range filters
- methodology/explanation access

### 13. Artist Profile
- black/near-black visual polarity
- hero image + artist identity
- Crown score / rank / analyzed catalog
- album carousel
- overview / music / bars / news / stats
- technique fingerprint
- top songs / top bars / recent news

### 14. Album Profile
- artwork / metadata
- album Barology score
- track list with song scores
- lyric-density heat strips
- album-wide intelligence fingerprint

### 15. Song — Lyrics
- song metadata
- clean vertically scrolling lyric view
- semantic span highlighting
- Lyrics / Map / Discussion controls
- full-screen horizontal swipe to Barology
- persistent access to Talk to This Song chat

### 16. Song — Barology
- opens aligned to the lyric/bar position from Lyrics mode
- exact highlighted span
- interpretation count
- canonical breakdown
- evidence + connected bars
- confidence/status/provenance
- support / oppose
- Add What Barology Missed
- Breakdown / Debate views
- persistent access to Talk to This Song chat

### 17. Song — Talk to This Song
- persistent AI conversation scoped to the selected song
- context includes current bar/span, existing interpretations, artist catalog, corpus context, and evidence
- user can propose a meaning conversationally
- accepted hypothesis can trigger scoped Mini-Gauntlet, update canonical breakdown, and credit contributor
- on mobile this may be an expandable composer/sheet rather than a separate navigation destination

### 18. Human Profile
- white/warm-white visual polarity
- same structural shell as Artist Profile
- Barologist rating / catches / AI misses / validation rate
- Activity / Catches / Doubts / Artists / Badges
- expertise by artist and technique

### 19. Top Breakdowns
- Recently Analyzed
- Most Complex
- Highest Rated
- Most Discussed
- Most AI Misses
- Trending
- song cards include score, density, interpretations, human contributions, and heat strip

## V1 incremental screens

### 20. Barology Hub
- Recent / Trending / Top Scores / AI Misses / Disputed

### 21. AI Misses
- unresolved bars
- recently validated catches
- hardest unsolved interpretations
- contributor leaderboard

### 22. Disputes
- active disputed interpretations
- evidence comparison
- qualified community voting
- re-Gauntlet status

### 23. Release Calendar
- albums/singles coming this week/month/year
- artist and album follow/watch actions

### 24. Artist Technique Detail
- wordplay, rhyme engineering, storytelling, reference depth, schemes, etc.
- evidence drilldown to songs/bars

### 25. Barology Map
- song/verse complexity heat map
- jump to dense regions
- relationship visualization for connected spans

### 26. Contributor Expertise Detail
- per-artist contribution history
- per-technique accuracy
- first finds
- successful challenges

### 27. Search Results / Intelligence Search
- semantic questions such as “Jay-Z Biggie references” or “hardest triple entendres”
- entity + graph aware results rather than title-only matching

## FUTURE surfaces

- internal Corpus Studio
- moderator/adjudicator workspace
- methodology and benchmark explorer
- artist claim/verification portal
- creator/artist self-annotation portal
- research chat over Barology corpus
- personalized watchlists
- notification center
- advertising/sponsorship management surfaces

## Supporting overlays / states

These are not separate primary destinations:

- command drawer / hamburger navigation
- interpretation bottom sheet
- Talk to This Song expanded composer
- add-missed-meaning composer
- structured challenge reason sheet
- evidence/source viewer
- connected-bar jump preview
- share card composer
- filter/sort sheet
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
