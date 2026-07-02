# VoiceFit 작업 로그

## 2026-07-01 (커머스 패키지 MVP 인수인계)

- ✅ 네이버 블로그 URL 3개 크롤링/말투 분석 흐름 확인
- ✅ Supabase DNS 실패를 로컬 fallback으로 우회해 말투/글 저장 개발 지속
- ✅ mock off 상태에서 실제 Claude 커머스 패키지 생성 확인(3130자, mock 문구 없음)
- ✅ 생성 결과 UI를 textarea 1개에서 섹션별 탭/카드 구조로 변경
- ✅ 검수 화면을 블로그/쇼츠/릴스/고지 탭으로 분리
- ✅ `사용 안 함` 감사 fail 시 발행 버튼 잠금
- ✅ 생성 화면 수정본을 검수 이동 전 저장하도록 보강
- ✅ `.voicefit-local/` gitignore 추가
- ✅ 검증: `npm.cmd run test:commerce`, `npm.cmd run lint`, `npm.cmd run build`
- ✅ 커머스 패키지 9섹션화: `쇼츠 제작 지시서` 추가(0~3초 후킹/장면/자막/B-roll/TTS/컷 타이밍)
- ✅ 생성 결과 탭·검수 쇼츠 탭·빠른 복사에 쇼츠 제작 지시서 반영
- ✅ 검증: `npm.cmd run test:commerce` 27/0, `npm.cmd run lint`, `npm.cmd run build`
- ✅ 9:16 쇼츠 MP4 샘플 생성 MVP 추가: render plan JSON → FFmpeg 자막 영상 → 다운로드 라우트
- ✅ 검수 화면 쇼츠 기능은 기본 개발중 잠금으로 전환 (`NEXT_PUBLIC_SHORTS_RENDER_ENABLED=1`일 때만 노출)
- ✅ 검증: `npm.cmd run test:shorts` 9/0, 실제 MP4 1080x1920/20초 생성 확인
- ✅ 말투 분석 강화: 이모지 타이밍, 사진 타이밍, 띄어쓰기, 줄넘김, 문장부호, AI티 위험 요소를 profile_json에 추가
- ✅ 생성/재생성/채점 경로에 말투 지문 잠금 규칙 반영
- ✅ 실제 저장된 네이버 블로그 3글 원문으로 최신 말투 지문 분석 재검증(이모지/사진/띄어쓰기/줄넘김/문장부호/AI티 위험 추출)
- ✅ 로컬 fallback 방문 후기 생성→채점→재생성→재채점 루프 구현·검증
- ✅ 말투 점수 75점 미만이면 생성 화면 검수 이동, 검수 화면 발행, publish API 발행 차단
- ✅ 방문 후기 실테스트: 42점 → 구조 가이드 수정 후 78점 → 재생성 피드백 후 84점
- ✅ 사진 배치 로직을 `src/lib/image-placement.ts`로 분리하고 Vision 권장 위치 기반 삽입/폴백 테스트 추가
- ✅ 로컬 이미지 fallback 추가: 업로드 파일 저장, Vision 분석 결과 저장, 공식 이미지 URL 저장, 검수/발행 HTML 이미지 치환
- ✅ 검증: `npm.cmd run test:image` 6/0, `npm.cmd run test:voice` 6/0, `npm.cmd run test:commerce` 27/0, `npm.cmd run test:shorts` 9/0, `npm.cmd run lint`, `npm.cmd run build`
- ✅ dev server 실행 확인: `http://localhost:3000`, `/generate` 200
- ✅ 외부 검수 반영: 운영 완성도 60% 재분류, Phase 0 안전 정리(커밋/키 회전/Supabase/vacax split-brain)를 최우선 작업으로 승격
- ✅ 명령 축소 실험: 방문 후기에서 후킹/마케팅/정형 구조 명령 제거. 정형 소제목/구분선은 줄었지만 90점대는 미도달(78→82)
- ✅ 채점 기준 보정: 시그니처 표현은 체크리스트가 아니라 참고 샘플로 평가, 코드가 붙인 주소/지도 헤더는 말투 평가에서 제외
- ✅ 원문 few-shot 샘플 적용: 생성/재생성/채점에 원문 문단 샘플 포함, 방문 후기/상품 글 장르별 샘플 선택 보정
- ✅ 방문 후기 2-pass 말투 변환 적용: 초안 생성 후 사실 유지·말투만 재입히기. 실테스트 82점
- ✅ 생성 화면 자동 보정 루프 추가: 방문 후기/일상 글은 85점 미만이면 1회 자동 재생성 후 재채점
- ⚠️ 한계 확인: 현재 원문이 상품 후기 중심이라 방문 후기 90점대는 미도달. 같은 장르 방문 후기 원문 추가 필요
- ✅ 검증: `npm.cmd run test:voice` 6/0, `npm.cmd run test:commerce` 27/0, `npm.cmd run test:shorts` 9/0, `npm.cmd run lint`, `npm.cmd run build`
- 📌 운영 룰 추가: VoiceFit은 경제적 자유 문서를 적극 활용하되, 억지·과장·부자연스러운 돈벌이 톤은 금지
- 🚨 다음 핵심: 실제 사진 3~5장 포함 방문 후기 검증 후 사진 타이밍/사진 주변 문장까지 완성
- ✅ Phase 0 안전 정리 일부 완료: 코드 repo 보안 스캔 후 `815ec5e` 커밋/push
- ✅ vacax split-brain 해소: `Documents\Codex\vacax` 구본은 백업 보존, 최신 `C:\Users\vacma\vacax`로 junction 연결

---



---



## 2026-05-28 (세션 6 — 저장상태 점검)

- 🔍 어제(세션5) 저장 확인: VoiceFit 코드(d04f9c6)·운영문서(be976a0) 정상 저장 — 손실 없음

- 🚨 누락 발견: 라우드소싱 신설 + apex_aura 앱명 리브랜딩이 미커밋 상태 (어제 VoiceFit만 커밋 후 렉으로 종료)

- ✅ 누락분 복구 커밋(986f8c4) + push

- 📌 VoiceFit 자체 진척 없음 (NEXT 3개 그대로 유지)



## 2026-05-27 (세션 5 — 쿠팡 상품평 후킹 보강)

- 🚨 발견: 쿠팡 상품평이 후킹 무적용(시스템 프롬프트에 HOOK/경제적자유 누락, ANTI_AI_TONE만) → 밋밋

- ✅ `COUPANG_REVIEW_COPY` 신설 (첫 줄 후킹 + 마무리 + '도움돼요' CTA, 제공자 태도)

- ✅ generate·regenerate 라우트 둘 다 wiring (drift 방지) + tsc 통과

- ✅ Claude 프로젝트 지침 파일 작성 (`coupang_review_claude_project.md`) — API 비용 0 직접 작성용, 앱과 동일 규격 + 공정위 대가성 고지 강제

- 📌 git: 어제 커밋 2개(5576c83·36d097f) 로컬 정상, push는 Vercel 키 세팅 후 보류 유지(ahead)



## 2026-05-26 (세션 4 — 품질 대개편 + 쿠팡 상품평)

- ✅ AI 모델 gpt-4.1-nano → Claude Sonnet 4.6 (말투 "외국인 한국어" 해소)

- ✅ 방문기 네이버 사진 자동소싱 제거 (제3자 저작권/약관) → 할루시네이션·어색사진 동반 해결

- ✅ 품질 가드: 자연스러움·AI티·이미지 선별·패딩·협찬 고지 보존

- ✅ 정보헤더(주소·전화·지도폴백)+대문사진, 이미지 클립보드 붙여넣기(Ctrl+V)

- ✅ 서식 그대로 복사 발행 (네이버·티스토리 반자동)

- ✅ 큐레이션(상품) 전용 강한 카피 블록 (욕구·CTA·제공자 태도)

- ✅ 쿠팡 상품평 모드 신설 (평문·1000자+·사진10장·링크X)

- 🚨 티스토리 공식 API 2024.2 종료 확인 → 발행 반자동 복사로 결정 (AP-022)

- 📌 voicefit 코드 커밋(5576c83 + 쿠팡), push는 Vercel ANTHROPIC_API_KEY 세팅 후



## 2026-05-20 (세션 3 — 프로젝트 회고)

- ✅ Vercel 배포 완료: voicefit-phi.vercel.app (프라이빗, 친구 4명 테스트)

- ✅ 이미지 슬롯 명시 방식 도입 (`<사진1_음식>` 슬롯)

- ✅ 네이버 플레이스 비공식 API 활용 (주소/영업시간/방문자사진)

- ✅ VacAX 파이프라인 실전 가동 (전 직군 순차 실행)

- 🚨 gpt-4.1-nano 포맷 지시 불이행 → AP-017 등재

- 🚨 PowerShell 한글 인코딩 깨짐 → AP-016 등재

- 🚨 티스토리 OAuth 미완, UTM 미구현

- 📌 절반 성공 평가: MVP 작동, 품질 도달까지 2~3배 시간 소모



## 2026-05-18 (세션 2)

- ✅ 광고 톤 가드레일 시스템 프롬프트 추가

- ✅ 쿠팡 파트너스 법적 고지 자동삽입 (발행+미리보기)

- ✅ Unsplash 폴백 제거 (A안 단독)

- ✅ 버그 수정: 빈 제목, JSON 파싱, span 타입, 빈 검색어

- ✅ UX 개선: 온보딩 URL 스택 칩, 저장된 말투 재사용, 이미지 안내

- 🚨 개발자 에러 오버레이 미확인 (캡처 대기)



## 2026-05-18 (세션 1)

- ✅ vacax 운영 시스템 폴더 구축 (active/system/knowledge/archive)

- ✅ CLAUDE.md 작성 (세션 시작/종료 자동 행동 정의)

- ✅ VoiceFit 운영 문서 5개 작성 (STATE/NEXT/DECISIONS/LOG/code_path)

- ✅ 이미지 정책 확정: 쿠팡 파트너스 A안 (D-006 해소)

- ✅ D단 마커 치환 버그 수정: markdown.ts regex 강화 + generate/route.ts IMAGES 섹션 형식 개선

- 📌 다음: 이미지 정책 결정 → 버그 수정



## 2026-05-17

- 🔄 이미지 정책 7번째 변경 시도 (업로드 + AI 생성)

- 🚨 외부 평가 3회 받음 — "시스템 부재가 진짜 문제"

- ✅ 평가 통합: Claude Skills + 파일 기반 운영으로 전환 결정

- 📌 시뮬레이터 직군 신설 (D-006 안티패턴 예방)



## 2026-05-16

- ✅ Playwright 네이버 자동 포스팅 구현 완료

- ✅ 5개 제약 합의 후 진행

- 🚨 D단 마커 치환 버그 발견 (`![image-1]` 텍스트로 보임)



## 2026-05-15

- ✅ MVP 화면 3개 작동 확인

- ✅ #4 URL 크롤링, #1 글자색, #3 블로그 포맷 적용



## 2026-05-14

- ✅ 개발팀 Claude Code 지시서 6개 작성

- ✅ Supabase + Vercel 세팅

- ✅ 화면 A/B/C 구현 시작



## 2026-05-13

- ✅ G2 게이트 통과 (옵션 A 확정)

- ✅ PRD v1.0 완성 (9개 섹션)

- ✅ UX 와이어프레임 완성



## 2026-05-12

- ✅ G1 게이트 통과 (조건부 GO)

- ✅ 시장조사 3개 종합 (기획팀 + NotebookLM + 웹 Claude)

- ✅ 프로젝트 본질 재정의 (말투 개인화)



---



## 마지막 갱신

2026-07-02

- 커머스 `not_used/curation` 감사 룰을 우회 체험담 표현까지 확장하고, `/publish` API에서도 감사 fail 발행을 422로 차단. Supabase 도메인은 NXDOMAIN 확인.
- 대시보드에 로컬 전용 시스템 상태 배너 추가. Supabase DNS 실패, 로컬 fallback 글/말투 개수, mock OFF, 쇼츠 잠금 상태를 앱 안에서 확인 가능.
## 2026-07-02
- 5명 폐쇄 테스트 준비: 대시보드 디자인을 작업 흐름 중심으로 개편하고, `SHARE_ACCESS_CODE` 기반 접근 게이트와 localtunnel 임시 공유 경로를 추가했다.
