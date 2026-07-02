# Claude Functional Brief — HairFit MVP

작성일: 2026-07-02

## 역할
너는 HairFit MVP의 기능 품질 개선 담당이다. Codex가 제품 방향과 최종 검수의 head 역할을 맡고, Claude는 코드 구현/점검/테스트를 보조한다.

HairFit은 단순 헤어스타일 놀이 앱이 아니라 **미용사용 상담 보조 앱**이다. 핵심 차별점은 다음 3개다.

1. 손님 얼굴 인상 유지
2. 자연스러운 헤어 합성/미리보기
3. 얼굴 분석 기반의 짧고 설득력 있는 상담 근거

이번 작업은 디자인 대개편이 아니라 **기능적 타당성**에 집중한다.

## 위치
- 코드 repo: `C:\Users\vacma\Desktop\apps\hairfit-mvp`
- 운영 문서: `C:\Users\vacma\vacax\active\hairfit`
- 현재 코드 브랜치: `codex/design-pass-2`

## 절대 금지
- `.env.local`, `server/.env`, API 키, 토큰 내용 읽기/출력/커밋 금지.
- 실제 이미지 생성 호출 금지. `hairfit:real`, `gpt-once`, `gpt-three`, `flux-*` 실행 금지.
- 얼굴 사진/개인 사진을 repo에 복사하거나 커밋 금지. 테스트용 임시 복사본을 만들면 작업 후 반드시 삭제.
- 랜덤 인터넷 얼굴 사진으로 실제 API 테스트 금지.
- 앱 방향을 "일반 소비자 헤어 놀이"로 바꾸지 말 것.
- 디자인 전면 개편, 랜딩 페이지화, 포트폴리오 패키징 작업 금지.

## 먼저 읽을 파일
운영 문서:
- `C:\Users\vacma\vacax\active\hairfit\STATE.md`
- `C:\Users\vacma\vacax\active\hairfit\EVALS.md`
- `C:\Users\vacma\vacax\active\hairfit\LEARNINGS.md`
- `C:\Users\vacma\vacax\active\hairfit\NEXT.md`

코드:
- `src/lib/types.ts`
- `src/lib/analysis/analyzeFace.ts`
- `src/lib/analysis/faceMeasurements.ts`
- `src/lib/analysis/photoQuality.ts`
- `src/lib/analysis/photoReadiness.ts`
- `src/lib/recommendation/recommendStyles.ts`
- `src/lib/styleLibrary/styleLibrary.ts`
- `src/screens/CaptureScreen.tsx`
- `src/screens/ResultsScreen.tsx`
- `src/screens/ReasonModal.tsx`
- `src/state/AppContext.tsx`

## 현재 확인된 사실
- 남성 스타일 라이브러리 9종 ready.
- 추천 엔진은 스타일 라이브러리 기반 스코어링으로 바뀌었음.
- 얼굴형 경계 흔들림 완화를 위해 인접 얼굴형 점수와 안정 타이브레이크가 들어가 있음.
- 사진 등록 단계에 MediaPipe 기반 각도 게이트가 있음.
- CEO 제공 3장 테스트 결과:
  - 정면 1장: `ready`, measured, 추천 안정.
  - 틀어진 2장: `blocked`, 강제 분석 시 mock fallback과 추천 변화 발생.
- 실제 생성 품질은 synthetic 기준 상담용 통과이나, 완전 동일인 보존 주장은 금지.

## 작업 목표
다음 항목을 순서대로 점검하고, 명백히 개선 가능한 것은 직접 구현한다.

### 1. 얼굴 분석값 → 추천 로직 타당성 점검
목표: 같은 얼굴/비슷한 입력에서 추천이 과하게 흔들리지 않고, 미용사가 납득할 만한 스타일이 나오게 한다.

점검할 것:
- `scoreStyle()`의 가중치가 지나치게 특정 항목에 쏠리지 않는지.
- `faceShape`, `foreheadExposure`, `midface`, `jaw`, `cheekbone`, `eyeSpacing`이 실제 추천에 의미 있게 반영되는지.
- `maintenance`, `density`, `hairType`, `vibe`, `currentLength`가 추천을 덮어쓰거나 무시되지 않는지.
- `hairDesign.confidence`가 `mock` 또는 `estimated`일 때 추천을 더 보수적으로 안정화할 필요가 있는지.
- blocked 사진은 추천 단계까지 가지 않는 것이 맞는지, 혹시 fallback 추천이 화면에 노출되는 경로가 없는지.

가능한 개선:
- 점수 계산을 작게 분리해 `scoreBreakdown` 또는 내부 디버그 가능한 구조로 정리.
- 얼굴형보다 `hairDesign`의 앞머리/가르마/볼륨 설계값을 추천 점수에 더 직접 반영.
- 신뢰도 낮은 분석에서는 안정 스타일 bias를 더 강하게 주거나, 결과 문구를 `상담용 추정`으로 낮춤.

주의:
- 추천 다양성을 위해 억지로 랜덤을 넣지 말 것.
- 같은 입력이면 결과는 deterministic 해야 한다.
- LLM 호출 기반 추천으로 바꾸지 말 것. 지금은 로컬/규칙 기반 우선.

### 2. 상담 문구/근거 문구 타당성 개선
목표: 결과 카드의 문장이 실제 얼굴 분석값과 스타일 특징에 맞게 짧고 설득력 있게 나오게 한다.

점검할 것:
- `buildStyleOneLine`
- `buildStyleFitReason`
- `buildStyleCustomerScript`
- `buildReferenceFitCopy`
- `ResultsScreen.tsx`의 `faceBasisPoints`, `faceMetricCards`, `FitBasisStrip`
- `ReasonModal.tsx`

문구 원칙:
- 손님 단점을 직접 지적하지 말 것.
- “연구결과상” 같은 과장 표현 금지. 현재 분석은 MediaPipe proxy + 상담용 추정이다.
- “미간/중안부/이마/윤곽” 같은 근거는 실제 `FaceAnalysis` 값과 연결될 때만 사용.
- 3개 카드가 같은 말을 반복하면 설득력이 떨어진다. 스타일별 차이를 반영할 것.
- 미용사가 손님에게 바로 말할 수 있는 짧은 문장이어야 한다.

좋은 방향:
- “중안부가 길게 잡혀서 윗볼륨을 과하게 세우기보다 앞머리 흐름으로 시선을 한 번 끊는 쪽입니다.”
- “이마 노출이 낮게 잡혀서 무거운 풀뱅보다 결을 갈라 답답함을 줄이는 안입니다.”
- “옆볼륨은 넓히기보다 정리해서 정면 폭이 커 보이지 않게 잡는 쪽입니다.”

나쁜 방향:
- “못생겨 보이는 부분을 보완”
- “황금비라서 무조건”
- “콧볼 때문에 앞머리”
- 분석값과 무관한 뷰티 일반론

### 3. 사진 각도 게이트 UX/기능 점검
목표: 미용사가 현장에서 사진을 다시 찍어야 하는 이유를 즉시 이해하게 한다.

점검할 것:
- `CaptureScreen.tsx`의 `PhotoReadinessCard`
- `photoReadiness.ts`
- `photoQuality.ts`

개선 후보:
- `blocked`일 때 “왜 재촬영인지”가 더 직관적으로 보이게 문구 개선.
- `ready/warning/blocked/unavailable`의 버튼 문구가 현장 흐름에 맞는지 확인.
- `warning`은 진행 가능해야 하지만, 결과 화면에도 `상담용 추정` 느낌이 남는지 확인.
- MediaPipe 로드 실패/느림에서 UX가 멈추지 않는지 확인.

검증:
- 정면 사진: `ready`
- 약한 흔들림: 가능하면 `warning`
- 큰 회전/측면: `blocked`
- 모델 로드 실패: `unavailable`, 진행 가능하되 추정 문구 노출

### 4. 회귀 테스트/검증 도구 보강
목표: 추천 로직이 고쳐질 때마다 같은 얼굴에서 추천이 튀는지 빨리 확인하게 한다.

가능한 구현:
- 실제 얼굴 사진 없이 `FaceAnalysis` fixture 기반 추천 테스트 스크립트 추가.
- 예: `scripts/check-recommendation-fixtures.mjs` 또는 TS 빌드에 맞는 가벼운 검증 스크립트.
- 테스트해야 할 fixture:
  - long + high forehead
  - round + wide cheekbone
  - heart + low forehead
  - square + strong jaw
  - estimated/mock confidence
- 출력은 각 fixture별 추천 3종과 주요 근거.

주의:
- 새 테스트 프레임워크 설치는 가급적 피함.
- 기존 `npm.cmd run typecheck`, `npm.cmd run build`, `npm.cmd run hairfit:check-assets`는 반드시 통과.
- 스크립트 추가 시 `package.json` script도 함께 추가 가능.

### 5. 레퍼런스 이식 흐름 기능 점검
목표: 미용사가 직접 고른 레퍼런스를 보여주는 흐름이 자동 추천과 헷갈리지 않게 한다.

점검할 것:
- `ReferenceUploadScreen.tsx`
- `recommendFromReference`
- `transferReferenceHair`
- `referenceHairPolicy`

확인 포인트:
- 자동 추천이 아닌 “미용사 선택 레퍼런스 적용”임이 명확한지.
- 권한/출처 확인 없이는 진행되지 않는지.
- 레퍼런스 결과의 근거 문구가 자동 추천처럼 과잉 분석하는 척하지 않는지.
- 실제 생성 버튼/비용 가드가 안전한지.

## 산출물
작업 후 다음을 남겨라.

1. 변경 요약
2. 수정 파일 목록
3. 실행한 검증 명령과 결과
4. 추천 로직/문구에서 발견한 리스크
5. 다음에 CEO가 직접 봐야 할 화면/질문

## 필수 검증
최소:
```powershell
npm.cmd run typecheck
npm.cmd run build
npm.cmd run hairfit:check-assets
```

가능하면 브라우저 mock 흐름도 확인:
홈 -> 동의 -> 사진/샘플 -> 성향 -> 모드 -> 결과

실제 이미지 생성 호출은 하지 않는다.

## 커밋 정책
- 작업 단위가 명확하면 코드 repo에서 커밋 가능.
- 커밋 전 `git status`, `git diff --cached --name-only` 확인.
- 얼굴 사진, `.env`, run_logs, 임시 테스트 이미지가 staged 되면 즉시 제거.
- 커밋 메시지는 기능 기준으로 짧게.

예:
- `fix: align recommendation reasons with face analysis`
- `feat: add recommendation fixture check`
- `fix: clarify photo angle gate copy`

## 최종 판단 기준
통과:
- 같은 입력이면 추천이 deterministic.
- 얼굴 분석값과 추천/문구가 서로 연결됨.
- 미용사가 손님에게 읽어줄 수 있는 짧은 문장.
- 각도/품질이 나쁜 사진은 추천이 튀기 전에 막거나 낮은 신뢰도로 표시.
- 비용 발생 없음.

실패:
- 랜덤 추천.
- 분석값과 무관한 그럴듯한 문구.
- “황금비/연구결과” 같은 과장.
- 사진 각도 불량인데 정상 분석처럼 보임.
- 실제 생성 API 호출.
