# v2.13.4 QA Report

## Scope
Focused release for Custom Study focus-mode semantics.

## Changes verified

### Meaning focus
New/Seen learning chain:
- introduction
- meaning
- delayed meaning confirmation

Meaning focus no longer injects Listening/Reverse/Spelling as an adaptive secondary skill.

### Listening focus
- introduction
- meaning foundation
- listening

### Reverse focus
- introduction
- meaning foundation
- reverse

### Spelling focus
- introduction
- meaning foundation
- spelling

Candidate selection filters to `simpleFrench()`-eligible forms.

### Auto mix
Existing adaptive secondary-skill behavior remains.

## Skill-evidence invariant
Only the actually attempted skill is recorded.
A completed Meaning-focused target does not imply card-wide mastery and does not advance Listening/Reverse evidence.

## Static QA
- JavaScript syntax: PASS
- card count: 2,866
- unique IDs retained
- CARDS corpus unchanged from v2.13.3
- EN_DATA corpus unchanged from v2.13.3
- spelling-eligible cards under current rule: 2,167 / 2,866

## Known open issue
Finite-session spacing is not fully hardened.

Delayed follow-up/retry tasks are scheduled several logical turns ahead, but the finite selector may jump to a future task if there is no currently available work.

Therefore, v2.13.4 must **not** be described as guaranteeing 3–5 actual intervening learner questions in every narrow/tail session.

See `V2_13_3_CUSTOM_STUDY_QA.md` for the full Custom QA findings.
