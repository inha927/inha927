# 플러그인 · 스킬 감사 보고서

작성일: 2026-08-05
대상 계정: inha927@gmail.com
마켓플레이스: `knowledge-work-plugins` (약 50개 전수 조사)

---

## 1. 현재 상태

### 활성화된 플러그인 (25)

| 영역 | 플러그인 |
|---|---|
| 디자인·크리에이티브 | design, canva, figma, adobe-for-creativity, miro, brand-voice |
| 엔지니어링 | engineering |
| 비즈니스 | operations, product-management, marketing, sales, finance, human-resources, legal, small-business, customer-support, productivity |
| 데이터·리서치 | data, enterprise-search, bio-research, brightdata-plugin, searchfit-seo, apollo |
| 기타 | pdf-viewer, postiz |

### 활성화된 스킬 (30)

- **문서 생산** — docx, pptx, pdf, xlsx (Anthropic 퍼스트파티)
- **디자인** — design, design-system, brand, banner-design, slides, ui-styling, ui-ux-pro-max
- **개발 프로세스(superpowers 계열)** — using-superpowers, brainstorming, writing-plans, executing-plans, test-driven-development, systematic-debugging, subagent-driven-development, dispatching-parallel-agents, requesting-code-review, receiving-code-review, verification-before-completion, using-git-worktrees, finishing-a-development-branch, writing-skills
- **기타** — humanizer, skill-creator, morning, session-start-hook

---

## 2. 진단

### 커버리지 공백

기존 25개 플러그인은 **비즈니스 지식노동**에 편중되어 있고, 사용자가 지목한 작업군 중 다음이 비어 있었다.

| 작업군 | 기존 커버리지 | 판정 |
|---|---|---|
| 제안서 | marketing, docx/pptx 스킬 | 충분 — 단 리서치 근거 수집 도구 부재 |
| 게임 기획서 | product-management | 부분 — 밸런스/스펙 데이터 관리 수단 없음 |
| 코딩 | engineering | 부분 — 최신 웹 스택 가이던스·테스트 산출 도구 없음 |
| 영상 제작·편집 | adobe-for-creativity, canva | **공백** — 프로그래매틱 미디어 파이프라인 전무 |
| 게임 개발 | 없음 | **공백** |
| 앱 개발 | engineering | **공백** — 앱 빌더·인증·배포 경로 없음 |
| UI/UX 시안 | design, figma, ui-ux-pro-max 스킬 | 충분 |
| 디자인 제작 | design, canva, adobe | 충분 |

### 스킬 중복

디자인 스킬 7종(design, design-system, brand, banner-design, slides, ui-styling, ui-ux-pro-max)이 서로 상당 부분 겹친다. `design` 스킬 설명 자체가 로고·CIP·슬라이드·배너·아이콘·소셜을 모두 포함한다고 명시하므로, `design` + `ui-ux-pro-max`(고유한 검색형 DB) 2종만 남기고 나머지 5종은 정리 여지가 있다.

반면 superpowers 계열 14종은 `engineering` 플러그인과 **중복이 아니다**. engineering은 산출물(리뷰·ADR·인시던트 문서)을, superpowers는 작업 규율(TDD·디버깅 순서·검증 게이트)을 담당한다. 둘 다 유지가 맞다.

docx/pptx/pdf/xlsx는 대체할 플러그인이 카탈로그에 없다. 유지.

---

## 3. 선정 결과 — 15종

공백 영역을 메우는 것을 1순위로, 최근 3개월(2026-05~08) 등록분에 가중치를 두어 선별.

### 영상 제작·편집 (신규 영역)
- **Cloudinary** — 이미지·영상 업로드/변환/자동 편집/최적화 파이프라인
- **Pixeltable** (2026-06) — 비디오·이미지·오디오 멀티모달 데이터 처리, 프레임 추출·인덱싱

### 앱·게임 개발 (신규 영역)
- **Base44** — AI 풀스택 앱 빌더, 프로토타입 생성부터 배포까지
- **Qt Development Skills** (2026-06) — C++/QML 데스크톱·크로스플랫폼 앱 및 게임 툴 UI
- **Auth0** — 앱 인증·로그인 구현
- **Val Town** — TypeScript 엔드포인트·크론 즉시 배포
- **GrowthBook** (2026-07) — A/B 테스트·피처 플래그, 출시 후 지표 검증

### 코딩 보강
- **Modern Web Guidance** (2026-07) — 최신 웹 표준·프레임워크 가이던스, 자격증명 불필요
- **Qodo** — 코드 리뷰·테스트 자동 생성

### 기획·리서치 보강
- **Tavily** (2026-06) — 실시간 웹 리서치 검색
- **Airtable** — 게임 밸런스 테이블·콘텐츠 스펙·제안서 트래킹 DB
- **TinyFish** (2026-07) — 웹 에이전트 자동화, 대량 데이터 추출

### 파이프라인·관리
- **Zapier** — 워크플로 자동화 접착제
- **Sanity** — 헤드리스 CMS
- **Plugin Management** — 플러그인 커스터마이즈 및 MCP 서버 구성

### 검토 후 제외

| 플러그인 | 제외 사유 |
|---|---|
| wix, b12 | 웹사이트 빌더 — canva/figma와 목적 중복 |
| monday-com | productivity 플러그인과 중복 |
| clickhouse, cockroachdb, qdrant | 인프라 DB — data 플러그인으로 충분, 자격증명 부담 |
| signoz, honeycomb, grafana-cloud, buildkite, fastly | 운영 모니터링·CI — 현재 작업군과 무관 |
| stackhawk(2종), vanta | 보안 컴플라이언스 — 현재 작업군과 무관 |
| carta(3종), daloopa, lseg, bigdata-com | 금융 데이터 — finance 플러그인으로 충분 |
| zoominfo, lusha, nimble, apollo, adspirer, vibe-prospecting | 세일즈 인텔리전스 — sales 플러그인과 중복 |
| zoom, slack, intercom, twilio | 커뮤니케이션 — 별도 커넥터 영역 |
| learn-with-coursera, datarobot, atlan, product-tracking | 우선순위 낮음 |

---

## 4. 제약 사항

- **계정 단위 플러그인 설치는 프로그래매틱 API가 없다.** 사용 가능한 경로는 `SuggestPluginInstall` 설치 카드뿐이며, 최종 활성화는 사용자가 카드에서 직접 수행한다. 완전 무인 설치는 플랫폼상 불가능하다.
- 이 세션은 원격 컨테이너에서 실행된다. 컨테이너의 `claude plugin` CLI는 마켓플레이스가 등록되어 있지 않고(`No marketplaces configured`), 설치하더라도 컨테이너 종료 시 소멸하므로 계정·PC에 반영되지 않는다.
- 컨테이너의 `~/.claude/skills`는 세션 전용 사본이다. 사용자 PC 또는 claude.ai 계정의 스킬을 이 세션에서 삭제·수정할 수 없다. 3절의 스킬 중복 정리는 권고이며, 실행은 claude.ai 설정 또는 로컬 `~/.claude/skills`에서 직접 해야 한다.
- 카탈로그의 플러그인 메타데이터에 설치 수·평점 필드가 비어 있어(`install_count: null`, `library_metrics: null`) 인기도 기반 정렬은 불가능했다. 등록일과 기능 적합성으로 대체 선별했다.
