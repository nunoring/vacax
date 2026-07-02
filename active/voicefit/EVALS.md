# VoiceFit — EVALS

검증 기준과 회귀 테스트 기록.

## 현재 통과 기준

- [x] 네이버 블로그 URL 3개 추가 성공
- [x] 말투 분석 mock 성공
- [x] 상품 URL 자동 입력 fallback 성공
- [x] 커머스 패키지 mock 생성 성공
- [x] 커머스 패키지 실제 Claude 생성 성공: 3130자 생성
- [x] 실제 생성 결과에 mock 문구 없음 확인
- [x] `npm run lint`
- [x] `npm run build`
- [x] 인앱 브라우저에서 `/generate` 흐름 직접 확인
- [x] `사용 안 함` 모드에서 사용 후기성 표현 fail 처리 (`npm.cmd run test:commerce`)
- [x] 채널별 검수 화면 UX 구현: 블로그 / 쇼츠 / 릴스 / 고지 탭
- [x] 정책 감사 fail 시 발행 버튼 잠금
- [x] 커머스 패키지 9섹션화: `쇼츠 제작 지시서` 포함
- [x] 쇼츠 제작 지시서 mock/파서 테스트: 0~3초 후킹, 자막, B-roll, TTS, 컷 타이밍 확인
- [x] `npm.cmd run test:commerce` 27 passed / 0 failed
- [x] 쇼츠 render plan 테스트: `npm.cmd run test:shorts` 9 passed / 0 failed
- [x] 로컬 FFmpeg MP4 생성 API 확인: `POST /api/posts/[id]/shorts/render` 200
- [x] 생성 MP4 다운로드 API 확인: `GET /api/posts/[id]/shorts/video` 200, `video/mp4`
- [x] ffprobe 확인: 1080x1920, 20초
- [x] 말투 지문 정규화 테스트: `npm.cmd run test:voice` 6 passed / 0 failed
- [x] 말투 채점 기준에 layout 포함: 줄넘김·문단 길이·사진/이모지 타이밍 감점 가능
- [x] 실제 저장된 네이버 블로그 3글 원문으로 최신 말투 지문 분석 재검증: 이모지 타이밍, 사진 타이밍, 띄어쓰기, 줄넘김, 문장부호, AI티 위험요소 추출 성공
- [x] Supabase DNS 실패 상태에서 로컬 방문 후기 생성→채점→재생성→재채점 루프 검증
- [x] 방문 후기 말투 점수 개선 확인: 42점(정형 소제목/구분선) → 78점(소제목 제거) → 84점(재생성 피드백)
- [x] 75점 미만 발행 API 차단 확인: 로컬 post 직접 publish 요청 422
- [x] 명령 축소 실험: 방문 후기에서 후킹/마케팅/정형 구조 명령 제거, 점수 62→채점 보정 78→재생성 82
- [x] 원문 few-shot + 장르별 샘플 선택 테스트 추가: 방문 후기는 장소/먹은 경험 샘플 우선
- [x] 2-pass 말투 변환 적용 후 실제 방문 후기 테스트: 82점. 말투는 개선됐으나 현재 원문이 상품 후기 중심이라 방문 후기 90점대 미도달
- [x] 생성 화면 자동 보정 루프 추가: 방문 후기/일상 글 85점 미만 시 1회 자동 재생성 후 재채점
- [x] 사진 배치 단위 테스트: `npm.cmd run test:image` 6 passed / 0 failed
- [x] 사진 타입 우선순위 보정 확인: `테이블` 키워드가 있어도 음식/제품 사진은 내부 사진으로 오분류하지 않음
- [x] 로컬 이미지 fallback 빌드 확인: `/api/local-images/[...path]`, 업로드/해석/소싱/검수/발행 라우트 TypeScript 통과
- [x] dev server 확인: `http://localhost:3000/generate` 200, 없는 로컬 이미지 경로 404
- [x] `npm.cmd run lint`
- [x] `npm.cmd run build`

## Quality Score 기록

(아직 없음)
