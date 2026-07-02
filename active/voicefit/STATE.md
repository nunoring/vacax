# VoiceFit 현재 상태

## 프로젝트 정보
- 이름: VoiceFit 기반 AI 커머스 패키지 생성 도구
- 목표: 쿠팡/제휴 상품 입력 → 블로그 글, 쇼츠 대본, 쇼츠 제작 지시서, 쇼츠 설명란, 릴스 캡션, CTA, 제휴 고지, 실험 가설, 발행 전 체크리스트를 한 번에 생성하는 부업 콘텐츠 작업대 MVP
- 코드 위치: `code_path.txt` 참조

## 현재 단계
블로그 자동화 중심으로 재정렬 중. 말투 분석을 AI티 제거용 지문 분석(이모지 타이밍, 사진 타이밍, 띄어쓰기, 줄넘김, 문장부호 리듬)으로 강화했고, 로컬 fallback에서도 방문 후기 생성→채점→재생성→발행 게이트가 동작함.

## 진행도
로컬 개발 루프 92% / 운영 완성도 약 60%

## 현재 상태 요약
- 네이버 블로그 URL 3개 크롤링/말투 분석 흐름 확인 완료
- Supabase DNS 실패로 DB 저장 불가 → 로컬 fallback으로 개발 지속
- `VOICE_PROFILE_MOCK=0`, `COMMERCE_PACK_MOCK=0` 상태
- 쿠팡 API 키 없어도 상품 URL은 상품칸에 자동 반영되게 수정
- 임의 상품 mock 생성과 실제 Claude 커머스 패키지 생성 모두 검증
- 생성 결과 UI를 textarea 1개에서 섹션별 탭/카드 구조로 변경
- 로컬 post fallback에서도 mock off면 실제 Claude 호출하도록 수정
- 검수 화면을 블로그/쇼츠/릴스/고지 탭으로 분리
- 정책 감사 fail 시 발행 버튼 잠금
- 생성 화면에서 수정한 본문을 검수 이동 전 저장하도록 보강
- 커머스 패키지를 9섹션으로 확장: 쇼츠 제작 지시서(후킹/장면/자막/B-roll/TTS/컷 타이밍) 추가
- 쇼츠 제작 지시서 → render plan JSON → 로컬 FFmpeg 1080x1920 MP4 생성 라우트 추가
- 검수 화면에 쇼츠 MP4 샘플 생성 기능 추가. 단 기본 UI에서는 개발중으로 잠금
- 말투 프로필에 `emoji_timing`, `line_break_style`, `punctuation_style`, `ai_tell_risks` 추가
- 생성/재생성/채점 경로에 말투 지문 잠금 규칙 반영
- 로컬 fallback에서 방문 후기 생성/채점/재생성 지원. Supabase DNS 실패 상태에서도 블로그 자동화 루프 유지
- 말투 점수 75점 미만이면 생성 화면 검수 이동과 검수 화면 발행/API 발행을 차단
- 실제 네이버 블로그 3글 기반 저장 원문으로 최신 말투 지문 분석 재검증: 이모지/사진/띄어쓰기/줄넘김/문장부호/AI티 위험요소 추출 성공
- 방문 후기 실제 Claude 생성 테스트: 42점 → 구조 가이드 수정 후 78점 → 재생성 피드백 후 84점
- 방문 후기 명령 축소 실험: 후킹/마케팅/정형 구조 명령을 빼고 말투 우선 규칙만 적용. 정형 소제목/구분선은 줄었지만 점수는 78→82 수준으로, 90점대에는 few-shot 원문 예시/2-pass 말투 변환이 필요
- 말투 복제 강화: 원문 문단 few-shot 샘플을 생성/재생성/채점에 포함하고, 방문 후기/상품 글 장르별 샘플 선택 보정 추가. 방문 후기에는 2-pass 말투 변환 적용
- 실테스트 결과: few-shot만 적용 시 72~78점, 2-pass 적용 후 82점. 현재 학습 원문이 상품 후기 중심이라 방문 후기 90점대에는 같은 장르 원문 데이터가 더 필요
- 생성 화면 자동 보정 루프 추가: 방문 후기/일상 글은 생성 후 85점 미만이면 1회 자동 재생성→재채점
- 사진 배치 로직 분리: Vision 분석의 `placement_index`, `generated_paragraph`, 사진 타입(외관/내부/메뉴판/음식/제품)을 기준으로 본문 적정 위치에 삽입
- Supabase 장애 상태에서도 사진 흐름이 막히지 않도록 로컬 이미지 fallback 추가: 업로드 저장, Vision 분석 결과 저장, 공식 이미지 URL 저장, 검수/발행 HTML 이미지 치환
- 검증: `npm.cmd run test:image` 6/0, `npm.cmd run test:commerce` 27/0, `npm.cmd run test:shorts` 9/0, `npm.cmd run test:voice` 6/0, `npm.cmd run lint`, `npm.cmd run build`
- 로컬 dev server: `http://localhost:3000` 실행 중. `/generate` 200 확인
- 2026-07-02 외부 검수 반영: 현재 92%는 로컬 개발 루프 기준이며, 실발행/실사진/Supabase/쿠팡 API/수익 측정이 남아 운영 완성도는 약 60%로 재분류
- `ROADMAP.md` 추가: Phase 0 안전 정리 → Phase 1 블로그 실사용 → Phase 2 수익/측정 → Phase 3 GO/KILL → Phase 4 쇼츠 조건부 확장
- Phase 0 일부 완료: 코드 repo 보안 스캔 후 `815ec5e` 커밋/push 완료, `Documents\Codex\vacax` 구본은 백업 후 최신 `C:\Users\vacma\vacax`로 junction 연결
- 커머스 정책 감사 강화: `not_used/curation`에서 개봉·언박싱·도착·착용·섭취처럼 사용 단어를 피한 체험담 표현도 fail로 잡음
- 검수 UI뿐 아니라 `/api/posts/[id]/publish` 서버 라우트에서도 커머스 감사 fail이면 422로 발행 차단
- Supabase DNS 재진단: `bviwpsptjwoogsjrsays.supabase.co`는 `Non-existent domain`으로 확인됨
- `/api/system/status`와 대시보드 상태 배너 추가: Supabase DNS/쿼리 상태, 로컬 fallback 카운트, mock/쇼츠 잠금 상태를 로컬에서 즉시 확인. Vercel 배포 환경에서는 비활성화
- Supabase DNS 장애 때 대시보드가 로딩에 묶이지 않도록 `/api/posts`, `/api/voice-profiles`에서 DNS preflight 후 로컬 fallback 즉시 반환
- 말투 저장/선택 UX 추가: 온보딩 저장 목록, 대시보드 현재 말투 셀렉터, 생성 화면 셀렉터가 같은 선택값을 공유
- 상품글 72점 고착 1차 해소: product에 2-pass 말투 변환+자동 보정 루프 적용, 광고 규칙 재주입 제거. 앱 실험 72점 → 78점, 검수 이동/정책 감사 pass 확인

## 활성 Blocker
1. ~~Supabase DNS 실패~~ → 2026-07-02 저녁 복구 확인 (검증 글이 실제 DB에 저장/삭제됨). 로컬 fallback 데이터 → DB 마이그레이션 재검증 필요
2. 쿠팡 파트너스 API는 최종 승인 회원만 키 발급 가능 → 현재는 파트너스 링크 수동 생성/붙여넣기 우선
3. 네이버 자동 발행은 운영용 검증 미완
4. 방문 후기 사진 업로드/배치 흐름은 실제 사진 묶음으로 Claude Vision 호출까지 추가 검증 필요
5. 쇼츠 MP4는 개발중으로 기본 잠금. 블로그 자동화 완성도가 우선

## 보안/커밋 주의
- 코드 repo `.env.local`에 API 키/토큰 있음 → 절대 커밋 금지
- 코드 repo `.voicefit-local/`은 로컬 테스트 데이터 → 커밋 금지
- API 키가 대화/터미널 출력에 노출된 적 있음 → 실제 운영 전 키 회전 권장

## 마지막 갱신
2026-07-02 (상품글 72점 고착 1차 해소)
---

## 2026-07-02 추가 상태
- 5명 폐쇄 테스트용 대시보드 디자인으로 개편: 상품 1개 -> 블로그/상품 홍보/말투 분석 작업 흐름을 첫 화면에서 바로 보이게 정리.
- Notion 영상/UX 패턴 반영: 예쁜 랜딩보다 작업 상태, 다음 행동, 채널별 결과 확인을 우선하는 구조로 정리.
- 테스트 공유용 접근 게이트 추가: `SHARE_ACCESS_CODE`가 있으면 `/access`에서 암호 입력 후 12시간 쿠키로 접근.
- 공유 방식은 임시 localtunnel 사용: 정식 출시가 아니라 5명 폐쇄 테스트용. PC/dev server/tunnel이 켜져 있어야 유지됨.
- 주의: 사용자별 계정/데이터 분리는 아직 없음. 테스트 참여자는 같은 Supabase/로컬 운영 데이터 흐름을 공유하므로 민감 계정 입력 금지.
