# TEF Vocab Loop v2.13.0 — QA Report

## Baseline

- App: `TEF_Vocab_Loop_v2_13_0.html`
- Cards: **2866**
- Unique IDs: **2866**
- A1-A2: **1465**
- B1-B2: **1401**
- English sidecar entries: **2866**
- App version: **2.13.0**
- Data schema: **3**
- Session schema: **3**

## Static checks performed

- JavaScript syntax (`node --check`): **PASS**
- 2,866 card count: **PASS**
- 2,866 unique card IDs: **PASS**
- English sidecar covers all card IDs: **PASS**
- `todayModeNew25` path/string present: **PASS**
- `todayModeReview` path/string present: **PASS**
- Custom `newMix` selector present: **PASS**
- `relearnMeaning` path/string present: **PASS**
- Sentence graduation library remains present: **PASS**
- Dedicated sentence study page remains present: **PASS**
- Session schema version 3 present: **PASS**

## Data regression check

Compared with v2.12.0 baseline:

- card IDs / levels / categories / French headwords / Korean meanings / French examples / Korean example translations are unchanged in v2.13.0: **PASS**

v2.13.0 is therefore a learning-flow/session update, not another corpus rewrite.

## v2.13.0 behavior to validate in real use

1. **Today — Auto**
   - behaves like adaptive Smart Session,
   - new intake still responds to backlog and pace.

2. **Today — At least 25% New**
   - New intake remains visible over a long run when New cards exist,
   - retries / Seen followups / learning-chain tasks may temporarily take priority.

3. **Today — Review only**
   - never introduces a never-seen New card.

4. **Custom — At least 25% New**
   - 20 targets → at least 5 New when supply permits,
   - 30 → at least 8,
   - 50 → at least 13.

5. **Meaning relearn**
   - wrong or `모르겠어요` on meaning → Relearn Meaning,
   - French + meaning + pronunciation shown,
   - delayed meaning retest occurs after intervening questions.

6. **Resume / migration**
   - existing learner progress loads,
   - active sessions behave correctly after session-schema 3 update,
   - JSON export/import remains usable.

## Known platform limitation

Android local HTML (`file://` / `content://`) Back/exit interception cannot be guaranteed because the host viewer/browser may consume Back before page JavaScript receives it.

This is not treated as a blocker for the current direct-open workflow; stable HTTPS/PWA or native/WebView packaging is the future solution if strict control is required.

## Release note

The repository documentation in this update package was refreshed to v2.13.0 so a future development session no longer starts from the obsolete v2.9.2 handoff state.
