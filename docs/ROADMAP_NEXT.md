# TEF Vocab Loop — ROADMAP NEXT

**Current baseline:** v2.13.4

The product direction remains:

**Recognition → Recall → Production**

Do not prioritize feature count over learning value or reliability.

## Priority 1 — finite Custom spacing hardening

The most important open QA item is the finite-session queue behavior.

Current issue:
when no task is currently available, the finite selector can take the earliest future task and effectively advance logical turn time. That can reduce the number of **real intervening learner interactions** before:
- a new-word meaning test,
- a delayed retry,
- a follow-up confirmation.

Goal:
preserve the existing “several questions later” learning principle in finite Custom sessions, not just in logical turn numbers.

Do not solve this with immediate duplicate questions or meaningless filler.

## Priority 2 — canonical topic grouping for Level = All

Equivalent source categories currently appear separately under Level = All, for example:

- `LES VERBES` / `Les verbes`
- `ADJECTIFS` / `L’adjectif`
- `PRÉPOSITIONS` / `Les prépositions`
- `L’ENDROIT` / `L’endroit`
- `LA PROFESSION` / `La profession`
- `OBJETS` / `L’objet`

Preferred solution:
add a canonical grouping layer for selection/display while preserving the underlying source category strings.

## Priority 3 — available-count-aware session size

Narrow scopes may contain fewer than 20/30/50 eligible cards.

Improve setup UX so target size does not silently shrink.

Possible directions:
- show `사용 가능 N개`
- disable impossible sizes
- or show the effective target before start

Spelling-focus availability must be calculated **after** spelling eligibility filtering.

## Priority 4 — small Custom Study UX cleanup

- Review-only empty state should explicitly say there are no review cards in the selected scope.
- Keep setup visually light.
- Do not overload the screen with pre-session statistics unless they directly help the choice.

## Priority 5 — progressive sentence recall

After Custom Study hardening, the strongest learning-feature candidate is the missing bridge between Copy and full Recall:

1. full sentence visible
2. one target chunk blank
3. several chunks blank
4. translation + reduced cue
5. full production

Typing should remain retrieval practice, not mechanical keyboard labor.

## Later architecture items

- multi-skill Weak representation
- stronger Mastered evidence
- clearer Weak / Hard / ★ semantics
- better distractors while preserving ambiguity safety
- sentence Recommended curation precision
- PWA / Android wrapper if stronger native-back/offline behavior becomes necessary
- optional sync/login only when cross-device progress justifies the complexity

## Explicitly not a priority

- ranking/social features
- arbitrary gamification
- changing already-good examples just to make them different
- weak third-party HTML-viewer compatibility at the cost of Chrome/GitHub Pages stability

## Current stable focus behavior — v2.13.4

- Meaning = meaning → delayed meaning confirmation
- Listening = meaning foundation → listening
- Reverse = meaning foundation → reverse
- Spelling = meaning foundation → spelling
- Auto mix = adaptive
- Spelling target pool excludes ineligible forms

Do not regress this behavior while fixing finite-session spacing.
