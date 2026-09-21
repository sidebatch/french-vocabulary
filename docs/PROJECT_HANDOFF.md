# TEF Vocab Loop — PROJECT HANDOFF

**Current baseline:** `TEF_Vocab_Loop_v2_13_5.html`  
**Read first in a new session.** For the full reasoning/history, read `TEF_Vocab_Project_History.md`.

---

## 1. What this project is

A Korean/English bilingual French vocabulary learning app built as a single offline-friendly HTML file.

Primary goals:

- learn a 2,866-card A1-A2/B1-B2 French vocabulary corpus,
- support pronunciation-heavy learning,
- distinguish different kinds of knowledge,
- schedule delayed review,
- work smoothly on Android,
- preserve progress locally,
- stay focused rather than becoming a general language-learning platform.

The user prefers a modern, uncluttered UI and gives detailed real-use feedback.

---

## 2. Static corpus

- 2,866 unique vocabulary cards.
- A1-A2: 1,465.
- B1-B2: 1,401.
- Source rows before within-level duplicate collapse: 2,917.
- Korean source definitions are preserved as source data.
- Every card has example fields and a TTS-safe pronunciation field.

Typical card fields:

- `id`
- `level`
- `category`
- `fr`
- `ko`
- `pages`
- `occurrences`
- `cf`
- `tts`
- `exFr`
- `exKo`
- `exKind`

Do not change IDs casually; progress is keyed by card ID.

---

## 3. Learning-state model

Visible states:

**New → Seen → Learning → Familiar → Mastered**

plus **Weak** as current instability.

Definitions:

- **New**: never introduced.
- **Seen**: introduction viewed, but no real core quiz attempt.
- **Learning**: real learning has begun.
- **Familiar**: stronger core-skill evidence.
- **Mastered**: stronger spaced evidence, including long-interval success.
- **Weak**: recent repeated instability; recoverable.

Key rule:

> **Seeing is not learning.**

`확인했어요` alone must not count as Learning.

---

## 4. Skills

Tracked independently:

- meaning
- listening
- reverse
- spelling

Spelling is reinforcement and **not a mandatory mastery gate**.

Errors should affect the relevant skill, not wipe out the entire card.

---

## 5. Scheduling principles

- New word is introduced before testing.
- First meaning test appears after intervening questions.
- Errors reappear after several intervening questions.
- Pending retry duplication is prevented.
- Same-day repeated success should not over-promote a card.
- Spaced success matters more than same-session repetition.
- Review intervals broadly follow same-session → 1d → 3d → 7d → 14d → 30d → 60d.

---

## 6. Study selection

Whole-topic custom study intentionally uses **category-balanced selection**.

Reason: earlier code effectively selected the first N cards after priority sorting, which reflected PDF/source order and caused verb-heavy sessions.

Current intent:

- preserve weak/review/new priorities,
- balance categories within the relevant pool,
- respect an explicitly selected category.

Seen unfinished items should receive high continuation priority.

---

## 7. New-word back behavior

The back arrow after an accidental `확인했어요` is a **safe previous-introduction replay**.

It does not roll back progress/scheduling.

Reason: the UX need is “show me the word I accidentally skipped,” not “reverse the engine.”

---

## 8. Answer feedback layout invariant

Final intended visual hierarchy:

- answer feedback background
  - result
  - word/meaning/status
  - word audio / slow word audio
- separate white example card
  - French example
  - Korean example
  - sentence audio / slow sentence audio
- Next

Do not put word-audio controls inside the white example card again.

The user explicitly rejected that merged-background look.

Also keep the redundant system-like explanatory sentence removed.

---

## 9. Word library

Word tab is a personal vocabulary library.

Tapping a word opens a bottom sheet containing:

- word/meaning,
- level/category/status,
- word TTS,
- example + translation,
- example TTS,
- skill bars,
- last study,
- next review,
- answer stats,
- star/hard toggle.

PDF source/page is intentionally not shown in the UI.

---

## 10. Sentence library

Bottom tabs:

**오늘 · 학습 · 단어 · 문장 · 설정**

Sentence tab supports:

- Recommended / All,
- search,
- level filter,
- category filter,
- normal/slow sentence TTS,
- jump to linked word detail.

Recommended is intentionally selective.

At v2.6 QA:

- 353 / 2,866 examples recommended
- A1-A2: 78
- B1-B2: 275
- curated: 269
- reviewed: 84

Interpretation: these are sentences worth studying **as sentences**, not the only acceptable examples in the app.

---

## 11. TTS rule

Display and speech text are separate.

Example:

- display: `l'expression (f.)`
- TTS: `l'expression`

Do not blindly strip all parentheses because some parentheses contain real lexical variants.

---

## 12. Session persistence

Active study sessions are resumable.

Home can show:

- progress,
- source/type,
- continue,
- start over.

Exiting study saves the current session.

Completed sessions clear the saved active session.

Long closed-app time should not count as study duration.

---

## 13. Spelling

Current QA found 2,166 / 2,866 cards eligible under the simple-form spelling rule.

Behavior includes:

- exact accepted,
- accent-only differences can be “almost correct,”
- early leniency in some article cases,
- stricter later checking,
- complex multi-form cards excluded.

Spelling remains non-mandatory for mastery.

---

## 14. Persistence and portability

The single HTML contains:

- app logic,
- static corpus,
- examples.

Learner progress is stored in browser storage.

For development continuity:
- HTML is enough.

For learner-progress continuity:
- HTML + exported JSON backup is needed.

---

## 15. QA expectations

The environment has not reliably supported full GUI browser automation.

Use:

- JS syntax checks,
- card-count assertions,
- data integrity checks,
- targeted logic tests,
- learning-state simulations.

Then rely on real Android testing for final visual/mobile behavior.

---

## 16. Do not break these

- 2,866 stable card identities.
- Seen ≠ Learning.
- skill independence.
- spelling not required for mastery.
- delayed retry.
- category-balanced whole-topic study.
- safe intro replay.
- resumable session.
- word/example audio visual separation.
- TTS display/speech separation.
- direct-open Android HTML workflow.
- existing progress compatibility.

---

## 17. Current likely next work

High-value candidates:

1. Better distractor quality.
2. Word-library state filters.
3. Review generic/template sentence quality.
4. Later: selective cloze questions from high-value examples.

Before implementing any of these, read the relevant sections of the full history.

---

## 18. New-session instruction

When continuing in a new GPT session, say:

> This is an existing project. Read `PROJECT_HANDOFF.md` first, then `TEF_Vocab_Project_History.md`, then inspect the HTML. Preserve the documented product decisions unless I explicitly ask to change them. Before modifying code, identify which existing decisions the change touches. After modifying, update the documentation and QA notes.
---

## 19. Post-v2.6 comprehensive audit

A deeper audit identified several items that should be handled before major new features.

Read `QA_AUDIT_v2_6.md` and `ROADMAP_NEXT.md`.

Highest priority:

1. prevent Seen from starving overdue reviews,
2. make Seen backlog reduce new-word intake,
3. replace single `weakSkill` with multi-skill weakness,
4. strengthen Mastered spaced-evidence logic,
5. separate Weak / Hard / ★ semantics,
6. preserve due-date priority inside category balancing,
7. decide Today level scope.

The recommended next release is **v2.7 Learning Engine Hardening**.
---

## 20. v2.7 Smart Session direction

The user decided that fixed daily counts do not match real use because study volume can vary greatly by day.

A Smart Session design was simulated before implementation.

Read:

`SMART_SESSION_DESIGN_v2_7.md`

Decision:

- Today study should become dynamic/continuous.
- The engine should choose the next task after every interaction.
- Fixed daily new/review caps should no longer be the central scheduler.
- Custom study remains fixed-size.
- New-word pace should adapt to Due/Seen/Weak backlog.
- Implementation was completed in `TEF_Vocab_Loop_v2_7.html`.
---

## 21. v2.7 implementation contract

A detailed implementation contract now exists:

`V2_7_IMPLEMENTATION_SPEC.md`

Most important rule:

> Today Study and Custom Study are two different session types operating on one shared global learner record.

Session queues/retries must be revalidated against latest global progress when resumed, because the other mode may have changed the same card.

Recommended release split:
- v2.7: Smart Session + Today/Custom synchronization
- v2.8: multi-skill Weak + Mastered redesign
- v2.9: distractor/ambiguity quality

This split is safer than changing all core learning-state logic at once.
---

## 22. v2.7 implemented baseline

`TEF_Vocab_Loop_v2_7.html` is now the current implementation baseline.

Today Study:
- continuous Smart Session,
- no fixed daily completion size,
- dynamic next-task selection,
- adaptive New pacing.

Custom Study:
- remains finite,
- retains level/category/size/focus controls.

Session storage:
- Today and Custom can coexist in separate session slots.
- Both write to one shared global learner record.
- saved tasks are revalidated against latest card progress on resume.

Important v2.7 safety behavior:
- v2.6 fixed Today queue is retired during migration,
- card-level progress remains,
- finite Custom session can be retained,
- New/Retry delays in Smart use real intervening interactions,
- Weak cards have a Smart-session anti-spam cooldown,
- Smart daily visible counters reset across calendar days.

Read `V2_7_QA_REPORT.md` before changing the Smart scheduler.

Still deferred:
- multi-skill Weak
- Mastered evidence redesign
- Weak/Hard/★ separation
- distractor/ambiguity work
---

## 22. v2.7.1 automatic spelling rule

Real-device testing found that v2.7 automatic/mix study never produced spelling.

Fixed in v2.7.1.

Important distinction:
- `CORE` remains meaning/listening/reverse for mastery logic.
- spelling remains optional for mastery.
- automatic practice MUST still include spelling as reinforcement for eligible simple French forms.

Do not remove spelling from auto practice merely because it is not a mastery gate.

---

## 23. v2.7.2 number-display rule

Actual French number-value cards display Arabic numerals in the UI.

Example:
- `vingt` → `20`, not `스물`
- `cent` → `100`, not `백`

The original PDF Korean definitions remain stored unchanged.

Only true numeric values use the numeral presentation layer; `le nombre`, `le numéro`, `le chiffre`, etc. are ordinary vocabulary and keep Korean meanings.

Numeric answer choices should stay numeric as well.

---

## 24. v2.7.3 number-display rule

Number presentation is intentionally split:

- **1–99:** Arabic numerals
- **100 and above:** original Korean number words (`백/천/만/억...`)

Do not convert large values back to long Arabic-number strings unless the user explicitly asks.

---

## 25. v2.8.0 bilingual invariant

Current baseline: `TEF_Vocab_Loop_v2_8_0.html`.

The app supports Korean and English study/interface modes.

Do not break these rules:
- one French card corpus,
- one shared learner-progress record,
- original `ko` and `exKo` source data remain intact,
- English content is a sidecar keyed by the same card IDs,
- 1–99 true number cards use Arabic numerals in both modes,
- 100+ number cards use Korean wording in Korean mode and English wording in English mode,
- category values remain original source strings; visible labels are localized,
- an unanswered quiz rerenders after language switching.

English content is complete structurally but bulk-generated. Do not claim every English line was individually human-reviewed.

---

## 26. v2.8.1 bottom-nav size invariant

The compact v2.7-style bottom navigation is intentional.

- icon: 20px
- label: original 10px button text size

Do not apply the icon span font-size rule to translated label spans.

---

## 27. v2.8.2 spelling/TTS invariants

Spelling:
- no `_ _ _` letter-grid display,
- normal continuous text input,
- hint is opt-in,
- hint reveals only the beginning,
- hinted correct answers count as correct but do not advance spelling strength.

TTS:
- never speak grammar shorthand such as `+ inf`, `+ ind`, `+ sub`, `+ cond`, `qn`, `qc`.
- display notation and spoken text remain separate concerns.

---

## 28. v2.8.3 streak calendar

The header streak pill is intentionally clickable.

It opens a month calendar based on the existing `state.studyDays` history:
- purple fill = studied day,
- purple outline = today,
- previous/next month navigation,
- current streak + visible-month study-day count.

Do not create a separate calendar progress store.

---

## 29. v2.8.4 responsive-calendar invariant

The calendar grid cell and the visible date circle are intentionally separate.

- `.calendarDay` = seven-column layout cell
- `.calendarDate` = bounded visual marker
- never restore `aspect-ratio:1/1` on the whole grid cell
- keep `repeat(7,minmax(0,1fr))`
- keep viewport-aware modal max-height/overflow protections

This was required by real Android testing.

---

## 30. v2.8.5 today-calendar invariant

Calendar semantics are intentionally separated:

- purple fill = studied day,
- warm-colored date number = today,
- today before study = hollow neutral circle,
- today after study = purple filled circle but the date number keeps the today accent.

Do not use purple outline alone to mean today.

---

## 31. v2.8.6 calendar-class invariant

Do not use the generic class `today` on calendar date cells.

The Home screen already uses `.today` for its layout.

Calendar current-day state must use:
- `.calendarDay.isToday`

This prevents mobile layout CSS from shifting the current date.

---

## 32. v2.9.0 example-quality baseline

Current baseline: `TEF_Vocab_Loop_v2_9_0.html`.

A staged example-quality rewrite has begun.

v2.9.0 changes 286 low-value A1-A2 examples and synchronizes:
- `exFr`
- `exKo`
- English sidecar example `e`

Do not mass-regenerate the remaining corpus blindly.

Next content passes should prioritize:
1. B1-B2 `L’adjectif` `C'est ...` placeholders,
2. `On parle souvent de ... dans les médias`,
3. repetitive location templates,
4. repetitive health/history/society templates.

Use `EXAMPLE_UPGRADE_v2_9.tsv` to audit this pass.

---

## 33. v2.9.1 example-quality baseline

Current baseline: `TEF_Vocab_Loop_v2_9_1.html`.

Example-quality work now includes:
- v2.9.0: 286 rewrites
- v2.9.1: 167 additional rewrites

Major removed template families:
- mass `J'aime ...`
- B1-B2 adjective bare `C'est ...`
- `On parle souvent de ... dans les médias.`
- `Nous passons près de ...`

Continue staged review rather than regenerating all remaining examples at once.

---

## 34. v2.9.2 example-quality baseline

Current baseline: `TEF_Vocab_Loop_v2_9_2.html`.

Cumulative staged rewrite counts:
- v2.9.0: 286
- v2.9.1: 167
- v2.9.2: 159
- cumulative: **612 examples**

Removed major low-value families now include:
- `J'aime ...`
- B1-B2 bare adjective `C'est ...`
- `On parle souvent de ... dans les médias`
- `Nous passons près de / du ...`
- `Je parle souvent avec ...`
- `Le médecin examine ...`
- `On voit souvent ... dans la nature`

Next recommended bulk pass:
environment + news + religion + history generic frames.



---

## 35. v2.9.3 high-confidence example cleanup

v2.9.3 completed the five explicitly queued template families from the v2.9.2 handoff:

- `Ce cours porte sur ...` — 34
- `Ce documentaire parle de/du ...` — 28
- `Le journal parle de/du ...` — 24
- `Ce livre parle de/du ...` — 26
- `Le médecin parle de/du ...` — 32

Total: 144 changed cards.

French, Korean, and English examples were updated together. Card IDs, original meanings, and learner state stayed intact.

---

## 36. v2.10 sentence typing practice

The Sentence tab evolved from a browsing library into a sentence-production training entry point.

Two independent practice modes were added:

- **Copy**: show French + translation and type the sentence while understanding it.
- **Recall**: show only the translation and reconstruct the French sentence.

Important answer-checking decisions:

- initial capitalization does not cause failure,
- final `. ! ?` does not cause failure,
- accents, spelling, articles, prepositions, conjugation, and internal structure remain meaningful,
- wrong portions are highlighted for correction.

Per-sentence counts are stored separately for Copy and Recall.

Graduation rule:

- 15 completions in a mode = graduated in that mode,
- Copy graduation and Recall graduation are independent,
- graduated sentences are browsable in a separate graduation library.

The Sentence tab remains a library/hub; actual typing practice runs on a separate study screen and has resumable session state independent from word-study sessions.

---

## 37. v2.11 mobile/back-navigation and sentence-practice hardening

Real phone use drove several UI corrections:

- Copy-mode Confirm button was expanded to full width when it is the only action.
- Sentence page horizontal overflow was fixed across narrow mobile widths.
- Keyboard-height cases were adjusted so the input and primary action do not overlap.
- Word-detail bottom sheet uses history state so Android Back closes the sheet first when the browser delivers the event.
- App-level accidental-exit protection was added for normal web navigation flows.

Known platform limitation:

`file://` / `content://` HTML viewers may consume Android Back before the page receives it. A future HTTPS/PWA or native/WebView wrapper is the stronger solution if strict exit interception is required.

Recall-graduation semantics were also hardened:

> A Recall repetition counts toward 15/15 only when the learner answers correctly on the first attempt before revealing the answer.

Correct-after-edit and Answer-Revealed are still useful practice but do not inflate Recall graduation.

Session results distinguish:

- first-try correct,
- correct after correction,
- answer revealed.

---

## 38. v2.11.4 and v2.12 example-quality completion phase

v2.11.4 changed 45 additional clearly low-value or incorrect examples.

v2.12.0 then performed a **full-corpus audit of all 2,866 cards** and changed 583 high-confidence examples.

The audit targeted:

- repetitive boilerplate,
- low-learning-value frames,
- unnatural collocations,
- target-word sense mismatches,
- weak home/object/place/study/food/personality/travel/country/animal/profession templates.

Examples of sense corrections include:

- `arrêter`: bus-stopping sense → arrest sense matching the stored meaning,
- `vers`: approximate-time sense → direction sense,
- `responsable`: noun use → adjective construction,
- `tendre`: verb use → adjective/personality use.

Important content principle:

Do not rewrite a sentence merely because it is simple. Number/ordinal/month examples and other simple sentences may be exactly appropriate for their card.

The large template-cleanup phase is now substantially complete. Ongoing example QA should mostly be driven by real study and clear semantic issues.

---

## 39. v2.13 study-intent control

The user wanted explicit control over whether a session introduces new vocabulary.

Today now opens with three modes:

- **Auto** — existing adaptive Smart logic,
- **At least 25% New** — newly selected card mix maintains at least about 25% unintroduced New cards when available,
- **Review only** — no unintroduced New cards.

Custom Study has the same new-word-mix selector.

For finite Custom Study, the 25% policy is concrete: e.g. 20 targets → at least 5 New when enough New cards exist.

For continuous Today Study, the ratio applies to ongoing card selection rather than every visible interaction, because retries and learning-chain followups may temporarily dominate the screen.

---

## 40. v2.13 meaning-relearn loop

A wrong or `모르겠어요` answer on a meaning question now triggers a support step before retry:

1. fail/unknown meaning,
2. show **Relearn Meaning** with French + meaning + pronunciation,
3. learner confirms,
4. meaning is retested after intervening questions.

This applies specifically to meaning recognition. Listening/reverse errors are not all routed through the full introduction screen.

The reason is pedagogical: if the learner genuinely does not know the meaning, repeating the same multiple-choice question without re-teaching the association is low-value.

---

## 41. Current baseline / do not regress

Current baseline: `TEF_Vocab_Loop_v2_13_0.html`

Additional current invariants:

- Today has Auto / 25% New / Review-only intent control.
- Custom has the same new-word-mix control.
- Meaning failure can enter Relearn Meaning before delayed retest.
- Sentence Copy and Recall histories are independent.
- Recall graduation requires first-try unrevealed success.
- Sentence practice has a separate resumable session.
- v2.12 audited the full example corpus; future mass rewrites require a specific reason.
- local-file Android Back interception is best-effort, not guaranteed by the browser host.

Current highest-value future work:

1. selective cloze / progressive hint reduction,
2. multi-skill Weak,
3. stronger Mastered spaced evidence,
4. Weak / Hard / ★ separation,
5. reverse ambiguity guard,
6. distractor improvement,
7. library filters/sorting/search,
8. Recommended sentence curation,
9. backup/migration robustness,
10. later PWA/native/cloud packaging.


---

## 30. v2.13.1–v2.13.4 recent invariants

### Meaning / distractor QA
Real-use screenshots are high-value semantic QA evidence.
If a multiple-choice item has more than one defensible answer, fix the source meaning or ambiguity instead of expecting the learner to infer intent.

Keep close-but-distinct confusables. Block genuine overlap.

### Intentional browser reload
The app has a global `beforeunload` protection layer.
When the app itself intentionally reloads after saving state, it must explicitly mark that exit as allowed.
Do not remove genuine leave protection just to silence internal reload warnings.

### Calendar daily stats
- `studyDays` = the learner studied on that date.
- `dailyStats` = numeric detail recorded from v2.13.3 onward.

Never backfill old dates with guessed counts from cumulative attempts or last-attempt timestamps.

### Custom focus semantics — v2.13.4
The selector is a real focus control:

- `mix`: adaptive secondary logic
- `meaning`: meaning → delayed meaning confirmation
- `audio`: meaning foundation → listening
- `reverse`: meaning foundation → reverse
- `typing`: meaning foundation → spelling

A finite session target being complete does **not** mean the whole card is mastered.
Only actually attempted skills should advance.

Spelling focus filters candidates through `simpleFrench()` so the learner does not choose Spelling and unexpectedly receive another skill because a form is ineligible.

### Primary deployment target
GitHub Pages + Chrome is the primary real-use target.
Single-file direct-open HTML remains useful, but weak Android HTML Viewer compatibility is not a reason to destabilize the deployed browser experience.

---

## 31. Current unresolved Custom Study QA

See `reports/V2_13_3_CUSTOM_STUDY_QA.md`.

Open items:
1. finite-session future-task fallback can collapse intended real-interaction spacing;
2. Level = All exposes equivalent semantic topics under different raw category names;
3. narrow scopes can request 20/30/50 even when fewer candidates exist;
4. Review-only empty state is generic.

The finite-spacing item affects learning behavior and should be handled before cosmetic Custom Study improvements.


---

## 32. v2.13.5 Custom Study hardening

v2.13.5 closes the four highest-priority Custom Study QA findings from v2.13.4.

### Real interaction spacing
Finite Custom sessions now try to preserve actual learner interactions before delayed New tests/retries/follow-ups instead of merely jumping logical turn numbers.

When no task is currently available, the scheduler prefers:
1. promoting an in-session future New introduction, then
2. a focus-compatible bridge question from an already completed in-scope target.

Only when a scope is too small to produce valid bridge work does the old future-turn fallback remain.

QA on standard 10-card New25 sessions:
- 1,000 simulated runs
- minimum non-immediate chain gap: 3 interactions
- gaps under 3: 0
- logical-time fallback: 0

### Canonical topics under Level = All
Equivalent source categories are grouped only in Custom selection/display:
- Verbs
- Adjectives
- Prepositions
- Places
- Professions
- Objects

Underlying `category` values stay unchanged for data integrity.

### Available-count-aware size
Custom availability is calculated after:
- level
- topic
- focus mode
- New-word policy

Spelling focus therefore counts only `simpleFrench()`-eligible forms.
Review-only counts only introduced cards.

Impossible 20/30/50 choices are disabled.
Scopes under 10 cards receive an exact dynamic size option.

### Review-only zero state
If the selected review scope has zero eligible cards:
- show a specific review-empty message,
- disable Start.

### Regression invariant
Do not regress v2.13.4 focus semantics while maintaining spacing:
- Meaning = meaning only
- Listening = meaning foundation → listening
- Reverse = meaning foundation → reverse
- Spelling = meaning foundation → spelling
- Auto mix = adaptive

### Current next step
Before new features, perform a short real-device pass on GitHub Pages + Android Chrome.
