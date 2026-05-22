# Apex Aura — STATE

**진행도:** 95%
**단계:** Claude 안정화 + 2단계 호출 구조 + 풍부한 결과 콘텐츠. 페이지 4(컨설팅 리포트) 재배치 검증 대기.
**최종 문서 기준:** 2026-05-23

## 활성 Blocker (출시 차단급)
- 🔴 **API 키 4종 APK 평문 박힘** — Anthropic/Gemini/Unsplash/RevenueCat. 프록시 백엔드 필요 (Cloudflare Workers 권장)
- 🔴 **AgeGate 없음 + 외모 평가** — Play Store 정책 위반 위험. 미성년 차단 필요
- 🟡 `kDevMode = true` → RevenueCat 프로덕션 키 받은 후 false로
- 🟡 RevenueCat 프로덕션 키 미발급 (CEO 직접)

## 현재 완료된 것
- Firebase Functions 제거 → Flutter 직접 호출
- 메인 AI: **Claude Haiku 4.5** (Anthropic REST + Vision)
- 앱 리브랜딩: **닮은꼴 찾기**
- 컨설팅 페르소나 강화 (30만원 컨설턴트 톤)
- 응답 스키마 확장 (appearance_tier, weaknesses, lookalike_celebs, animal_distribution)
- 동물상 선택 UI 제거 → 사용자=사진+성별만
- 셀럽 사진 조달 (한국어 위키피디아)
- **구독제 일원화** (광고 제거)
- 보안: config.dart gitignore + config.example.dart 템플릿
- **2단계 호출 구조**: 메인(필수 콘텐츠 ~20초) + 백그라운드 styling (makeup/fashion ~10초)
- **JSON balancer**: 응답 max_tokens 잘려도 graceful 복구
- **컨설팅 도구 박스** prompt 인라인: 삼정비/황금비/헤어 5분류/컬러 시즌 4타입/메이크업·그루밍 공식
- **한국 셀럽 카탈로그 30명** (위키피디아 페이지 있는 솔로 배우/가수)
- **후킹 1**: AI 등급 카드에 "변화 시 7→9점, 상위 25%→8%" 화살표
- **후킹 3**: 액션카드 끝에 "단 N가지 변화로 갭 N% 축소" 배너
- **AI 추천 변신 방향** 배지 (목표 동물상 자동 선택임 명시)
- **페이지 4 재배치**: "3박자 솔루션" → "컨설팅 리포트" (단점 + 솔루션 + 액션카드 + 갭 축소 배너)
- **남성 메이크업 추가**: BB/톤업/컨실러 등 가벼운 화장 추천 분기
- **패션 룩 2개로 확장** + rationale 자세히 (얼굴형/체형/컬러 시즌 매칭)
- **메이크업 가이드 이미지 제거** (Unsplash 매칭 부정확)
- **패션 사진 BoxFit.contain** + height 200 (잘림 방지)

## 기술 스택
Flutter / Dart 3.x · **Claude Haiku 4.5** · ML Kit · RevenueCat · Wikipedia/Unsplash
