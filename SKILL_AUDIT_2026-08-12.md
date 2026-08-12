# 스킬 · 플러그인 최신성 검토 (2026-08-12)

대상: inha927@gmail.com — 스킬 30종, 플러그인 25종

---

## 요약

1. **스킬 30종 중 9종이 깨져 있다.** SKILL.md만 있고 그 문서가 참조하는 파일 83개가 없다. 하필 디자인·UI 스킬 7종이 전부 여기 해당한다.
2. **superpowers 계열은 오늘(8/12) v6.3.0이 나왔다.** 계정 사본은 7/28 업로드본이라 v6.2.0 세대다.
3. **ui-ux-pro-max는 v2.13.0 플러그인으로 나와 있다.** 계정 사본은 v1 세대 문서다.
4. **플러그인 25종은 최신이다.** 자동 업데이트가 돌고 있어 조치할 것이 없다.
5. 지난 턴에 제안한 15종은 아직 설치되지 않았다.

---

## 1. 무결성 검사 — 깨진 스킬 9종

각 SKILL.md가 참조하는 경로가 실제로 존재하는지 전수 검사했다.

| 스킬 | 누락 파일 | 결과 |
|---|---:|---|
| design | 26 | 로고·CIP·아이콘 생성 스크립트 전부 없음. 설명의 "55 styles, Gemini AI, 50 deliverables"가 전부 동작 불가 |
| design-system | 17 | 토큰 참조 문서 7종 + 슬라이드 데이터 CSV 8종 + search-slides.py 없음 |
| brand | 13 | 보이스 프레임워크, 로고 규칙, 타이포 스펙 등 전부 없음 |
| ui-styling | 9 | shadcn/Tailwind 참조 7종 + 생성 스크립트 2종 없음 |
| ui-ux-pro-max | 3 | **search.py 없음** — "검색 가능한 로컬 DB"의 검색기가 통째로 빠짐 |
| banner-design | 5 | 배너 규격표, Gemini 배치 처리, 스크린샷 스크립트 없음 |
| slides | 5 | 레이아웃 패턴, HTML 템플릿, 카피라이팅 공식 없음 |
| using-superpowers | 3 | 타 런타임 도구 매핑 참조 없음 (Claude Code 단독 사용 시 영향 적음) |
| writing-skills | 2 | 타 런타임 도구 매핑 참조 없음 (영향 적음) |

**정상 (파일 수)**: docx 61, pptx 56, xlsx 53, skill-creator 18, pdf 12, freeze-tag-uefn 4, morning 3, seedance-2-5-prompts 1(80KB 자체 완결)

### 이게 동기화 누락이 아니라 원본 문제인 근거

같은 동기화 경로로 내려온 docx가 61개 파일, pptx가 56개 파일을 온전히 갖고 있다. 다중 파일 스킬을 보존하는 메커니즘이라는 뜻이다. 따라서 단일 파일로 내려온 9종은 업로드 시점부터 SKILL.md만 올라간 것이다.

### 추가 의존성 결손

`banner-design`은 설명에 "Uses ui-ux-pro-max, **frontend-design**, ai-artist, ai-multimodal skills"라고 명시한다. 이 중 `frontend-design`, `ai-artist`, `ai-multimodal`은 계정에 아예 없다.

---

## 2. 버전 격차

### superpowers 계열 13종

계정 사본 업로드일 2026-07-28 → v6.2.0(7/23) 세대. 현재 최신은 **v6.3.0 (2026-08-12)**.

놓치고 있는 v6.3.0 변경점:
- brainstorming이 작업 규모에 맞춰 스케일 — 작은 작업에서 문서화 단계를 건너뜀
- subagent 컨트롤러가 계획 충돌 시 멈추던 문제 해결
- 같은 형태의 소규모 작업을 한 번의 디스패치로 묶음

### ui-ux-pro-max 및 디자인 스킬 6종

계정 사본은 v1 세대 문서(84 styles / 192 palettes / 74 font pairings 표기). 업스트림은 `nextlevelbuilder/ui-ux-pro-max-skill`, GitHub 116k stars, **플러그인 v2.13.0**.

v2.0에서 추가된 것: **Design System Generator** — 161개 산업별 추론 규칙으로 프로젝트 요구사항을 분석해 완성된 디자인 시스템을 생성.

계정의 design / banner-design / slides / ui-styling / design-system / brand 6종도 **전부 이 저장소에서 나온 것**이다. 즉 7종이 한 플러그인으로 묶여 있다.

---

## 3. 플러그인 25종 — 조치 불필요

`design` 플러그인이 version `0030`, updated_at `2026-08-10`. 카탈로그 자동 업데이트가 정상 동작 중이므로 수동 갱신할 것이 없다.

---

## 4. 권고 — 스킬을 플러그인으로 교체

깨진 파일을 하나씩 채우는 것보다 플러그인으로 갈아타는 쪽이 낫다. 플러그인은 파일 트리를 통째로 들고 오고 자동 업데이트된다.

### 4.1 최우선

| 조치 | 명령 | 효과 |
|---|---|---|
| superpowers 플러그인화 | `/plugin install superpowers@claude-plugins-official` | 개별 스킬 13종 대체, v6.3.0로 점프, 이후 자동 갱신 |
| ui-ux-pro-max 플러그인화 | `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill`<br>`/plugin install ui-ux-pro-max@ui-ux-pro-max-skill` | 깨진 디자인 스킬 7종 대체, v2.13.0 + Design System Generator |
| frontend-design 설치 | `/plugin install frontend-design@claude-plugins-official` | banner-design의 누락 의존성 해소. Anthropic 공식 최다 설치(약 277k) |

교체 후 계정에서 지울 스킬: `design`, `design-system`, `brand`, `banner-design`, `slides`, `ui-styling`, `ui-ux-pro-max` + superpowers 계열 13종.

남길 스킬: `docx`, `pptx`, `xlsx`, `pdf`, `skill-creator`, `morning`, `humanizer`, `seedance-2-5-prompts`, `freeze-tag-uefn` — 전부 온전하거나 대체재가 없다.

### 4.2 작업 영역별 추가 (공식 마켓플레이스)

모두 `@claude-plugins-official`이라 마켓플레이스 등록 없이 바로 설치된다.

- **hyperframes** — HTML로 쓰고 애니메이션·자막 포함 비디오로 렌더 (HeyGen). 영상 제작 작업에 직결
- **cloudinary** — 미디어 변환·최적화
- **code-simplifier** — 동작 보존하며 코드 정리
- **code-review** — 신뢰도 스코어 기반 자동 리뷰
- **codspeed** — 벤치마크·플레임그래프·프로파일링
- **coderabbit** — 40종 정적 분석기 결합 리뷰
- **mintlify** — 문서 사이트
- **claude-md-management** — CLAUDE.md 품질 감사, 세션 학습 반영

---

## 5. 제약

- 위 플러그인들은 GitHub 마켓플레이스(`claude-plugins-official`, `ui-ux-pro-max-skill`) 소속이라 claude.ai 계정 카탈로그(`knowledge-work-plugins`)에 없다. 따라서 지난 턴에 쓴 설치 카드로는 설치할 수 없고, Claude Code CLI 또는 데스크톱 앱의 플러그인 설정에서 직접 실행해야 한다.
- 무결성 검사는 이 세션 컨테이너에 동기화된 사본을 대상으로 했다. 판단 근거는 4절 상단에 적었다.
- 계정 스킬 삭제는 이 세션에서 불가능하다. claude.ai 설정에서 직접 수행해야 한다.

---

## 참고

- https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- https://github.com/obra/superpowers
- https://github.com/anthropics/claude-plugins-official
- https://claude.com/plugins/frontend-design
