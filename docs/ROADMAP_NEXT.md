# TEF Vocab Loop — Next Work Roadmap

**Baseline:** v2.13.0  
**Roadmap principle:** strengthen the learning loop before adding social/account surface area.

---

# Priority 0 — Protect user progress and release safety

- Export JSON before large local-file upgrades.
- Keep the previous stable HTML snapshot.
- Verify 2,866 cards / recent progress after GitHub deployment.
- Improve import validation and explicit schema migration handling.
- Consider last-backup timestamp / gentle backup reminder later.

---

# Priority 1 — Progressive sentence retrieval (highest learning-value feature)

Current sentence endpoints:

- Copy: full French visible.
- Recall: translation only; produce full French.

Missing bridge:

**progressive cloze / hint reduction**.

Possible progression:

1. full sentence visible,
2. one target chunk blank,
3. several chunks blank,
4. translation only,
5. full sentence production.

Goal:

- make typing retrieval practice rather than keyboard labor,
- reduce support gradually,
- reuse the improved example corpus,
- avoid making every sentence unnecessarily exhausting.

Do not automatically tie this to the current 15-count graduation until real-use behavior is tested.

---

# Priority 2 — Learning-engine evidence quality

## Multi-skill Weak

Current architecture historically centered on one `weakSkill` slot.
A card can realistically be weak in listening and reverse at the same time.

Target:
- allow simultaneous weak skills,
- recover each skill from appropriate evidence,
- avoid one skill erasing another skill's weakness.

## Mastered evidence

Strengthen spaced evidence so Mastered is not granted from stale/global evidence that does not represent all core skills well.

Spelling remains non-mandatory.

## Weak / Hard / ★ separation

Keep meanings distinct:

- Weak = current engine instability,
- Hard = performance-based difficulty,
- ★ = user-saved/manual importance.

---

# Priority 3 — Quiz fairness and quality

## Reverse ambiguity guard

Especially in English mode, one meaning can map to multiple valid French answers.

Examples of risk:
- `number` → `le nombre` / `le numéro`
- `about/regarding` → `au sujet de` / `à propos de`
- `although` → `bien que` / `quoique`

Options:
- add context,
- avoid ambiguous reverse multiple choice,
- accept multiple valid targets where structurally safe,
- use sentence/cloze instead.

## Better distractors

Improve with:
- same part of speech,
- same category,
- semantic closeness,
- form similarity,
- learner confusion history,
- ambiguity penalty.

---

# Priority 4 — Word/Sentence library usability

Word library:
- status filters: New / Seen / Learning / Familiar / Mastered / Weak / ★ / review-needed,
- sorting: A-Z / recent / due / weakest / source order,
- accent-insensitive search,
- optional local issue flag (`⚑ 검토 필요`).

Sentence library:
- improve Recommended precision,
- consider explicit curation fields/tags,
- useful tags: collocation / verb+preposition / everyday / connective / TEF reusable / grammar construction.

---

# Priority 5 — Real-use QA followups

- confirm sentence-only study should/should not count toward streak/studyDays,
- refine Back behavior for graduation library if still awkward,
- review browser `beforeunload` vs intentional internal reload/navigation behavior,
- continue individual example QA during actual study,
- test v2.13.0 New-intake modes under realistic long sessions.

---

# Priority 6 — Packaging / public release later

After the learning engine and content loop are stable:

- stable GitHub Pages / HTTPS deployment,
- installable PWA,
- Android WebView/native wrapper if strict Back/exit handling is needed,
- login/cloud sync only if cross-device use justifies it,
- rankings/social features only if they improve learning rather than distort it.

Do not make account/social features the next priority.

---

# Immediate recommended next step

Use v2.13.0 in real study for a short period and observe:

1. Is 25% New the right minimum?
2. Does Review-only behave as expected?
3. Does Relearn Meaning feel helpful or repetitive?
4. At what Copy repetition count does copying become mechanical?
5. How difficult is full Recall before 15 repetitions?

Then design the cloze/hint-reduction layer from real evidence instead of guessing.
