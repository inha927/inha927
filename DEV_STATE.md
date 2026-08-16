# DEV_STATE

> 갱신: 2026-08-16 · 브랜치: `claude/uefn-mcp-server-setup-9hh020` · 레포: `inha927/inha927` (공개)

## 지금 목표

여러 프로젝트 × 여러 AI × 여러 기기에서 **같은 협업 규칙과 상태 관리**가 적용되는 구조 만들기. 이 레포가 그 공통 규칙의 보관처다.

## 완료된 것

- **공통 AI 협업 프로토콜** — `AGENTS.md` (v1.0). GPT·Codex·Cursor 등에 복붙 전달용이자, 도구들이 자동 인식하는 표준 파일
- **`CLAUDE.md`** — Claude Code가 `@AGENTS.md`로 프로토콜을 자동 로드
- **`/dev-state`·`/resume` 커맨드 v2** — 프로젝트 형태 인식형: 정본형(`AGENTS.md`+`Docs/`) / 단일형(`DEV_STATE.md`) / 없음. 정본형에서는 인수인계 문서를 갱신하고 DEV_STATE.md를 만들지 않는다
- **종합 검토 문서** — `docs/ai-workflow-architecture.md` (3계층 모델, 프로젝트별 판정, 기기 전역 적용 지도)
- **UEFN MCP 조사** — `docs/uefn-mcp-decision.md`. 결론: 보류, 도입 트리거와 절차 명시
- 플라이 이스케이프 현황판 아티팩트(92f37c04…) 실물 확인 — 프로젝트 폴더에 이미 정본 체계(`AGENTS.md`+`Docs/`+인수인계+테스트 기록+AI 잠금)가 있음을 확인

## 핵심 결정과 이유

- **3계층 분리** — 방법·지식은 공통, 상태는 프로젝트별. 경계 기준은 "변하는 속도"
- **플라이 이스케이프에 DEV_STATE.md 추가 금지** — 이미 더 정교한 정본 체계가 있다. 정본이 둘이 되면 체계가 죽는다. 커맨드가 그 체계를 인식하는 쪽으로 해결
- **아티팩트 = 사람용 대시보드 고정** — 다른 AI는 아티팩트를 읽고 쓸 수 없다. AI가 읽고 쓰는 곳은 항상 프로젝트 파일
- **FREEZE TAG 상태는 당분간 스킬에** — 기획 단계라 프로젝트 폴더가 없다. UEFN 프로젝트 생성일에 플라이 이스케이프 구조로 이관
- **새 private 레포·아티팩트 수정 안 함** — 이유는 architecture 문서 마지막 절

## 핵심 파일

| 경로 | 역할 |
|---|---|
| `AGENTS.md` | 공통 AI 협업 프로토콜 (복붙 전달용 원본) |
| `CLAUDE.md` | Claude Code용 로더 (@AGENTS.md) |
| `.claude/commands/dev-state.md` | `/dev-state` — 형태 인식형 상태 압축 |
| `.claude/commands/resume.md` | `/resume` — 형태 인식형 재개 |
| `docs/ai-workflow-architecture.md` | 종합 검토: 3계층, 프로젝트별 판정, 기기 적용 지도 |
| `docs/uefn-mcp-decision.md` | UEFN MCP 조사·도입 절차 |
| `DEV_STATE.md` | 이 문서 |

## 테스트·검증 상태

- 아티팩트 내용 실측 (WebFetch) — **통과.** 정본 체계 존재 확인
- `claude mcp list` → MCP 미설치 — **통과**
- 슬래시 커맨드 실제 로드 — 이 레포 세션에서 스킬 목록에 뜨는 것 확인. **PC에서는 미검증**
- GPT·Codex가 AGENTS.md를 실제로 따르는지 — **미실행** (사용자가 전달해야 시작)

## 알려진 문제

- 이 레포는 **공개**다. 게임 기획 세부·수치는 두지 않는다 (CLAUDE.md에 명시)
- `dev.epicgames.com`·`forums.unrealengine.com`이 이 환경 프록시에서 차단 — UEFN 공식 문서는 PC에서 재확인
- 클라우드 세션은 플라이 이스케이프 프로젝트 파일(UEFN Revision Control 동기화)을 읽을 수 없다 — 아티팩트만 가능

## 실패한 접근

- **클라우드 세션에 UEFN MCP 설치** — 컨테이너에 UEFN이 없다. MCP는 UEFN이 도는 PC에서만
- **컨테이너 `~/.claude/`에 영속 저장** — 세션 종료 시 소멸. 영속은 레포·claude.ai 계정 설정만
- **플라이 이스케이프에 DEV_STATE.md 이식** — 정본 이중화라 기각. 커맨드가 기존 체계를 인식하는 방식으로 대체

## 다음 할 일

1. **[사용자]** GPT 등 다른 AI에 `AGENTS.md` 전문 붙여넣기 (메모리/프로젝트 지침으로)
2. **[사용자]** claude.ai 개인 설정에 한 줄 추가 + (선택) 스킬에 프로토콜 요약 추가
3. **[사용자]** PC 1회 설치 — `.claude/commands/` 2개 복사 (`docs/ai-workflow-architecture.md`의 명령 참조)
4. PC에서 `/dev-state`·`/resume` 동작 확인, 플라이 이스케이프 폴더에서 `/resume`이 정본형을 타는지 확인
5. FREEZE TAG UEFN 프로젝트 생성일: 정본형 구조 복제 + 스킬의 project-state 이관
6. UEFN MCP: 보류 유지. 트리거 조건은 `docs/uefn-mcp-decision.md`
