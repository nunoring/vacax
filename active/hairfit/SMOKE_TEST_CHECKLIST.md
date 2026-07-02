# HairFit Smoke Test Checklist

Updated: 2026-07-01

## Scope
포트폴리오 패키징 제외. 앱 기능/완성도 검증만 다룬다.

## Cost Guard
- 기본은 `npm.cmd run hairfit:mock`.
- 실제 생성은 CEO 승인 전 실행 금지.
- 실제 생성 승인 시 1컷만 실행하고 호출 횟수/비용/provider를 기록.

## Common Checks
- Build: `npm.cmd run build`
- Asset: `npm.cmd run hairfit:check-assets`
- Console: browser error/warn 없음
- Proxy: mock 모드 `realEnabled=False`
- Empty/fallback: 사진 없음 또는 생성 실패 시 빈 화면 없음

## Flow A. AI 추천 3컷
1. 홈 -> 새 상담 시작
2. 필수 동의 2개 체크
3. 사진 없음 -> 샘플로 먼저 보기
4. 성향 입력 일부 선택
5. 자동 추천 선택
6. 결과 화면 확인
   - 3개 카드 표시
   - 각 카드 이미지가 SVG placeholder가 아님
   - `손님에게 이렇게` 표시
   - `얼굴 분석 근거` 표시
   - `근거 보기` 3개 표시
7. 1개 선택 -> 저장
8. 상세 기록 확인
   - 고객명 표시
   - 선택 스타일 표시
   - 상담 메모 표시
   - 원본 사진 저장 안 함 표시

## Flow B. 레퍼런스/미용사 선택
1. 홈 -> 새 상담 시작
2. 필수 동의 2개 체크
3. 사진 없음 -> 샘플로 먼저 보기
4. 레퍼런스 헤어 적용 선택
5. HairFit 기본 스타일 9종 노출 확인
6. 1개 스타일 선택
7. 결과 화면 확인
   - 원본/레퍼런스/적용 비교 표시
   - 레퍼런스와 적용 이미지가 선택 스타일로 표시
   - 손님 사진 없을 때 SVG 적용 placeholder 대신 스타일 미리보기 표시
8. 저장 화면 확인
   - 결과 품질 체크가 바로 보임
   - 얼굴 유지/유사도/자연스러움/상담 사용성 1~5점 입력 가능
9. 상세 기록 확인
   - 평가 점수 표시
   - 얼굴 유지 4점 이상이면 통과 표시
   - provider가 `미리보기 · 스타일 에셋`처럼 읽힘

## Sample 5 Photo Test
실제 또는 테스트용 얼굴 사진 5장 확보 후 실행.

각 샘플마다 기록:
- 샘플 ID
- 사진 조건: 정면/각도/조명/얼굴 크기
- 얼굴 분석 confidence: measured / estimated / mock
- 추천 3컷 표시 여부
- 문장 반복 여부
- 얼굴 유지 점수
- 헤어 자연스러움 점수
- 상담 사용성 점수
- 실패 시 fallback 정상 여부

통과 기준:
- 5장 중 5장 모두 빈 화면 없음
- 5장 중 4장 이상 상담 사용성 3/5 이상
- 실제 생성 테스트 시 얼굴 유지 4/5 이상인 샘플이 최소 1개
