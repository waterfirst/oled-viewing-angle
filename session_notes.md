# 세션 정리 노트 — 2026-05-03

## 완료 작업

### 1. 렛유인 바이브코딩 1강 스크립트
- `lecture01_script.md` 생성 (1시간 분량, 9개 섹션)
- edge-tts로 TTS 음성 생성 후 전송 완료 (파일은 EC2에서 삭제)

### 2. Culture Voyager (문화저널)
- 교토 매거진 커버 이미지 삽입 (`assets/e1_kyoto.jpg`)
- 최신 발행순 정렬 (교토 2026.05 → 쇼생크 2026.05)
- 교토 여행편: YouTube 에러 수정, R leaflet 지도 추가, 목차 돌아가기 버튼
- URL: https://waterfirst.github.io/culture-voyager/

### 3. Insight Lab
- 최신 발행순 정렬 — 11개 발행 완료 글을 "최신 발행" 섹션으로 이동
- 번역 시스템 data-k 속성으로 리팩터링
- URL: https://waterfirst.github.io/insight-lab/

### 4. Chimera AI (키메라)
- 최신 발행순 정렬 — 6개 주간/특별 보고서 날짜순 통합
- URL: https://waterfirst.github.io/chimera-ai/

### 5. Alpha Hunter (알파헌터)
- 최신 발행순 정렬 — 7개 발행물 날짜순 통합
- URL: https://waterfirst.github.io/alpha-hunter/

### 6. R leaflet 패키지 도입
- JS Leaflet → R leaflet 코드블록으로 교체 (CLAUDE.md에 규칙 반영)
- 시스템 의존성: `libgdal-dev libudunits2-dev libgeos-dev libproj-dev cmake`
- 참고: https://bigdata-anlysis.tistory.com/34

## EC2 정리
- 대용량 파일 145MB+ 삭제 (mp3, PDF, 중복 HTML, PNG)
- /tmp 클론 저장소 전부 삭제
- 메모리: 62% 사용 (75% 이하 유지)

## CLAUDE.md 업데이트 항목
- Culture Voyager 관련 프로젝트 추가
- R leaflet 지도 규칙 추가 (JS 직접 삽입 금지)
- YouTube iframe 직접 사용 규칙 추가
- 저널 공통 규칙 추가 (발행일 역순 정렬, 여행 콘텐츠 필수 요소)

## 다음 세션 참고
- 새 콘텐츠 발행 시 각 저널의 "최신 발행" 섹션 맨 위에 추가
- 교토 QMD 소스: `culture-voyager/output/e1_kyoto.qmd`
- 목차 돌아가기 템플릿: `culture-voyager/output/_nav_back.html`
