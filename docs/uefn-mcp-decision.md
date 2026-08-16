# UEFN MCP 서버 — 조사 결과와 도입 절차

> 조사일 2026-08-16 · 결론: **지금은 도입 보류**

## 결론 먼저

| 질문 | 답 |
|---|---|
| 설치됐나 | **아니다.** `claude mcp list` → `No MCP servers configured` |
| 여기 설치하면 되나 | **안 된다.** 클라우드 리눅스 컨테이너에 UEFN이 없다 |
| 어디에 설치해야 하나 | **UEFN이 도는 네 PC** |
| 지금 필요한가 | **아니다.** Verse 코드 작성 단계에는 값이 없다 |
| 언제 필요한가 | 장치 대량 배치 시작 / 컴파일 에러 복붙 왕복 반복 |

## 왜 이 환경에서는 안 되나

UEFN MCP 서버는 **UEFN 에디터 프로세스에 붙는** 물건이다. 구조가 2프로세스다.

```
Claude Code  ←→  MCP 서버(외부 파이썬)  ←→  리스너(UEFN 내부)  ←→  UEFN 에디터
```

오른쪽 두 개가 네 PC에서 돌아야 한다. 클라우드 세션은 GitHub 레포만 클론된 격리 컨테이너라 네 PC의 프로세스에 도달할 경로가 없다. 앱 종류(웹/데스크톱/VS Code) 문제가 아니라 **실행 위치** 문제다.

| 실행 위치 | 동작 |
|---|---|
| PC의 VS Code 확장 / 터미널 CLI / 데스크톱 앱 | ✅ |
| 클라우드 세션 | ❌ |

세 곳에서 동일하게 쓰려면 user 스코프로 등록한다. `-s local`(기본값)은 등록한 디렉토리에서만 보인다.

```
claude mcp add -s user uefn -- python C:\path\to\uefn_mcp_server.py
```

## 후보

| 레포 | 성격 |
|---|---|
| [KirChuvakov/uefn-mcp-server](https://github.com/KirChuvakov/uefn-mcp-server) | 에디터 직접 제어. 28개 툴. ★62 |
| [quangdang46/uefn-verse-mcp](https://github.com/quangdang46/uefn-verse-mcp) | 라이브 UEFN 브릿지 |
| [Verse UEFN](https://mcpmarket.com/server/verse-uefn) | Verse 코드를 API 다이제스트로 검증 (에디터 제어 아님) |

KirChuvakov 기준 툴 구성:

- **Actors** — 스폰 / 삭제 / 트랜스폼 / 선택 / 조회
- **Assets** — 목록 / 검색 / 이름변경 / 복제
- **Level·Viewport** — 레벨 저장, 카메라 이동, 프로젝트 정보
- **System** — `execute_python`(에디터 내 임의 파이썬 실행), 에디터 로그 읽기

요구사항: Python 3.10+ / `pip install mcp` / UEFN 프로젝트 설정에서 **Python Editor Script Plugin** 활성화.

UEFN Python은 Epic 공식 기능이다 ([Python Tools in UEFN](https://dev.epicgames.com/documentation/fortnite/python-tools-in-uefn)). 비공식 해킹이 아니다.
※ 조사 시점에 이 도메인이 프록시에서 차단돼 검색 결과로만 확인했다. **PC에서 직접 열어 재확인할 것.**

## 되는 것 / 안 되는 것

| 되는 것 | 안 되는 것 |
|---|---|
| 액터 스폰·이동·삭제 | 플레이테스트 |
| 에셋 목록·검색·정리 | API에 노출 안 된 장치 옵션 패널 클릭 |
| 레벨 저장, 카메라 이동 | Push Changes / 세션 시작 **[미확인]** |
| 에디터 로그 읽기 → 컴파일 에러 진단 | 재미 판단 |
| `.verse` 파일 작성·수정 | ← **MCP 없어도 이미 된다** |

마지막 줄이 판단의 핵심이다. **Verse 코딩 자체는 MCP가 필요 없다.** MCP가 더하는 값은 "쓴 코드가 실제로 컴파일되는지 직접 확인"하는 부분이다.

그리고 화면·마우스 제어가 아니다. **API 호출**이다. 노출된 함수만 부를 수 있다.

## 리스크

| 리스크 | 내용 |
|---|---|
| **검증 실패** | Python으로 만든 에셋 일부는 validation·publish에서 실패한다 (Epic 문서 경고). 게시가 목표면 직격 |
| **임의 코드 실행** | `execute_python`은 PC에서 아무 파이썬이나 돌린다. 개인 레포다 |
| **버전 드리프트** | UEFN은 2~3주마다 바뀐다. 에디터 API가 흔들리면 툴이 죽는다 |
| **크래시** | 문서에 이미 경고 — UI 만들 때 `tk.Tk()` 쓰면 에디터가 죽는다. `tk.Toplevel()` 쓸 것 |
| **되돌리기** | 잘못 스폰·삭제한 걸 되돌리는 건 자동이 아니다 |
| **상시 가동** | 에디터가 켜져 있고 리스너가 붙어 있어야 한다 |

## 토큰

- **늘어남** — 툴 정의가 컨텍스트에 실린다. 28개면 3~8k **[추정]**. 대량 조회(`list_assets` 등) 결과도 비싸다
- **줄어듦** — Claude Code는 MCP 툴을 지연 로딩한다(이름만 싣고 스키마는 필요할 때). 그리고 **에러 로그 복붙 왕복이 사라진다** — 왕복 한 번이 툴 정의 전체보다 비싸다
- **[추정]** 요청당 고정비는 조금 오르고, 총 세션 토큰은 오히려 줄 가능성이 높다

## 도입 절차 (조건 충족 시)

1. **레포 코드를 먼저 읽는다.** `execute_python`은 PC 전권이다. 안 읽고 켜지 않는다
2. **빈 테스트 프로젝트**에 먼저 건다. FREEZE TAG 본 프로젝트 아님
3. UEFN 프로젝트 설정에서 Python Editor Script Plugin 활성화
4. `pip install mcp`, Python 3.10+ 확인
5. `claude mcp add -s user uefn -- python <경로>`
6. **Python으로 만든 에셋으로 publish validation을 반드시 한 번 돌려본다.** Epic이 경고한 지점이다
7. 통과하면 본 프로젝트에 적용
