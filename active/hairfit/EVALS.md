# HairFit MVP EVALS

## 2026-07-02 기능 패스 Codex 검수
- Finding: Claude 패스 보고의 "출처 선택 + 권한 체크 전 진행 차단"과 달리, 업로드 레퍼런스가 `sourceType: unknown` 상태에서도 권한 체크만 하면 진행 가능했다.
- Fix: `canUseReference`가 `hasImage && sourceType !== "unknown" && permissionChecked`를 요구하도록 수정하고, ReferenceUploadScreen에 sourceType 전달.
- Verification: `npm.cmd run typecheck`, `npm.cmd run build`, `npm.cmd run hairfit:check-assets`, `npm.cmd run hairfit:check-recs` 통과.
- Commit: `9b5a1ac fix: require reference source selection` pushed to `codex/design-pass-2`.
- Pending: 실제 파일 업로드 화면에서 출처 선택 + 권한 체크박스 버튼 활성화 수동 검수 1회.

## 2026-07-02 기능 타당성 패스 (Claude)
- Scope: 추천 로직·상담 문구·사진 게이트·회귀 도구·레퍼런스 가드 (CLAUDE_FUNCTIONAL_BRIEF_2026-07-02).
- Change: scoreStyle → scoreStyleBreakdown 항목 분해. hairDesign(앞머리/윗볼륨/옆볼륨) 설계값을 추천 점수에 직접 반영 — 근거 문구와 추천이 같은 설계 엔진 출처.
- Change: 분석 신뢰도 낮을수록(mock ×4, estimated ×2) 안정 스타일 bias 강화.
- Change: 손님 설명 문장을 기장별 상담 포인트로 차별화. 3카드 중간 문장 동일 반복 제거 (브라우저에서 3종 상이 확인).
- Change: 사진 게이트 fail 원인(multi_face/face_small/yaw/tilt) 분리 + 원인별 재촬영 행동 안내 1줄. warning 버튼 문구 [일부 추정으로 진행].
- Change: 결과 화면에 mock/estimated 신뢰도 안내 문구 노출 (사진 있는데 실측 실패한 경우).
- Guard fix: 레퍼런스 이식이 real proxy 설정 시 분석 단계에서 confirm 없이 자동 유료 호출되던 경로 제거 — 미리보기 우선 + 카드별 [레퍼런스 실제 합성] confirm 버튼.
- Guard fix: 업로드 레퍼런스는 출처 선택 + 사용 권한 체크 전 진행 차단. 라이브러리 스타일은 자동 통과.
- New tool: `npm.cmd run hairfit:check-recs` — FaceAnalysis fixture 7종 회귀 체크 (deterministic/기장 3종/금지 표현/문구 중복/mock 안정화). PASS.
- Verification: typecheck 통과, build 통과, check-assets 9/9 ready, check-recs PASS.
- Browser mock flow: 홈 → 동의 → 샘플 → 성향 → 자동 추천 → 결과 → 근거 모달 → 선택 → 저장 → 상세 통과. 레퍼런스 모드 라이브러리 선택 → 결과 → mock 미리보기 통과. console error/warn 0.
- Real generation: 실제 유료 호출 0회.
- Commits: e965631, b3e6a32, 4ab7d1d, c601426 (branch codex/design-pass-2).
- 미검증: 파일 업로드 경로(자동화 주입 불가 — 수동 필요), 업로드 레퍼런스 출처 UI 실화면, blocked/warning 실사진 게이트.

## 2026-07-01
- Build: `npm.cmd run build` 통과.
- Mock flow: 홈 -> 동의 -> 사진 -> 성향 -> 모드 -> 결과 확인.
- Home: 사진 / 3컷 / 상담 흐름 노출 확인.
- Mode: 선택 카드가 실제 button으로 잡히는 것 확인.
- Results: "손님에게 이렇게", "얼굴 분석 근거"가 바로 보이는 것 확인.
- Real generation: 실제 이미지 생성 호출 0회. 품질 테스트 미진행.

## 2026-07-01 스타일 에셋 교체
- Asset check: `npm.cmd run hairfit:check-assets` 통과. 9/9 ready.

## 2026-07-01 비용 가드 UX 보강
- Change: AI 추천 3컷 자동 실제 생성 기본 OFF.
- Change: 결과 카드의 비용 발생 액션을 `이 카드 실제 생성`으로 명확화하고 confirm을 항상 거치도록 수정.
- Env: `VITE_AUTO_GENERATE_AI_THREE=1`일 때만 3컷 자동 실제 생성 허용.
- Build: `npm.cmd run build` 통과.
- Typecheck: `npm.cmd run typecheck` 통과.
- Asset check: `npm.cmd run hairfit:check-assets` 통과.
- Browser: localhost 홈/mock 배지 확인. 파일 업로드 자동화는 현재 브라우저 API 제약으로 수동 검수 필요.
- Build: `npm.cmd run build` 통과.
- Mock server: `realEnabled=False`, 실제 유료 호출 없음.
- Visual QA: display/reference contact sheet 생성.
- Note: 브라우저 캡처 도구에서 centered phone-frame screenshot 좌표 왜곡이 있어 DOM/CSS 수치와 콘솔 로그로 보조 확인. 앱 콘솔 error/warn 없음.

## 2026-07-01 기능 자가 테스트
- AI 추천 mock flow: 홈 -> 동의 -> 샘플 사진 -> 성향 -> 자동 추천 -> 결과 -> 선택 -> 저장 -> 상세 기록 통과.
- 결과 화면: `손님에게 이렇게`, `얼굴 분석 근거`, 3개 `근거 보기`, 3개 선택 버튼 확인.
- 결과 이미지: SVG placeholder 없음. `/style-library/men/{soft_ivy,see_through_dandy,leaf}/display.webp` 사용 확인.
- Reference flow: 홈 -> 동의 -> 샘플 사진 -> 레퍼런스 모드 -> 9종 스타일 라이브러리 -> 애즈펌 선택 -> 결과 -> 저장 통과.
- Reference 저장: 품질 평가 4/5 입력, 상세 기록에서 `얼굴 유지 통과`, `미리보기 · 스타일 에셋` 확인.
- Browser console: error/warn 없음.
- Build: `npm.cmd run build` 통과.
- Typecheck: `npm.cmd run typecheck` 통과.
- Asset check: `npm.cmd run hairfit:check-assets` 통과. 9/9 ready.
- Smoke checklist: `SMOKE_TEST_CHECKLIST.md` 작성 완료.
- Git/key guard: 코드 폴더는 Git repo 아님. `.gitignore`에 `.env.*`/`*.local` 포함. `.env.local` 존재, 내용 미확인.
- Real generation: 실제 유료 이미지 호출 0회.

## 2026-07-01 실제 생성 1차 테스트
- Approval: CEO가 필요 시 실제컷 생성 허용.
- Real calls: 2회. `gpt-image-2` via Replicate. 기록 비용 $0.08.
- Input: synthetic 고객 사진 1장 + 시스루 댄디컷 reference.
- v1 평가: 얼굴 유지 3.5/5, 헤어 자연스러움 4/5, 상담 사용성 4/5.
- Improvement: 얼굴 윤곽, 귀 위치, 피부 보정 금지, crop/framing 유지 프롬프트 강화.
- v2 평가: 얼굴 유지 4/5, 헤어 자연스러움 4/5, 상담 사용성 4/5.
- CEO 육안 검수: v2는 같은 사람으로 보인다고 판단.
- Output: `REAL_GENERATION_TEST_2026-07-01.md`에 경로/점수 기록.
- Guard: 테스트 후 `npm.cmd run hairfit:mock` 실행. proxy `realEnabled=false`, Vite 200 확인.
- Build: `npm.cmd run build` 통과.
- Typecheck: `npm.cmd run typecheck` 통과.
- Asset check: `npm.cmd run hairfit:check-assets` 통과. 9/9 ready.

## 2026-07-01 테스트 사진 정책
- 랜덤 인터넷 얼굴 사진은 사용하지 않음.
- 이유: 실제 호출 시 얼굴 이미지가 외부 API로 전송되므로, 내부 테스트라도 초상/라이선스/약관 리스크가 있음.
- 대안: synthetic 얼굴 5장 또는 동의/라이선스가 명확한 테스트 사진만 사용.

## 2026-07-01 synthetic 5장 실제 생성 테스트
- Input: synthetic 남성 얼굴 5장.
- Final output: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-real-comparison-2026-07-01.jpg`
- Final set: 5/5 실제 생성 성공.
- Score: 얼굴 유지 4/5 이상 4장, 상담 사용성 3/5 이상 5장.
- Pass: 기준 통과.
- CEO 육안 검수: 완전 같은 사람은 아니지만 얼추 비슷함. 상담용 MVP 기준 통과, 완벽한 동일인 보존 주장은 금지.
- Cost: 최종 세트 기준 $0.20, 개선/재시도 포함 기록 비용 $0.44.
- Improvement: GPT Image 계열 `aspect_ratio` 기본값을 `auto`로 변경. 원본/결과 크기 일치 확인.
- Improvement: `semi_leaf/reference.webp`를 얼굴 포함 레퍼런스에서 헤어 crop reference로 교체.
- Risk: 긴 기장/리프 계열은 얼굴 드리프트가 일부 남음.
- Guard: 테스트 후 proxy `realEnabled=false`, Vite 200 확인.

## 2026-07-01 얼굴 유지 표현 조정
- CEO 피드백: 완전 같은 사람은 아니지만 얼추 비슷함.
- Change: 앱/README 문구를 "완벽한 얼굴 유지"가 아니라 "상담용 얼굴 인상 유지" 기준으로 조정.
- Typecheck: `npm.cmd run typecheck` 통과.
- Build: `npm.cmd run build` 통과.

## 2026-07-01 긴 기장 reference 리스크 개선
- Risk found: `leaf`, `semi_wolf` reference에 얼굴 노출이 있어 긴 기장 합성 시 얼굴 인상 드리프트 가능성이 높았음.
- Change: `leaf/reference.webp`는 hair-only backup으로 교체, `semi_wolf/reference.webp`는 hair-dominant crop으로 교체.
- Visual QA: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\long-reference-risk-fixed-2026-07-01.jpg`
- Real smoke: synthetic sample 4 + `semi_wolf` 실제 1컷 생성.
- Output: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-real-04-semi_wolf-2026-07-01.png`
- Score: 얼굴 인상 유지 4/5, 헤어 자연스러움 4/5, 상담 사용성 4/5. 완전 동일인은 아니지만 상담용 통과.
- Cost: `gpt-image-2` via Replicate 성공 호출 1회, 기록 비용 $0.04.
- Guard: 테스트 후 `npm.cmd run hairfit:mock` 실행, proxy `realEnabled=false` 확인.

## 2026-07-01 mock 회귀 재검수
- Browser flow: 홈 -> 동의 -> 샘플 사진 -> 성향 -> 자동 추천 -> 결과 -> 선택 -> 저장 -> 상세 기록 통과.
- Home: mock 배지, 사진/3컷/상담 흐름, 최근 기록, 새 상담 시작 확인.
- Consent: 필수 동의 2개 선택 전 `사진 등록하기` disabled, 선택 후 enabled 확인.
- Photo: 촬영/불러오기 file input 노출 확인. 자동화 표면에서 파일 선택 주입은 미지원이라 실제 업로드는 수동 검수로 남김.
- Results: 3개 결과 카드, `손님에게 이렇게`, `얼굴 분석 근거`, `근거 보기`, `이걸로 선택`, `상담 메모 · 저장` 확인.
- Fix: 결과 카드 fallback 문구의 `손님 사진 없이` 표현 제거. 화면에서 `실제 합성 전 스타일 미리보기를 표시합니다.` 노출 확인.
- Save/detail: 테스트 고객명/메모 저장 후 상세 기록에서 원본 얼굴 사진 `저장 안 함`, 결과 이미지 `저장됨`, 상담 메모 `저장됨` 확인.
- Browser console: error/warn 없음.
- Verification: `npm.cmd run typecheck`, `npm.cmd run hairfit:check-assets`, `npm.cmd run build` 통과.
- Guard: proxy health `realEnabled=false`, Vite 200 확인.

## 2026-07-02 디자인 리프레시 1차
- Trigger: CEO 피드백 "디자인이 초딩이 만든 것 같음".
- Applied patterns: ❌-05 이모지/가벼운 장식 자동생성 티 회피, ✅-01 정보 위계 명확화.
- Research direction: 모바일 HIG/Material/NNG류 원칙에서 색 역할 제한, 표면/구분선 기반 위계, 사진/핵심 작업 우선, 시각적 신뢰감 강화 원칙만 반영.
- Change: 전체 design token을 업무툴 톤으로 조정. 큰 라운드/과한 그림자/세리프 로고/크림·클레이 장식/칩 과다 사용 축소.
- Change: 홈은 dark hero/floating card에서 흰 업무 대시보드형 구조로 변경.
- Change: 모드 선택은 귀여운 카드형 선택지에서 실제 작업 옵션형 패널로 변경.
- Change: 결과 화면은 크림 상담 박스/초록 박스 대신 사진 중심 카드 + 리포트형 상담 문장 + 표 형태 근거로 정리.
- Change: 동의/사진/분석중/저장/기록/상세/근거 모달까지 같은 톤으로 정리.
- Browser flow: 홈 -> 동의 -> 샘플 사진 -> 성향 -> 자동 추천 -> 결과 통과.
- Browser check: 홈 mock 배지/새 상담, 결과 3카드/상담문/얼굴 분석 근거/미리보기 문구 확인.
- Browser console: error/warn 없음.
- Verification: `npm.cmd run typecheck`, `npm.cmd run hairfit:check-assets`, `npm.cmd run build` 통과.
- Guard: proxy health `realEnabled=false`, Vite 200 확인.

## 2026-07-02 얼굴 각도 보조 게이트 3장 테스트
- Input: CEO 제공 동일 인물 사진 3장(정면, 틀어진 컷 2장). 테스트용 복사본은 public 임시 폴더에만 두고 테스트 후 삭제.
- Real generation: 실제 이미지 생성 호출 0회.
- Test path: 브라우저에서 앱과 같은 `checkPhotoReadiness -> analyzeFace -> recommendStyles` 순서 실행.
- Result 1: `ready`, yawProxy 0.883, tilt -1.84도, confidence `measured`. 추천: 드롭컷 / 시스루 댄디컷 / 세미울프컷.
- Result 2: `blocked`, yawProxy 0.044, tilt -8.87도. 모델 기준 측면급으로 판단. 강제 분석 시 mock 폴백으로 추천이 바뀜.
- Result 3: `blocked`, yawProxy 0.420, tilt -6.91도. fail 경계 아래라 재촬영 권장. 강제 분석 시 mock 폴백으로 추천이 바뀜.
- Finding: 게이트가 필요한 이유 확인. 틀어진 사진을 강제로 진행하면 얼굴형/추천이 크게 흔들림.
- Fix: MediaPipe 로드 지연 시 사진 단계가 무한 `확인 중`에 묶이지 않도록 `checkPhotoReadiness`에 9초 타임아웃 추가.
- Verification: `npm.cmd run typecheck`, `npm.cmd run build` 통과.
- Guard: 테스트용 이미지/HTML 삭제 완료. 얼굴 사진 repo commit 없음.
