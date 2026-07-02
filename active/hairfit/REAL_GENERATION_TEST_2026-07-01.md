# HairFit Real Generation Test

Date: 2026-07-01

## Scope
실제 GPT/Replicate 생성 품질 1차 확인. 실존 고객 사진이 아니라 synthetic 테스트 얼굴 1장 기준.

## Cost Guard
- 실제 호출: 2회
- Provider: `gpt-image-2` via Replicate
- 기록 비용: $0.04 x 2 = $0.08
- 테스트 후 `npm.cmd run hairfit:mock` 실행, proxy `realEnabled=false` 확인

## Inputs
- Customer: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\real-test-customer-synthetic-2026-07-01.png`
- Style: 시스루 댄디컷
- Reference: `public/style-library/men/see_through_dandy/reference.webp`

## Outputs
- v1: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\real-gpt-once-see-through-dandy-2026-07-01.png`
- v2: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\real-gpt-once-see-through-dandy-v2-2026-07-01.png`
- Compare: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\real-gpt-once-comparison-2026-07-01.jpg`

## Evaluation
v1:
- 얼굴 유지: 3.5/5. 눈·코·입은 유지되지만 얼굴이 살짝 정돈되고 갸름해진 느낌.
- 헤어 자연스러움: 4/5. 시스루 댄디 흐름은 자연스러움.
- 상담 사용성: 4/5. 손님 앞에서 보여줄 수 있는 수준.

v2:
- 얼굴 유지: 4/5. v1보다 윤곽/피부 보정 느낌이 줄어 통과선.
- 헤어 자연스러움: 4/5. 앞머리·볼륨이 상담용으로 충분함.
- 상담 사용성: 4/5. "이 정도 앞머리 흐름이면 인상이 부드러워진다"는 상담 근거와 함께 사용 가능.
- CEO 육안 검수: 같은 사람으로 보인다고 판단.

## Code Change From Test
- `server/prompt.mjs`: 얼굴 윤곽, 귀 위치, 피부 보정 금지, crop/framing 유지 조건 강화.
- `src/lib/styleLibrary/styleLibrary.ts`: 스타일 negative prompt에 face slimming, skin smoothing, changed crop 등 추가.

## Remaining Risk
- synthetic 1장 기준이라 실제 고객 사진 품질을 대표하지 않음.
- 출력 비율이 원본과 달라 보이면 얼굴 인상이 달라 보일 수 있음.
- 실제 샘플 5장 테스트 전에는 "실사용 품질 통과"로 단정하지 않음.
