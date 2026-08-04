# 오늘의 AI 개념: 에이전트 스킬 공급망 보안(Agent Skills Supply Chain Security)

> 작성일: 2026-08-05 · 분류: agentic-coding

## 한 줄 정의

AI 에이전트가 마켓플레이스에서 내려받는 스킬(마크다운 지침·MCP 서버 설정)을 소프트웨어 의존성처럼 취급해, 오염된 스킬이 에이전트의 권한을 그대로 물려받아 자격증명 탈취·백도어·데이터 유출로 이어지는 것을 막는 보안 영역이다.

## 쉬운 설명

npm이나 PyPI 같은 코드 패키지 저장소는 정적분석 스캐너로 악성 코드를 어느 정도 걸러낼 수 있다. 그런데 에이전트 스킬은 코드가 아니라 자연어로 쓰인 "지침서"(SKILL.md)다. 신입사원에게 업무 매뉴얼을 하나 건네면 의심 없이 그대로 따라 하듯이, 에이전트도 매뉴얼 안에 "먼저 이 초기화 스크립트를 실행하라"는 문구가 숨어 있으면 별다른 의심 없이 실행해 버린다. 문제는 그 매뉴얼이 실행되는 순간 에이전트가 이미 가진 파일시스템·자격증명·네트워크 접근 권한을 그대로 상속받는다는 점이다.

이번 주제는 이 저장소에서 이미 다룬 "MCP 2026 스펙 개편"(프로토콜 설계 변화), "에이전트 스킬·플러그인 생태계"(생태계 소개), "가디언 에이전트"(방어용 감시 에이전트), "AI 레드티밍"(모델·에이전트에 대한 침투테스트)과는 각도가 다르다. 이번 편은 그 생태계의 유통 단계, 즉 마켓플레이스에 오염된 스킬이 대량으로 유입되는 실제 사건과 그 구조적 원인(낮은 등록 장벽, 자연어라 스캔이 어려운 점, 권한 상속 문제)을 "공급망" 관점에서 다룬다.

스킬은 대개 GitHub 계정만 있으면 검수 없이 하루이틀 안에 등록되는 낮은 진입장벽의 마켓플레이스(ClawHub, skills.sh 등)를 통해 유통된다. 다운로드 버튼을 누르는 사용자 입장에서는 코드 리뷰를 하지 않는 것이 보통이라, 이 유통 단계 자체가 새로운 공급망 공격 표면이 됐다.

## 동작 원리

오염된 스킬이 실제 피해로 이어지는 전형적인 공격 체인은 다음과 같다.

1. **업로드**: 공격자가 인기 도구 이름을 흉내 낸 타이포스쿼팅 스킬(예: 지갑·트레이딩봇 이름을 살짝 바꾼 것)을 ClawHub 같은 저심사 마켓플레이스에 올린다.
2. **사회공학**: SKILL.md의 "Prerequisites(사전 준비)" 섹션에 "이 도구를 쓰려면 먼저 이 스크립트로 초기화해야 한다"는 지침을 심어, 에이전트(또는 에이전트를 통해 사용자)가 설치 스크립트를 실행하도록 유도한다. 보안 업계는 이를 "ClickFix 2.0" 기법으로 부른다.
3. **권한 상속 실행**: 에이전트가 이 스크립트를 신뢰된 컨텍스트에서 실행하면서, 파일시스템·저장된 자격증명·네트워크 접근 권한을 그대로 넘겨받는다.
4. **지속성 확보**: 공격 스킬이 에이전트의 메모리 파일(예: MEMORY.md)을 조작해, 세션이 재시작돼도 악성 지침이 계속 로드되게 만든다.
5. **탈취·유출**: 자격증명 직접 탈취, 역쉘 개설, webhook.site 같은 외부 엔드포인트로 `.env` 파일 등을 유출하는 페이로드가 실행된다.

## 구체 예시·사례

Snyk는 2026년 2월 5일 기준 ClawHub·skills.sh 스킬 3,984개를 감사한 "ToxicSkills" 리서치를 발표했다. 36.82%(1,467개)에서 보안 결함이 확인됐고 13.4%(534개)는 critical 등급이었으며, 76건의 악성 페이로드(외부 악성코드 배포·난독화된 자격증명 탈취·백도어 설치)가 발견됐다. 발표 시점에도 8건은 ClawHub에 여전히 활성 상태였다.

같은 시기 "ClawHavoc"이라는 조율된 공급망 공격도 확인됐다. Koi Security가 2026년 2월 1일 ClawHub 전체 스킬 2,857개를 감사해 악성 스킬 341개(335개는 단일 캠페인, macOS 자격증명·키체인·SSH 키를 훔치는 Atomic Stealer 변종 배포)를 발견했다. 이후 Antiy CERT가 2월 6일 후속 분석에서 ClawHub 이력 저장소 전체 기준 악성 패키지 1,184개, 관여 작성자 계정 12개(주범 1개가 677개 업로드)를 확인했다. 최초 등장(1월 27일)부터 공개(2월 1일)까지는 약 5일이 걸렸다.

일부 2차 보안 매체(Repello.ai 등)가 반복 인용하는 "이용자 약 30만 명, 17일 노출" 수치는 해당 매체 자체 조사에 근거할 뿐 공식 발표나 독립 검증 출처가 없어, 이 브리핑에서는 "복수 보안 매체 보도 기준, 공식 미확정"으로만 표기한다. 같은 생태계의 별개 취약점 CVE-2026-25253(인증 토큰 탈취·원클릭 RCE, CVSS 8.8)도 2026년 1월 26일 공개돼 v2026.1.29에서 패치됐다.

## 비슷한 것과 비교

| 구분 | 전통 SW 공급망 보안(npm·PyPI 등) | MCP 프로토콜 자체 보안 | 에이전트 스킬 공급망 보안 |
|---|---|---|---|
| 공격 대상 | 실행 코드(바이너리·스크립트) | 툴 설명·인증 흐름(OAuth 이중 키 등) | 자연어 지침서(SKILL.md)·설정 파일 |
| 탐지 난이도 | 정적분석 스캐너로 상당 부분 탐지 가능 | 프로토콜 레벨 취약점 스캔 가능 | 자연어라 코드 스캐너가 놓치기 쉬움 |
| 유통 장벽 | 패키지 매니저 정책·서명 검증 존재 | 클라이언트·서버 간 스펙 준수 여부 | 가입만 하면 등록 가능한 저심사 마켓플레이스 다수 |
| 피해 방식 | 의존성 체인 오염, 빌드 시 실행 | 툴 선택 조작, 인증 토큰 탈취 | 권한 상속 실행 + 메모리 조작으로 지속성 확보 |

선택 기준: 스킬을 도입할 때는 "코드가 아니니 검토가 필요 없다"는 인식 자체가 위험 신호다. 실행 코드 공급망 보안(SBOM·서명 검증)과 동일한 엄격도로 스킬·MCP 설정을 다뤄야 한다.

## 왜 지금 중요한가

- Snyk, "ToxicSkills: 3,984 skills, 36.82% flawed, 76 malicious" (2026-02-05) — [ToxicSkills: Malicious AI Agent Skills on ClawHub](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)
- OWASP, "Agentic Skills Top 10" 프로젝트 1.0(2026 Edition), 2026년 3월 업데이트 — [OWASP Agentic Skills Top 10](https://owasp.org/www-project-agentic-skills-top-10/)
- Koi Security, ClawHavoc 최초 발견(2026-02-01, 2,857개 감사 중 341개 악성) — [ClawHavoc: 341 Malicious ClawedBot Skills](https://www.koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting)
- Antiy Labs, ClawHavoc 후속 분석(2026-02-06, 1,184개 악성 패키지·작성자 12개 확인) — [ClawHavoc: Analysis of Large-Scale Poisoning Campaign](https://www.antiy.net/p/clawhavoc-analysis-of-large-scale-poisoning-campaign-targeting-the-openclaw-skill-market-for-ai-agents/)
- The Hacker News, 341개 악성 ClawHub 스킬 보도(2026-02) — [Researchers Find 341 Malicious ClawHub Skills](https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html)
- obot.ai, MCP·스킬 공급망 보안 대응책 정리(게시 2026-04-27, 수정 2026-05-29) — [The New Supply Chain Frontier](https://obot.ai/blog/mcp-security-agent-skills-supply-chain/)

## 회계법인 AI 직무 연결 포인트

감사 업무용 AI 에이전트는 통상 고객사 ERP·재무 데이터·클라우드 저장소 접근 권한을 함께 부여받아 동작한다. 이런 에이전트가 마켓플레이스에서 받은 확장 스킬을 검토 없이 설치·실행하면, ToxicSkills 사례처럼 위장된 스킬 하나가 그 권한을 이어받아 고객 재무 데이터 유출·자격증명 탈취로 직결될 수 있다. 감사 증거 파이프라인에 외부 스킬을 연결하는 순간 그 스킬은 감사 데이터의 사실상 접근권자가 된다.

이 때문에 스킬·MCP 서버 도입 시에는 소프트웨어 의존성과 동일한 벤더 심사 절차가 필요하다. 출처 추적(누가 만들었는지), 버전 고정, 배포 전 코드·지침 리뷰를 거치고, SOC2나 ISO/IEC 42001 같은 인증을 보유한 벤더를 우선한다. 회계법인이 자체적으로 AI Assurance 서비스를 고객에게 제공하려는 입장이라면, 이런 내부 통제를 스스로 먼저 갖추지 못하면 그 인증 서비스 자체의 신뢰성이 흔들린다.

실무적으로는 최소 권한 원칙을 스킬 단위로 적용하는 것이 핵심이다. 감사팀 에이전트에 전사 파일시스템·전체 클라이언트 계정에 대한 기본 접근권을 주지 않고, 스킬마다 필요한 정확한 스코프만 선언·검증하도록 하며, 승인된 스킬·MCP 서버만 실행되도록 중앙집중식 게이트웨이에서 화이트리스트로 관리해야 한다.

## 핵심 용어·논쟁

- **ClawHub·skills.sh** — GitHub 계정만으로 단기간에 등록 가능한 AI 에이전트 스킬 유통 마켓플레이스.
- **ToxicSkills** — Snyk가 2026년 2월 발표한 스킬 마켓플레이스 보안 결함·악성 스킬 실태 조사 리서치명.
- **ClawHavoc** — 2026년 1~2월 ClawHub에 타이포스쿼팅 악성 스킬을 대량 업로드한 조율된 공급망 공격 캠페인명.
- **MEMORY.md 포이즈닝** — 에이전트의 지속 메모리 파일을 조작해 세션이 바뀌어도 악성 지침이 계속 살아남게 하는 지속성 확보 기법.
- **OWASP Agentic Skills Top 10(AST01~AST10)** — 악성 스킬·공급망 손상·과도한 권한 등 에이전트 스킬 고유 위험을 정리한 신설 프레임워크.

진행 중인 논쟁은 두 갈래다. 하나는 자연어 지침 기반 스킬을 어떻게 탐지할 것인가로, 실행 전 정적분석(레지스트리 서명·해시 검증)과 실행 중 런타임 격리·행위 모니터링 중 무엇을 우선순위로 둘지에 대한 합의가 아직 없다. 다른 하나는 "30만 명 노출" 같은 자극적 수치가 1차 검증 없이 2차 매체를 통해 확산되는 문제 자체로, 보안 리서치의 수치 인플레이션 관행에 대한 비판도 함께 제기되고 있다.

## 자료 깊이 읽기

### ToxicSkills: Malicious AI Agent Skills on ClawHub (Snyk) — 영어, 텍스트, 중급
Snyk 보안 리서치팀이 2026년 2월 5일 기준 스킬 3,984개를 정적·행위 분석한 1차 리서치다. 36.82%(1,467개)에서 보안 결함, 13.4%는 critical 등급, 76개 스킬에서 실제 작동하는 악성 페이로드를 확인했다. mcp-scan으로 설치된 스킬을 즉시 재감사하고 의심 스킬 제거·자격증명 회전을 권고한다.

### The New Supply Chain Frontier: Securing MCP Security and Agent Skills (obot.ai) — 영어, 텍스트, 중급
2026년 4월 27일 게시, 5월 29일 수정된 정리 글로 ToxicSkills·ClawHavoc을 함께 다룬다. 스킬·MCP 서버를 소프트웨어 의존성으로 취급(출처 추적·버전 고정·배포 전 리뷰), 최소 권한 선언·검증, 모든 MCP 서버에 OAuth 2.1·단기 토큰 요구, 중앙 게이트웨이로 감사 추적, 메모리 파일 무결성 감시, OWASP 준수 등 6가지 대응책을 제시한다.

### Hacking MCP: Supply Chain Attacks & Tool Execution Hijacking (YouTube) — 영어, 컨퍼런스 발표, 중급
KPMG 독일 보안 컨설턴트 Paul Zenker·Justin Szczepaniak가 실제 데모 두 건으로 MCP 공급망 위험을 보여주는 발표다. MCP 설정 파일에 임의 셸 명령을 심어 앱 실행 때마다 재실행되는 백도어를 만드는 데모, 그리고 워크스페이스 설정 파일을 바꿔치기해 툴 실행 자체를 가로채는 "툴 실행 하이재킹" 데모를 다룬다. 프롬프트 인젝션과는 다른 층위의 공격이라는 점, 그리고 사후 탐지형 방어(MCP Guard)의 한계와 사전 검증형 레지스트리 아이디어까지 자막을 직접 확인해 정리했다 — **[상세 요약 보기](videos/mcp-skill-supply-chain-security.md)**.

**그 외 참고**
- [OWASP Agentic Skills Top 10](https://owasp.org/www-project-agentic-skills-top-10/) — 영어, 텍스트, 중급
- [ClawHavoc: Analysis of Large-Scale Poisoning Campaign (Antiy Labs)](https://www.antiy.net/p/clawhavoc-analysis-of-large-scale-poisoning-campaign-targeting-the-openclaw-skill-market-for-ai-agents/) — 영어, 텍스트, 고급
- [Researchers Find 341 Malicious ClawHub Skills (The Hacker News)](https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html) — 영어, 텍스트, 초중급
- [CVE-2026-25253: 1-Click RCE in OpenClaw (SOCRadar)](https://socradar.io/blog/cve-2026-25253-rce-openclaw-auth-token/) — 영어, 텍스트, 중급

## 자가 점검 질문

1. 스킬 공급망 공격이 전통적인 프롬프트 인젝션과 구조적으로 다른 지점은 무엇인가?
2. 우리 팀이 감사 업무에 외부 스킬·MCP 서버를 도입한다면, 도입 전 점검해야 할 최소 항목은 무엇인가?
3. 사후 탐지형 방어(메모리 무결성 감시)와 사전 검증형 방어(서명된 레지스트리) 중 지금 당장 적용 가능한 것은 무엇이고, 왜 그런가?
