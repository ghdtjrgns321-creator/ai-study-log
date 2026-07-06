# 오늘의 AI 개념: 백그라운드 서브에이전트와 알림 훅(Background Subagents & Notification Hooks)

> 작성일: 2026-07-06 · 분류: claude-code

## 한 줄 정의

Claude Code가 하위 작업을 맡은 서브에이전트를 메인 대화를 막지 않고 백그라운드에서 실행하고, 작업이 끝나거나 입력이 필요해지면 알림 훅으로 사용자에게 알려주는 기능이다.

## 쉬운 설명

기존에는 서브에이전트(Task 도구로 호출하는 하위 AI)를 부르면 메인 세션이 그 작업이 끝날 때까지 기다려야 했다. 2026년 7월 1일 배포된 버전(v2.1.198)부터는 서브에이전트가 기본적으로 백그라운드에서 실행되어, 메인 세션은 그동안 다른 작업을 계속하다가 서브에이전트가 끝나면 알림을 받는 방식으로 바뀌었다.

비유하자면, 예전에는 부장이 신입사원 한 명에게 조사를 시켜놓고 그 사람이 끝낼 때까지 팔짱 끼고 기다려야 했다면, 이제는 여러 명에게 동시에 일을 맡기고 자기 할 일을 하다가 보고가 들어오면 그때 확인하는 식이다. `/tasks` 명령으로 지금 백그라운드에서 뭐가 돌고 있는지 확인할 수 있고, `Ctrl+B`로 실행 중인 작업을 즉시 백그라운드로 보낼 수도 있다.

알림 훅(Notification hook)은 서브에이전트가 입력을 기다리거나(`agent_needs_input`) 작업을 마쳤을 때(`agent_completed`) 발동되는 훅이다. 훅 자체는 알림을 막거나 내용을 바꿀 수 없고, 대신 데스크톱 알림을 띄우거나 사내 슬랙으로 전달하는 등의 부수효과를 붙이는 용도로 쓰인다.

기존 서브에이전트 개념과의 차이는 실행 모델에 있다. Task 도구로 서브에이전트를 부르는 것 자체는 이전에도 가능했지만 기본은 동기 실행(끝날 때까지 대기)이었다. 이번 변화는 비동기·백그라운드를 기본값으로 바꾸고, 훅이라는 관측 지점을 표준화한 것이 핵심이다.

## 왜 지금 중요한가

Claude Code 공식 changelog에 따르면 v2.1.198(2026년 7월 1일)에서 "Subagents now run in the background by default, so Claude keeps working while they run and is notified when they finish"라는 변경과 함께, 백그라운드 세션이 입력을 기다리거나 끝났을 때 `Notification` 훅이 `agent_needs_input`/`agent_completed` 이벤트로 발동되는 기능이 추가됐다. 바로 다음 날인 v2.1.199(7월 2일)에서는 슬래시 스킬을 이어붙여 최대 5개까지 한 번에 불러오는 스킬 스태킹 기능도 함께 들어왔다.

- [Claude Code changelog](https://code.claude.com/docs/en/changelog)
- [Hooks reference](https://code.claude.com/docs/en/hooks)
- [How and when to use subagents in Claude Code](https://claude.com/blog/subagents-in-claude-code)

## 회계법인 AI 직무 연결 포인트

여러 계정과목별 조서 검토나 잔액 확인처럼 서로 독립적인 하위 작업을, 각각 서로 다른 서브에이전트에 병렬로 맡기고 하나가 끝날 때마다 알림을 받아 검토하는 워크플로우를 구성할 수 있다. 실제로 이 브리핑 자동화 자체가 그런 백그라운드 서브에이전트 방식으로 동작한다.

알림 훅을 사내 메신저(Slack·Teams)에 연동하면, 야간에 돌려둔 배치성 감사 스크립트(예: 전수 거래 이상탐지)가 끝났을 때 담당 회계사에게 바로 알려줄 수 있어 상시감사(continuous auditing) 체계와 자연스럽게 맞물린다.

다만 백그라운드 서브에이전트는 사전 승인된 권한만 자동으로 실행되고 나머지는 자동으로 거부되므로, 회계 데이터나 고객 정보에 접근하는 자동화를 설계할 때는 어떤 권한을 사전 승인할지, 그리고 그 승인 범위가 적절한지를 신중히 검토해야 한다.

## 학습 자료

- [Claude Code changelog](https://code.claude.com/docs/en/changelog) — 영어, 텍스트, 중급
- [Hooks reference](https://code.claude.com/docs/en/hooks) — 영어, 텍스트, 중급
- [How and when to use subagents in Claude Code](https://claude.com/blog/subagents-in-claude-code) — 영어, 텍스트, 입문
- [Claude Code Hooks: Complete Guide to All 12 Lifecycle Events](https://claudefa.st/blog/tools/hooks/hooks-guide) — 영어, 텍스트, 중급

## 자가 점검 질문

1. 서브에이전트가 "백그라운드 기본 실행"으로 바뀌면서 기존 동기 실행 방식과 무엇이 달라지는가?
2. 감사 업무에서 여러 계정과목 조서를 병렬 서브에이전트로 나눠 처리한다면, 어떤 순서·의존관계를 고려해야 하는가?
3. 알림 훅에 사내 데이터를 흘려보낼 때 어떤 보안·정보보호 리스크를 점검해야 하는가?
