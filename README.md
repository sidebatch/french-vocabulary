# TEF Vocab Loop

개인용 **TEF Canada 프랑스어 어휘 학습 앱**입니다.

현재 기준 버전: **v2.13.5**

앱은 single-file HTML 구조이며, GitHub Pages에서는 `index.html`이 최신 실행 파일입니다.

## 주요 기능

- A1–B2 프랑스어 단어 **2,866개**
- 한국어 / 영어 학습 모드
- 뜻 / 듣기 / 역방향 / 철자 스킬 추적
- New / Seen / Learning / Familiar / Mastered / Weak 상태
- 간격 반복 복습과 delayed retry
- Today Smart Session
  - 자동
  - 새 단어 최소 25%
  - 복습만
- 맞춤 학습
  - 레벨
  - 주제
  - 단어 수
  - 집중 방식
  - 새 단어 구성
- 뜻 오답 시 `뜻 다시 익히기 → delayed retest`
- 단어 라이브러리 + 상세 학습 기록
- 문장 라이브러리
- 보고 따라쓰기 / 뜻 보고 쓰기
- 문장별·모드별 15회 졸업
- 프랑스어 단어 / 예문 TTS
- 학습 캘린더 + 날짜별 상세 학습량 기록
- JSON 학습 기록 백업 / 복원

## v2.13.x 주요 변경

### v2.13.5
- 맞춤 학습의 `집중 방식` 의미를 실제 출제와 일치시킴.
- 뜻: 소개 → 뜻 → delayed 뜻 재확인.
- 듣기: 소개 → 기본 뜻 확인 → 듣기.
- 역방향: 소개 → 기본 뜻 확인 → 역방향.
- 철자: 소개 → 기본 뜻 확인 → 철자.
- 자동 혼합은 기존 adaptive secondary 로직 유지.
- 철자 집중에서는 철자 가능한 카드만 후보로 사용.

### v2.13.3
- 학습 캘린더의 학습한 날짜를 눌러 상세 기록을 볼 수 있도록 추가.
- v2.13.3 이후 날짜별로 단어 문제 수, 새 단어 수, 정답률, 문장 연습량 등을 저장.
- 기존 날짜는 과거 버전에 상세 통계가 없었기 때문에 학습 여부만 보존.

### v2.13.2
- 앱 내부의 의도적인 `location.reload()`가 `beforeunload` 보호와 충돌해 Chrome의 `Reload site?` 경고가 뜨던 문제 수정.
- 실제 브라우저 이탈 보호는 유지.

### v2.13.1
- 뜻/문법 표기 29개 고확신 수정.
- 객관식 distractor ambiguity guard 강화.
- `la brosse à dents`, `au lieu de + inf` 등 실제 학습 중 발견된 문제 수정.

### v2.13.0
- Today와 Custom에 Auto / 새 단어 최소 25% / 복습만 추가.
- 뜻 문제 오답·모르겠어요에 Relearn Meaning 단계 추가.

## 파일 구조

```text
index.html
TEF_Vocab_Loop_v2_13_5.html
README.md
GITHUB_UPDATE_README.md
NEW_SESSION_START_HERE.md
NEXT_SESSION.md
PROJECT_STATUS.md
archive/
docs/
  PROJECT_HANDOFF.md
  TEF_Vocab_Project_History.md
  CHANGELOG.md
  QA_NOTES.md
  ROADMAP_NEXT.md
  reports/
  example-audits/
```

## 중요한 프로젝트 원칙

- 카드 수는 **2,866개**를 유지한다.
- 카드 ID는 임의로 바꾸지 않는다.
- `Seen`은 `Learning`이 아니다.
- 새 단어는 소개 전에 문제로 출제하지 않는다.
- 오답은 즉시 반복하지 않고 delayed retry를 사용한다.
- 뜻/듣기/역방향/철자는 각각 독립된 증거다.
- 철자는 강화 학습이며 Mastered의 필수 조건이 아니다.
- Today와 Custom은 서로 다른 세션이지만 하나의 global learner record를 공유한다.
- 예문 수정 시 French / Korean / English를 함께 동기화한다.
- 이미 좋은 예문은 불필요하게 다시 수정하지 않는다.

## 집중 방식 규칙 — v2.13.5

맞춤 학습에서 `집중 방식`은 실제 문제 유형을 의미합니다.

- `뜻`: New/Seen도 secondary를 자동 Listening/Reverse로 보내지 않고 뜻을 다시 확인
- `듣기`: 뜻 기반을 먼저 만든 후 Listening으로 진행
- `역방향`: 뜻 기반을 먼저 만든 후 Reverse로 진행
- `철자`: 뜻 기반을 먼저 만든 후 Spelling으로 진행하며, 철자 불가 카드는 세션 후보에서 제외
- `자동 혼합`: 기존 adaptive algorithm 유지

뜻을 여러 번 맞혀도 듣기/역방향 스킬까지 학습한 것으로 간주하지 않습니다.

## 학습 캘린더

`studyDays`는 학습 날짜 자체를 보존합니다.

v2.13.3부터는 별도 `dailyStats`에 날짜별 상세 통계를 함께 저장합니다.

기존 과거 날짜는 이전 버전에서 상세량을 기록하지 않았으므로 정확한 문제 수/정답률을 소급 복원하지 않습니다.

## 저장 / 배포

학습 진행도는 브라우저 저장소에 저장됩니다.

같은 GitHub Pages origin에서 `index.html`만 업데이트하면 기존 학습 진행도는 일반적으로 유지됩니다.

`file://` 로컬 HTML과 `https://` GitHub Pages는 서로 다른 저장 공간이므로, 환경을 옮길 때는 JSON 백업/복원을 권장합니다.

일반 Android HTML Viewer는 JavaScript/history/touch 이벤트 지원이 불완전할 수 있습니다. 현재 실제 배포 기준은 **GitHub Pages + Chrome**입니다.

## 현재 다음 우선 QA

v2.13.5에서 기존 Custom Study 우선 수정 4개를 정리했습니다.

다음은 새 기능보다 먼저 실제 Android Chrome에서:
1. Meaning / Listening / Reverse / Spelling Custom 세션의 체감 간격 확인
2. narrow topic에서 사용 가능 개수/disabled size 확인
3. Review-only 빈 범위 안내 확인
4. 기존 진행도와 resume 회귀 확인

그 다음 높은 학습가치 후보는 문장 partial cloze / progressive hint reduction입니다.

---

Current baseline: **TEF Vocab Loop v2.13.5**
