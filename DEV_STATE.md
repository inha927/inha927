# DEV_STATE

> 갱신: 2026-08-16 · 갱신자: Claude · 브랜치: `claude/uefn-mcp-server-setup-9hh020` · 레포: `inha927/inha927` (공개)

## 지금 목표

여러 프로젝트 × 여러 AI × 여러 기기에서 같은 협업 규칙이 적용되는 구조. 이 레포가 공통 프로토콜의 **원본** 보관처다.

## 완료된 것

- **공통 프로토콜 v2.0** (`AGENTS.md`) — Claude v1.0 + Codex 전역 설정 통합본. 조항별 판정은 `docs/ai-workflow-architecture.md`의 판정표
- `/dev-state`·`/resume` 커맨드 v2.0 — 표준 시작 문구 실행형, 8KiB 한도, 소유권 준수
- UEFN MCP 조사 (`docs/uefn-mcp-decision.md`) — 보류, 도입 트리거 명시
- 플라이 이스케이프: 아티팩트 실물 확인 + Codex가 PC에서 표준 구조 전환 완료 [확인: Codex 보고]
- **FREEZE TAG 앵커 분기 사고 발견** — 스킬 project-state(v3.2 사용자 확정) ↔ Drive FREEZETAG_04(v4.0, 매일 06:00 자동 작업의 참조 대상)가 서로 모순. 상세는 architecture 문서

## 핵심 결정과 이유

- **전 프로젝트 단일 구조**: 루트 `AGENTS.md`(≤24KiB) + `DEV_STATE.md`(≤8KiB), 심층은 `Docs/` 온디맨드. v1.0의 2형태 구분은 폐지 (Codex 통합 판정)
- **상태 앵커는 프로젝트당 1개** + 이관 표지 의무 — FREEZE TAG 분기 사고가 근거
- **원본-사본 버전 대조** — 사본 4곳(Codex 전역·PC Claude·claude.ai 설정·프로젝트 루트)은 이 레포 원본 버전으로 대조

## 핵심 파일

| 경로 | 역할 |
|---|---|
| `AGENTS.md` | 공통 프로토콜 **v2.0 원본** |
| `CLAUDE.md` | Claude Code 로더 (@AGENTS.md) |
| `.claude/commands/dev-state.md` · `resume.md` | 세션 닫기/열기 커맨드 |
| `docs/ai-workflow-architecture.md` | 판정 기록 (Codex 통합 판정표, FREEZE TAG 사고, 설치 절차) |
| `docs/uefn-mcp-decision.md` | UEFN MCP 조사 |

## 게이트·테스트 현황

- 커맨드 PC 동작 — **NOT_RUN**
- 플라이 이스케이프 DEV_STATE의 Revision Control 동기화 (Check-in Changes 포착 여부) — **NOT_RUN** [출처: Codex 보고의 UNKNOWN]
- GPT·Codex가 v2.0을 실제 준수하는지 — **NOT_RUN**

## 알려진 문제

- **FREEZE TAG 앵커 분기** — 사용자 판정 전까지 양쪽 다 정본 아님. 06:00 자동 작업이 v3.2 미반영 앵커를 읽는 중
- Codex 전역 `%USERPROFILE%\.codex\AGENTS.md`는 Codex 자체 작성 구버전 — v2.0으로 교체 필요
- 이 레포는 공개 — 게임 기획 세부·수치 금지
- `dev.epicgames.com` 등이 이 환경 프록시에서 차단 — 공식 문서는 PC에서 확인

## 실패한 접근

- 클라우드 세션에 UEFN MCP 설치 — 컨테이너에 UEFN이 없다
- 컨테이너 `~/.claude/`에 영속 저장 — 세션 종료 시 소멸
- 플라이 이스케이프에 인수인계-정본 방식 유지(v1.0 판정) — 현장이 DEV_STATE 방식으로 전환·승인되어 철회
- 상태 앵커 다중화 (스킬+Drive+아티팩트 병행) — FREEZE TAG 분기 사고의 원인. 재발 금지

## 다음 할 일

1. **[사용자] FREEZE TAG 앵커 판정** — 권고: v3.2 기준 + v4.0 정정사항 병합한 v5를 한 곳에, 나머지엔 이관 표지, 06:00 작업 참조 교체
2. **[사용자] 사본 배포** — Codex 전역본을 v2.0으로 교체, claude.ai 개인 설정 한 줄, PC `~/.claude/` 설치
3. **[사용자·PC]** 플라이 이스케이프 DEV_STATE.md가 Revision Control Check-in에 잡히는지 확인 → 결과를 그쪽 DEV_STATE에 기록
4. PC에서 `/resume`·`/dev-state` 동작 확인
5. FREEZE TAG UEFN 프로젝트 생성일: 표준 구조 이관
