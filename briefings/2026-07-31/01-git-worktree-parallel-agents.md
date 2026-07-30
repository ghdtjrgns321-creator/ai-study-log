# 오늘의 AI 개념: Git Worktree 기반 병렬 에이전트 실행(Parallel Agent Isolation via Git Worktree)

> 작성일: 2026-07-31 · 분류: agentic-coding

## 한 줄 정의

여러 코딩 에이전트가 같은 폴더의 같은 파일을 동시에 고치다 서로 덮어써 망가지는 문제를, 브랜치마다 독립된 작업 폴더를 만들어주는 git worktree로 막는 방식이다.

## 쉬운 설명

에이전틱 코딩 도구가 늘면서 자연스럽게 나오는 요구가 "에이전트 여러 개를 동시에 돌리고 싶다"는 것이다. 가장 단순한 방법은 터미널 두 개를 열고 각각 Claude Code를 실행하는 것이지만, 두 세션이 같은 디렉터리를 공유하면 한 에이전트가 파일을 고치는 도중 다른 에이전트가 그 파일을 읽어 절반만 수정된 상태를 근거로 작업을 이어가는 충돌이 생긴다.

git에는 원래 커밋·브랜치·히스토리를 담는 "저장소 본체(object store)"와, 실제로 디스크에 보이는 파일들인 "작업 디렉터리(working tree)"가 개념적으로 분리되어 있다. 평소에는 이 둘이 1대1로 묶여 있어서 한 폴더는 한 번에 한 브랜치만 보여준다. git worktree는 이 결합을 풀어, 저장소 본체는 하나만 유지한 채 서로 다른 브랜치를 체크아웃한 여러 개의 작업 디렉터리를 동시에 둘 수 있게 한다.

비유하면 본체 저장소는 원본 문서이고, 각 worktree는 그 문서를 부서별로 복사해 각자 다른 페이지를 동시에 고칠 수 있게 만든 사본이다. 사본끼리는 서로의 수정 내용을 실시간으로 침범하지 않지만, 결국 같은 원본 히스토리를 공유하기 때문에 나중에 다시 합칠 수 있다.

이는 서브에이전트나 에이전트 팀 같은 "작업 조율" 개념과는 층위가 다르다. 서브에이전트는 하나의 세션 안에서 작업을 누구에게 맡길지 조율하는 것이고, worktree는 그렇게 맡겨진 작업이 파일 시스템 차원에서 서로 부딪히지 않도록 격리하는 것이다. 실제로는 두 가지를 함께 쓴다 — 서브에이전트를 만들 때 "격리 방식: worktree"로 지정하면, 그 서브에이전트는 작업이 끝나면 자동으로 정리되는 임시 작업 디렉터리를 받는다.

## 동작 원리

```
① git worktree add ../프로젝트-기능명 -b 새브랜치 origin/main
     → 저장소 본체(.git)는 하나 그대로, 새 디렉터리 + 새 브랜치 생성
② 각 worktree 디렉터리에서 별도로 Claude Code(또는 Codex) 세션 실행
     → 세션 A: 디렉터리 X, 브랜치 feature-a
     → 세션 B: 디렉터리 Y, 브랜치 feature-b
③ 두 세션은 서로 다른 디스크 경로의 파일만 읽고 쓴다
     → 같은 파일을 동시에 건드릴 물리적 여지가 없음
④ 각 브랜치를 커밋 → 원격에 푸시 → PR로 병합
⑤ 세션 종료 시 worktree 자동 정리(커밋 안 된 변경이 없으면)
```

Claude Code에서는 `claude --worktree 이름` 명령으로 `.claude/worktrees/이름/` 아래에 격리된 작업 폴더와 `worktree-이름`이라는 새 브랜치를 자동 생성한다. `.env`처럼 git이 추적하지 않는 파일은 `.worktreeinclude` 파일에 패턴을 적어두면 새 worktree를 만들 때마다 자동으로 복사된다. 커스텀 서브에이전트 설정에 `isolation: worktree`를 지정하면, 그 서브에이전트가 실행될 때마다 임시 worktree가 만들어지고 변경 사항 없이 끝나면 자동으로 제거된다.

## 구체 예시·사례

한 실전 튜토리얼 영상에서는 "AI 에이전트 프로젝트"라는 하나의 저장소 안에 `dashboard-creation`(백엔드에 DeFi Llama 연동 기능 추가)과 `hubspot-access`(프론트엔드에 전체선택/해제 체크박스 추가) 두 개의 worktree를 만들고, 화면을 분할해 각 디렉터리에서 별도의 코딩 에이전트 세션을 동시에 돌린다. 두 작업이 끝난 뒤 각 디렉터리에서 `git status`를 확인하면 한쪽은 PHP 백엔드 파일만, 다른 쪽은 HTML/CSS 프론트엔드 파일만 바뀌어 있어 서로 영향을 주지 않았음이 확인되고, 각각 별도 PR로 staging 브랜치에 병합된다.

## 비슷한 것과 비교

| 구분 | Git Worktree | 서브에이전트 / 에이전트 팀 |
|---|---|---|
| 격리 대상 | 파일 시스템(디스크 상의 작업 디렉터리) | 작업 자체(누가 무엇을 할지 조율) |
| 목적 | 여러 세션이 같은 파일을 동시에 건드리지 못하게 차단 | 하나의 세션 안에서 하위 작업을 위임·조율 |
| 병렬성의 형태 | 서로 다른 브랜치·다른 폴더에서 완전히 독립적으로 진행 | 같은 목표를 향해 협력하거나 역할을 분담 |
| 함께 쓰기 | 서브에이전트에 `isolation: worktree`를 지정해 결합 가능 | 결합 시 각 서브에이전트가 자기만의 임시 worktree를 받음 |

선택 기준: 오늘 처리할 작업이 서로 파일을 공유하지 않는 두 개 이상이거나, 하나의 설계 결정에 대해 서로 다른 접근을 모두 시도해보고 싶다면 worktree를 쓴다. 반대로 작업 하나가 코드베이스 전체에 걸쳐 있거나 성격이 탐색적이라면 단일 세션을 유지하는 편이 낫다.

## 왜 지금 중요한가

Claude Code는 `--worktree` 플래그와 서브에이전트 worktree 격리를 공식 문서로 제공하고 있으며, Cursor의 Parallel Agents는 최대 8개의 에이전트를 각각 독립된 worktree에서 동시에 돌리는 기능을, OpenAI의 Codex CLI도 worktree 기반 병렬 실행을 지원한다. 즉 특정 벤더의 실험 기능이 아니라 주요 에이전틱 코딩 도구 전반이 같은 패턴으로 수렴하고 있다는 점에서 지금 실무에 바로 적용할 가치가 있는 기법이다.

- [worktree를 사용하여 병렬 세션 실행 — Claude Code 공식 문서](https://code.claude.com/docs/ko/worktrees)
- [Claude Code로 12배 병렬 개발하기 — Worktree x Agents Team 실전기](https://www.gpters.org/dev/post/12x-parallel-development-claude-JEr2GK2Yya8YSwd)

## 회계법인 AI 직무 연결 포인트

회계법인이 감사·세무 업무를 지원하는 내부 자동화 도구(예: 계정과목별 이상거래 점검 스크립트, 내부통제 테스트 자동화)를 자체 개발할 때, 매출채권·재고·고정자산처럼 서로 독립적인 여러 계정과목의 검증 로직을 worktree별로 나눠 동시에 개발·테스트하면 개발 속도를 높이면서도 각 로직이 서로의 코드를 침범해 망가뜨리는 사고를 줄일 수 있다.

내부통제 자동화 플랫폼처럼 여러 통제 항목(위험평가·설계평가·운영평가·미비점 관리)을 병렬로 구현해야 하는 프로젝트에서는, 항목별로 worktree를 나눠 각각의 에이전트에게 맡기고 완료된 것부터 순차적으로 병합하는 방식이 실무적으로 유용하다.

영상에서 소개한 "동일 작업을 두 worktree에 맡겨 결과를 비교해 채택하는" 패턴은, 정답이 하나로 정해지지 않은 이상거래 탐지 규칙 설계처럼 여러 접근법을 모두 구현해본 뒤 더 나은 쪽을 고르는 상황에 그대로 적용할 수 있다.

## 핵심 용어·논쟁

- **Object store** — git 저장소의 커밋·브랜치·히스토리 전체가 저장되는 본체. worktree가 여러 개여도 이것은 하나만 공유된다.
- **Working tree** — 실제 디스크에 파일로 보이는 체크아웃 상태. worktree마다 별도로 존재한다.
- **.worktreeinclude** — git이 추적하지 않는 `.env` 등의 파일을 새 worktree 생성 시 자동 복사하도록 지정하는 설정 파일.
- **isolation: worktree** — 커스텀 서브에이전트 설정에서, 해당 서브에이전트가 실행될 때마다 임시 worktree를 받도록 지정하는 옵션.
- **에이전트 대 에이전트 비교 패턴** — 같은 작업을 두 worktree에서 각각 진행시켜 결과를 비교한 뒤 더 나은 쪽만 채택하는 활용법.

worktree 기반 병렬화가 실제 생산성을 얼마나 끌어올리는지는 아직 표준화된 정량 벤치마크가 없고, 대부분 개별 개발자의 경험담 수준에 머물러 있다. 또한 병합 시 여러 worktree의 변경 범위가 우연히 겹치면 결국 병합 충돌을 사람이 해결해야 한다는 한계는 그대로 남는다.

## 자료 깊이 읽기

### worktree를 사용하여 병렬 세션 실행 — 한국어/공식 문서/중
Claude Code 공식 문서. `--worktree` 플래그로 격리된 worktree를 생성하는 방법, 기본 브랜치 선택 규칙(`origin/HEAD` 기준, `worktree.baseRef` 설정으로 로컬 HEAD 기준 전환 가능), `.worktreeinclude`로 gitignore된 파일을 자동 복사하는 방법, 서브에이전트에 `isolation: worktree`를 지정해 임시 worktree를 자동 발급·정리하는 방법, PR 번호로 바로 worktree를 만드는 법(`claude --worktree "#1234"`), git 외 버전관리 시스템을 위한 `WorktreeCreate`/`WorktreeRemove` 훅까지 다룬다.

### Git Worktrees Explained — Run Multiple AI Agents in Parallel (Claude Code Tutorial) (YouTube) — 영어/영상/중
개인 개발자가 실제 화면 녹화로 worktree 생성부터 두 개의 코딩 에이전트를 동시에 운용해 서로 다른 기능(백엔드 연동, 프론트엔드 UI)을 완성하고 각각 PR로 병합하기까지 전 과정을 시연한다. "에이전트 대 에이전트 비교" 패턴과 tmux 결합 운용법까지 자막을 직접 확인해 정리했다 — **[상세 요약 보기](videos/git-worktree-parallel-agents.md)**.

**그 외 참고**
- [Claude Code Git Worktree Setup: Run Multiple Agents in Parallel](https://www.youtube.com/watch?v=ryGJLXruUxs) — 영어, YouTube, 초급
- [Claude Code로 12배 병렬 개발하기 — Worktree x Agents Team 실전기](https://www.gpters.org/dev/post/12x-parallel-development-claude-JEr2GK2Yya8YSwd) — 한국어, 블로그, 중급

## 자가 점검 질문

1. git worktree가 왜 같은 디렉터리에서 에이전트 두 개를 그냥 실행하는 것보다 안전한지, object store와 working tree 개념으로 설명해보라.
2. worktree와 서브에이전트(또는 에이전트 팀)는 각각 무엇을 격리·조율하는지 역할 차이를 말해보라.
3. 병렬로 진행한 여러 worktree의 작업을 병합할 때 여전히 남는 리스크는 무엇이며 어떻게 완화할 수 있는가?
