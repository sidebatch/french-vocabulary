# TEF Vocab Loop

개인용 **TEF Canada 프랑스어 어휘 학습 앱**입니다.

현재 기준 버전: **v2.13.0**

앱은 single-file HTML 구조이며, `index.html` 하나만으로 실행됩니다.

## 주요 기능

- A1–B2 프랑스어 단어 2,866개
- 한국어 / 영어 학습 모드
- 뜻 / 듣기 / 역방향 / 철자 학습
- New / Seen / Learning / Familiar / Mastered / Weak 상태 추적
- 간격 반복 복습
- 오늘 학습 Smart Session
- 오늘 학습 모드
  - 자동
  - 새 단어 최소 25%
  - 복습만
- 맞춤 학습
  - 레벨
  - 주제
  - 단어 수
  - 집중 방식
  - 새 단어 구성
- 뜻 문제 오답 시 `뜻 다시 익히기` 단계
- 단어 상세 학습 기록
- 문장 라이브러리
- 문장 따라쓰기 / 뜻 보고 쓰기
- 문장별 15회 졸업 시스템
- 프랑스어 단어 / 예문 TTS
- 학습 캘린더
- JSON 학습 기록 백업 / 복원

## 현재 버전에서 중요한 변경

### v2.13.0

- 오늘 학습에서 학습 구성을 직접 선택할 수 있도록 변경
  - 자동
  - 새 단어 최소 25%
  - 복습만
- 맞춤 학습에도 새 단어 구성 옵션 추가
- 뜻 문제를 틀리거나 `모르겠어요`를 선택하면
  `뜻 다시 익히기 → 일정 간격 후 뜻 재시험` 흐름 추가

### v2.12.0

- 전체 2,866개 예문 품질 감사
- 학습 가치가 낮거나 의미가 어긋난 예문 583개 수정
- 프랑스어 / 한국어 / 영어 예문 동기화
- 카드 ID와 학습 진행 구조 유지

## 파일 구조

```text
index.html
TEF_Vocab_Loop_v2_13_0.html
NEW_SESSION_START_HERE.md
NEXT_SESSION.md
README.md
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

- `index.html` — GitHub Pages에서 실행되는 최신 앱
- `TEF_Vocab_Loop_v2_13_0.html` — 현재 버전 스냅샷
- `NEW_SESSION_START_HERE.md` — 새 개발 세션 시작용 요약
- `NEXT_SESSION.md` — 다음 작업 시작점
- `docs/PROJECT_HANDOFF.md` — 프로젝트 핵심 규칙과 현재 구조
- `docs/TEF_Vocab_Project_History.md` — 전체 개발 이력과 결정 배경
- `docs/CHANGELOG.md` — 버전별 변경사항
- `docs/QA_NOTES.md` — QA 기록
- `docs/ROADMAP_NEXT.md` — 앞으로의 개발 방향

## 중요한 프로젝트 원칙

- 카드 수는 **2,866개**를 유지
- 카드 ID는 임의로 변경하지 않음
- `Seen`은 `Learning`과 다름
- 새 단어는 소개 전에 문제로 출제하지 않음
- 오답은 즉시 반복하지 않고 몇 문제 뒤 다시 출제
- 철자는 강화 학습이며 Mastered의 필수 조건이 아님
- 오늘 학습은 고정 일일 quota가 없는 continuous Smart Session
- 맞춤 학습과 오늘 학습은 하나의 글로벌 학습 기록을 공유
- 예문을 수정할 때는 프랑스어 / 한국어 / 영어를 함께 맞춤
- 이미 좋은 예문은 불필요하게 다시 수정하지 않음

## 학습 데이터

학습 진행도는 브라우저 저장소에 저장됩니다.

HTML 파일을 업데이트해도 같은 GitHub Pages 주소를 계속 사용하는 경우
기존 진행 기록은 일반적으로 유지됩니다.

다만 다른 origin으로 이동하거나 로컬 HTML(`file://`)과 GitHub Pages(`https://`) 사이를 이동하면
진행도가 자동으로 이어지지 않을 수 있으므로 JSON 백업을 권장합니다.

## 개발 방향

현재 핵심 방향은 단순한 단어 암기보다:

**단어 → 표현 → 문장 → 직접 생성**

으로 발전시키는 것입니다.

다음 주요 후보:

- 문장 부분 빈칸 학습
- 힌트 감소 방식
- 빈칸 → 전체 문장 생성
- Multi-skill Weak 개선
- Mastered 판정 근거 강화
- 역방향 문제 의미 중복 방지
- 오답 보기 품질 개선

---

Current baseline: **TEF Vocab Loop v2.13.0**
