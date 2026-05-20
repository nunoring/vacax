# Flutter 앱 개발 실전 교훈

## 아키텍처
- **Firebase Functions 레이어는 AI 직접 호출 가능하면 제거** — 배포 사이클 느리고 환경변수 관리 복잡
- `kDevMode = true` 상태로 출시하면 수익 0원 — 출시 직전 체크리스트 필수
- RevenueCat 테스트 키 → 프로덕션 키 교체가 출시의 실질적 마지막 단계

## ML Kit 얼굴 분석
- `face_ratio`, `eye_gap_ratio`, `eye_angle` 키로 faceData에 저장됨
- 다중 사진 평균값으로 안정성 향상 가능 (`analyzeMultiplePhotos`)
- 오프라인 동작, 무료 → AI 대신 수치 계산에 활용할 것

## 폴백 설계
- Flutter 폴백(`_buildFallbackResponse`)과 Firebase 폴백(`getFallbackResponse`) 두 레이어 분리
- Flutter 폴백에 `first_impression`, `three_factor`, `makeup_steps`, `fashion_looks` 빠지면 Pro 페이지 먹통
- **폴백은 Pro 전체 구조를 포함해야 함**

## 자동 승인 설정
- `~/.claude/settings.json`에 `permissions.allow` 배열로 Read/Write/Edit/Bash/PowerShell 추가
- 프로젝트마다 재설정 불필요 — 글로벌 설정

## 이미지 저작권
- 셀럽 사진 앱에 직접 내장 → 저작권 위반
- 대안: 이름 표시 + 네이버/Google 이미지 검색 링크 연결
- AI 생성 일러스트는 저작권 문제 없음
