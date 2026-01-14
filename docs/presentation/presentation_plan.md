# JEJU-LOG 발표 구성안 (현행 구현 기준)
마지막 업데이트: 2026-01-13

## 발표 구성
| 파트 | 내용 | 근거 |
| --- | --- | --- |
| 문제 정의 | 장소성/기록 문제 | 기획 요약 |
| 솔루션 | 캡션/해시태그/번역 | `docs/spec/functional-spec.md` |
| 기술 | Django API + OpenAI | `backend/dialect_converter/` |
| 데모 | `/api/dialect/*` 호출 흐름 | `frontend/vite.config.js` |
| 한계 | CI 미정, 관계 추론 입력 비활성 | `docs/plan/master_plan.md` |

## 데모 흐름
1. 프론트 실행: `npm run dev`
2. `/api/dialect/generate-captions-batch/` 호출
3. 결과 캡션 확인
4. Cognito Identity Pool 기반으로 프론트에서 S3로 직접 PNG 업로드(PutObject)
