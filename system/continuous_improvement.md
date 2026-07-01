# VacAX Continuous Improvement Loop v1

목적: 작업 결과물 품질과 VacAX 운영 시스템을 매 세션 조금씩 개선한다. 단, 새 직군/Skill/복잡한 구조를 만들지 않고 기존 파일에 최소 변경으로 흡수한다.

## 자동 실행 시점

- 작업 종료 루틴에서 `Quality Score` 작성 직후
- 외부용 결과물이 반려됐을 때
- CEO가 "같은 말", "맴돈다", "비효율", "결과물 맘에 안 듦"이라고 말했을 때
- `/audit` 또는 "시스템 점검" 실행 시

## 입력 신호

아래 중 하나라도 있으면 개선 후보를 만든다.

| 신호 | 의미 | 우선 기록 위치 |
|---|---|---|
| Quality Score 17점 이하 | 산출물/운영 실패 | `knowledge/failures.md` |
| 같은 실패 2회 | 재발 위험 | `knowledge/patterns.md` 안티패턴 후보 |
| 같은 실패 3회 | 시스템 규칙 필요 | `AGENTS.md`/`CLAUDE.md` 또는 프로젝트 `RULES.md` |
| Golden 후보 2회 | 재사용 가능 | `knowledge/goldens.md` |
| Golden 재현 3회 | 검증된 패턴 | `knowledge/patterns.md` VP 후보 |
| 외부용 결과물 반려 | 품질 기준 부족 | `knowledge/quality-bar.md` |
| CEO가 직접 교정 | AI 판단 실패 | `knowledge/patterns.md` 또는 관련 knowledge |
| 반복 수작업 발생 | 자동화/템플릿 후보 | `system/templates/` 또는 해당 프로젝트 문서 |

## 개선 대상 선택

항상 가장 낮은 레벨부터 고친다.

1. 한 프로젝트만 해당 → `active/[project]/RULES.md` 또는 `LEARNINGS.md`
2. 여러 프로젝트에 재사용 → `knowledge/patterns.md`, `failures.md`, `goldens.md`
3. 모든 세션에 적용 필요 → `system/*.md`
4. 에이전트 행동 자체를 바꿔야 함 → `AGENTS.md`/`CLAUDE.md`

`AGENTS.md`/`CLAUDE.md`는 최후 수단이다. 1회성 취향, 임시 실험, 아직 검증 안 된 가설은 올리지 않는다.

## 자동 개선 절차

```text
1. 신호 포착
2. 실패/성공을 한 줄로 정의
3. 반복 횟수 판정
4. 가장 낮은 레벨의 문서 선택
5. 1~3줄 규칙 또는 체크 항목으로 추가
6. 다음 세션에서 자동 적용될 트리거 명시
7. LOG 또는 종료 요약에 변경 파일 기록
```

## 개선 기록 형식

```text
[System Improvement]
신호:
원인:
변경:
적용 트리거:
다음 검증:
```

## 품질 개선 게이트

문서에 규칙을 추가하기 전 아래 4개를 통과해야 한다.

- 재현 가능: 다음 세션의 AI가 같은 상황을 알아볼 수 있는가
- 실행 가능: "조심"이 아니라 구체 행동으로 쓰였는가
- 최소 변경: 기존 루프를 깨지 않고 붙는가
- 검증 가능: 다음 결과물에서 성공/실패를 확인할 기준이 있는가

하나라도 실패하면 규칙 승격 대신 `LOG.md` 또는 `LEARNINGS.md` 후보로만 남긴다.

## 금지

- 새 직군/Skill 추가 제안
- `apps` 코드 폴더를 운영 시스템 개선 명목으로 수정
- 검증 안 된 1회성 취향을 전역 규칙으로 승격
- 큰 구조 변경을 council/CEO 확인 없이 자동 적용
- 운영 문서를 길게 늘려서 다음 세션 로딩 비용을 키우기
