# JEJU-LOG 로컬 설정/실행
마지막 업데이트: 2026-01-13

## 개요
이 문서는 로컬 개발 환경에서 JEJU-LOG를 실행하는 절차를 정리합니다.

## 사전 준비
- Node.js + npm
- Python + pip
- 선택: Python 가상환경 (venv 등)

## 의존성 설치
### 통합 설치
```bash
npm run install:all
```

### 개별 설치
```bash
# Frontend
npm install

# Backend
cd backend
pip install -r requirements.txt
```

## 환경 변수 설정
### backend/.env
```dotenv
SECRET_KEY=change-me
DEBUG=True
OPENAI_API_KEY=your-openai-key
OPENWEATHER_API_KEY=your-openweather-key
TEXT_ONLY_CAPTION=false
```

### frontend/.env
```dotenv
VITE_GEMINI_API_KEY=your-gemini-key
```

- 민감 정보는 절대 커밋하지 마세요.
- `OPENWEATHER_API_KEY` 미설정 시 기본 날씨 값으로 동작합니다.

## 로컬 실행
```bash
npm run dev
```

- Frontend: `http://localhost:5173`
- Backend: `http://localhost:8000`
- Swagger: `http://localhost:8000/api/docs/`

## Docker 실행
```bash
docker compose up --build
```

- `docker-compose.yml`은 `backend/Dockerfile`, `frontend/Dockerfile`을 사용합니다.
- 실행 전 `backend/.env`, `frontend/.env`를 준비하세요.

## 개별 실행
- `npm run dev:front`
- `npm run dev:back`

## 빌드/프리뷰
```bash
npm run build
npm run --workspace=frontend preview
```

## 데이터/저장 위치
| 항목 | 경로 |
| --- | --- |
| SQLite DB | `backend/db.sqlite3` |
| 최종 결과 이미지 | `backend/data/final_result/` |

## 백엔드 DB 초기화
- 마이그레이션이 필요하면 `backend/`에서 아래 명령을 실행하세요.
```bash
python manage.py migrate
```
