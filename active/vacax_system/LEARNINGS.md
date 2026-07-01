# VacAX System LEARNINGS

이 프로젝트에서 나온 교훈을 저장한다. 2회 이상 반복되면 `knowledge/patterns.md` 후보, 3회 반복되면 `system/continuous_improvement.md` 기준으로 운영 규칙 승격 후보.

## 목록

2026-07-01 | 성공 | 자동 가동은 무거운 전체 audit가 아니라 얇은 Always-On 학습 루프가 맞다. | Boot/Black Box/Learning Close만 상시 실행하고 audit는 조건부로 유지.
2026-07-01 | 성공 | 기록만 쌓으면 부족하고, 기록 → 평가 → 패턴 → 규칙 → 다음 작업 적용까지 닫혀야 시스템이 강해진다. | 종료 루틴에서 Quality Score 직후 Continuous Improvement 후보 판정.
2026-07-01 | 성공 | VacAX 없이 진행한 다른 창도 회수 요약만 흡수하면 버리지 않아도 된다. | `system/open_thread_recovery.md`로 1일 최대 2개 창만 회수.
2026-07-01 | 실패/보정 | 별도 Head 채팅을 만들라고 설명하면 VacAX의 자동 기록/회수 목적과 충돌한다. | Head는 상설 채팅이 아니라 필요 시 실행되는 통합 패스다. 각 담당 채팅이 자기 프로젝트 Head 역할을 겸한다.
