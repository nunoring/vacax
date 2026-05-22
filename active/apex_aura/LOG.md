# Apex Aura — LOG

2026-05-20 | 세션 시작 — 노션/코드 기반 현황 파악, active/apex_aura 운영 문서 생성
2026-05-20 | GPT 복귀(content filter 우회 프롬프트) + Free 페이월 강화(액션카드 잠금/컨설턴트 리포트 잠금) + 셀럽 레퍼런스 3요소 의무화 + 어필리에이트 쿠팡 검색 버튼 복원 배포완료
2026-05-21 | 아키텍처 전면 재설계 — Firebase Functions 제거, Flutter→Gemini 직접 호출(gemini_service.dart). 일일 쿼터 소진으로 실제 응답 테스트 미완.
2026-05-21 | 전사회의 후 대규모 UX 강화 — 동물상 복합%(ML Kit), 셀럽 닮은꼴 카드(네이버 검색 연결), 공유 전용 카드, 갭→여정 프레이밍, 동물상 상세 모달(배지 탭), Gemini 희망언어 프롬프트 재설계, 남성 그루밍 분기, 레이더 레전드 추가.
2026-05-22 | 메인 AI를 Gemini→Claude Haiku 4.5로 전환 (ClaudeService 신규, Anthropic REST+Vision, 이미지 압축, 재시도). 앱 리브랜딩(닮은꼴 찾기). 컨설팅 페르소나 강화(1회 30만원 톤, 직설+단점+비의료 솔루션). appearance_tier/weaknesses 스키마 확장. 동물상 선택 UI 제거(사용자=사진+성별만). 셀럽 사진 조달(위키피디아). Unsplash 패션이미지. AdMob 보상형 동영상(테스트 ID). 에러 처리 강화(가짜 fallback 제거). FLAG_SECURE 해제(스크린샷 허용). config.dart gitignore+example 템플릿. Anthropic 서버 불안정으로 실제 테스트 보류.
2026-05-22 | [메타] vacax 운영 시스템 강화 — `경제적 자유 초월차선` 1500만원 PDF 전체 OCR + 29챕터 분석. 5개 핵심(6상자/6단계/N그래프/제공자 태도/절세) 정제본 2개 신규(`knowledge/copywriting-rules.md`, `knowledge/business-setup.md`). CLAUDE.md에 콘텐츠·상품 생산 표준 + 직군 책임 강화(/strategist·/builder·/growth) + 자동 트리거 매핑 + 상황 인덱스 자동 참조 룰 박음. 이제 사용자가 평소 말투로만 질문해도 책 이론 자동 적용. apex_aura·voicefit 모두 자동 룰 적용 대상.
2026-05-22 | 전사회의 후 광고(AdMob) 제거 → 구독제 일원화. ad_service.dart 삭제, google_mobile_ads 패키지 제거, AndroidManifest AdMob meta-data + AD_ID permission 제거. 보완점 12개 식별 (출시 차단급 5개: API 키 프록시 백엔드/AgeGate/빌드마커/FLAG_SECURE 토글/에러메시지 정리). NEXT에 우선순위 반영.
2026-05-23 | Claude 호출 안정화 사이클 13번 — TimeoutException/max_tokens 잘림 반복 진단 + 처방. 최종: 2단계 호출 구조 (메인 ~20초 + 백그라운드 styling ~10초) + JSON balancer로 graceful 복구 + maxTokens 4096 + 도구 박스(삼정비/황금비/헤어5분류/컬러시즌/메이크업·그루밍 공식) prompt 인라인 + 셀럽 카탈로그 30명(남15/여15) 박음. 후킹 1(7→9점 변신 화살표) + 후킹 3(갭 N% 축소 배너) 추가. 페이지 4 재배치(3박자 솔루션→컨설팅 리포트). 남성 메이크업 추가(BB/톤업/컨실러). 패션 룩 2개로 확장 + 얼굴형/체형/컬러시즌 매칭 rationale. 메이크업 가이드 이미지 제거. 패션 사진 BoxFit.contain + height 200. banned_words 제거(오탐 차단). AI 추천 변신 방향 배지. 안티패턴 AP-018~021 knowledge 박음.
