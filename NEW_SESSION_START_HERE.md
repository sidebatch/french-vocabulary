# NEW SESSION — START HERE

## 현재 기준 버전

**TEF Vocab Loop v2.13.5**

새 세션에서는 `index.html` 또는 `TEF_Vocab_Loop_v2_13_5.html`을 최신 기준으로 사용한다.

현재 핵심 데이터:

- 프랑스어 학습 카드: **2,866개**
  - A1-A2: 1,465
  - B1-B2: 1,401
- 한국어 + 영어 이중 언어 UI/뜻/예문
- 두 언어 모드는 **하나의 공용 학습 진행도**를 사용
- 카드 ID는 `v0001` ~ `v2866`로 안정적으로 유지
- Data schema: **3**
- Session schema: **3**
- 앱은 단일 HTML로도 동작하며 Android direct-open 사용도 계속 지원

---

## 지금 앱의 핵심 방향

단순히 “보면 아는 단어”를 늘리는 앱이 아니라,

**Recognition → Recall → Production**

방향으로 발전시키는 프로젝트다.

현재 연결 구조:

- 단어 소개
- 뜻 인식
- 듣기
- 역방향 회상
- 철자
- 좋은 예문
- 문장 보고 따라쓰기
- 뜻만 보고 문장 전체 생성

향후 높은 가치 후보는 **부분 빈칸 회상(cloze) → 전체 생성** 사이 단계를 추가하는 것이다.

---

## 학습 상태 / 스킬 불변 규칙

상태:

- New
- Seen
- Learning
- Familiar
- Mastered
- Weak

중요:

> **Seen ≠ Learning**

새 단어 소개만 보고 나간 카드는 Seen이다. 실제 문제를 풀어야 Learning으로 넘어간다.

스킬:

- `meaning`: French → meaning
- `listening`: audio → meaning
- `reverse`: Korean/English → French
- `spelling`: typed French

`spelling`은 강화용이며 **Mastered 필수 조건이 아니다.**

오답 재시험은 즉시 반복하지 않고 일반적으로 몇 문제 뒤 다시 낸다.

---

## Today Study — v2.13.0

Today는 끝이 정해진 일일 quota가 아니라 **continuous Smart Session**이다.

Today 시작 시 사용자가 세 가지 모드를 선택한다.

1. **자동**
   - Due / Seen / Weak backlog를 보고 New 유입을 자동 조절
2. **새 단어 최소 25%**
   - 새로 선택하는 카드 중 New가 최소 약 25%가 되도록 보장
   - retry / 방금 배운 카드의 후속 확인 같은 학습 체인은 우선 처리될 수 있음
3. **복습만**
   - 아직 소개되지 않은 New 카드는 내지 않음
   - Seen / Due / Weak / 이미 학습한 카드만 사용

진행 중인 Today 세션이 있으면 기록을 유지한 채 모드를 바꿔 이어갈 수 있다.

---

## Custom Study — v2.13.0

Custom은 사용자가 선택한:

- level
- category
- word count
- focus mode
- new-word mix

으로 만드는 **finite session**이다.

집중 방식:

- 자동 혼합
- 뜻
- 듣기
- 역방향
- 철자

새 단어 구성:

- 자동
- 새 단어 최소 25%
- 복습만

예: 20개 + 새 단어 최소 25%라면 New가 충분할 경우 최소 5개를 New로 구성한다.

Today / Custom은 세션은 다르지만 **같은 global learner record**를 사용한다.

---

## 새 단어 / 뜻 재학습 흐름

새 단어가 실제로 선택되면:

1. 먼저 French + 뜻 + 발음 소개
2. 몇 문제 뒤 `meaning` 문제
3. 맞으면 secondary skill로 진행

v2.13.0 추가 규칙:

- 뜻 고르기에서 오답 또는 `모르겠어요`
- → **뜻 다시 익히기** 화면
- → French + 뜻 + 발음 재확인
- → 몇 문제 뒤 meaning 문제 재시험

듣기/역방향 오답까지 매번 introduction으로 되돌리지는 않는다.

---

## 문장 타이핑 시스템

문장 탭은 라이브러리/연습 진입 허브이고, 실제 연습은 별도 학습 화면에서 진행한다.

두 모드:

### 1. 보고 따라쓰기

- French 예문 표시
- 한국어/영어 번역 표시
- 문장을 보면서 그대로 입력
- 문장별 완료 횟수를 별도 저장

### 2. 뜻 보고 쓰기

- 번역만 표시
- French 전체 문장을 직접 입력
- 첫 시도 정답 / 수정 후 정답 / 정답 보기 통계를 구분
- **졸업 카운트는 정답 공개 전 첫 시도 정답일 때만 증가**

공통:

- 문장별 / 모드별 카운트는 완전히 독립
- 각 모드 **15회 = 졸업**
- 졸업 문장은 모드별 🎓 라이브러리에 저장
- 한 모드에서 졸업해도 다른 모드에는 영향 없음
- 첫 글자 대/소문자와 마지막 `. ! ?`는 정답 판정에서 무시
- 악센트, 철자, 관사, 전치사, 동사 활용 등은 그대로 검사
- 틀린 부분은 빨간색으로 비교 표시
- 문장 연습 세션은 단어 학습 세션과 별도로 저장/이어하기 가능

---

## 예문 품질 프로젝트 현재 상태

예문은 단순히 target word를 포함하는 게 아니라 가능하면 다음 중 하나 이상을 가르쳐야 한다.

- 실제 생활 상황
- 동사 + 전치사 구조
- 자연스러운 collocation
- 명사와 자주 결합하는 동사
- 재사용 가능한 B1-B2 표현
- TEF speaking/writing에 활용 가능한 구조
- 단어의 대표 의미가 드러나는 문맥

주요 작업 기록:

- v2.9.0: 286개 수정
- v2.9.1: 167개 수정
- v2.9.2: 159개 수정
- v2.9.3: 144개 고확신 반복 템플릿 수정
- v2.11.4: 45개 추가 정밀 수정
- v2.12.0: **2,866개 전체 audit 후 583개 수정**

주의: 위 숫자는 버전별 변경 건수이며, 같은 카드가 후속 audit에서 다시 개선될 수 있으므로 단순 합계를 “고유 카드 누계”라고 부르지 않는다.

v2.12.0에서는 특히 target-word sense mismatch도 수정했다.
예: `arrêter`, `vers`, `responsable`, `tendre`.

현재부터는 대규모 템플릿 청소보다 **실제 사용 중 발견되는 개별 예문 QA** 비중이 높다.

---

## Word / Sentence 탭

하단 탭:

**오늘 · 학습 · 단어 · 문장 · 설정**

Word detail:

- level / category / status
- French + meaning
- word TTS
- example + translation
- example TTS
- 4 skill bars
- current stage
- next review
- last study
- correct/wrong
- ★ / hard

Sentence:

- Recommended / All
- search
- level/category filter
- normal/slow TTS
- linked word detail
- 문장 타이핑 연습 진입
- 모드별 졸업 라이브러리

추천 예문은 “괜찮은 예문 전체”가 아니라 **문장 자체를 따로 외울 가치가 높은 문장**을 의미한다.

---

## 모바일 / 뒤로가기 관련

- 단어 상세 bottom sheet: Android 뒤로가기 → 상세창 닫기
- 문장 타이핑 화면: 뒤로가기 → 문장 탭 복귀
- 일반 화면: accidental exit 방지를 위한 종료 확인 흐름 존재
- 단, `file://` / `content://` HTML Viewer나 일부 Chrome local-file 환경에서는 Android host가 back event를 먼저 가져가 페이지를 바로 닫을 수 있음
- 이 한계는 추후 GitHub Pages + PWA 또는 Android WebView/native wrapper에서 더 안정적으로 해결 가능

문장 입력 모바일 QA에서 가로 overflow 및 keyboard/확인 버튼 겹침 문제는 v2.11.3에서 수정했다.

---

## TTS 불변 규칙

화면 표시 문자열과 읽는 문자열은 분리한다.

예:

- display: `l'expression (f.)`
- speech: `l'expression`

`+ inf`, `+ sub`, `+ cond`, `qn`, `qc` 같은 문법 메타데이터는 읽지 않는다.
실제 lexical variant는 무작정 제거하지 않는다.

---

## 아직 남은 높은 가치 과제

우선순위 후보:

1. **Partial cloze / hint reduction**
   - 보고 따라쓰기와 뜻 보고 전체 쓰기 사이 단계
2. **Multi-skill Weak**
   - 현재 한 카드에서 동시에 여러 약점 스킬을 충분히 표현하지 못함
3. **Mastered evidence 강화**
   - 스킬별 spaced evidence 개선
4. **Weak / Hard / ★ 의미 분리**
5. **Reverse ambiguity guard**
   - 특히 English mode에서 같은 의미가 여러 French 답을 허용하는 경우
6. **Distractor 품질 개선**
7. **Word library 상태 필터 / sorting / accent-insensitive search**
8. 문장 추천 heuristic/curation 정밀화
9. backup/import robustness + explicit migrations
10. 이후 PWA / WebView / login / cloud sync 검토

---

## 파일 구조

GitHub 저장소 권장 구조:

- `index.html` — GitHub Pages 최신 앱
- `TEF_Vocab_Loop_v2_13_5.html` — 현재 스냅샷
- `NEW_SESSION_START_HERE.md`
- `NEXT_SESSION.md`
- `docs/PROJECT_HANDOFF.md`
- `docs/TEF_Vocab_Project_History.md`
- `docs/CHANGELOG.md`
- `docs/QA_NOTES.md`
- `docs/ROADMAP_NEXT.md`
- `docs/reports/V2_13_0_QA_REPORT.md`
- `docs/example-audits/V2_12_0_EXAMPLE_AUDIT.md`
- `archive/` — 이전 HTML 버전

---

## GitHub Pages 업데이트 시

같은 GitHub Pages origin의 `index.html`을 교체하는 경우 기존 브라우저 학습 기록은 일반적으로 그대로 유지된다.
그래도 큰 업데이트 전에는 JSON backup을 권장한다.

로컬 HTML (`file://` 또는 `content://`)과 GitHub Pages (`https://...github.io`)는 다른 origin이므로 저장소가 자동 이동하지 않는다.

안전한 순서:

1. 기존 앱 JSON backup export
2. 기존 HTML 보관
3. GitHub의 `index.html` 교체
4. Pages 배포 후 카드 수 / streak / 최근 학습 상태 확인
5. 필요하면 JSON import

---

## 새 세션에서 읽을 순서

1. `NEW_SESSION_START_HERE.md`
2. `docs/PROJECT_HANDOFF.md`
3. `docs/TEF_Vocab_Project_History.md`
4. `docs/CHANGELOG.md`
5. `docs/QA_NOTES.md`
6. `docs/ROADMAP_NEXT.md`
7. 최신 QA / example audit
8. `index.html`

새 세션에서는 **v2.13.5를 기준으로 기존 product decisions를 보존**한다.


---

## v2.13.1–v2.13.4 recent updates

### v2.13.1 — meaning / distractor QA
- Corrected 29 high-confidence meaning or grammar-notation issues found during real study.
- Added ambiguity guards so meaning/listening/reverse multiple-choice distractors do not present multiple defensible answers.
- Card IDs and examples remained stable.

### v2.13.2 — intentional reload
- Fixed Chrome's native `Reload site?` warning during app-owned reloads.
- Internal reloads bypass `beforeunload` only after state is saved.
- Genuine browser exit/reload protection remains.

### v2.13.3 — calendar daily detail
Studied dates became clickable and `dailyStats` was added.

From v2.13.3 onward, per-day detail can include:
- word questions
- new words
- correct / wrong
- accuracy
- sentence Copy
- sentence Recall

Older studied dates remain visible, but exact historical counts are not fabricated because older builds did not store them.

### v2.13.4 — Custom focus semantics
Custom focus now behaves as an actual focus contract:

- Meaning: introduction → meaning → delayed meaning confirmation
- Listening: introduction → meaning foundation → listening
- Reverse: introduction → meaning foundation → reverse
- Spelling: introduction → meaning foundation → spelling
- Auto mix: existing adaptive behavior

A Meaning-focused session advances meaning evidence only. It does not pretend Listening/Reverse were learned.

Spelling focus filters candidates through the existing simple-form eligibility rule instead of silently falling back to another skill.

## Highest-priority open QA
1. finite Custom session delayed tasks can lose real intervening-question spacing when no current task is available;
2. equivalent A1/B1 topic names should be canonicalized under Level = All;
3. requested size can exceed the available candidate pool in narrow scopes;
4. Review-only empty-state wording is still generic.

See:
- `docs/reports/V2_13_3_CUSTOM_STUDY_QA.md`
- `docs/reports/V2_13_4_QA_REPORT.md`


---

## v2.13.5 — Custom Study hardening

v2.13.4의 남은 Custom Study 우선 수정 4개를 안정화했다.

1. **실제 delayed spacing**
   - finite session이 낼 문제가 없다고 logical turn만 점프하는 것을 줄였다.
   - 가능한 경우 아직 소개하지 않은 session target을 먼저 소개하거나, 완료된 같은 session target에서 focus-compatible bridge 문제를 사용한다.
   - standard 10+ card QA에서는 최소 3개의 intervening interaction을 유지했다.

2. **Level = All canonical topics**
   - Verbs / Adjectives / Prepositions / Places / Professions / Objects 등 레벨별 raw category가 달랐던 동일 의미 주제를 Custom UI에서 하나로 묶었다.
   - underlying card category는 변경하지 않았다.

3. **available-count-aware size**
   - level/topic/focus/new-policy를 모두 적용한 후 사용 가능 카드 수를 계산한다.
   - 불가능한 20/30/50은 비활성화한다.
   - 10개 미만이면 정확한 동적 개수 옵션을 제공한다.

4. **Review-only empty state**
   - 복습 가능한 카드가 0개면 `이 범위에는 복습할 단어가 없습니다.`를 표시하고 시작을 비활성화한다.

QA:
- scheduler 1,000 runs
- Custom matrix 16,020 combinations
- 2,866 card IDs unchanged
- corpus unchanged
- JS syntax PASS

Important limitation:
아주 작은/퇴화된 범위에서는 실제 간격을 만들 카드 자체가 부족할 수 있다. 이 경우 범위 밖 단어를 억지로 가져오지 않고 last-resort fallback을 유지한다.

### 다음 세션
새 기능을 바로 추가하지 말고 먼저 실제 Android Chrome에서 짧게 회귀 확인한다.
그 후 가장 높은 가치 후보는 sentence partial cloze / progressive hint reduction이다.
