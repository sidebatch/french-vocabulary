# NEXT SESSION

Current baseline: **TEF Vocab Loop v2.13.4**

Read first:
1. `NEW_SESSION_START_HERE.md`
2. `PROJECT_STATUS.md`
3. `docs/PROJECT_HANDOFF.md`
4. `docs/TEF_Vocab_Project_History.md`
5. `docs/CHANGELOG.md`
6. `docs/QA_NOTES.md`
7. `docs/ROADMAP_NEXT.md`
8. `docs/reports/V2_13_3_CUSTOM_STUDY_QA.md`
9. `docs/reports/V2_13_4_QA_REPORT.md`
10. `index.html`

## Current product state

- 2,866 stable cards.
- Korean/English bilingual display with one shared learner record.
- Today = continuous Smart Session.
- Today modes: Auto / At least 25% New / Review only.
- Custom = finite session with level/topic/size/focus/new-word mix.
- Meaning failure can go through Relearn Meaning before delayed retest.
- Sentence practice has independent Copy and Recall modes and resumable state.
- 15 successful repetitions per sentence/mode = graduated.
- Calendar stores detailed per-day stats from v2.13.3 onward.
- v2.13.1 added meaning/distractor ambiguity QA.
- v2.13.2 fixed intentional reload vs beforeunload conflict.
- v2.13.4 aligned Custom focus semantics with actual question types.

## v2.13.4 Custom focus invariant

- Meaning: meaning → delayed meaning confirmation.
- Listening: meaning foundation → listening.
- Reverse: meaning foundation → reverse.
- Spelling: meaning foundation → spelling.
- Auto mix: adaptive secondary skill.
- Spelling focus candidate pool contains only `simpleFrench()`-eligible forms.

Do **not** convert a Meaning-only success into Listening/Reverse success.
Skill evidence remains independent.

## Highest-value next work

1. Fix finite-session spacing so 3–5 turns means real intervening learner interactions, even when no current task is available.
2. Canonicalize equivalent A1/B1 topic names when Level = All.
3. Make requested session size reflect available candidates.
4. Improve review-only empty-state wording.
5. After stability: design partial cloze / progressive hint reduction between Copy and full Recall.

## Critical invariants

- Preserve 2,866 stable card identities.
- Seen ≠ Learning.
- New cards must be introduced before testing.
- Meaning/listening/reverse/spelling stay independent.
- Spelling is reinforcement, not mandatory for mastery.
- Today and Custom share one global progress record.
- Failed items should not be immediately echoed.
- Word audio and example audio remain visually separated.
- TTS must not read grammar metadata.
- FR/KO/EN examples stay synchronized after content edits.
- Do not fabricate historical daily study statistics that were never stored.
