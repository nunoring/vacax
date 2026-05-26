# PDF 뷰어 — STATE

**상태:** 종료 — 개인용 (Play Store 출시 안 함)
**최종 문서 기준:** 2026-05-26
**목적(원):** 포트폴리오 출시 이력 → 시장성 없음 판정 → 개인 사용 앱으로 전환

## 출시 중단 사유 (시장 스캔)
- 알PDF = 광고 + 유료 광고제거(AD-ZERO) 모델로 장악
- "광고 없음·오프라인" 포지션을 앱 이름에 박은 경쟁자 다수 (PDF Reader - without ads, Fast PDF Reader 2026 등) → 차별점 0, 포지션 포화
- AI 요소 0 → 1순위(AI/AX 포트폴리오) 기여 약함
- 적용: Ch3.1 일방통행(들어갈 도로 없음) + Ch4 안 되는 사업

## 코드 상태
- 광고 완전 제거, `flutter analyze` 통과
- 폰 설치용 release APK 빌드 완료 (debug 서명): `build/app/outputs/flutter-apk/app-release.apk` (51.6MB)
- 출시 전용 산출물(keystore/release 서명/key.properties/bat) 제거, `build.gradle.kts` debug 서명 원복
- git 미시작 (개인용이라 불필요)

## 결론
추가 투자 0. archive 이동 대상. 집중은 AI/AX 포트폴리오로 복귀.

## 기술 스택
Flutter / Dart 3.x · pdfx · file_picker · provider · shared_preferences · pdf · share_plus
