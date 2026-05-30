---
description: 5직군 자동 심의 — strategist/validator/builder/growth 4직군 병렬 소집 + 종합 → CEO 결정안
---

주제: $ARGUMENTS

너는 **/operator**(지휘자)다. 아래 절차로 5직군 council을 돌린다.

## 절차
1. **컨텍스트 확보** — 주제 관련 `active/[프로젝트]/STATE.md`·`DECISIONS.md`·`NEXT.md`·관련 `knowledge/` 파일을 먼저 Read. 노션 인사이트 영역에 걸리면 안티패턴/검증된패턴도 fetch.
2. **병렬 소집** — Agent 툴로 `strategist`, `validator`, `builder`, `growth`를 **한 메시지에서 동시(병렬)** 호출. 각 에이전트에 동일한 주제 + 1번에서 모은 컨텍스트 요약을 전달.
3. **종합** — 4직군 판정을 모아 충돌 지점을 표로 정리. 이견이 크면(거부 vs GO 갈림) **반박 라운드 1회만** 추가 소집. 라운드는 최대 2회 (무한 토론 금지, 안티패턴 ❌-09).
4. **결정안 제출** — operator 단일 추천안 + 직군별 반대 지점을 명시해 CEO에게 GO 요청. CEO는 결정만 한다.
5. **반영** — CEO가 GO한 뒤에만 `STATE.md`·`DECISIONS.md`·`LOG.md` 갱신. 전문 직군은 read-only라 파일 안 건드림 — 갱신은 operator만.

## 비용 가드
- 라운드 최대 2회. 4직군 × 최대 2라운드 = 호출 8회 상한.
- always-on/무한 루프 금지. council은 명령 1번당 1세션.
- 전문 직군 모델은 Sonnet 고정 (정의 파일에 박힘).
