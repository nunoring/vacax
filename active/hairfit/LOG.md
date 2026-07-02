# HairFit MVP LOG

2026-07-01 | Notion의 Claude Design/웹제작 요약 원칙을 화면에 직접 적용. 홈/결과/모드 흐름 개선, build 및 mock 흐름 검증 완료. 다음은 스타일 에셋 6종 교체.
2026-07-01 | VacAX 점검: 스타일 에셋 9종 중 3종 ready, 6종 ok_small placeholder 성격 확인. 다음 작업을 에셋 교체 -> mock QA -> 승인 후 1컷 실생성으로 압축.
2026-07-01 | 스타일 에셋 6종(`drop_cut`, `texture_crop`, `as_perm`, `shadow_perm_dandy`, `semi_leaf`, `semi_wolf`) `display.webp`/`reference.webp` 교체. 9/9 ready 확인. mock/preview 카드가 display 에셋을 쓰도록 코드 연결. build 통과.
2026-07-01 | 완성 로드맵 작성. 1차 완성 기준은 상용 출시가 아니라 포트폴리오 제출 가능한 상담 MVP로 정의.
2026-07-01 | 앱 기능 보강/자가 테스트: 9종 스타일 라이브러리 레퍼런스 선택 UI 연결, 손님 사진 없는 reference sample은 스타일 미리보기로 fallback, reference 품질 평가 UI 노출. AI 추천/레퍼런스 mock 흐름 모두 저장까지 통과.
2026-07-01 | 자동 검증 마감: build/typecheck/style asset check 통과, smoke checklist 작성, 코드 폴더 non-git 및 `.env.*` ignore 상태 확인. 실제 유료 생성 0회 유지.
2026-07-01 | 실제 생성 2회 테스트. synthetic 고객 + 시스루 댄디 기준 v1 얼굴 유지 3.5/5, 프롬프트 강화 후 v2 얼굴 유지 4/5. 테스트 후 mock/stub 재잠금.
2026-07-01 | 비용 가드 UX 보강: AI 추천 3컷 자동 실제 생성 기본 OFF, 카드별 `이 카드 실제 생성`으로 1컷씩 실행. build/typecheck/assets 통과.
2026-07-01 | CEO가 v2 실제 생성 결과를 같은 사람으로 보인다고 검수. 5장 테스트는 랜덤 인터넷 얼굴 대신 synthetic 얼굴 세트로 진행하기로 정리.
2026-07-01 | synthetic 5장 실제 생성 테스트 완료. 최종 5/5 생성 성공, 얼굴 유지 4/5 이상 4장, 상담 사용성 3/5 이상 5장. `aspect_ratio=auto`, 세미리프 hair-crop reference 개선 반영.
2026-07-01 | CEO 육안 검수: 5장 결과는 완전 동일인은 아니지만 얼추 비슷함. 상담용 MVP는 통과로 보되, "완벽한 얼굴 유지" 표현은 금지.
2026-07-01 | 앱/README 문구를 "상담용 얼굴 인상 유지" 기준으로 조정. typecheck/build 통과.
2026-07-01 | 긴 기장 reference 리스크 개선: leaf/semi_wolf reference를 hair 중심으로 교체하고 semi_wolf 실제 1컷 smoke test 통과. 테스트 후 mock 재잠금.
2026-07-01 | mock 회귀 재검수 완료: 홈-동의-샘플-성향-자동추천-결과-저장-상세 통과. fallback 문구를 "실제 합성 전 스타일 미리보기"로 수정, build/typecheck/assets 통과.
2026-07-02 | 디자인 리프레시 1차: 초딩 느낌 피드백 반영. 라운드/그림자/크림 장식/칩 과다를 줄이고 업무툴형 홈·결과·모드·기록 톤으로 정리. build/typecheck/assets와 mock 흐름 통과.
2026-07-02 | CEO 육안 피드백: 1차 디자인은 너무 창백함. 다음 디자인 패스는 대비, 사진 존재감, 살롱 프리미엄 무드 보강으로 재설정.
2026-07-02 | 앱 완성 로드맵 재작성. 포트폴리오 패키징 제외, 디자인 2차 -> 실제 업로드 QA -> 미용사 피드백 카피 -> 실제 생성 가드 -> 신뢰성 점검 순서로 정리.
2026-07-02 | 중간저장: 현재 앱은 mock/stub 모드로 열려 있음. 다음 1수는 디자인 2차 패스, 이후 실제 파일 업로드 QA와 미용사 피드백 카피 반영.
2026-07-02 | 외부 모델 도움으로 ROADMAP 상세판 갱신 확인. 상품성 기준에서 Phase 0(git/정본 정리) 우선으로 NEXT 순서 수정.
2026-07-02 | 추천 안정화: 얼굴형 일치 점수 과가중을 낮추고 인접 얼굴형/안정 타이브레이크 적용. mock 동일 조건 반복 추천 동일 확인. VacAX hairfit self-junction 복구.
2026-07-02 | 사진 각도 보조 게이트 추가: 등록 사진을 MediaPipe landmark로 사전 확인해 안정/주의/재촬영을 표시하고 심한 각도는 진행 차단. typecheck/build 및 샘플 흐름 통과.
2026-07-02 | CEO 제공 동일 인물 3장 각도 테스트: 정면 1장 ready, 틀어진 2장 blocked. 강제 진행 시 추천이 크게 흔들려 게이트 필요성 확인. readiness 9초 타임아웃 추가.
2026-07-02 | Claude 기능 개선 위임 지시서 작성: 추천 로직, 얼굴분석 근거 문구, 각도 게이트 UX, 회귀 테스트, 레퍼런스 흐름 점검 범위와 금지사항 정리.
2026-07-02 | Claude 기능 타당성 패스: hairDesign 기반 추천 스코어링(breakdown), 신뢰도별 안정 bias, 손님 문구 3카드 차별화, 사진 게이트 원인별 재촬영 안내, 레퍼런스 자동 과금 경로 제거 + 출처/권한 게이트, fixture 회귀 스크립트(check-recs) 추가. typecheck/build/assets/recs + mock 브라우저 흐름 통과, 유료 호출 0. 커밋 4건(codex/design-pass-2).
2026-07-02 | Codex 검수에서 업로드 레퍼런스 출처 unknown 진행 허점 발견 후 차단. typecheck/build/assets/recs 통과, `9b5a1ac`까지 codex/design-pass-2 push 완료.
2026-07-02 | CEO 정면 사진 + 시스루 댄디컷 실제 생성 1컷 시도. gpt-once로 1회 제한 후 실행했으나 Replicate output 이미지 없음으로 fallback placeholder 반환(`isMock=true`, `costUsd=0`). 즉시 mock 재잠금.
2026-07-02 | 실제 생성 실패 후 Replicate output 객체/배열 파싱과 실패 status/error 메시지 보강. `node --check`/build 통과, `12b124b` push. mock 재시작 완료.
2026-07-02 | 홈 화면의 중간/긴 기장 2장 미리보기 제거. 3컷 세트가 아니어서 어색하던 영역을 비용 가드/원본 선택 저장/레퍼런스 권한 확인 패널로 교체. typecheck/build 통과, `2391715` push.
2026-07-02 | CEO 피드백 반영: 홈의 내부용 안전장치 패널 제거. 빠른 작업을 `기존 고객 검색`, `레퍼런스 바로 적용`으로 교체하고, 레퍼런스 직행 시 모드 선택을 건너뛰어 9개 기본 스타일 선택 화면으로 연결. typecheck/build 통과, `f0771fd` push.
2026-07-02 | 레퍼런스 바로 적용 흐름 재정렬: 홈 클릭 시 손님 사진보다 9개 기본 레퍼런스 카탈로그를 먼저 보여주고, 선택 후 사진/성향 입력으로 이동. 커스텀 업로드는 접기 섹션으로 이동. typecheck/build/assets 통과, `9711e12` push.
2026-07-02 | 홈 헤더 디자인 정리: `분석/추천/설명/보관` 4칸과 1-2-3 설명 박스를 제거해 중복 설명을 줄이고, 최근 고객 기록이 바로 이어지게 정리. typecheck/build 통과, `a0309da` push.
2026-07-02 | 남성 스타일 라이브러리 9개 -> 15개 확장: 크루컷, 투블럭 댄디컷, 다운펌 댄디, 콤마헤어, 가르마 포마드, 허쉬 리프컷 추가. 추천 회귀 통과, mock 안정 픽 유지. 신규 6개 에셋은 generator 기반 `ok_small` 임시급이라 미용사 테스트 전 그래픽 교체 후보. `fb22600` push.
2026-07-02 | 레퍼런스 카탈로그 선택 후 스타일 상세 패널 추가: 상담 한 줄, 기장, 앞머리/윗볼륨/옆볼륨/질감, 시술 태그, 핵심 근거 3줄 표시. typecheck/build/assets/recs 통과, `0838852` commit.
2026-07-02 | 신규 남성 스타일 6종 에셋을 실제 생성 이미지로 교체: display는 모델컷, reference는 얼굴 영향 적은 머리 구조 레퍼런스. 레퍼런스 화면은 짧은/중간/긴 기장으로 분류, 홈의 `9개 기본 스타일 선택` 문구 제거. assets 15/15 ready, typecheck/build/recs 통과, real 호출 후 mock disarm, `cf5df88` push.
2026-07-02 | 스타일 분류 조정: 드롭컷과 투블럭 댄디컷을 짧은 기장에서 중간 기장으로 이동. assets/recs/typecheck/build 통과, `37ef878` push.
2026-07-02 | CEO 정면 사진으로 GPT Image 2 실제 1컷 테스트(시스루 댄디). `IS_MOCK=false`, 비용 $0.04, 생성 후 즉시 mock disarm. 얼굴 보존은 대체로 양호하나 피부/인상 정돈감 약간 있어 추가 프롬프트 조정 후보.
2026-07-02 | CEO 정면 사진으로 앱 3컷 생성 경로 실제 테스트: 소프트 아이비/시스루 댄디/세미리프 3콜, 전부 `IS_MOCK=false`, 총 $0.12, 생성 후 즉시 mock disarm. 2/3번 얼굴 보존 양호, 1번 짧은 컷은 얼굴·크롭 변화가 더 커 프롬프트 보강 후보.
