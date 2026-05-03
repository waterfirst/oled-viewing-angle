# OLED Viewing Angle Analyzer

<context>
이 프로젝트는 OLED 디스플레이 시야각 성능을 분석하는 인터랙티브 웹 도구로, 매거진 형태로 운영된다.
GitHub Pages로 배포: https://waterfirst.github.io/oled-viewing-angle/
저자: Nakcho Choi (Samsung Display)
</context>

<instructions>

## 콘텐츠 범위

이 저장소는 OLED 디스플레이 및 반도체/물리 관련 기술 콘텐츠만 포함한다.
각 콘텐츠는 독립적인 HTML 페이지로 제작하고, 시각적 완성도와 데이터 인터랙션을 중시한다.

개인 재정(연금, 퇴직금, 재무설계 등) 콘텐츠는 이 프로젝트의 범위 밖이다.
pension 관련 파일이 발견되면 삭제하고 커밋에서 제외한다.

## 관련 프로젝트 (별도 저장소)

- Chimera AI (주간 증시): https://github.com/waterfirst/chimera-ai — 매주 보고서를 업로드하고 목차에 반영
- Alpha Hunter (히든젬): https://github.com/waterfirst/alpha-hunter
- Insight Lab (인문학x과학): https://github.com/waterfirst/insight-lab
- Culture Voyager (문화저널): https://github.com/waterfirst/culture-voyager

</instructions>

<technical_stack>

## 기술 스택

R + ggplot2로 차트를 생성한다. Plotly는 파일 용량이 비대해지므로 사용하지 않는다.
Quarto (.qmd)로 보고서를 렌더링하며, 아래 설정을 따른다:

- `lightbox: true` — 차트 클릭 시 줌인 가능
- `self-contained: true` — 단일 HTML 배포
- `dev: ragg_png` — CJK 폰트 렌더링에 필요
- 폰트: `"Noto Sans CJK KR"` 시스템 폰트를 직접 사용한다. showtext는 Quarto knitr 환경에서 충돌하므로 사용하지 않는다.
- 색상: 6자리 hex만 사용한다 (`"#aaaaaa"`). 3자리 hex(`"#aaa"`)는 Quarto+ragg 조합에서 "invalid RGB specification" 에러를 발생시킨다.
- 지도: R `leaflet` 패키지를 사용한다. JS Leaflet 직접 삽입 금지. 참고: https://bigdata-anlysis.tistory.com/34
- YouTube: Quarto `{{< video >}}` shortcode 대신 직접 `<iframe src="https://www.youtube.com/embed/...">` 사용 (self-contained 모드에서 shortcode 에러 발생)

</technical_stack>

<journal_rules>

## 저널 공통 규칙

모든 저널(Insight Lab, Chimera AI, Alpha Hunter, Culture Voyager)의 목차 페이지는 **발행일 역순**으로 정렬한다.
- "최신 발행(Published)" 섹션을 최상단에 배치, 최신 → 과거 순
- 미발행 콘텐츠는 기존 카테고리별 섹션에 유지
- 새 콘텐츠 발행 시 "최신 발행" 섹션 맨 위에 추가

여행 콘텐츠 필수 요소:
- R leaflet 기반 여행 궤적 지도 (명소 마커 + Day별 경로 + 범례)
- 상단 fixed + 하단 CTA "목차로 돌아가기" 버튼
- 목차 돌아가기 버튼 템플릿: `output/_nav_back.html`

</journal_rules>

<investigate_before_answering>
코드를 수정하기 전에 반드시 해당 파일을 읽어라.
열지 않은 파일의 내용을 추측하지 말고, 실제 코드를 확인한 뒤 답변한다.
</investigate_before_answering>

<avoid_overengineering>
요청된 변경만 수행한다. 버그 수정에 주변 코드 정리를 추가하지 않는다.
변경하지 않은 코드에 docstring, 주석, 타입 어노테이션을 추가하지 않는다.
한 번만 사용하는 로직에 헬퍼 함수나 추상화를 만들지 않는다.
</avoid_overengineering>

<frontend_aesthetics>
새 HTML 페이지를 만들 때, 매거진 전체의 디자인 일관성을 유지한다.
기존 index.html의 다크 테마(#0d1117 배경), 색상 시스템(--accent:#58a6ff, --accent2:#f78166), 레이아웃 패턴을 참고한다.
Inter, Roboto, Arial 같은 범용 폰트 대신 프로젝트 기존 폰트 스택(-apple-system, BlinkMacSystemFont, 'Segoe UI')을 유지한다.
</frontend_aesthetics>

<session_protocol>

## 세션 종료 프로토콜

세션을 어떻게 종료하느냐가 컨텍스트 관리와 코드 품질에 직결된다.
모든 세션 종료 시 아래 5단계를 순서대로 수행한다.

### 1. Cleanup (정리)
- 임시 파일, 테스트 출력물, 디버그 코드를 삭제한다
- `git status`로 의도하지 않은 변경 사항이 없는지 확인한다
- node_modules, .knit.md 등 생성된 중간 산출물을 정리한다

### 2. Verify (확인)
- 변경한 코드가 정상 동작하는지 확인한다 (quarto render, 브라우저 테스트 등)
- `git diff`로 최종 변경 내역을 리뷰한다
- 깨진 링크, 누락된 파일, 문법 오류가 없는지 점검한다

### 3. Reflect (배움)
- 이번 세션에서 발견한 기술적 제약이나 해결 패턴을 기록한다
  (예: "3자리 hex가 Quarto+ragg에서 에러를 일으킨다")
- 실수가 있었다면 원인과 방지책을 파악한다
- 다음에 같은 작업을 더 빠르게 할 수 있는 방법을 메모한다

### 4. Persist (기억)
- 새로 발견한 규칙이나 제약을 이 CLAUDE.md에 반영한다
- 진행 중인 작업이 있으면 상태를 파일에 기록한다 (progress.txt, TODO 등)
- git commit 메시지에 변경의 "왜"를 담는다

### 5. Ship (인계)
- `git push`로 변경 사항을 원격에 반영한다
- 다음 세션(또는 다른 에이전트)이 이어받을 수 있도록 컨텍스트를 남긴다:
  현재 상태, 남은 작업, 주의사항
- 사용자에게 결과 URL과 변경 요약을 전달한다

</session_protocol>

## Repository Structure

```
index.html          — 메인 OLED 시야각 분석기 (v2.0)
data.csv            — 측정 데이터
data_clean.csv      — 정제된 데이터
CLAUDE.md           — 프로젝트 규칙 (이 파일)
```
