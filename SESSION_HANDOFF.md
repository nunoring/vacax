# SESSION HANDOFF — 2026-06-16

> 새 채팅에서 "이어서" + 이 파일 붙이면 바로 재개 가능. (멀티 프로젝트 세션)

---

## 이번 세션 한 일 (요약)
1. **유튜브 지식 라이브러리 정본화** — 노션 토글 페이지로 통합(39편) + AI참조 작업별 인덱스. 잘못 만들었던 DB는 폐기.
2. **학습 로드맵 확정** — 파워유저→빌더, 핵심레버 = **Eval**(AI 품질 측정). 노션 저장.
3. **yt-rag** — RAG 톱다운 학습 프로젝트(작동). 유튜브 라이브러리 의미검색.
4. **rfp-deck** ⭐ — 과거 제안서 슬라이드 **2축 RAG**(내용+구조) + **비전 구조태깅**. = 이번 세션 최강 포폴 조각. **색인 백그라운드 진행 중.**
5. **라우드소싱 workflow_v1 → v1.1** — 툴스택 2026 SOTA 교체(프리미엄) + Image-First 방법론 + 입상작 패턴.
6. **시스템 수정** — "같은 답 맴돌기" 재발 방지 룰 3곳(메모리/CLAUDE.md/council.md)에 박음.

---

## 🔄 백그라운드 진행 중 (확인 먼저)
- **rfp-deck 비전 색인**: `apps/rfp-deck/vision_index.py` 실행 중. 965장 중 ~280+ 진행(2026-06-16 기준). 
  - 확인: `apps/rfp-deck/data/vision_tags.json` 개수 / `tasklist | grep POWERPNT`
  - 완료 시 `slides.json`에 `vision` 필드 병합됨. 죽었으면 `python vision_index.py` 재실행(이어감).

---

## ⏭️ 열린 액션 (다음 세션 우선순위)
1. [ ] **rfp 색인 완료 확인** → 비전태그(layout_one_line)를 구조검색(svec)에 통합 = search 품질↑
2. [ ] **rfp-deck v1** = RFP 텍스트 → 필요섹션·평가항목 추출 → 섹션별 자동검색 → **커버리지 표**(누락0)
3. [ ] **rfp-deck v2** = 무손실 조립(조립 지시서 → PPT 수동 / win32com COM 자동). python-pptx 재구성 금지(깎임)
4. [ ] **rfp-deck 포폴 글쓰기** — "RFP 100장 지옥 → 2축 RAG 재사용 자동화" 케이스 (데이터 sanitize, 회사자산 노출 X)
5. [ ] **라우드소싱 첫 발(출품)** — 서울디자인 AI영상(14일·선점·DDP권위) OR K포럼(6/22·VIVID). PHASE A 실행에 **공모 요강 필요**
6. [ ] **DB 오배치 10행 수동 삭제** — 노션 "유튜브 요약본 DB"(a0a1e01c)의 2026-06-15 ①~⑩
7. [ ] 보정점(rfp-deck): 내용검색 목차/표지 오염 다운랭크, 이미지-차트 인식(비전이 해결)
8. [ ] 공모전 목록 정렬 글리치(사용자 작업)

---

## 📍 파일·위치 맵
- 유튜브 정본: 노션 페이지 `373f60ad-716f-81d9-bc85-e6bccaa15adc` ("학습" 하위) — DB(`a0a1e01c`)는 레거시
- 학습 로드맵: 노션 `381f60ad-716f-81f9-802d-c3a9ab1df19b`
- **yt-rag**: `C:\Users\vacma\Desktop\apps\yt-rag\` (extract/embed/search, Gemini 임베딩)
- **rfp-deck**: `C:\Users\vacma\Desktop\apps\rfp-deck\` (extract/embed/search/vision_index) — **회사자산, .gitignore, commit 절대 X**. 입력 = [과거 제안서 폴더, 로컬 8개/965장]
- 라우드소싱: `vacax\active\loudsourcing\` — `workflow_v1.md`(v1.1), `consistency_protocol.md`, STATE/NEXT/LOG
- 시스템 수정: `vacax\CLAUDE.md`(반복·정체 원칙), `.claude\commands\council.md`(라운드0), `memory\feedback_no_looping_stale_answers.md`

---

## 🔑 핵심 결정·맥락 (다음 세션이 알아야)
- **생성 스택 = 프리미엄(~5만/월)**: 이미지 MJ v8.1+Ideogram / 영상 Kling 3.0+Runway Gen-4.5 / 음성 클로바더빙·음악 Suno Pro / 편집 Vrew+CapCut. **방법 = Image-First**(이미지서 일관성 고정 후 I2V). Veo3는 건별.
- **콘테스트 = 테스트베드+포폴(워크플로=본자산), 당선=로또 보너스, 본수익 X.** 30개 다 X, 1개 파이프라인 뽑고 곁다리. 하루 1.5h, 1순위(이직) 안 잠식.
- **Eval = 학습/포폴 차별화 레버** (남들 안 함, VacAX Validator 철학과 직결).
- **맴돌기 방지 룰 발효**: 반복요청="내 답 틀림" 신호 / 문서≠최신(3주+ 재검증) / council 라운드0 프레임점검.
- rfp-deck "구조 재활용"이 핵심(내용 달라도 레이아웃 맞으면 재사용) → 비전 태깅이 그걸 잡음.

---

## 다음 세션 시작법
새 채팅: "이 핸드오프 이어서" + 이 파일(`vacax/SESSION_HANDOFF.md`) 내용 붙이기 → ① rfp 색인 상태부터 확인 → 위 열린 액션 순서대로.
