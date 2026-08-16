# DEV_STATE

> 갱신: 2026-08-16 · 브랜치: `claude/uefn-mcp-server-setup-9hh020` · 레포: `inha927/inha927`

## 지금 목표

두 가지가 걸려 있다.

1. **컨텍스트 아카이브 습관 정착** — 세션마다 대화가 길어져 토큰이 "과거 회상"에 낭비되는 문제. `DEV_STATE.md` + 슬래시 커맨드로 해결. ← 이번 세션 작업
2. **UEFN MCP 서버 도입 여부 결정** — 조사만 끝났고 설치는 보류 상태

## 완료된 것

- **UEFN MCP 서버 조사 완료.** 결론: **설치하지 않았고, 이 환경에는 설치해도 무의미하다.**
  - `claude mcp list` → `No MCP servers configured` (실행해서 확인)
  - 이 세션은 클라우드 리눅스 컨테이너. UEFN은 Windows/Mac 데스크톱 앱이라 붙을 대상이 없다
  - 브랜치 이름만 `uefn-mcp-server-setup`이고 실제 산출물은 없었다
- **DEV_STATE 워크플로 구축.** `/dev-state`(압축 저장), `/resume`(읽고 이어가기) 두 커맨드 추가

## 핵심 결정과 이유

**UEFN MCP는 지금 붙이지 않는다.** 현재 작업이 Verse 코드 작성·설계 단계라서다.
`.verse`는 텍스트 파일이고 파일 툴로 이미 다룰 수 있다 — MCP 없이도 된다.
MCP가 실제로 더해주는 값은 ① 에디터 로그를 직접 읽어 컴파일 에러 진단 ② 레벨에 장치 대량 배치, 이 둘인데 아직 그 단계가 아니다.
**도입 시점: 장치 대량 배치가 시작되거나, 컴파일 에러 복붙 왕복이 반복될 때.**

**도입한다면 순서가 정해져 있다.** `execute_python`은 PC 전권을 준다 → ① 레포 코드 먼저 읽기 ② 빈 테스트 프로젝트에서 검증 ③ publish validation 통과 확인 ④ `-s user` 스코프로 등록(VS Code·CLI·앱 통일).

**커맨드는 레포에 넣는다.** 컨테이너의 `~/.claude/`는 세션 종료 시 사라진다. 레포의 `.claude/commands/`만 남는다.

## 핵심 파일

| 경로 | 역할 |
|---|---|
| `DEV_STATE.md` | 이 문서. 프로젝트 상태 스냅샷 |
| `.claude/commands/dev-state.md` | `/dev-state` — 현재 상태를 이 문서로 압축 |
| `.claude/commands/resume.md` | `/resume` — 이 문서를 읽고 중단 지점부터 재개 |
| `README.md` | GitHub 프로필 README (이 레포의 원래 용도) |
| `docs/uefn-mcp-decision.md` | UEFN MCP 조사 결과 상세 — 툴 목록, 리스크, 설치 절차 |

## 테스트·검증 상태

- 자동 테스트 **없음** (문서·설정 파일뿐이라 대상이 없다)
- `claude mcp list` 실행해서 MCP 미설치 확인 — **통과**
- 슬래시 커맨드 실제 로드 여부 **미검증**. 다음 세션에서 `/dev-state` 쳐보면 바로 확인된다

## 알려진 문제

- **`dev.epicgames.com`, `forums.unrealengine.com`이 네트워크 프록시에서 차단된다.** UEFN 공식 문서를 직접 열 수 없어 검색 결과로만 확인했다. 중요한 스펙은 PC에서 직접 열어 재확인할 것
- **UEFN Python으로 만든 에셋은 publish validation에서 실패할 수 있다** (Epic 문서 경고). 게시가 목표라면 직격탄
- **Verse 컴파일·Push Changes를 Python API로 할 수 있는지 [미확인].** 된다고 가정하지 말 것
- 이 레포는 원래 GitHub 프로필 README 전용이다. FREEZE TAG 본 프로젝트는 PC의 UEFN 프로젝트 폴더에 따로 있다 — 그쪽에도 같은 `.claude/commands/`를 복사해야 한다

## 실패한 접근

- **이 클라우드 세션에 UEFN MCP를 설치하려는 시도.** 컨테이너에 UEFN이 없다. 다시 시도하지 말 것 — MCP 서버는 UEFN이 도는 PC에서 실행돼야 한다
- **`~/.claude/`에 커맨드·스킬 배치.** 컨테이너가 회수되면 사라진다. 영속이 필요한 건 레포에

## 다음 할 일

1. PC에서 `/dev-state`, `/resume`이 실제로 뜨는지 확인
2. `.claude/commands/` 두 파일을 **PC의 FREEZE TAG UEFN 프로젝트 폴더에 복사**. 모든 프로젝트에 적용하려면 `~/.claude/commands/`로
3. FREEZE TAG 쪽에서 `/dev-state` 한 번 돌려 초기 스냅샷 생성
4. UEFN MCP는 보류. 위 "도입 시점" 조건이 오면 `docs/uefn-mcp-decision.md`의 절차대로 진행
