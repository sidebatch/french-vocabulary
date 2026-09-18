# v2.13.1 Meaning / Distractor QA Report

## Scope
Targeted QA after real-study screenshots exposed:
- incorrect or misleading source meanings,
- grammar-notation issues,
- multiple-choice questions with more than one defensible answer.

## High-confidence content fixes
29 meaning/notation fixes were applied.

Examples:
- `la brosse à dents`: 치약 브러시 → 칫솔
- `국자로` → 국자
- `acide`: 신성의 → 산성의
- `disponible`: 유연한 → 이용 가능한 / 시간이 되는
- `épuisant` / `épuisé`: 지치게 하는 / 지친
- `la crève`: 중병 → 심한 감기·몸살
- `au lieu de + inf/ind` → `au lieu de + inf`
- `à condition que + ind/sub` → `à condition que + sub`

## Distractor QA
Added ambiguity guards so semantically overlapping answers are less likely to appear together in:
- meaning
- listening
- reverse

The goal is not to make distractors easy. Close-but-distinct confusables remain useful; genuinely overlapping valid answers should not compete in one question.

## Integrity
- card count unchanged: 2,866
- stable IDs retained
- example corpus unchanged
- learning-state model unchanged
