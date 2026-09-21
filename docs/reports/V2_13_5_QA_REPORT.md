# TEF Vocab Loop v2.13.5 — Custom Study Hardening QA

## Scope
v2.13.4에서 남아 있던 Custom Study의 우선 수정 항목 4개를 한 번에 정리한 안정화 버전이다.

1. finite Custom session의 delayed-task 간격 붕괴
2. Level = All의 중복 의미 주제
3. 선택 가능한 단어 수보다 큰 20/30/50 선택 문제
4. Review-only 빈 범위의 모호한 안내

## 1. Finite-session real spacing hardening

### 변경
- New intro → first meaning: 기존 `turn + 3~5`에서 `turn + 4~6`으로 조정해 현재 interaction 이후 최소 3개의 실제 interaction slot을 확보하도록 수정.
- first meaning → focused secondary: `turn + 4~6`.
- 일반 retry: `turn + 4~6`.
- Meaning 오답은 Relearn 화면을 본 뒤 pending retry의 `availableAt`을 다시 밀어, Relearn 직후 즉시 재시험되는 것을 방지.
- 현재 낼 task가 없을 때 logical turn을 바로 점프하지 않고:
  1. 아직 소개하지 않은 session target intro를 안전하게 앞당기거나,
  2. 이미 완료된 같은 session target에서 focus-compatible reinforcement bridge question을 생성.
- 정말 bridge를 만들 수 없는 극소 범위에서만 기존 future-turn fallback을 허용하고 `spacingFallbacks`에 기록.

### Scheduler simulation
실제 v2.13.5 함수들을 추출해 10-card New25 finite session을 반복 시뮬레이션했다.

- runs: 1,000
- Meaning-focused runs 중 절반은 첫 meaning answer를 의도적으로 틀리게 하여 Relearn → Retry 경로 포함
- minimum non-immediate chain gap: **3 intervening interactions**
- gaps under 3: **0**
- logical-time fallback: **0**
- bridge tasks were actually exercised, proving tail-session filler path was used

Focus-specific regression:
- Meaning: target skills = meaning only
- Listening: meaning + listening
- Reverse: meaning + reverse
- Spelling: meaning + spelling
- all four modes kept minimum gap 3 in the 10-card New25 simulation

Important limitation:
A degenerate/tiny session with too few distinct usable targets can make real spacing mathematically impossible. In that case the app retains a last-resort fallback rather than inventing out-of-scope words. Standard 10+ card Custom sessions exercised in QA did not hit this fallback.

## 2. Canonical topic grouping for Level = All

The following raw source category pairs are now shown as one semantic Custom topic when Level = All:

- `LES VERBES` + `Les verbes` → Verbes / Verbs
- `ADJECTIFS` + `L’adjectif` → Adjectifs / Adjectives
- `PRÉPOSITIONS` + `Les prépositions` → Prépositions / Prepositions
- `L’ENDROIT` + `L’endroit` → Endroits / Places
- `LA PROFESSION` + `La profession` → Professions
- `OBJETS` + `L’objet` → Objets / Objects

Underlying card `category` strings are unchanged. The canonical layer applies to Custom setup/selection only.

Combined card counts:
- Verbs: 548
- Adjectives: 160
- Prepositions: 130
- Places: 181
- Professions: 97
- Objects: 104

When a specific level is selected, that level's original raw category list remains available.

## 3. Available-count-aware session size

Custom setup now recalculates the eligible pool after:
- level
- topic
- focus
- New-word policy

Spelling mode availability is calculated **after** `simpleFrench()` filtering.
Review-only availability is calculated **after** introduced-card filtering.

Behavior:
- impossible 20/30/50 sizes are disabled
- if fewer than 10 cards are available, a dynamic exact-size option is inserted
- setup shows the current available card count
- Start is disabled when availability is zero
- availability refreshes when opening the Study page, so progress changes from other sessions are reflected

Reference checks:
- A1-A2 `LES INSTRUMENTS DE MUSIQUE`: 10 cards → 20/30/50 are not valid choices
- Spelling eligible corpus remains 2,167 / 2,866

## 4. Review-only empty state

Korean:
`이 범위에는 복습할 단어가 없습니다.`

English:
`There are no review words in this range.`

The Start button is disabled when the selected review scope has zero eligible cards.

## Combination QA
Exact v2.13.5 Custom selection functions were extracted and tested across synthetic learner states.

Dimensions:
- progress state: fresh / half-introduced / all-introduced
- level: ALL / A1-A2 / B1-B2
- every available topic including canonical ALL-level groups
- focus: mix / meaning / audio / reverse / typing
- policy: auto / new25 / review
- size: 10 / 20 / 30 / 50

Total combinations exercised: **16,020**

Assertions:
- duplicate selected IDs: 0
- level leakage: 0
- topic leakage: 0
- Spelling-ineligible cards in typing focus: 0
- New cards in Review-only: 0
- New25 minimum failures where supply allowed it: 0

Result: **PASS**

## Corpus / integrity regression
v2.13.4 → v2.13.5:

- cards: 2,866 → 2,866
- unique IDs: 2,866
- CARDS SHA-256 unchanged: `fb0cae781bb9d08273fe2f38f5318a0ab52afc3aabb6a71ee248bdc15e966a1b`
- EN_DATA entries: 2,866
- EN_DATA SHA-256 unchanged: `1d434ca6b6c9c621f3ce381ba3afed8aa1928cafac287461eaa19dd15b939373`
- JavaScript syntax (`node --check`): PASS
- backup filename updated to `tef-vocab-loop-v2_13_5-backup.json`

## Runtime QA note
A headless Chromium run was attempted, but this environment blocks browser navigation to both localhost and `file://` via administrator policy. Therefore no claim of full browser E2E automation is made. Final touch/layout behavior should still be checked on the real Android Chrome deployment target.
