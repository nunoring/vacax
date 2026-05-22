# Apex Aura — NEXT

## 우선순위 (전사회의 2026-05-22 기준 — 서버 정상화 안 와도 가능)
1. **API 키 프록시 백엔드** — Cloudflare Workers, 4시간. APK 키 노출 사고 차단 (출시 차단급)
2. **AgeGate 복원** — 첫 진입 1회 클릭, 2시간. Play Store 정책 위험 (출시 차단급)
3. **에러 메시지 + 빌드마커 정리** — 1시간. 개발자 정보 사용자 노출 차단
4. **FLAG_SECURE 토글** — paywall 진입 시 ON / 결과화면 OFF, 30분
5. **paywall + 공유카드 카피 6단계 적용** — 2~3시간. knowledge/copywriting-rules.md 적용
6. **lookalike 응답시간 80→40초** — Claude 메인 호출에 합치기, 1~2시간
7. **Unsplash 단품 키워드 전환** — 룩 일관성 회복, 1시간

## Anthropic 서버 정상화 후
8. Claude API 실제 응답 테스트 — 전 페이지 동작, 응답 시간, banned word 발동 여부
9. 결과 품질 검토 — 컨설팅 톤(직설/단점/솔루션) 실작동, 동물상/셀럽 정확도

## CEO 직접 (병렬)
10. RevenueCat 프로덕션 키 발급 → kDevMode = false 처리

## 출시 준비
11. 베타 5명 테스트
12. Play Console 제출 — 스크린샷, 설명, 개인정보처리방침
13. 동물상 일러스트 7종 (이모지 대체)
