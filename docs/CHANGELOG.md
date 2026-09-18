# TEF Vocab Loop — CHANGELOG

This changelog is intentionally concise. See `TEF_Vocab_Project_History.md` for reasoning and detailed feedback.

## Pre-v2
- Built earlier flashcard/PWA-style vocabulary app.
- Confirmed direct-open HTML works on Android.
- Shifted toward a 말해보카-inspired micro-quiz learning loop.

## v1 / first Loop build
- French→Korean multiple choice.
- Korean→French multiple choice.
- audio→meaning.
- spelling input.
- delayed error reappearance.
- TTS.
- hard/starred words.
- IndexedDB.
- JSON backup.

## v2.0
- Rebuilt learning engine around separate skills:
  - meaning
  - listening
  - reverse
  - spelling
- Added state-based learning model.
- Added delayed retries and dynamic task selection.
- Added time-separated review stages.
- Spelling made non-mandatory for mastery.
- Added confusable distractor data.
- Added richer dashboard/status data.

## v2.1
- Added example sentence + Korean translation for all 2,866 cards.
- Added normal/slow sentence TTS.
- Added per-card TTS text separate from display text.
- Removed spoken grammar metadata such as `(f.)` / `(m.)`.
- Improved example quality and removed previous safe-placeholder examples.
- Refined answer-feedback UI.
- Removed redundant system-like feedback text.
- Iterated on word-audio placement:
  - first moved it into the example block,
  - then separated it back out visually after user feedback.
- Final layout: word audio in feedback area; example alone in white card.

## v2.2
- Fixed whole-topic custom study source-order bias.
- Added category-balanced selection while preserving priority.
- Added safe previous-new-word replay/back control.
- Replay does not roll back learning state.

## v2.3
- Added `Seen` state.
- `확인했어요` alone no longer counts as Learning.
- First actual quiz response begins Learning.
- Previously Seen unfinished words resume from a meaning test.
- Added Seen to dashboard.
- Mobile status grid adjusted for 6 states.

## v2.4
- Turned Word tab into a vocabulary library.
- Added mobile bottom-sheet word detail.
- Added word/example TTS inside detail.
- Added all four skill bars.
- Added last/next review info and stats.
- Added star toggle in detail.
- Removed PDF page/source from visible Word-tab UI.

## v2.5
- Added resumable active study sessions.
- Home shows in-progress study with continue/start-over.
- Manual exit persists session.
- Completion clears active session.
- Original focus mode survives resume.
- Active study time avoids counting long app-closed periods.
- Performed targeted spelling QA.
- Confirmed 2,166 / 2,866 cards currently spelling-eligible.

## v2.6
- Added Sentence tab.
- Bottom navigation is now:
  - 오늘
  - 학습
  - 단어
  - 문장
  - 설정
- Added Recommended / All sentence views.
- Added sentence search, level/category filters.
- Added normal/slow sentence TTS.
- Added link to associated word detail.
- Added heuristic recommendation scoring for reusable learning value.
- v2.6 recommended set:
  - 353 total
  - 78 A1-A2
  - 275 B1-B2
  - 269 curated
  - 84 reviewed


## v2.7
- Replaced fixed Today target list with continuous Smart Session.
- Today now chooses the next task dynamically after every interaction.
- Removed visible daily New/review caps from Today scheduling.
- Added `새 단어 속도: 적게 / 보통 / 많이`.
- Added adaptive new-word credit that slows under Due/Seen/Weak backlog.
- Today Smart Session and finite Custom Study now have separate active-session slots.
- Both modes continue to update one shared global card-progress record.
- Added cross-mode stale-task/retry revalidation.
- Preserved global Seen behavior across Today and Custom.
- Strengthened Smart New/retry spacing to actual 3–5 intervening interactions.
- Added session-local Weak anti-spam cooldown without changing the global Weak model.
- Added daily reset of Smart visible counters while preserving scheduler continuity.
- Introduced app/data/session schema version constants.
- v2.6 card progress is preserved during migration.
- Obsolete v2.6 fixed Today future queue is retired during migration.
- Existing finite Custom session can be retained.
- Added v2.7 backup filename/schema handling.

## v2.7.1
- Fixed Auto/Mix study never selecting spelling.
- Root cause: automatic review used only the three CORE skills (`meaning`, `listening`, `reverse`), while spelling was only reachable through forced `철자` mode.
- Auto mode now includes spelling as reinforcement for eligible simple French forms.
- New-word secondary task: spelling is selected about 20% of the time when eligible.
- Existing/due auto review: spelling can appear at a lower rate so core due reviews still dominate.
- Spelling remains non-mandatory for Familiar/Mastered.
- Forced Meaning/Listening/Reverse/Spelling modes are unchanged.
- Corrected the browser tab title from the legacy `v2.1` label to `v2.7.1`.

## v2.7.2
- Number vocabulary now displays Arabic numerals in the learning UI instead of Korean number words.
- Examples:
  - `un` → `1`
  - `vingt et un` → `21`
  - `cent` → `100`
  - `mille` → `1,000`
  - `million` → `1,000,000`
- Numeric multiple-choice distractors are also displayed as numerals, so a number question does not mix `스물`, `서른`, etc.
- Reverse and spelling prompts use numerals as well.
- The original Korean source meanings remain unchanged inside the embedded vocabulary data.
- Search can match both the original Korean source meaning and the displayed numeral.

## v2.7.3
- Refined number display after real-use feedback.
- Values below 100 stay as Arabic numerals:
  - `un` → `1`
  - `vingt et un` → `21`
  - `quatre-vingts` → `80`
- Values from 100 upward now use the original Korean number words:
  - `cent` → `백`
  - `mille` → `천`
  - `un million` → `백만`
  - `cent millions` → `일억` (source wording preserved)
- This keeps small numbers visually fast while preserving Korean large-number unit intuition (`백/천/만/억`) for bigger values.

## v2.8.0
- Added a Korean / English study-language switch in Settings.
- The selected language changes the interface, meanings, example translations, quiz prompts/answers, category labels, Word library, and Sentence library.
- Added English content for all 2,866 cards: 2,866 meanings and 2,866 example translations.
- French source text, stable card IDs, Korean source meanings, and Korean example translations remain unchanged.
- Korean and English modes share one learner-progress record.
- Search includes French, Korean, and English content.
- 1–99 number values display as Arabic numerals in both modes.
- 100+ number values use Korean number words in Korean mode and English number wording in English mode.
- Fixed the v2.7.3 numeric-recognition edge case by separating all 58 numeric cards from the 1–99 display override.
- Changing language during an unanswered quiz rerenders the current question to prevent stale choices from being judged against the new language.
- English content was bulk-generated and structurally QA-checked; it was not individually human-edited card by card.

## v2.8.1
- Fixed bottom navigation label text becoming too large after the bilingual/i18n update.
- Root cause: v2.8.0 wrapped nav labels in `<span data-i18n=...>`, while the old `.bottom span` rule gave every span the 20px icon size.
- Icon size remains 20px.
- Bottom labels return to the original inherited 10px button size, matching the v2.7.x appearance.

## v2.8.2
- Redesigned spelling questions:
  - removed the spaced underscore/letter-grid hint,
  - spelling now starts with a clean normal text input,
  - added an optional `힌트 보기 / Show hint` control,
  - hint reveals only the beginning of the answer (`b…`, `l'e…`, `le t…`).
- A correct answer after using the hint still counts as correct, but does not advance the spelling step; it is treated as weaker evidence.
- Hint use is stored on the current task so it survives a saved/resumed session.
- Fixed French TTS reading grammar shorthand such as `+ inf`, `+ ind`, `+ sub`, `+ cond`, `qn`, and `qc`.
- Corrected the 20 known TTS strings that still contained grammar placeholders.
- Added a runtime speech-cleaning fallback so future shorthand metadata is not spoken.

## v2.8.3
- Made the streak pill interactive.
- Tapping `연속 N일 / N-day streak` opens a visual study calendar.
- Current month highlights every recorded study day.
- Today is outlined separately.
- Added previous/next month navigation so older study history can be viewed.
- Calendar summary shows study days in the visible month and the current streak.
- Calendar UI is localized for Korean and English.
- Uses the existing `studyDays` history, so no learning-progress migration is required.

## v2.8.4
- Rebuilt the streak calendar layout as a responsive component after real Android testing exposed overflow and oversized date circles.
- Calendar cells and date markers are now separate:
  - the 7-column grid controls alignment,
  - a small centered date circle controls the studied/today marker.
- Removed `aspect-ratio` from the whole grid cell, which caused giant circles on some mobile widths.
- Added responsive safeguards for:
  - narrow phones,
  - short/landscape screens,
  - tablets,
  - desktop widths.
- Calendar modal now uses viewport-aware width/max-height and internal scrolling instead of overflowing the screen.
- Weekday header and dates use the same seven-column sizing model.

## v2.8.5
- Refined the visual treatment for **today** in the streak calendar.
- Before studying today:
  - today's date number uses a distinct warm accent color,
  - the date sits inside an unfilled neutral-outline circle.
- After studying today:
  - the circle fills purple like every other studied day,
  - today's date number keeps the distinct accent color so it remains identifiable as today.
- Updated the calendar legend to reflect the new today marker.

## v2.8.6
- Fixed today's calendar circle appearing lower than the other dates.
- Root cause: the calendar used class `today`, which collided with the existing Home-page `.today` layout CSS (`display:grid`, `margin-top:20px`, etc.).
- Renamed the calendar-only state class to `isToday`.
- Today's marker now stays vertically aligned with every other date while preserving the v2.8.5 color/fill behavior.

## v2.9.0
- Started the large Example Quality Upgrade.
- Replaced **286** low-value A1-A2 examples with practical, contextual sentences.
- Removed the mass template pattern `J'aime [noun]` from the targeted food/sports/clothing/accessory/drink sections.
- Reworked many one-line `C'est [adjective]` examples into contexts that show actual usage.
- Updated French examples, Korean translations, and English translations together.
- Preserved all 2,866 card IDs, vocabulary meanings, categories, TTS, and learning progress compatibility.
- Added `EXAMPLE_UPGRADE_v2_9.tsv` so every changed sentence can be audited old-vs-new.

## v2.9.1
- Continued the Example Quality Upgrade with **167** additional rewrites.
- Replaced all 80 B1-B2 `L’adjectif` bare `C'est ...` placeholders.
- Replaced all 34 `On parle souvent de ... dans les médias.` society templates.
- Replaced all 53 `Nous passons près de ...` location templates.
- Updated French example + Korean translation + English translation together.
- Preserved card IDs, vocabulary meanings, TTS, categories, and learning-progress compatibility.
- Added `EXAMPLE_UPGRADE_v2_9_1.tsv` for full old/new auditing.

## v2.9.2
- Continued Example Quality Upgrade with **159** additional rewrites.
- Removed the remaining A1-A2 low-value template families:
  - `Nous passons près du ...` (45)
  - `Je parle souvent avec ...` (30)
  - `Le médecin examine ...` (45)
  - `On voit souvent ... dans la nature` (39)
- Replaced them with practical contexts for places, family/people, body/health, and nature.
- Updated French, Korean, and English examples together.
- Preserved 2,866 card IDs, source meanings, TTS, categories, and progress compatibility.
- Added `EXAMPLE_UPGRADE_v2_9_2.tsv` for line-by-line auditing.



## v2.9.3
- Rewrote the remaining 144 high-confidence repetitive example families queued by v2.9.2.
- Removed `Ce cours porte sur...`, documentary/news/book/doctor generic families targeted in the handoff.
- Updated French, Korean, and English examples together.
- Preserved card IDs, source meanings, and learner-state compatibility.

## v2.10.0
- Added sentence typing practice inside the Sentence feature.
- Added two separate modes: Copy (French + translation visible) and Recall (translation only).
- Kept sentence practice separate from word `spelling` skill progress.

## v2.10.1
- Sentence checking now ignores initial capitalization and final `. ! ?` differences.
- Kept accents/spelling/grammar-sensitive differences strict.
- Added red highlighting/comparison for wrong portions.

## v2.10.2
- Added per-sentence Copy and Recall practice counts.
- Counts persist and do not remove a sentence from future random practice.
- Improved mobile action placement so checking does not require unnecessary scrolling.

## v2.10.3
- Fixed Copy mode single Confirm action occupying only the left half of a two-column action grid.
- Confirm now uses full width when it is the only action.

## v2.10.4
- Added independent 15-repetition graduation for Copy and Recall.
- Added mode-specific graduated sentence library.
- Added current-sentence `n/15` progress display.

## v2.11.0
- Moved sentence typing into a dedicated study screen instead of embedding the full exercise in the Sentence library.
- Added resumable sentence-practice session state independent from word-study sessions.

## v2.11.1
- Integrated word-detail bottom sheet with browser history so Android Back can close the sheet when the host forwards the event.

## v2.11.2
- Added broader accidental-exit/back-navigation protection for normal browser navigation flows.
- Preserved X/overlay close behavior for dialogs.
- Documented local HTML viewer limitation: some hosts intercept Android Back before page JavaScript.

## v2.11.3
- Recall graduation now increments only for first-try correct answers before answer reveal.
- Split sentence results into first-try correct / corrected / answer revealed.
- Fixed Sentence-page mobile horizontal overflow.
- Improved short-viewport/keyboard layout so input and primary action do not overlap.

## v2.11.4
- Rewrote 45 additional clearly low-value or incorrect examples.
- Continued synchronized French/Korean/English example updates.

## v2.12.0
- Performed a full-corpus audit of all 2,866 example sentences.
- Rewrote 583 high-confidence low-value, repetitive, unnatural, or sense-mismatched examples.
- Corrected target-sense mismatches including `arrêter`, `vers`, `responsable`, and `tendre`.
- Verified 2,866 cards, 2,866 English sidecar entries, unique IDs, valid `cf` references, and no empty FR/KO/EN examples.
- Preserved original vocabulary meanings and non-example card fields.

## v2.13.0
- Added Today study-intent picker: Auto / At least 25% New / Review only.
- Added the same New-word mix control to Custom Study.
- Finite Custom `25% New` reserves at least one quarter of targets for unintroduced New cards when available.
- Continuous Today `25% New` maintains New intake over ongoing selection while allowing retries/learning-chain tasks to take priority.
- Review-only mode blocks unintroduced New cards.
- Added Relearn Meaning flow after a wrong/unknown meaning answer before delayed meaning retest.
- Bumped session schema to 3.
- Preserved the 2,866-card corpus and v2.12.0 example content.


## v2.13.1
- Ran targeted meaning/grammar-notation QA after real-study screenshots exposed ambiguous and incorrect answer content.
- Corrected 29 high-confidence meaning/notation issues without changing card IDs.
- Added distractor ambiguity guards for overlapping/synonymous pairs in meaning/listening/reverse multiple choice.
- Preserved distinct close-confusable cases.

## v2.13.2
- Fixed Chrome `Reload site? Changes that you made may not be saved.` appearing after intentional in-app reloads.
- Internal app reloads now bypass `beforeunload` only after persistence.
- Genuine browser-leave/reload protection remains.

## v2.13.3
- Added clickable studied dates in the streak calendar.
- Added `dailyStats` persistence for date-level study detail from v2.13.3 onward.
- Daily detail includes word questions, New words, correct/wrong, accuracy, Sentence Copy, and Sentence Recall activity.
- Historical study dates from older versions remain visible but do not receive invented numeric statistics.

## v2.13.4
- Aligned Custom Study focus mode with actual question behavior.
- Meaning focus now uses meaning → delayed meaning confirmation.
- Listening focus uses meaning foundation → listening.
- Reverse focus uses meaning foundation → reverse.
- Spelling focus uses meaning foundation → spelling.
- Auto mix preserves adaptive secondary-skill selection.
- Spelling-focus candidate selection now excludes forms that are not eligible under `simpleFrench()`.
- Preserved separate skill evidence: Meaning-only success does not advance Listening/Reverse.
- JS syntax QA passed; 2,866-card and English sidecar corpora unchanged.
