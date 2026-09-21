# TEF Vocab Loop — ROADMAP NEXT

**Current baseline:** v2.13.5

The product direction remains:

**Recognition → Recall → Production**

## Priority 0 — real-device regression before any new feature

v2.13.5 closed the previously identified Custom Study hardening items.

Verify on GitHub Pages + Android Chrome:
- Meaning wrong → Relearn → retry does not come back immediately
- Listening focus stays Listening after meaning foundation
- Reverse focus stays Reverse after meaning foundation
- Spelling focus stays Spelling and uses only eligible forms
- Level=All shows canonical semantic topics
- narrow scopes disable impossible session sizes
- Review-only with zero eligible cards shows the specific message
- saved finite sessions resume correctly

Do not start a new feature until this pass is acceptable.

## Priority 1 — progressive sentence retrieval

After regression, the strongest new learning-value candidate is still the missing bridge between Copy and full Recall:

1. full sentence visible
2. one target chunk blank
3. several chunks blank
4. translation + reduced cue
5. full production

Goal:
- increase retrieval gradually
- avoid turning sentence practice into mechanical typing
- reuse the existing improved example corpus
- keep Copy and Recall history interpretable

Do not automatically merge this with the current 15-count graduation system until the progression logic is tested.

## Priority 2 — learning-engine evidence quality

Later:
- multi-skill Weak representation
- stronger Mastered spaced evidence
- clearer Weak / Hard / ★ semantics
- continued distractor quality work with ambiguity safety

## Priority 3 — library usability

Possible later improvements:
- Word status filters / sorting
- accent-insensitive search
- stronger Sentence Recommended curation
- optional issue/report flag for individual content QA

## Packaging later

Only after the learning loop is stable:
- PWA polish
- Android wrapper if native Back/offline behavior justifies it
- cloud sync/login only if cross-device progress becomes important

## Explicitly not a current priority

- rankings/social
- arbitrary gamification
- large feature expansion
- weak third-party HTML viewer compatibility at the cost of Chrome stability

## v2.13.5 stable Custom invariants

- finite delayed chains prefer real intervening interactions
- Meaning = meaning only
- Listening = meaning foundation → listening
- Reverse = meaning foundation → reverse
- Spelling = meaning foundation → spelling
- Auto mix = adaptive
- Level=All canonical topic grouping affects selection/display only
- session size reflects current eligible pool
- Review-only zero scope cannot start
