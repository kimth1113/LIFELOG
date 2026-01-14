# JEJU-LOG 발표 마스터 (현행 구현 기준)
마지막 업데이트: 2026-01-13

## 핵심 메시지
- 사진 한 장에서 캡션/해시태그/번역까지 자동화
- 프론트(Vite) + 백엔드(Django) + OpenAI API의 실제 구현 흐름

## 기술 근거 매핑
| 기능 | 구현 근거 |
| --- | --- |
| 캡션 생성 | `backend/dialect_converter/content_generator.py` |
| 해시태그 생성 | `backend/dialect_converter/hashtag_chain.py` |
| 번역 | `backend/dialect_converter/translation_loader.py` |
| 위치/날씨 | `backend/dialect_converter/views.py` |
| API 라우팅 | `backend/dialect_converter/urls.py` |
| 프론트 호출 | `frontend/src/utils/translateApi.js` |

## 발표 아웃라인 (예시)
1. 문제 정의: 장소성과 기록의 부재
2. 솔루션 개요: 사진 기반 자동 캡션/해시태그
3. 시스템 구성: React + Django + OpenAI API
4. API 흐름: `/api/dialect/*` 요청/응답
5. 위치/날씨 보정: 좌표 기반 API 처리
6. 데모 시나리오: 촬영 → 해시태그 → 캡션 → 저장
7. 한계/다음 단계: 배포 자동화, 관계 추론 고도화
