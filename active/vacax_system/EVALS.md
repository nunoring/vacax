# VacAX System EVALS

이 프로젝트의 검증 기준과 회귀 테스트를 저장한다.

## 현재 통과 기준

- [x] 시작 시 Boot 기준 문서 존재
- [x] 작업 중 Black Box 기록 기준 존재
- [x] 종료 시 Learning Close 기준 존재
- [x] 품질 점수표 존재
- [x] stale check 기준 존재
- [x] 열린 창 회수 프로토콜 존재
- [x] continuous improvement 기준 존재
- [x] 별도 Head 채팅 없이 담당 채팅이 자기 프로젝트 기록을 닫는 원칙 존재
- [ ] 실제 다음 담당 채팅에서 Boot가 해당 `active/[project]`를 정상 인식하는지 확인

## 회귀 테스트

```text
2026-07-01 | rg로 Always-On / Stale Check / Quality Score / continuous_improvement 참조 확인 | 통과 | 문서 연결 확인
2026-07-01 | git status --short 확인 | 통과 | 변경 파일 다수 존재, 커밋 보류
2026-07-01 | Headless 담당 채팅 원칙 문서화 | 통과 | `system/always_on_loop.md`, `system/open_thread_recovery.md`
```

## Quality Score 기록

```text
2026-07-01 | 28/30 | Golden 후보, 실제 운영 재현 전 전역 golden 등재 보류 | 다음 담당 채팅 Boot와 종료 기록으로 검증
```

## System Improvement 기록

```text
2026-07-01 | 기록만 쌓고 개선 루프가 닫히지 않는 문제 | system/continuous_improvement.md, AGENTS.md, CLAUDE.md, system/quality_scorecard.md | 다음 종료 루틴에서 개선 후보가 실제로 작성되는지 확인
```
