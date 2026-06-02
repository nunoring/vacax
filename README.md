# VacAX — 1인 AI 워크플로우 스튜디오

> AI를 도구로 쓰는 게 아니라, AI와 함께 회사를 운영하는 실험

---

## 무엇을 만드는가

AX/AI 기획 포트폴리오 4개월 프로젝트.  
혼자서 전략가·검증자·개발자·마케터·오케스트레이터를 AI와 함께 돌린다.

현재 진행 중인 프로젝트: VoiceFit · 라우드소싱 · 주식 트레이딩 리서치

---

## 시스템 구조

```
CEO (임용후)
  │
  ├── Claude Code (메인 오케스트레이터)
  │     ├── /council   — 5역할 찬반토론 의사결정
  │     ├── /audit     — 시스템 자동 점검
  │     ├── /watch     — 영상 분석
  │     └── /deep-research
  │
  ├── Notion          — 인사이트 라이브러리 · 프로젝트 문서
  └── GitHub          — 운영 기록 (vacax) · 코드 (apps 별도)
```

**핵심 원칙**: 모든 상태는 파일에 기록. AI 기억에 의존 금지.

---

## 직군 시스템

| 역할 | 담당 |
|------|------|
| 🔴 Challenger | 반론·리스크 발굴 |
| 🟢 Advocate | 기회·강점 발굴 |
| 🟡 Realist | 실행 가능성 판단 |
| 🔵 Market | 고객·시장 관점 |
| ⚪ Synthesizer | 수렴·결정안 도출 |

중요 결정마다 `/council`로 토론 → CEO 최종 확정.

---

## 운영 흔적

- `active/` — 진행 중 프로젝트별 STATE·NEXT·DECISIONS·LOG
- `knowledge/` — 축적된 교훈 (AI API·Flutter·제품·마케팅)
- `system/` — 공통 템플릿·운영 규칙

---

## 만든 사람

임용후 · AX/AI 기획 이직 준비 중  
공공 B2B 사업기획 2년 → AI 워크플로우 설계로 전환  
`vacman950@gmail.com`
