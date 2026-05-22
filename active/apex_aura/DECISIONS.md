# Apex Aura — DECISIONS

## [2026-05-13] 방향 A 확정 (19세 풀버전 유지)
- 외모 점수 + 어필리에이트 + 메이크업 4단계 + 패션 룩 2개 전부 살림
- AgeGate(생년월일 자기 입력) 제거 → GPT 이중 안전망으로 대체

## [2026-05-13] AI 티 제거가 최우선
- CEO 원칙: "급하게 마무리 안 해도 돼, 완성도 다 챙겨라, AI 티 좀 없애라"
- Block D가 가장 중요한 이유: "원하는 상으로 바뀔 수 있을만한 해결책을 제시하지 않는 것 같다"는 CEO 우려 직접 해결

## [2026-05-21] Firebase Functions 제거 → Flutter Gemini 직접 호출
- 이유: GPT content filter / Claude 결제 버그 / 배포 반복 실패로 Firebase 경로 폐기
- Gemini 2.0 Flash 직접 호출 (gemini_service.dart), 서버 없음

## [2026-05-21] AI provider: GPT → Claude → Gemini 순으로 변경
- Claude: Anthropic 결제 버그로 사용 불가
- GPT: content filter로 외모 분석 전량 거부
- Gemini: content filter 없음, 무료 쿼터 존재

## [2026-05-21] 앱 핵심 가치 2축 확정
- 재미 (동물상 + 뛰어난 UI) + 희망 (개선 지침)
- 모든 화면 설계 이 두 축으로 평가

## [2026-05-07] Firebase Functions 백엔드 유지
- Claude Sonnet Vision으로 분석 (GPT-4o 아님)
- ML Kit(오프라인 수치) + Claude(해석) 조합 유지

## [2026-05-22] 메인 AI를 Gemini → Claude Haiku 4.5로 영구 전환
- 이유: Gemini 일일 쿼터 제한 + content filter 보수성 + 외모 분석 디테일 부족
- Claude Haiku 4.5: content filter 약함 + 컨설팅 톤(직설/단점 명시) 우수
- Anthropic REST API 직접 호출 (lib/services/claude_service.dart), 서버 없음
- Gemini는 fallback/병행 옵션으로만 유지

## [2026-05-22] 앱 이름 변경: Apex Aura → 닮은꼴 찾기
- 이유: 한국 시장 타깃 — 영문 추상 네이밍보다 직관적 한국어 네이밍이 검색·공유 강함
- 부제: "AI 외모 컨설턴트 · 24시간 무제한"
- Android label / main.dart title / home 헤더 동시 교체

## [2026-05-22] 동물상 선택 UI 제거
- 이유: 사용자 선택이 결과에 큰 영향 없음 + 입력 단계 줄여 전환율↑
- ML Kit가 현재 동물상 자동 판정 + AI가 변신 방향(target_animal) 자유 추천
- 사용자 입력: 사진 + 성별 2가지만

## [2026-05-22] 컨설팅 페르소나 강화 (30만원 컨설턴트 톤)
- 이유: AI 티 제거 + 위로형 무난한 표현이 변별력 없음
- 직설적 + 단점 명시 + 비의료 솔루션 묶음 (헤어/메이크업/패션/그루밍)
- 의료 권유 금지 (병원/클리닉/주사/주입 banned word)

## [2026-05-22] Anthropic 서버 불안정 → 실 테스트 보류
- Claude API 호출 반복 실패, 서버 정상화까지 작업 중단
- 코드는 완성, 안정화 대기 후 즉시 테스트 재개

## [2026-05-22] 광고(AdMob) 제거 → 구독제 일원화
- 이유: 광고+구독 동시 = 무료/유료 가치 차이 모호 + UX 손실(분석 전 광고 30초)
- 1인 스튜디오 운영 복잡도 ↓ (AdMob 정책/실 ID 발급/테스트 부담 제거)
- 무료/유료 분리는 코드 그대로 유지: Free schema(결과 일부) / Pro(풀 + makeup/fashion)
- 제거 범위: ad_service.dart, google_mobile_ads 패키지, AndroidManifest AdMob meta-data, AD_ID permission

## [2026-05-22] 전사회의 — 출시 차단급 5개 식별
- API 키 APK 평문 (프록시 백엔드 필요), AgeGate 부재, 빌드마커/개발자정보 노출, FLAG_SECURE 전역해제, 에러메시지 모호어
- 강 권고 7개: 응답시간 80초, 이미지 압축 768px, Unsplash 일관성, 컨설팅 톤 안전장치, 재시도 횟수, 페이월 차별화, 카피 6상자/6단계
- NEXT에 우선순위 반영
