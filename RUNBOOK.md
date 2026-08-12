# 실행 가이드 — 어디서 뭘 실행하나

세 시스템이 서로 다르다. 스크린샷의 디렉터리(Anthropic/파트너 탭)는 claude.ai 계정 카탈로그라서,
거기서는 superpowers·ui-ux-pro-max·frontend-design을 설치할 수 없다. 그것들은 Claude Code 마켓플레이스 소속이다.

| 하려는 것 | 어디서 |
|---|---|
| 깨진 스킬 9종 삭제 | claude.ai 설정 → 사용자 지정 → 스킬 |
| 이전 감사에서 고른 15종 | claude.ai 설정 → 사용자 지정 → 플러그인 |
| superpowers / ui-ux-pro-max / frontend-design / hyperframes | Claude Code 터미널 |

**순서: ① 설치 → 동작 확인 → ③ 삭제.** 반대로 하면 그 사이 디자인 기능이 비고,
둘 다 켜두면 같은 이름 스킬이 중복돼 지침이 충돌한다.

---

## ① Claude Code 터미널 (권장)

터미널에서 `claude` 실행 후 순서대로.

### 1. 공식 마켓플레이스 — 등록 불필요

`claude-plugins-official`은 Claude Code 최초 대화형 실행 시 자동 등록된다.

```
/plugin install frontend-design@claude-plugins-official
/plugin install hyperframes@claude-plugins-official
/plugin install code-simplifier@claude-plugins-official
```

`Marketplace "claude-plugins-official" not found`가 나오면:

```
/plugin marketplace add anthropics/claude-plugins-official
```

### 2. superpowers

```
/plugin install superpowers@claude-plugins-official
```

실패 시 자체 마켓플레이스 경유:

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

### 3. ui-ux-pro-max — 외부 마켓플레이스라 추가 필요

```
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

### 4. 활성화

설치 요약이 `Plugin is now active.`면 생략. `Run /reload-plugins to activate.`면:

```
/reload-plugins
```

프롬프트 캐시 무효화 경고가 뜨면 `/reload-plugins --force`.

### 5. 외부 마켓플레이스 자동 업데이트 켜기

서드파티 마켓플레이스는 자동 업데이트가 **기본 꺼짐**이다.
이번에 확인된 버전 뒤처짐이 그대로 반복되므로 반드시 켠다.

```
/plugin
```

→ **Marketplaces** 탭 → `ui-ux-pro-max-skill` 선택 → **Enable auto-update**

공식 Anthropic 마켓플레이스는 기본 켜짐이라 손댈 것 없다.

### 설치 스코프

설치 시 스코프를 묻는다.

- **User** — 내 모든 프로젝트에서 사용 (이 경우 권장)
- **Project** — 이 저장소 협업자 전원, `.claude/settings.json`에 기록
- **Local** — 이 저장소에서 나만

### 확인

```
/plugin list
```

---

## ② 데스크톱 앱 — 터미널을 쓰지 않을 경우

`/plugin`이 이 환경에서 지원되지 않는다고 나올 때만 사용한다.

**설정 → Claude Code → 플러그인** → `찾아보기` / `추가 ∨` → 마켓플레이스 추가 →
`nextlevelbuilder/ui-ux-pro-max-skill` 입력

주의: **사용자 지정 → 플러그인** 화면(폴더 선택 / 플러그인 탐색)은 Cowork 쪽이라
CLI 플러그인 대신 계정 플러그인이 뜰 수 있다. 데스크톱 앱이 CLI 플러그인 자리에
Cowork 플러그인을 보여주는 문제가 보고돼 있어(anthropics/claude-code#38008)
이 경로는 터미널보다 덜 확실하다.

---

## ③ claude.ai 계정 설정

### 스킬 삭제 — 설정 → 사용자 지정 → 스킬

참조 파일이 없어 동작하지 않는 9종:

```
design  design-system  brand  banner-design  slides
ui-styling  ui-ux-pro-max  using-superpowers  writing-skills
```

superpowers 플러그인이 같은 내용을 가져오므로 함께 지울 12종:

```
brainstorming  test-driven-development  systematic-debugging
writing-plans  executing-plans  subagent-driven-development
dispatching-parallel-agents  requesting-code-review  receiving-code-review
verification-before-completion  using-git-worktrees  finishing-a-development-branch
```

**남길 것** — 온전하거나 대체재가 없다:

```
docx  pptx  xlsx  pdf  skill-creator  morning  humanizer
seedance-2-5-prompts  freeze-tag-uefn
```

### 플러그인 — 설정 → 사용자 지정 → 플러그인 → 탐색

이전 감사에서 고른 15종(Cloudinary, Tavily, Base44 등)은 계정 카탈로그
`knowledge-work-plugins` 소속이라 이 화면이 맞다.

---

## 주의

- `/plugin marketplace remove`는 **그 마켓플레이스에서 설치한 플러그인을 함께 삭제**한다.
- 플러그인은 사용자 권한으로 임의 코드를 실행한다. 신뢰하는 출처만 추가한다.
- 설치 후 스킬이 안 보이면 `rm -rf ~/.claude/plugins/cache` 후 Claude Code 재시작.
- `/plugin`이 unknown command면 Claude Code를 갱신한다
  (`npm install -g @anthropic-ai/claude-code@latest` 또는 `brew upgrade claude-code`).

---

## 참고

- https://code.claude.com/docs/en/discover-plugins
- https://github.com/anthropics/claude-plugins-official
- https://github.com/obra/superpowers-marketplace
- https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
