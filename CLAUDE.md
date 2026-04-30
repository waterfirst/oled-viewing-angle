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

</technical_stack>

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

## Repository Structure

```
index.html          — 메인 OLED 시야각 분석기 (v2.0)
data.csv            — 측정 데이터
data_clean.csv      — 정제된 데이터
CLAUDE.md           — 프로젝트 규칙 (이 파일)
```
