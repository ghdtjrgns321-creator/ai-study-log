# 오늘의 AI 개념: 클로드 시큐리티 플러그인(Claude Security Plugin)

> 작성일: 2026-08-06 · 분류: agentic-coding

## 한 줄 정의

클로드 시큐리티 플러그인은 Claude Code 세션 안에서 여러 서브에이전트가 역할을 나눠 저장소 전체 또는 변경사항을 감사하듯 훑어 취약점을 찾고, 발견 사항을 독립적으로 재검증한 뒤 검토용 패치 파일까지 만들어주는 온디맨드 보안 스캐너다.

## 쉬운 설명

이 플러그인은 상시 배치된 사내 코드 리뷰어가 아니라, 필요할 때 부르는 외부 침투테스트 팀에 가깝다. 평소에는 개발자 옆에 없다가, `/claude-security` 명령으로 호출하면 저장소 구조를 먼저 읽고 아키텍처를 지도로 그린 뒤, 위협 모델을 세우고, 취약점을 전수조사하고, 마지막으로 그 결과를 다른 에이전트가 다시 검증하는 별도 프로세스로 움직인다.

이 저장소는 2026-07-18에 "보안 가이던스 플러그인(security-guidance)"을 이미 다뤘는데, 두 플러그인은 이름은 비슷해도 역할이 다르다. security-guidance는 Claude가 코드를 쓰는 그 세션 안에서 파일 편집마다 패턴을 검사하고, 턴이 끝날 때마다 diff를 리뷰하고, 커밋·푸시 시 더 깊게 훑어 그 자리에서 고치는 "실시간 자기검열"이다. 반면 claude-security 플러그인은 코드가 이미 존재하는 상태에서 사람이 명시적으로 호출해 저장소나 diff 전체를 깊게 감사하는 "온디맨드 정밀 감사"다. 공식 문서는 이 둘을 각각 "In session"과 "On demand, deep scan"으로 명확히 구분한다.

기존 정적분석(SAST) 도구와도 다르다. SAST는 정규식·패턴 매칭으로 "위험해 보이는 코드"를 전부 잡아내 오탐이 쌓이는 방식인 반면, 이 플러그인은 여러 에이전트가 데이터 흐름을 따라가며 비즈니스 로직 수준에서 취약점을 추론하고, 그 결과를 별도 에이전트가 다시 검증해 걸러낸다. 이 구조가 성능의 핵심이다.

## 동작 원리

`/claude-security`를 실행하면 메뉴에서 세 작업(저장소 스캔, 변경사항 스캔, 패치 제안) 중 하나를 고른다. 내부적으로는 대략 아래 순서로 진행된다(공식 문서와 복수 매체 보도를 종합).

1. **인벤토리/아키텍처 매핑** — 저장소를 컴포넌트 단위로 나누고 규모·비용을 안내한다.
2. **위협 모델링** — 컴포넌트별로 진입점과 신뢰 경계를 정리한다.
3. **취약점 리서치(전수조사)** — 공격자가 닿을 수 있는 코드를 중심으로 여러 리서처 에이전트가 병렬로 훑는다. 테스트·픽스처·벤더 코드는 배경으로 취급한다.
4. **독립 검증** — 발견 사항을 작성한 에이전트와 별개인 검증자가 반증을 시도해 살아남은 것만 보고서에 남긴다. 공식 문서는 스캔이 비결정적이라 같은 코드를 두 번 스캔해도 결과가 달라질 수 있다고 명시한다.
5. **패치 제안** — `/claude-security`를 다시 실행해 "Suggest patches"를 고르면, 원본과 격리된 스크래치 사본에서 패치를 작성하고, 작성자와 다른 에이전트가 "이 발견을 해결하는가/새 취약점을 만들지 않는가/동작을 바꾸지 않는가" 세 가지를 확인한 뒤에만 패치를 내놓는다.

결과는 저장소 안에 `CLAUDE-SECURITY-<timestamp>/` 디렉터리로 남는다(`CLAUDE-SECURITY-RESULTS.md`, `.jsonl`, 리비전 스탬프, `patches/`). 패치는 자동 적용되지 않고 `git apply`로 직접 적용해야 한다.

## 구체 예시·사례

회계법인 내부 개발팀이 정산 자동화 API 저장소에서 `/claude-security scan my branch`로 배포 전 브랜치를 스캔한다고 가정하자. 커밋된 diff만 스캔 대상이므로 작업 중인 미커밋 변경은 먼저 커밋해야 한다. 스캔이 끝나면 `CLAUDE-SECURITY-RESULTS.md`에 `F1` 같은 발견 ID로 취약점 유형·심각도·확신도·재현 시나리오·권고안이 정리된다. 이후 `/claude-security`로 "Suggest patches"를 골라 F1을 지정하면, 검증을 통과한 패치가 `patches/F1.patch`로 생성되고, 개발자는 `git apply CLAUDE-SECURITY-<timestamp>/patches/F1.patch`로 직접 적용한 뒤 별도 PR로 리뷰를 받는다. 테스트가 없는 코드라면 패치 노트에 "테스트 없이 검토됨"이라고 명시돼, 신뢰 수준을 스스로 밝힌다.

## 비슷한 것과 비교

| 구분 | 시점 | 도구 | 커버리지 |
| --- | --- | --- | --- |
| 세션 내 | 코드 작성 중 | security-guidance 플러그인 | Claude가 그 세션에서 쓴 코드의 흔한 취약점, 그 자리에서 수정 |
| 온디맨드·단발 | 요청 시 1회 | `/security-review` | 현재 브랜치에 대한 1회성 점검 |
| 온디맨드·심층 | 요청 시 | claude-security 플러그인 | 저장소·diff 전체의 멀티에이전트 스캔, 독립검증된 발견과 패치 |
| PR 시점 | PR 생성 시 | Code Review(팀/엔터프라이즈) | 전체 코드베이스 맥락의 정합성·보안 리뷰 |
| 매니지드 | 상시 모니터링 | Claude Security 제품(엔터프라이즈) | 연결된 저장소를 호스팅형으로 상시 감시 |

선택 기준은 한 줄로 정리된다: 코드를 쓰는 동안 즉시 고치려면 security-guidance, 배포 전 저장소나 브랜치를 깊게 감사하려면 claude-security 플러그인을 쓴다. 참고로 "Claude Security"라는 이름의 별도 매니지드 제품(claude.ai/security, 엔터프라이즈 전용)도 있어 브랜드가 겹치므로 혼동하지 않도록 주의가 필요하다.

## 왜 지금 중요한가

Anthropic은 2026년 7월 22일경 claude-security 플러그인을 베타로 출시했다. 공식 문서에 따르면 Claude Code v2.1.154 이상, 모든 유료 플랜에서 사용 가능하며(Pro는 `/config`에서 다이나믹 워크플로우를 켜야 한다), Python 3.9.6 이상과 Git이 필요하다(전체 스캔은 Git 없이도 가능). 설치는 `/plugin install claude-security@claude-plugins-official` 한 줄이다.

- [Scan your codebase for vulnerabilities](https://code.claude.com/docs/en/claude-security)
- [Catch security issues as Claude writes code](https://code.claude.com/docs/en/security-guidance)
- [claude-security plugin README](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/claude-security)

## 회계법인 AI 직무 연결 포인트

회계법인이 내부 도구나 클라이언트용 대시보드를 AI로 코딩하는 사례가 늘면서, 이런 자동 취약점 스캐너는 "감사 대상 시스템을 감사하는 도구"가 아니라 감사법인 자신의 개발 파이프라인을 지키는 보안 통제로 쓰인다. AI가 짠 코드를 사람이 전부 재검토하기 어려운 상황에서, 별도 에이전트가 그 코드를 다시 훑어 검증하는 구조는 필수적인 안전장치다.

특히 "발견한 에이전트와 검증하는 에이전트를 분리한다"는 설계는 감사의 이중검토 원칙, 즉 작성자와 검토자를 분리하는 준비자-검토자 분리(segregation of preparer/reviewer) 통제와 구조적으로 닮았다. 면접에서 이 유사성을 짚으면 "AI 거버넌스를 감사 통제 프레임으로 설명할 줄 안다"는 인상을 줄 수 있다. 같은 사람(또는 같은 모델 인스턴스)이 작성과 검증을 겸하면 확증편향이 생기듯, AI 코드 리뷰에서도 작성 에이전트와 검증 에이전트의 독립성이 신뢰성의 핵심이다.

EY 캔버스, 삼일PwC AX노드처럼 회계법인이 자체 AI 감사 에이전트를 개발하는 사례가 늘어날수록, 그 에이전트를 만드는 코드 자체의 보안 취약점 관리도 회계법인의 새로운 리스크 관리 영역이 된다. 감사 도구가 뚫리면 그 위에서 나온 감사 증거의 신뢰성 자체가 흔들리기 때문에, 개발 파이프라인 보안은 더 이상 IT팀만의 문제가 아니라 품질관리 체계의 일부로 다뤄져야 한다.

## 핵심 용어·논쟁

- **멀티에이전트 스캔** — 아키텍처 매핑·위협모델링·취약점 리서치·검증을 각각 다른 에이전트가 맡아 나눠 수행하는 구조.
- **독립 검증(verification)** — 발견을 작성한 에이전트와 다른 에이전트가 반증을 시도해, 통과한 것만 보고서에 남기는 단계. 오탐을 줄이는 핵심 장치다.
- **패치 제안(patch proposal)** — 자동 적용되지 않고 `git apply`로 사람이 직접 적용해야 하는 검토용 패치 파일.
- **비결정성(nondeterminism)** — 같은 코드를 스캔해도 실행마다 발견 결과가 달라질 수 있다는 공식 문서의 명시. 감사 증적으로 신뢰하려면 리비전 스탬프로 "어느 커밋을, 어느 강도로 스캔했는지"를 반드시 함께 남겨야 한다.
- **security-guidance와의 관계** — 이름이 비슷해 혼동하기 쉽지만 전자는 세션 내 즉시 수정, 후자는 온디맨드 심층 감사로 역할이 다르다.

현재 논쟁점은 "비결정적 스캔 결과를 감사·규제 맥락에서 얼마나 신뢰할 수 있는가"이다. 같은 저장소를 두 번 스캔해 다른 결과가 나온다면, 규제기관이나 품질관리 부서 입장에서는 "몇 번 스캔해야 충분한가", "어느 결과를 공식 기록으로 남길 것인가"라는 절차 표준화 문제가 남는다.

## 자료 깊이 읽기

### Scan your codebase for vulnerabilities (공식 문서) — 영어, 텍스트, 중급
Anthropic 공식 문서 원문. 설치법(`/plugin install claude-security@claude-plugins-official`), 전제조건(Claude Code v2.1.154+, 유료 플랜, Python 3.9.6+, Git), `/claude-security` 메뉴의 3개 작업, 결과 디렉터리 구조(`CLAUDE-SECURITY-RESULTS.md`/`.jsonl`/리비전 스탬프/`patches/`), 패치가 절대 자동 적용되지 않는다는 점, 그리고 security-guidance·`/security-review`·Code Review·매니지드 Claude Security 제품과의 위치를 비교한 표까지 담고 있다. 이번 브리핑의 1차 근거다.

### claude-security 플러그인 GitHub README — 영어, 텍스트, 중급
공식 플러그인 저장소(anthropics/claude-plugins-official)의 README로, 설치·실행 흐름과 결과물 구조를 다시 확인할 수 있는 보조 출처다. 공식 문서와 내용이 일치해 교차검증에 사용했다.

### Claude Security Plugin: How It Works & How to Install (buildfastwithai.com) — 영어, 텍스트, 중급
서드파티 블로그로, 공식 문서에는 명시되지 않은 6단계 파이프라인(Inventory→Threat Model→Research→Sweep→Panel→Adversarial)과 오케스트레이터·매핑·리서처 단계에 쓰이는 모델 등급 차이를 보도 형태로 소개한다. 공식 수치는 아니므로 "복수 매체 보도"로 표시해 참고했다.

**그 외 참고**
- [Anthropic Releases Claude Security Plugin for Claude Code in Beta](https://www.marktechpost.com/2026/07/22/anthropic-releases-claude-security-plugin-for-claude-code-in-beta-a-multi-agent-vulnerability-scanner-that-runs-in-your-terminal/) — 영어, 텍스트, 입문(베타 출시 보도)
- [Claude Code Security Plugin: Three-Layer Scanning, Free](https://www.digitalapplied.com/blog/claude-code-security-plugin-three-layer-scanning-2026) — 영어, 텍스트, 중급(security-guidance와의 계보 비교)

이번 주제를 전용으로 다루는 유튜브 영상은 찾지 못했다. 검색 상위에 뜬 영상 중 하나(`5v_XH1lxvVI`)는 yt-dlp로 자막을 직접 받아 확인했으나, 내용을 보니 claude.ai/security에서 접근하는 별도의 매니지드 엔터프라이즈 제품(공식 문서가 "Managed | Claude Security, Enterprise plan"으로 분류한 그 제품)을 다루고 있어 오늘 브리핑의 주제인 Claude Code CLI용 플러그인과는 다른 대상이었다. 잘못된 자료를 상세 요약으로 포장하지 않기 위해 영상 상세 요약 파일은 작성하지 않았다.

## 자가 점검 질문

1. claude-security 플러그인과 security-guidance 플러그인의 차이를 "시점"과 "실행 주체"라는 두 축으로 설명할 수 있는가?
2. 우리 팀이 AI로 만든 내부 감사 도구 저장소에 이 플러그인을 도입한다면, 어느 시점(PR 전/배포 전/정기 주기)에 어떤 작업(전체 스캔/변경사항 스캔/패치 제안)을 붙일 것인가?
3. 스캔 결과가 비결정적이라는 한계를 감안할 때, 이 도구의 발견 사항을 감사 증적이나 품질관리 기록으로 남기려면 어떤 절차적 보완(재스캔 횟수, 리비전 스탬프 보존 등)이 필요한가?
