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
