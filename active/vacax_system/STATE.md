# VacAX System STATE

날짜: 2026-07-01
상태: Always-On 자가발전 루프 v1 구현 완료 + Headless 담당 채팅 구조로 보정
진행도: 100% (운영 규칙 반영 기준)

## 현재 상태

- Boot / Black Box / Learning Close 루프가 `AGENTS.md`, `CLAUDE.md`, `system/always_on_loop.md`에 연결됨.
- 별도 `VacAX Head` 채팅은 필수가 아님. 각 담당 채팅이 자기 프로젝트의 Head 역할을 겸함.
- `active/vacax_system/`은 상설 지휘 채팅이 아니라 공통 운영 프로토콜 기록 위치.
- 품질 점수표, stale 체크, 열린 창 회수, continuous improvement 기준이 시스템 문서로 추가됨.
- 주요 active 프로젝트에 `LEARNINGS.md`, `EVALS.md`가 추가되어 다음 작업부터 학습/평가 기록 가능.
- Head 채팅 전제는 제거. 실제 사용 데이터가 쌓일 때만 추가 개선.

## Blocker

- 커밋 전 민감정보 diff 점검 필요.
- 코인단타/AI부업/이력서포폴 담당 프로젝트 폴더는 시작 시 생성 필요.
- VoiceFit 커머스팩 실제 API 1회 생성 및 Supabase migration 확인 미완료.

## 다음 목표

각 담당 채팅을 별도 Head 없이 시작 가능하게 하고, 담당별 첫 Boot 때 필요한 active 폴더를 생성한다.
