---
description: DEV_STATE.md를 갱신해 세션을 닫는다 (프로토콜 v2.0 — 8KiB 한도, 소유권 준수)
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git branch:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(wc:*), Bash(ls:*)
---

# 상태 아카이브 (/dev-state)

목표: **다음 세션(어느 AI든)이 루트의 `AGENTS.md`+`DEV_STATE.md` 두 파일만 읽고 바로 이어서 작업할 수 있게 한다.**

## 1. 먼저 확인한다 (추측 금지)

```
1. git status / git diff / git log --oneline -20   (git 저장소인 경우)
2. 기존 DEV_STATE.md — 단, 코드·실제 파일과 어긋나면 실제가 정답이다
3. 테스트·빌드 결과 — 돌려본 것만. 안 돌렸으면 NOT_RUN
4. Docs/AI 작업 잠금/ — 내가 만든 잠금이 남아 있으면 해제
```

## 2. 루트 `DEV_STATE.md`를 갱신한다 (없으면 생성)

표준 형식 (공통 프로토콜 §3):

```markdown
# DEV_STATE
> 갱신: YYYY-MM-DD HH:MM · 갱신자: <AI 이름> · (git이면) 브랜치
## 지금 목표
## 완료된 것            (검증 방법까지)
## 핵심 결정과 이유      (왜 — 이게 제일 가치 있다)
## 핵심 파일            (경로 + 한 줄 역할)
## 게이트·테스트 현황    (정본 출처 명시. 실행 안 했으면 NOT_RUN)
## 알려진 문제
## 실패한 접근          (재시도 금지 목록)
## 다음 할 일           (첫 항목부터 바로 실행 가능하게)
```

## 3. 규칙

- **크기 한도 8KiB.** 쓰고 나서 `wc -c DEV_STATE.md`로 확인한다. 넘으면 심층 문서(`Docs/`)로 빼고 링크만 남긴다
- **소유권:** 실기 PASS/FAIL은 테스트 기록 문서가 정본이다 (있으면 거기 먼저 기록). DEV_STATE의 게이트 표는 사본 — 정본 출처를 명시한다. **실행 안 한 검증은 절대 PASS로 적지 않는다**
- 확인된 사실만. `[확인: 출처]` / `[추정]` / `[미확인]` 표기. 다른 AI의 보고는 `[확인: ○○ 보고]`
- 해결된 이슈·끝난 논의는 삭제. 의미 있는 옛 상태는 역사 문서로 이동 (삭제 아님)
- **민감정보(비밀번호·토큰·키·쿠키) 절대 금지**
- 코드 붙여넣기 금지 — 경로와 역할만

## 4. 동기화

- **일반 git 저장소:** 상태 파일 변경만 커밋하고 푸시한다 (다른 기기·클라우드 세션이 읽도록)
- **UEFN 프로젝트 루트:** git 금지 — Revision Control이 동기화한다. 체크인은 사용자가 에디터에서 하므로, 갱신 후 "Check-in Changes에 DEV_STATE.md가 잡히는지 확인해달라"고 알린다

## 5. 마지막

무엇을 추가·삭제·수정했는지, 파일 크기와 함께 3줄로 보고한다.
