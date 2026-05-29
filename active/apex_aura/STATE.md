# Apex Aura — STATE

**진행도:** 97%
**단계:** Play 출시자산 전부 준비 완료(AAB·512아이콘·피처그래픽·PRIVACY 공개 URL). 실제 분석 결과 퀄 검증 + 무료 출시 결정 대기.
**최종 문서 기준:** 2026-05-29

## 활성 Blocker
- 🔴 **실제 Claude 분석 결과 미검증** — 서버 불안정으로 실 테스트 계속 보류. 출력 퀄(일반론 여부)이 출시 가치 좌우. **출시 전 1건 테스트가 최우선**
- 🔴 **API 키 APK 평문** — 프록시 백엔드 필요(출시 후 가능). 임시 방어 = Anthropic 하드캡
- 🟡 **Anthropic spending 하드캡 미설정** (CEO) — 무료 출시 전 필수, 손실 상한 고정
- 🟡 `kDevMode=true` — 무료 출시엔 OK(Pro 전체개방). 수익화 시 RevenueCat 키+false

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
- **[2026-05-29] AgeGate 복원 + 진입 연결** (_EntryGate: 생년월일 DatePicker+만14세 차단, 로컬 저장) → 출시 블로커 해소
- **[2026-05-29] release AAB 빌드 성공** (서명O, 업로드 가능) + Play 자산: PRIVACY 공개 URL(github blob), 피처그래픽 1024×500, 512 아이콘, 스크린샷 17장(제출 시 8장 선별), 데이터safety/등급 초안

## 기술 스택
Flutter / Dart 3.x · **Claude Haiku 4.5** · ML Kit · RevenueCat · Wikipedia/Unsplash
