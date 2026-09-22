# 부업 툴박스

쿠팡/네이버쇼핑 셀러를 위한 개인용 AI 툴 대시보드.
단일 HTML 파일 + localStorage 기반, 서버 없음.

## 배포

- **배포 주소**: https://ndh3954-prog.github.io/shopping-toolbox-free/ (GitHub Pages, `main` 브랜치 `/ (root)`)
- **단축 URL (강의/공유용)**: https://tinyurl.com/budeop-toolbox
- 저장소: https://github.com/ndh3954-prog/shopping-toolbox-free
- 로컬 프로젝트 폴더: `~/shopping-toolbox-free` (main 파일은 `index.html`)
- 수정할 때: `index.html`을 고쳐서 커밋 후 `git push` 하면 1~2분 내 반영됨

## 기능

1. **상세페이지 제작기** — 플랫폼(쿠팡/네이버) x 카테고리별 규칙이 내장된 프롬프트로 상세페이지 초안을 AI로 생성
2. **썸네일 생성기** — 스타일 프리셋 기반 이미지 프롬프트로 썸네일 이미지 생성
3. **마진 계산기** — 원가·수수료·배송비를 입력하면 실제 마진과 추천 판매가를 실시간 계산 (API 호출 없음)

기타:

- 헤더의 **데이터 백업** — 기록을 JSON으로 내보내기/가져오기
- 헤더의 **네이버 데이터랩 ↗** — 쇼핑인사이트 페이지 바로가기
- 헤더의 **다크/라이트 모드** 전환
- **API 키 설정** 모달 안에 발급 가이드 링크 (OpenAI/Gemini/Grok)

AI 모델은 빠르고 가벼운 기본 모델로 고정되어 있음 (직접 다른 모델로 바꿀 수 없음).

## 아키텍처

- 서버 없이, 브라우저에서 사용자의 API 키로 각 모델사(OpenAI, Google Gemini, xAI Grok)에 **직접 fetch 호출**. 모든 데이터는 `localStorage`에만 저장됨
- `file://`로 더블클릭해서 열면 API 호출이 막힐 수 있음 → 로컬 서버나 실제 호스팅에 올려서 사용 권장

### localStorage 키 목록

| 키 | 용도 |
|---|---|
| `toolbox_api_keys` | API 키 |
| `toolbox_detailpage_history` | 상세페이지 생성 기록 (최대 100개) |
| `toolbox_thumbnail_history` | 썸네일 생성 기록 (최대 30개) |
| `toolbox_margin_history` | 마진 계산 기록 (최대 50개) |
| `toolbox_theme` | 다크/라이트 테마 설정 |

업데이트를 배포해도 이 키들의 이름을 바꾸지 않는 한, 사용자 브라우저에 저장된 데이터는 그대로 유지됨.

## 유지보수 메모

이 폴더는 `~/shopping-toolbox`(전체 기능 버전)에서 일부 모듈만 남기고 손으로 정리해서 만든 경량 버전. 전체 버전에 기능을 추가/수정한 뒤 이쪽에도 반영하려면, 아래 3개 모듈(상세페이지 제작기·썸네일 생성기·마진 계산기)과 공통 UI(헤더, 설정 모달, 데이터 백업, API 키 가이드)에 해당하는 변경 사항만 골라서 다시 옮겨야 함. 전체 버전에만 있는 모듈(포맷 관리, CS 상담원, 관리자 페이지, Figma 갤러리, AI 배너 디자이너, AI 디자인 스튜디오)은 이 버전에 없음.
