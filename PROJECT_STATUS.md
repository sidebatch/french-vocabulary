# TEF Vocab Loop — PROJECT STATUS

**Current stable baseline:** `TEF_Vocab_Loop_v2_13_5.html`  
**GitHub Pages entry:** `index.html`

## Data
- Cards: 2,866
- A1-A2: 1,465
- B1-B2: 1,401
- Stable IDs retained
- Korean + English display/content
- Shared learner progress across UI languages

## Current learning architecture
- separate meaning/listening/reverse/spelling evidence
- Today: continuous Smart Session
- Custom: finite session
- New / Seen / Learning / Familiar / Mastered / Weak
- New cards introduced before testing
- delayed retry + Meaning Relearn
- Sentence Copy / Recall with independent 15-count graduation
- date-level calendar stats from v2.13.3 onward

## v2.13.5 Custom hardening
- finite delayed follow-up/retry uses real interaction spacing when bridge work is available
- future New introductions may be promoted to fill safe spacing
- completed in-scope targets can provide focus-compatible bridge reinforcement at session tails
- equivalent Level=All topics are canonicalized in the Custom UI
- session-size availability is calculated after all relevant filters
- impossible 20/30/50 sizes are disabled
- Review-only zero-card state uses a specific message and disabled Start

## QA
- scheduler simulation: 1,000 runs, gaps under 3 = 0, fallback = 0 in tested 10-card New25 sessions
- Custom selection matrix: 16,020 combinations PASS
- 2,866 unique IDs unchanged
- CARDS / EN_DATA hashes unchanged
- JS syntax PASS

## Current next step
Short real Android Chrome regression only. No new feature should be added before this check.

After regression, the highest-value feature candidate is progressive sentence retrieval / partial cloze.

## Deployment
Primary runtime: **GitHub Pages + Chrome**.
Older HTML snapshots belong in `archive/`; root keeps the current version snapshot only.
