# NEXT SESSION

Current baseline: **TEF Vocab Loop v2.13.0**

Read first:
1. `NEW_SESSION_START_HERE.md`
2. `docs/PROJECT_HANDOFF.md`
3. `docs/TEF_Vocab_Project_History.md`
4. `docs/CHANGELOG.md`
5. `docs/QA_NOTES.md`
6. `docs/ROADMAP_NEXT.md`
7. `docs/reports/V2_13_0_QA_REPORT.md`
8. `docs/example-audits/V2_12_0_EXAMPLE_AUDIT.md`
9. `index.html`

## Current product state

- 2,866 stable cards.
- Korean/English bilingual display with one shared learner record.
- Today = continuous Smart Session.
- Today modes: Auto / At least 25% New / Review only.
- Custom Study is finite and now also has new-word mix selection.
- New cards are introduced before testing.
- Failed/unknown meaning questions go through a Relearn Meaning screen before delayed retest.
- Sentence practice has two independent modes: Copy and Recall.
- Each sentence/mode tracks repetitions independently; 15 = graduated.
- Recall graduation increases only for first-try success before answer reveal.
- Sentence practice is a separate resumable study screen.
- v2.12.0 completed a full 2,866-example audit and changed 583 high-confidence examples.

## Product direction

Do not add features merely to increase feature count.
The long-term learning direction is:

**Recognition → Recall → Production**

The strongest next learning feature candidate is a selective cloze / hint-reduction step between copy typing and full sentence recall.

## Critical invariants

- Preserve 2,866 stable card identities.
- Seen ≠ Learning.
- Meaning, listening, reverse, and spelling remain independent.
- Spelling is reinforcement, not mandatory for mastery.
- Today and Custom share one global card progress record.
- New cards must be introduced before testing.
- Failed items should not be immediately echoed; delayed retry remains important.
- Word audio and example audio remain visually separated.
- TTS must not read grammar metadata.
- Sentence Copy and Recall counts remain independent.
- Recall 15/15 must mean genuine first-try recall, not corrected/revealed answers.
- Original vocabulary meanings must not be casually rewritten during example QA.
- French/Korean/English example translations must stay synchronized when an example changes.

## High-value next work

1. Real-use testing of v2.13.0 Smart new-word modes.
2. Partial cloze / progressive hint reduction design.
3. Multi-skill Weak model.
4. Mastered evidence hardening.
5. Weak / Hard / ★ semantic separation.
6. Reverse ambiguity guard, especially English mode.
7. Better distractors.
8. Word-library filters/sorting/search improvements.
9. Sentence Recommended curation precision.
10. Later packaging: PWA / Android wrapper / cloud sync if needed.
