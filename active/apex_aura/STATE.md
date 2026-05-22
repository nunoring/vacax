# Apex Aura — STATE

**진행도:** 97%
**단계:** Claude Haiku 4.5 전환 완료. Anthropic 서버 불안정으로 실제 테스트 보류, 정상화 대기.
**최종 문서 기준:** 2026-05-22

## 활성 Blocker
- **Anthropic 서버 불안정** — Claude API 호출 반복 실패, 서버 정상화 대기 중
- `kDevMode = true` → RevenueCat 프로덕션 키 받은 후 false로 변경
- RevenueCat 프로덕션 키 미발급 (CEO 직접)
- AdMob 실 광고 ID 미발급 (현재 테스트 ID — 출시 직전 교체)

## 현재 완료된 것
- Firebase Functions 제거 → Flutter 직접 호출
- 메인 AI: Gemini → **Claude Haiku 4.5** 전환 (Anthropic REST + Vision, 재시도/이미지 압축)
- 앱 리브랜딩: Apex Aura → **닮은꼴 찾기** (한국어 네이밍)
- 컨설팅 페르소나 강화 (1회 30만원 외모 컨설턴트 톤)
- 응답 스키마 확장 (appearance_tier, weaknesses 3개)
- 동물상 선택 UI 제거 → 사용자는 사진+성별만 입력
- 셀럽 사진 조달 (한국어 위키피디아 + asset 폴백)
- Unsplash 패션 이미지 조달
- 광고 통합: 보상형 동영상 (google_mobile_ads, 테스트 ID)
- 에러 처리 강화: 가짜 fallback 제거, 명확한 에러 메시지
- MainActivity FLAG_SECURE 해제 (스크린샷/스크롤 캡처 허용)
- 보안: config.dart gitignore + config.example.dart 템플릿

## 기술 스택
Flutter / Dart 3.x · **Claude Haiku 4.5 (메인)** · Gemini 2.0 Flash (보조) · ML Kit · RevenueCat · AdMob · Wikipedia/Unsplash
