# AI API 실전 교훈

## GPT-4o Vision
- **외모 분석 요청 → content filter 전량 거부** ("I'm sorry, I can't assist with that")
- 사람 얼굴 사진 + "분석해줘" 조합이 트리거
- 프롬프트 표현 바꿔도 구조적으로 막힘 → 해결 불가

## Claude Sonnet (Anthropic)
- 외모 분석 가능하나 **Anthropic 결제 버그 존재** (2026-05 기준)
- 결제 수단 등록해도 API 호출 시 billing error 발생
- 해결 전까지 사용 불가

## Gemini 2.0 Flash (Google)
- **외모 분석 content filter 없음** → 현재 채택
- 무료 쿼터: 15 RPM, 하루 1,500회 → 테스트 과정에서 소진 주의
- 재시도 로직 있으면 한 번에 3~6회 요청 → 쿼터 빨리 소진
- **Flutter SDK(`google_generative_ai`)로 직접 호출 권장** — Firebase Functions 불필요

## Firebase Functions + AI 조합
- 배포마다 5~10분 소요 → 디버깅 사이클 느림
- Secret Manager BOM 버그: PowerShell pipe로 시크릿 등록 시 BOM 문자 자동 추가
  - 해결: 코드에서 `.replace(/^﻿/, '').trim()` 방어 처리
  - 또는 파일로 쓸 때 `New-Object System.Text.UTF8Encoding $false` 명시
- **결론: AI 직접 호출이 가능하면 Firebase Functions 레이어 건너뛸 것**

## API 키 관리
- 채팅창에 API 키 붙여넣으면 로그에 노출됨 → 즉시 폐기 필요
- PowerShell `echo` 파이프 → BOM 붙음
- 안전한 등록법: 메모장에 UTF-8(BOM 없음)으로 저장 후 파일 경로 전달
