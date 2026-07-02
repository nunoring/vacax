# HairFit Sample 5 Real Generation Test

Date: 2026-07-01

## Scope
synthetic 남성 얼굴 5장으로 실제 헤어 합성 품질을 확인했다. 랜덤 인터넷 얼굴은 사용하지 않았다.

## Final Output
- Input contact: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-input-contact-2026-07-01.jpg`
- Final comparison: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-real-comparison-2026-07-01.jpg`

## Cost
- 최종 세트 기준 성공 호출: 5회, 기록 비용 $0.20
- 개선/재시도 포함 성공 호출: 12회, 기록 비용 $0.48
- 추가 smoke: sample 4 `semi_wolf` reference crop 검증 1회, 기록 비용 $0.04
- 실패/fallback: 2회
  - sample 1 soft ivy: `fetch failed`, 재시도 성공
  - sample 2 aspect `4:5`: Replicate 422, `auto`로 변경 후 성공
- 모든 테스트 후 `npm.cmd run hairfit:mock` 실행, proxy `realEnabled=false` 확인

## Final Scores
| Sample | Style | Face keep | Hair natural | Consult use | Notes |
|---|---:|---:|---:|---:|---|
| 1 | Soft ivy | 4/5 | 4/5 | 4/5 | 같은 사람으로 보임. 약한 피부/윤곽 정돈 있음. |
| 2 | See-through dandy | 4/5 | 4/5 | 4/5 | `auto` 비율 후 얼굴 길어짐 완화. |
| 3 | As perm | 4.5/5 | 4.5/5 | 4.5/5 | 가장 안정적. 상담용으로 바로 사용 가능. |
| 4 | Semi leaf | 3.5/5 | 4/5 | 3.5/5 | 긴 기장/리프 계열은 얼굴 드리프트가 남음. |
| 5 | Texture crop | 4/5 | 4/5 | 4/5 | 얼굴 유지와 스타일 변화 균형 양호. |

## Result
- Pass 기준: 얼굴 유지 4/5 이상 최소 3장, 상담 사용성 3/5 이상 최소 4장.
- 결과: 얼굴 유지 4/5 이상 4장, 상담 사용성 3/5 이상 5장.
- 판정: synthetic 5장 기준 통과.
- CEO 육안 검수: 완전 같은 사람은 아니지만 얼추 비슷함. 상담용 MVP로는 통과, "완벽한 동일인 보존"으로 말하면 과장.

## Product Changes From Test
- `server/referenceTransfer.mjs`: GPT Image 계열 기본 `aspect_ratio`를 `2:3`에서 `auto`로 변경. 원본/결과 크기가 같아져 얼굴 인상 왜곡이 줄어듦.
- `public/style-library/men/semi_leaf/reference.webp`: 얼굴이 크게 보이는 레퍼런스를 헤어 crop reference로 교체. 원본은 `reference.face-included.backup.webp`로 보존.
- `public/style-library/men/leaf/reference.webp`: 얼굴 노출이 적은 hair-only reference로 교체.
- `public/style-library/men/semi_wolf/reference.webp`: 얼굴 노출이 적은 hair-dominant crop reference로 교체.
- `scripts/run-sample5-once.mjs`: 1컷 단위 실제 생성 테스트 스크립트 추가.

## Extra Long-Hair Smoke
- Input: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-face-04.png`
- Output: `C:\Users\vacma\Desktop\apps\hairfit-mvp\run_logs\sample5-real-04-semi_wolf-2026-07-01.png`
- Score: 얼굴 인상 유지 4/5, 헤어 자연스러움 4/5, 상담 사용성 4/5.
- 판정: `semi_wolf`는 완전 동일인 보장은 아니지만 상담용 1컷 smoke 기준 통과.

## Remaining Risk
- 실제 고객 사진 기준은 아직 아님.
- 완전 동일인 수준은 아님. 결과 문구는 "상담용 참고 이미지"로 제한해야 함.
- 긴 기장/리프 계열은 reference 리스크를 줄였지만, 실제 고객 사진 기준으로는 여전히 보수적으로 검수해야 함.
- 미용사 피드백 전이라 상담 문장 현장감은 미검수.
