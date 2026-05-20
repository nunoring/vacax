# Apex Aura — STATE

**진행도:** 95%
**단계:** UX 전면 강화 완료. Gemini 쿼터 리셋 후 실제 응답 테스트 1회 필요.
**최종 문서 기준:** 2026-05-21

## 활성 Blocker
- **Gemini 일일 쿼터 소진** — 내일 자정(UTC) 리셋 OR Google Cloud 결제 활성화
- `kDevMode = true` → RevenueCat 프로덕션 키 받은 후 false로 변경
- RevenueCat 테스트 키 → 프로덕션 키 미발급 (CEO 직접)

## 현재 완료된 것
- Firebase Functions 제거 → Flutter Gemini 직접 호출 (gemini_service.dart)
- 동물상 복합 % 바 (ML Kit 수치 기반 7종 자동 계산)
- 셀럽 닮은꼴 카드 (네이버 검색 연결, 성별별 카탈로그)
- 공유 전용 카드 UI (동물상% + 점수 + 목표 1장 요약)
- 갭 → 여정 프레이밍 (변화별 갭 감소 수치)
- 동물상 상세 모달 (배지 탭 시 측정 기준 + 내 수치 비교)
- Gemini 프롬프트 희망 언어 재설계 (timeline/gap_reduction 필드)
- 남성 그루밍 루틴 분기 (메이크업 vs 그루밍)
- Free 페이월 강화 (액션카드 잠금, 컨설턴트 리포트 잠금)
- 어필리에이트 쿠팡 검색 버튼
- ML Kit + UI 완성도 100%

## 기술 스택
Flutter / Dart 3.x · Gemini 2.0 Flash (직접 호출) · ML Kit · RevenueCat
