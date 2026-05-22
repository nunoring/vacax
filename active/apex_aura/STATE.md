# Apex Aura — STATE

**진행도:** 92%
**단계:** Claude 전환 + 구독제 일원화. 전사회의 보완점 12개 도출 — 출시 차단급 5개 정리 필요.
**최종 문서 기준:** 2026-05-22

## 활성 Blocker (출시 차단급)
- 🔴 **API 키 4종 APK 평문 박힘** — Anthropic/Gemini/Unsplash/RevenueCat. 프록시 백엔드 필요 (Cloudflare Workers 권장)
- 🔴 **AgeGate 없음 + 외모 평가** — Play Store 정책 위반 위험. 미성년 차단 필요
- 🟡 **Anthropic 서버 불안정** — Claude API 반복 실패, 서버 정상화 대기
- 🟡 `kDevMode = true` → RevenueCat 프로덕션 키 받은 후 false로
- 🟡 RevenueCat 프로덕션 키 미발급 (CEO 직접)

## 현재 완료된 것
- Firebase Functions 제거 → Flutter 직접 호출
- 메인 AI: Gemini → **Claude Haiku 4.5** 전환 (Anthropic REST + Vision, 재시도/이미지 압축)
- 앱 리브랜딩: Apex Aura → **닮은꼴 찾기** (한국어 네이밍)
- 컨설팅 페르소나 강화 (1회 30만원 외모 컨설턴트 톤)
- 응답 스키마 확장 (appearance_tier, weaknesses 3개)
- 동물상 선택 UI 제거 → 사용자는 사진+성별만 입력
- 셀럽 사진 조달 (한국어 위키피디아 + asset 폴백)
- Unsplash 패션 이미지 조달
- **구독제 일원화** — 광고(AdMob) 제거, RevenueCat 단일 채널
- 에러 처리 강화: 가짜 fallback 제거, 명확한 에러 메시지
- MainActivity FLAG_SECURE 해제 (전역 — paywall 토글 필요)
- 보안: config.dart gitignore + config.example.dart 템플릿

## 기술 스택
Flutter / Dart 3.x · **Claude Haiku 4.5 (메인)** · Gemini 2.0 Flash (보조) · ML Kit · RevenueCat · Wikipedia/Unsplash
