# TEF Vocab Loop — PROJECT STATUS

**Current stable baseline:** `TEF_Vocab_Loop_v2_13_4.html`  
**GitHub Pages entry:** `index.html`

## Data
- Cards: 2,866
- A1-A2: 1,465
- B1-B2: 1,401
- Stable IDs retained
- Korean + English display/content
- Shared learner progress across UI languages

## Current learning architecture
- Global card progress with separate meaning/listening/reverse/spelling evidence
- Today: continuous Smart Session
- Custom: finite session
- New / Seen / Learning / Familiar / Mastered / Weak
- New cards introduced before testing
- Delayed retry
- Meaning Relearn flow
- Sentence Copy / Recall sessions and per-mode 15-count graduation
- Date-level calendar stats from v2.13.3 onward

## Current Custom focus behavior
- Auto mix: adaptive
- Meaning: meaning → delayed meaning confirmation
- Listening: meaning foundation → listening
- Reverse: meaning foundation → reverse
- Spelling: meaning foundation → spelling
- Spelling mode filters out ineligible card forms

## Known unresolved QA
- finite Custom delayed-spacing can collapse if no currently available task exists
- duplicate semantic topic labels exist across A1-A2/B1-B2 when Level = All
- requested session size can exceed available candidates in a narrow scope
- review-only empty-state wording is generic

## Deployment recommendation
Use GitHub Pages + Chrome as the primary runtime.
Keep the single HTML file for backup/offline inspection, but do not optimize for weak third-party HTML Viewer compatibility at the expense of the deployed browser experience.
