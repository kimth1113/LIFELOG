# JEJU-LOG 기능 명세 (현행 구현 기준)

마지막 업데이트: 2026-01-13

## 범위

### 포함

- 번역, 해시태그 추천, 캡션 생성
- 위치/날씨 조회 API
- 최종 결과 이미지 저장

### 제외

- 배포 자동화/CI
- 결제/로그인/권한 관리

## 시스템 구성

| 구분      | 기술                             | 근거                                                |
| --------- | -------------------------------- | --------------------------------------------------- |
| Frontend  | React + Vite                     | `frontend/package.json`, `frontend/vite.config.js`  |
| Backend   | Django + DRF                     | `backend/manage.py`, `backend/jeju_log/settings.py` |
| LLM       | OpenAI (`gpt-4o`, `gpt-4o-mini`) | `backend/dialect_converter/content_generator.py`    |
| 위치/날씨 | Reverse Geocode + OpenWeatherMap | `backend/dialect_converter/views.py`                |
| DB        | SQLite                           | `backend/jeju_log/settings.py`                      |

## 데이터/저장 경로

| 항목        | 경로                               | 설명                              |
| ----------- | ---------------------------------- | --------------------------------- |
| SQLite DB   | `backend/db.sqlite3`               | Django 기본 DB                    |
| 결과 이미지 | S3 `lifelog-upload-prod/uploads/*` | 프론트에서 직접 업로드(PutObject) |

## API 명세 요약

| 엔드포인트                              | 메서드 | 타입      | 필수 필드                 | 비고                                                          |
| --------------------------------------- | ------ | --------- | ------------------------- | ------------------------------------------------------------- |
| `/api/`                                 | GET    | JSON      | -                         | API 정보                                                      |
| `/api/docs/`                            | GET    | HTML      | -                         | Swagger UI                                                    |
| `/api/dialect/translate/`               | POST   | JSON      | `text`, `target_language` | en/ja/zh만 허용                                               |
| `/api/dialect/recommend-hashtags/`      | POST   | JSON      | `relationship`            | `location`, `dong`, `latitude`, `longitude`는 선택            |
| `/api/dialect/get-location-info/`       | POST   | JSON      | `latitude`, `longitude`   | reverse geocode + OpenAI 보정                                 |
| `/api/dialect/get-weather/`             | POST   | JSON      | `latitude`, `longitude`   | OpenWeatherMap 미설정 시 기본값                               |
| `/api/dialect/generate-captions-batch/` | POST   | multipart | `spot`, `relationship`    | 최대 3장 입력                                                 |
| (프론트) S3 직접 업로드                 | -      | -         | -                         | Cognito Identity Pool 기반으로 프론트에서 S3로 직접 PutObject |

## 주요 동작 흐름

1. 프론트에서 `/api/dialect/*` 호출 (Vite 프록시 사용)
2. 백엔드에서 OpenAI API 호출 및 처리
3. 결과를 프론트로 반환 또는 S3에 저장(프론트에서 직접 업로드)

## TODO / 확인 필요

- 현재 확인 필요 항목 없음.
