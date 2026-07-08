# 오늘의 AI 개념: 클로드 코드 매뉴얼 권한모드 기본값 전환(Claude Code Manual Permission Mode Default)

> 작성일: 2026-07-09 · 분류: claude-code

## 한 줄 정의

Claude Code v2.1.200(2026-07-03 출시)부터 CLI·VS Code·JetBrains 등 모든 실행 표면에서, 파일 편집·셸 명령·네트워크 요청 등 읽기 이외의 모든 작업에 사용자의 명시적 승인을 요구하는 "Manual" 모드가 표준 기본값으로 자리잡았다.

## 쉬운 설명

Claude Code는 원래도 "default"라는 설정값으로 파일을 고칠 때마다 승인을 묻는 동작을 갖고 있었다. 그런데 지난 몇 달간 승인 프롬프트를 건너뛰는 Auto 모드가 여러 플랜에 확대 적용되면서, 실질적으로 많은 사용자 환경에서 에이전트가 알아서 작업을 진행하는 흐름이 널리 퍼졌다. v2.1.200은 이 흐름에 제동을 걸어, "default" 모드에 "Manual"이라는 이름표를 명시적으로 붙이고 이를 모든 실행 표면의 표준으로 재확인했다.

비유하자면 신입 인턴에게 처음에는 모든 문서 발송 전에 팀장 결재를 받게 하다가(Manual), 일이 손에 익으면 특정 유형의 문서는 자동 발송하도록 권한을 넓혀주는(Auto) 구조와 비슷하다. 문제는 인턴이 일을 잘한다고 해서 조직이 자동으로 결재 라인을 없애서는 안 된다는 점인데, 그동안 이 자동화 범위가 조용히 넓어져 있었다. 이번 변경은 "새로 설치하거나 업데이트한 사람은 일단 결재 라인부터 다시 켜고 시작한다"는 방향으로 되돌린 것이다.

기존의 `bypassPermissions`(모든 검사 생략)나 `acceptEdits`(파일 편집만 자동 승인)와 달리, Manual 모드는 읽기를 제외한 모든 행위에 예외 없이 프롬프트를 띄운다는 점에서 가장 보수적인 모드다. Auto 모드처럼 별도의 AI 분류기가 위험도를 판단해 자동으로 넘어가는 절차 자체가 없다는 것이 핵심 차이다.

## 동작 원리

Manual 모드와 Auto 모드는 승인 여부를 결정하는 절차가 근본적으로 다르다.

Manual 모드(config 값 `default`)는 판단 로직이 없다. 읽기 작업만 무조건 통과시키고, 파일 쓰기·셸 명령·네트워크 요청 등 그 외 모든 행위는 종류를 가리지 않고 매번 사용자에게 승인을 묻는다. `.git`, `.claude`, `.vscode` 등 "보호된 경로"에 대한 쓰기는 `bypassPermissions`를 제외한 어떤 모드에서도 자동 승인되지 않는다.

Auto 모드는 반대로 별도의 분류기 모델이 판단을 대신한다. 공식 문서에 명시된 결정 순서는 다음과 같다. 1) 사용자가 설정한 허용·거부 규칙에 걸리면 즉시 결정(단, 보호 경로 쓰기는 규칙과 무관하게 항상 분류기로 보내짐), 2) 작업 디렉터리 안의 읽기·편집은 자동 승인, 3) 그 외 모든 행위는 분류기로 전달, 4) 분류기가 차단하면 Claude에게 사유가 전달되고 대안을 시도한다.

Anthropic 엔지니어링 블로그("How we built Claude Code auto mode")를 인용한 여러 매체에 따르면 이 분류기는 2단계 파이프라인이다. 1단계는 과잉 차단 쪽으로 편향된 빠른 단일 토큰 필터이고, 여기서 걸린 것만 2단계의 사고연쇄(chain-of-thought) 추론으로 재검토한다. 이 파이프라인의 실측 성능은 오탐률(안전한 행동을 차단) 0.4%, 미탐률(위험한 행동을 통과시킴) 17%로 보고되었다. 즉 100번 중 17번은 "과잉 행동"이 걸러지지 않고 실행될 수 있다는 뜻이며, 이 수치가 기본값을 다시 보수적으로 되돌린 배경 중 하나로 거론된다.

## 비슷한 것과 비교

| 모드 | 승인 없이 실행되는 범위 | 적합한 상황 |
| --- | --- | --- |
| `default`(Manual) | 읽기만 | 처음 시작, 민감한 작업, 회계·재무 데이터 관련 작업 |
| `acceptEdits` | 읽기 + 파일 편집 + `mkdir`/`mv`/`cp` 등 기본 파일시스템 명령 | 검토 중인 코드를 반복 수정할 때 |
| `plan` | 읽기만(편집 자체가 불가) | 변경 전 코드베이스 탐색·설계 |
| `auto`(연구 프리뷰) | 분류기 통과 시 사실상 전부 | 방향을 신뢰하는 장시간 작업 |
| `dontAsk` | 사전 승인된 도구만 | 잠긴 CI·스크립트 환경 |
| `bypassPermissions` | 전부(보호 경로 포함) | 인터넷이 차단된 격리 컨테이너·VM 전용 |

선택 기준은 단순하다. 결과를 되돌리기 어렵거나 민감한 데이터를 다루면 Manual, 이미 신뢰가 쌓인 반복 작업이면 acceptEdits, 변경 없이 조사만 할 때는 plan을 쓰고 auto·bypassPermissions는 각각 "연구 프리뷰의 자동화"와 "완전히 격리된 샌드박스"라는 좁은 용도에만 한정한다.

## 왜 지금 중요한가

Claude Code 공식 changelog는 v2.1.200(2026-07-03 출시) 항목에서 "CLI, `--help`, VS Code, JetBrains 전반에 걸쳐 'default' 권한 모드를 'Manual'로 변경했다"고 명시하고 있으며, `--permission-mode manual`과 `"defaultMode": "manual"`이 기존 `default` 표기와 함께 허용된다고 밝혔다. 이 라벨과 별칭은 v2.1.200 이상에서만 동작한다.

같은 문서에 따르면 상태 표시줄에 회색 `⏸ manual mode on` 배지를 띄워 현재 모드를 항상 보이게 하는 기능은 v2.1.203부터 추가되었다. 즉 "기본값을 되돌리는 변경"과 "그 상태를 눈에 띄게 만드는 변경"이 며칠 간격으로 순차적으로 이뤄진 셈이다.

TechTimes 보도는 이 변경에 별도의 공지 블로그나 보도자료가 동반되지 않았다고 전하며, 2026년 4월의 운영 서버 장애(Claude Code의 지시 오해석 관련)와 2026년 6월 Microsoft 보안 연구진이 공개한 Claude Code GitHub Action의 프롬프트 인젝션 취약점(CI/CD 워크플로 시크릿 노출 가능) 등이 배경으로 거론된다고 분석했다.

- [권한 모드 선택 - Claude Code Docs](https://code.claude.com/docs/en/permission-modes)
- [권한 모드 선택 - Claude Code Docs(한국어)](https://code.claude.com/docs/ko/permission-modes)
- [Claude Code changelog](https://code.claude.com/docs/en/changelog)
- [Claude Code Defaults to Human Approval: Auto Mode Requires Explicit Opt-In - TechTimes](https://www.techtimes.com/articles/319874/20260707/claude-code-defaults-human-approval-auto-mode-requires-explicit-opt.htm)

## 회계법인 AI 직무 연결 포인트

이 변경의 핵심은 "에이전트가 잘 작동하니 자동화 범위를 넓히자"가 아니라 "잘 작동하는 것과 별개로, 되돌리기 어려운 행위는 기본적으로 사람이 승인해야 한다"는 설계 철학이다. 이는 회계·감사에서 내부통제를 설계할 때의 기본 원칙과 정확히 같은 결이다. 재무제표에 영향을 주는 분개 수정, 감사조서 결론 반영, 고객 데이터 전송처럼 되돌리기 어렵거나 신뢰성에 직결되는 행위는 AI가 아무리 정확도가 높아도 자동 실행이 아니라 담당자 승인을 거치도록 기본값을 잠가두어야 한다는 뜻이다.

Auto 모드 분류기의 미탐률 17%라는 수치는 시사하는 바가 크다. 이는 "AI가 위험한 행동을 인식은 하지만, 사용자가 이미 그 범위까지 동의했는지 판단을 잘못하는" 경우가 실패의 주된 유형이라는 점과 맞물린다. 감사 업무에 비유하면, AI 에이전트가 "이 계정과목을 수정해도 된다"는 상위 지시를 받았을 때 그 지시가 구체적으로 어디까지의 조정을 포괄하는지(예: 특정 거래 취소까지 포함하는지) 오판할 수 있다는 뜻이며, 이는 업무 분장(segregation of duties)과 승인 한도(approval threshold)를 사람이 명시적으로 설정해야 하는 이유와 동일하다.

또한 Manual 모드가 매번 프롬프트를 남기고, Auto 모드에서 차단된 행위가 `/permissions`의 "최근 거부됨" 로그로 남는 구조는 감사 증거 관점에서도 유용한 설계다. AI 에이전트 도구를 회계법인 워크플로에 도입할 때, 어떤 행위가 자동 승인되고 어떤 행위가 반드시 사람의 서명을 거치는지, 그리고 그 판단 과정이 로그로 남는지를 벤더 평가 기준에 포함시키는 것이 IT 일반통제(ITGC) 실사에서 점점 중요해질 것으로 보인다.

## 핵심 용어·논쟁

- Manual 모드(구 default) — 읽기 외 모든 행위에 예외 없이 사람의 승인을 요구하는 가장 보수적인 권한 모드.
- Auto 모드 — 별도 분류기 모델이 위험도를 판단해 승인 프롬프트를 대부분 생략하는 연구 프리뷰 모드.
- 분류기(Classifier) — Auto 모드에서 각 행위를 실행 전에 평가하는 2단계 AI 파이프라인(빠른 필터 + 사고연쇄 재검토).
- 보호된 경로(Protected Paths) — `.git`, `.claude` 등 어떤 모드에서도(단, bypassPermissions 제외) 자동 승인되지 않는 경로.
- 승인 피로(Approval Fatigue) — 반복되는 승인 요청에 사용자가 습관적으로 "예"를 누르게 되어 승인 절차가 실효성을 잃는 현상.

현재진행형 논쟁은 자율성과 안전성의 트레이드오프다. Auto 모드 지지 측은 매번 승인을 누르는 절차 자체가 승인 피로를 유발해 오히려 위험한 행위도 무심코 통과시킬 수 있다고 본다. 반면 이번 기본값 회귀가 보여주듯, 분류기의 미탐률이 0에 가깝지 않은 이상 "기본은 보수적으로, 자동화는 옵트인으로" 두는 편이 낫다는 입장도 강하다. 아울러 이런 안전 관련 기본값 변경이 별도의 공지 없이 조용히 배포된 점을 두고, 투명성 측면에서 문제를 제기하는 시각도 있다.

## 자료 깊이 읽기

### 권한 모드 선택 - Claude Code 공식 문서 — 한국어/영어, 공식 문서, 중급
Manual(`default`)·`acceptEdits`·`plan`·`auto`·`dontAsk`·`bypassPermissions` 여섯 개 권한 모드를 표로 정리하고, 각 모드가 프롬프트 없이 허용하는 범위를 상세히 규정한다. Manual 라벨과 `manual` 별칭이 v2.1.200부터 지원된다는 점, 상태 표시줄의 `⏸ manual mode on` 배지는 v2.1.203부터 추가됐다는 점을 버전별로 명시한다. Auto 모드는 "연구 프리뷰이며 안전을 보장하지 않는다"고 공식적으로 경고하고 있고, 분류기가 차단하는 항목(강제 푸시, 프로덕션 배포, 시크릿 전송 등)과 허용하는 항목(작업 디렉터리 내 로컬 파일 작업 등)을 버전별 변경 이력과 함께 나열한다. `.git`, `.claude` 등 보호 경로는 `bypassPermissions`를 제외한 모든 모드에서 규칙 설정과 무관하게 항상 프롬프트가 뜨도록 설계되어 있다. 서브에이전트에도 동일한 분류기가 생성 시점·실행 중·종료 시점 세 단계로 적용된다는 세부 동작까지 다룬다.

### Claude Code Changelog — 영어, 공식 문서, 초급
v2.1.200(2026-07-03) 항목에서 "CLI, `--help`, VS Code, JetBrains 전반에 걸쳐 'default' 권한 모드를 'Manual'로 변경했다"는 한 줄짜리 공식 변경 내역을 확인할 수 있다. `--permission-mode manual`과 `"defaultMode": "manual"`이 기존 `default` 값과 함께 허용된다는 것, 이 표기가 v2.1.200부터 유효하다는 버전 정보를 정확히 제공한다. 짧은 문서지만 이번 브리핑에서 다루는 버전·날짜의 1차 근거가 된다.

**그 외 참고**
- [Claude Code Defaults to Human Approval: Auto Mode Requires Explicit Opt-In - TechTimes](https://www.techtimes.com/articles/319874/20260707/claude-code-defaults-human-approval-auto-mode-requires-explicit-opt.htm) — 영어, 뉴스 기사, 초급
- [How we built Claude Code auto mode: a safer way to skip permissions - Anthropic](https://www.anthropic.com/engineering/claude-code-auto-mode) — 영어, 공식 엔지니어링 블로그, 중급
- [자동 모드 구성 - Claude Code Docs(한국어)](https://code.claude.com/docs/ko/auto-mode-config) — 한국어, 공식 문서, 중급

## 자가 점검 질문

1. Manual 모드와 Auto 모드는 승인 여부를 결정하는 절차 자체가 어떻게 다른가?
2. 내가 속한 조직에서 재무 데이터를 다루는 AI 에이전트를 도입한다면, 어떤 행위 유형까지 Manual(사람 승인)로 남기고 어떤 유형을 자동화 대상으로 삼아야 할까?
3. Auto 모드 분류기의 미탐률 17%라는 수치는 이 기능을 실무에 도입할 때 어떤 리스크로 이어질 수 있는가?
