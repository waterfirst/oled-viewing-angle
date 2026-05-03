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

<chimera_weekly_report>

## 키메라 주간 리포트 — ETF 모멘텀 분석 체계

### 개인정보 보호 원칙

**절대 금지**: 개인연금, 퇴직연금, 포트폴리오 정보를 public GitHub 저장소에 올리지 않는다.
- 개인 자산 분석 결과는 텔레그램으로만 전송한다 (sendfile)
- chimera-ai, alpha-hunter 등 public 레포에 포트폴리오 데이터 커밋 금지
- ETF 분석 자체는 공개 가능하나, "내 보유 종목" 매칭 결과는 비공개

### ETF 분석 원칙

ETF 분석을 요청받으면 반드시 아래 순서로 퀀트 분석을 수행한다:
1. `etf_momentum_scrape.py`로 모멘텀 계산기 실행 (Playwright 자동화)
2. 현재 순위 정렬 → TOP 20 / 하위 20 분석
3. 순위 변동 정렬 → 급상승(가속) / 급하락(감속) TOP 15 분석
4. 섹터별 테마 분류 → 평균 모멘텀, ETF 개수, Tier 분류
5. 포트폴리오 매칭 → 보유 종목의 모멘텀 위치 점검
6. 데이터에 근거한 매수/매도 판정 (감정이 아닌 숫자로)

**절대 규칙**: 의견이 아닌 데이터로 말한다. 모멘텀 점수, 순위, 수익률 숫자를 항상 제시한다.

### 데이터 소스

- **ETF 모멘텀 계산기**: https://etf-v6-c3-617871724184.us-west1.run.app/
- **공공데이터포털 API 키**: `.env` 파일의 `DATA_GO_KR_SERVICE_KEY`
- **자동화 스크립트**: `etf_momentum_scrape.py` (Playwright 기반)
- **결과 데이터**: `etf_momentum_results.json`

### 모멘텀 계산 설정값

- 1주 가중치: 0 / 2주 가중치: 0 / 1개월 가중치: 12 / 3개월 가중치: 4 / 6개월 가중치: 2
- 최소 거래량: 10만주 / 최소 거래대금: 10억원 / 표시 순위: 100 / 순위 비교: 7일

### 키메라 리포트 구성 요소

1. **현재 순위 정렬** — TOP 20 / 하위 20 분석
2. **순위 변동 정렬** — 급상승(모멘텀 가속) / 급하락(모멘텀 감속) TOP 15
3. **섹터별 테마 분석** — 평균 모멘텀, ETF 개수, 대표 종목
4. **포트폴리오 매칭** — 보유 종목의 모멘텀 위치 점검
5. **시장 총평 및 투자 시사점**

### 2026-05-03 기준 ETF 모멘텀 핵심 발견

**섹터별 평균 모멘텀 순위:**
1. AI전력인프라: 1,098 (3개 ETF) — 가장 강한 테마
2. 신재생/태양광: 933 (6개 ETF) — 장기 모멘텀 최강
3. 원자력/SMR: 810 (5개 ETF) — 안정적 상위권
4. 2차전지/배터리: 698 (9개 ETF) — 단기 폭발적, 장기는 아직
5. 건설/조선/CAPEX: 698 (7개 ETF) — 건설 강세 vs 조선 약화 분화
6. 반도체/AI: 687 (21개 ETF) — 가장 넓은 강세, 종목 수 최다
7. 코스피 인덱스: 659 (22개 ETF) — 시장 전반 강세 확인
8. 방산: 514 (3개 ETF) — **순위 급락 중 (▼42~46), 모멘텀 꺾임**
9. 커버드콜: 456 (3개 ETF) — 강세장에서 구조적 언더퍼폼
10. 미국 시장: 568 (5개 ETF) — 레버리지 외 하위권, 한국 대비 약세

**순위 급상승 핵심 (모멘텀 가속 신호):**
- TIGER 200에너지화학레버리지 (New → 8위) — 에너지화학 급부상
- HANARO CAPEX설비투자iSelect (New → 22위) — 설비투자 사이클 시작
- HANARO Fn전기&수소차 (New → 24위) — 전기차/수소 부활
- KODEX 조선TOP10 (▲184 → 91위) — 극단적 순위 상승, 단기 반등 신호
- TIGER 200 에너지화학 (▲24 → 66위) — 화학 섹터 반등
- ACE 포스코그룹포커스 (▲22 → 87위) — 철강/소재 턴어라운드

**순위 급하락 핵심 (모멘텀 감속 경고):**
- KODEX 방산TOP10레버리지 (▼46 → 92위) — 방산 모멘텀 급격 악화
- PLUS K방산레버리지 (▼42 → 86위) — 방산 전체 하락
- TIGER 미국필라델피아반도체나스닥 (▼25 → 68위) — 미국 반도체 약세
- 2차전지 비레버리지 다수 (▼13~18) — 레버리지만 강하고 일반형은 둔화
- SOL 반도체후공정 (▼13 → 43위) — 후공정 모멘텀 꺾임

**포트폴리오 종목 모멘텀 현황:**
- RISE 네트워크인프라: 9위 (1,129점) — 최강 포지션, 추가 매수 1순위
- TIGER 코리아원자력: 16위 (946점) — 비중 0.8%는 너무 작음, 확대 필요
- TIGER 반도체TOP10: 29위 (745점) — ▲11 상승 중, 유지하되 과집중 주의
- SOL 조선TOP3플러스: 97위 (382점) — 6개월 +8.5%, 모멘텀 소진. 차익실현
- TIGER 200타겟위클리커버드콜: 69위 (543점) — 강세장 언더퍼폼 확인

### 2026 미국 중간선거 타임라인

- **선거일**: 2026년 11월 3일
- **역사적 패턴**: 중간선거 전 4~10월 약세(S&P500 평균 +2.9%) → 선거 후 12개월 평균 +12.4%
- **리밸런싱 전략**: 3단계 실행 (5월 즉시 / 6~8월 조정 매수 / 9~10월 최종 세팅)

</chimera_weekly_report>
