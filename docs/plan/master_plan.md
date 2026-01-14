# JEJU-LOG 계획 요약 (현행 구현 기준)
마지막 업데이트: 2026-01-13

## 현행 구현 요약
| 항목 | 현행 구현 | 근거 |
| --- | --- | --- |
| 프론트엔드 | React + Vite UI | `frontend/src/` |
| 백엔드 API | Django + DRF | `backend/dialect_converter/` |
| 캡션 생성 | OpenAI `gpt-4o`, `gpt-4o-mini` | `backend/dialect_converter/content_generator.py` |
| 해시태그 생성 | OpenAI `gpt-4o-mini` + reverse geocode | `backend/dialect_converter/hashtag_chain.py` |
| 번역 | OpenAI `gpt-4o-mini` | `backend/dialect_converter/translation_loader.py` |
| 저장소 | SQLite + 파일 저장 | `backend/db.sqlite3`, `backend/data/` |

## 미구현/확인 필요
- 배포 자동화: Docker 템플릿은 추가됨. CI는 미정.

## 유지/정리 원칙
- 기획/발표 자료는 코드 기준으로만 유지합니다.
- 코드와 불일치하거나 가정만 존재하는 내용은 문서에서 제거하거나 TODO로 표시합니다.
