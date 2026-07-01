# VacAX Stale Check v1

목적: "파일이 단일 진실" 원칙이 깨지는 순간을 빨리 잡는다.

## 시작 시 점검

프로젝트 시작/재개 시 아래를 확인한다.

1. `active/[project]/STATE.md` 마지막 갱신일
2. `active/[project]/NEXT.md` 마지막 갱신일과 마감 날짜
3. `active/[project]/LOG.md` 마지막 줄
4. `code_path.txt`가 있으면 코드 폴더의 최근 수정일 또는 git status
5. 코드 변경일이 운영문서 변경일보다 늦은지

## stale 판정

| 상태 | 기준 | 행동 |
|---|---|---|
| fresh | 운영문서가 코드/작업보다 최신 | 그대로 진행 |
| soft stale | 운영문서 7일 이상 미갱신 또는 LOG가 최근 작업을 반영 안 함 | Boot에서 경고, 작업 전 1줄 보정 |
| hard stale | 코드 변경이 운영문서보다 최신이거나 NEXT 마감이 지남 | 작업 전 STATE/NEXT/LOG 먼저 보정 |
| unknown | 코드 경로 없음, 외부 채팅만 있음 | `system/open_thread_recovery.md`로 회수 |

## 출력 형식

```text
[Stale Check]
STATE 기준일:
NEXT 기준일:
LOG 마지막 작업:
코드 상태:
판정:
먼저 보정할 문서:
```

## 코드 변경 감지 기준

가능하면 아래 순서로 확인한다.

1. 코드 repo의 `git status --short`
2. 코드 repo의 최신 commit/date
3. 코드 폴더의 최근 수정일
4. 자율작업 보고서 존재 여부

코드 변경이 있는데 운영문서가 오래됐으면 "작업 금지"가 아니라 "보정 먼저"다.

## NEXT 만료 처리

NEXT에 지난 날짜가 있으면 아래 중 하나로 즉시 정리한다.

- 완료: LOG에 결과 추가, NEXT에서 제거
- 미완: 새 기한과 이유 추가
- 폐기: DECISIONS 또는 LOG에 폐기 이유 1줄

기한 없는 `[CEO] 대기`는 금지한다. 반드시 날짜나 다음 확인 조건을 붙인다.

## 전체 audit와의 차이

Stale Check는 가벼운 시작 점검이다. 전체 audit가 아니다.

- Stale Check: 매번, 1~3분
- 전체 audit: 주 1회 또는 요청 시, 깊게
