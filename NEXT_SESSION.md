# NEXT SESSION

Current baseline: **TEF Vocab Loop v2.13.5**

Read first:
1. `NEW_SESSION_START_HERE.md`
2. `PROJECT_STATUS.md`
3. `docs/PROJECT_HANDOFF.md`
4. `docs/TEF_Vocab_Project_History.md`
5. `docs/CHANGELOG.md`
6. `docs/QA_NOTES.md`
7. `docs/ROADMAP_NEXT.md`
8. `docs/reports/V2_13_5_QA_REPORT.md`
9. `index.html`

## Current product state

- 2,866 stable cards with one shared Korean/English learner record.
- Today = continuous Smart Session.
- Custom = finite session with level/topic/size/focus/new-word mix.
- v2.13.4 focus semantics remain:
  - Meaning → meaning confirmation
  - Listening → meaning foundation → listening
  - Reverse → meaning foundation → reverse
  - Spelling → meaning foundation → spelling
  - Auto mix → adaptive
- v2.13.5 hardened real delayed spacing in finite Custom sessions.
- Level=All now merges equivalent semantic topics through a canonical UI layer.
- Custom setup computes available cards after level/topic/focus/new-policy filters and disables impossible sizes.
- Review-only with zero eligible cards has a specific empty-state message.
- Calendar detailed daily stats exist from v2.13.3 onward.
- Sentence Copy and Recall remain independent 15-count graduation modes.

## v2.13.5 QA result

- 1,000 scheduler simulations: minimum non-immediate chain gap = 3 interactions; gaps under 3 = 0; logical-time fallback = 0.
- 16,020 Custom selection combinations: duplicate IDs / level leakage / topic leakage / Spelling leakage / Review-only New leakage / New25 failures = 0.
- CARDS and EN_DATA corpora unchanged.
- JavaScript syntax PASS.

Important limitation:
tiny/degenerate scopes can make real spacing mathematically impossible. A last-resort fallback remains rather than pulling words outside the selected scope.

## Next work

Do **not** add a new feature immediately.
First perform short real-device regression on GitHub Pages + Android Chrome:
- Custom Meaning/Listening/Reverse/Spelling
- delayed retry after a wrong meaning
- canonical topic grouping under Level=All
- disabled impossible session sizes
- Review-only zero-card state
- saved-session resume

After that, the strongest new learning-feature candidate remains partial cloze / progressive hint reduction between sentence Copy and full Recall.

## Critical invariants

- Preserve 2,866 stable card IDs.
- Seen ≠ Learning.
- New cards are introduced before testing.
- Skill evidence remains independent.
- Spelling does not gate mastery.
- Today and Custom share global progress.
- Do not fabricate historical daily statistics.
- GitHub Pages + Chrome is the primary runtime target.
