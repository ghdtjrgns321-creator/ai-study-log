# 오늘의 AI 개념: 에이전틱 신원·접근관리(Agentic Identity and Access Management, Agentic IAM)

> 작성일: 2026-08-06 · 분류: ai-concept

## 한 줄 정의

자율 AI 에이전트가 다중 시스템을 오가며 스스로의 신원을 증명하고, 수행 중인 작업에 필요한 최소한의 권한만 실시간으로 부여받아 접근하도록 통제하는 신원·접근관리(IAM) 체계다.

## 쉬운 설명

회사 출입증 시스템을 떠올리면 이해가 쉽다. 기존 IAM은 "이 사람이 누구이고 어떤 부서 소속인지"를 확인해 문을 열어주는 방식으로 설계됐다. 그런데 이제 그 출입증을 들고 건물을 돌아다니는 것은 사람이 아니라, 사람을 대신해 여러 업무를 처리하는 AI 에이전트다. 문제는 이 에이전트가 사람의 출입증을 그대로 빌려 쓰거나, 한 번 발급받으면 영구히 모든 문을 열 수 있는 마스터키를 쥐고 다닌다는 데 있다. 에이전틱 IAM은 이 에이전트에게 사람과 구분되는 자기만의 신원증을 발급하고, 지금 이 순간 필요한 문만, 필요한 시간만큼만 열리는 열쇠로 바꾸는 접근이다.

기존 IAM과의 핵심 차이는 "누구를 전제로 설계됐는가"에 있다. OAuth 2.1·SAML·OIDC는 로그인해서 세션을 유지하는 인간 사용자를 전제로 만들어졌다. 반면 에이전트는 사람의 개입 없이 초당 여러 건의 API를 호출하고, 다른 에이전트에게 작업을 위임하고, 상황에 따라 매번 다른 권한을 요구한다. 정적인 스코프와 세션 기반 인증으로는 이런 동적 행위를 감당하지 못한다.

또 하나의 차이는 위임(delegation)이다. 사람 간 위임은 드물고 문서화되지만, 멀티에이전트 워크플로우에서는 에이전트 A가 에이전트 B에게, B가 다시 C에게 작업을 넘기는 위임 체인이 일상적으로 발생한다. 에이전틱 IAM은 이 체인 전체를 추적 가능하게 만드는 것을 목표로 한다.

## 동작 원리

Agentic IAM 프레임워크는 대체로 다음 흐름으로 동작한다(Cloud Security Alliance 백서 기준).

1. **신원 발급** — 에이전트마다 탈중앙화 신원 식별자(DID)를 부여해 사람·서비스 계정과 구분되는 고유 ID를 갖게 한다.
2. **역량 증명** — 신뢰할 수 있는 기관이 검증 가능한 자격증명(VC)을 발급해 에이전트의 역할·권한 범위·준수 상태를 암호학적으로 증명한다.
3. **탐색·신뢰 수립** — 에이전트 네이밍 서비스(ANS)가 DNS처럼 다른 에이전트나 도구를 찾고 신뢰를 확인한다.
4. **상황인식 정책 판단** — 제로 트러스트 정책 엔진이 요청 시점의 위험도·맥락·과거 행동 패턴을 근거로 접근 여부를 실시간으로 재계산한다.
5. **시한부 접근 부여(JIT)** — 승인되면 범위와 유효시간이 제한된 단기 토큰만 발급하고, 작업이 끝나면 자동 만료시킨다.
6. **행동 모니터링·이상탐지** — 에이전트의 실제 행동을 선언된 목적과 대조해 베이스라인에서 벗어나면 즉시 접근을 제한하거나 재검증을 요구한다.
7. **암호학적 감사** — 모든 행동을 에이전트 DID로 서명해 기록함으로써 부인방지와 위임 체인 추적을 가능하게 한다.

이 흐름의 요지는 "로그인 한 번으로 세션 유지"가 아니라 "모든 상호작용을 매번 새로 검증하는 연속적 인증"으로 패러다임이 바뀐다는 점이다.

## 구체 예시·사례

CSA와 Aembit이 2026년 공동 조사한 사례 중 한 금융 서비스 기업의 초기 구성을 보면 문제가 뚜렷하다. 이 회사는 Claude 기반 에이전트가 온프레미스·SaaS 시스템에 접근하도록 MCP 서버들과 연동했는데, 초기에는 인증·인가가 전혀 없었고 이후에도 에이전트가 사람의 IDP를 거쳐 사용자 본인의 권한을 그대로 위임받는 방식에 그쳤다. 사용자는 "이 애플리케이션이 금융 데이터 전체를 읽고 쓰도록 허용하시겠습니까"라는 팝업에 그냥 허용을 눌렀고, 그 결과 에이전트와 하위 MCP 서버가 장기 유효 자격증명을 그대로 보관하게 됐다. 로그에는 이 행동이 에이전트가 한 것인지 사람이 한 것인지 구분되지 않아 감사 추적이 불가능한 상태였다.

이 회사는 "블렌디드 아이덴티티(blended identity)" 모델로 전환해 문제를 해결했다. 요청마다 사용자 컨텍스트와 에이전트 신원을 함께 담은 신원 토큰을 발급하고, 실제 자원 접근에는 게이트웨이와 하위 시스템 사이에서만 통용되는 별도의 단기 접근 토큰을 쓰도록 분리했다. 그 결과 로그에는 "어떤 사용자가, 어떤 에이전트를 통해, 어떤 정책 아래, 어떤 자격증명으로" 접근했는지가 남게 됐다.

## 비슷한 것과 비교

| 구분 | 전통 IAM(OAuth 2.1·SAML·OIDC) | 비인간 신원 관리(NHI Governance) | 에이전틱 IAM |
| --- | --- | --- | --- |
| 전제 대상 | 로그인하는 인간 사용자 | 서비스 계정·API 키·봇 등 정적 비인간 신원 전반 | 자율적으로 의사결정하고 위임하는 AI 에이전트 |
| 권한 모델 | 정적 스코프, 세션 기반 | 장기 자격증명 인벤토리 관리 중심 | 상황인식 동적 권한, JIT 발급 |
| 핵심 과제 | 사용자 인증·SSO | 자격증명 소재 파악·순환·폐기 | 위임 체인 추적, 에이전트 간 상호인증, 의도 표현 |
| 대표 표준·기술 | OAuth 2.1, SAML, OIDC | 시크릿 매니저, CIEM | DID, VC, ANS, CAEP |

세 모델은 배타적이지 않고 중첩된다 — 에이전틱 IAM은 NHI 거버넌스의 원칙(가시성·순환·최소권한)을 계승하되, 에이전트 특유의 자율적 위임과 다중 에이전트 협업까지 다룬다는 점에서 범위가 더 좁고 깊다. 선택 기준은 단순하다: 관리 대상이 "스스로 판단해 다음 행동을 정하는 소프트웨어"라면 에이전틱 IAM의 통제(위임 추적·JIT·연속 인증)가 필요하다.

## 왜 지금 중요한가

Gartner는 2025년 8월 26일 보도자료에서 2026년까지 엔터프라이즈 애플리케이션의 40%가 태스크 특화 AI 에이전트를 갖추게 될 것으로 예측했다(2025년 5% 미만 대비). CSA가 Aembit과 함께 2026년 1월 IT·보안 실무자 200명 이상을 대상으로 진행한 설문(2026년 4월 웨비나에서 공개)에서는, 응답자의 68%가 "에이전트의 행동과 사람의 행동을 명확히 구분할 수 없다"고 답했고, 74%는 "에이전트가 필요 이상의 권한을 받고 있다"는 데 동의했다. 자격증명을 지속적으로 순환한다고 답한 조직은 20%에 그쳤다. Okta는 2026년 3월 2일 기고에서 클라우드 환경의 서비스 계정·API 키가 이미 인간 사용자 수를 넘어섰다고 짚었다. 실제로 Aembit은 2026년 4월 9일 RSA 컨퍼런스에서 "IAM for Agentic AI"를 정식 출시(GA)하며 블렌디드 아이덴티티·MCP 인가 서버를 제품화했다.

- [Agentic AI Identity and Access Management: A New Approach (CSA, 2025-08-18)](https://cloudsecurityalliance.org/artifacts/agentic-ai-identity-and-access-management-a-new-approach)
- [Gartner Predicts 40% of Enterprise Apps Will Feature Task-Specific AI Agents by 2026 (Gartner, 2025-08-26)](https://www.gartner.com/en/newsroom/press-releases/2025-08-26-gartner-predicts-40-percent-of-enterprise-apps-will-feature-task-specific-ai-agents-by-2026-up-from-less-than-5-percent-in-2025)
- [The role of AI in IAM: Securing the agentic frontier (Okta, 2026-03-02)](https://www.okta.com/identity-101/role-of-ai-in-iam/)
- [Aembit IAM for Agentic AI Is Now Generally Available (Security Boulevard, 2026-04)](https://securityboulevard.com/2026/04/aembit-iam-for-agentic-ai-is-now-generally-available/)

## 회계법인 AI 직무 연결 포인트

감사의 가장 기본적인 내부통제 개념 중 하나가 직무분리(Segregation of Duties)와 접근통제(Access Control)다. AI 에이전트가 ERP·회계시스템에 자율적으로 접근해 전표를 조회·수정하는 시대에는 "이 에이전트가 어떤 권한으로, 누구를 대신해, 무엇을 했는지"를 증명하는 것이 IT 일반통제(ITGC) 감사의 새로운 과제가 된다. 앞서 다룬 사례처럼 에이전트가 사람의 권한을 그대로 위임받아 로그상 구분이 안 되는 상태라면, 감사인은 "이 전표를 누가 승인했는가"라는 가장 기본적인 질문에 답할 수 없다.

SOX 404·ITGC 감사에서 승인자를 사람 기준으로 추적하던 관행이 에이전트 기준으로 바뀌면, 위임 체인 전체를 감사증적으로 남겨야 한다. 에이전틱 IAM이 제안하는 DID·VC·JIT 접근·암호학적 서명 로그는 바로 이 요구를 기술적으로 뒷받침하는 장치다. 감사인은 이제 "이 통제가 존재하는가"뿐 아니라 "이 통제가 에이전트의 동적 권한 변화를 실시간으로 따라가는가"까지 테스트해야 한다.

회계법인 자체도 예외는 아니다. 감사 에이전트(EY 캔버스, 삼일PwC AX노드 등)를 클라이언트 시스템에 연결할 때, 그 에이전트에게 최소권한·시한부 접근을 어떻게 부여하는지가 회계법인의 정보보안 실사(due diligence) 항목이 된다. 면접에서 "AI 에이전트를 감사 실무에 도입할 때 가장 먼저 확인할 통제는 무엇인가"라는 질문에 접근권한·감사증적 관점으로 답할 수 있다면 실무 이해도를 보여줄 수 있다.

## 핵심 용어·논쟁

- **DID(Decentralized Identifier)** — 중앙기관 없이 암호학적으로 검증 가능한 고유 신원 식별자.
- **VC(Verifiable Credential)** — 신뢰기관이 발급하는, 위변조를 검증할 수 있는 디지털 자격증명(역할·권한·준수 상태 등을 담음).
- **JIT 접근(Just-In-Time Access)** — 작업에 필요한 순간에만 발급되고 끝나면 자동 만료되는 시한부 권한.
- **위임 체인(Delegation Chain)** — 에이전트가 다른 에이전트에게 작업·권한을 넘기는 연쇄 관계와 그 추적 기록.
- **블렌디드 아이덴티티(Blended Identity)** — 사람의 컨텍스트와 에이전트 신원을 함께 담아 "누구를 대신해 무엇을 했는가"를 구분하는 신원 모델.

가장 큰 논쟁은 표준화 부재다. Okta·Microsoft(Entra Agent ID)는 기존 IAM 플랫폼을 확장하는 방향을, Aembit·Strata 같은 신생 벤더는 에이전트 전용 제어 플레인을 새로 만드는 방향을 택하고 있어, 아직 업계 전체가 합의한 단일 프로토콜이 없다. 이 상태에서 조직마다 에이전트 신원을 "사람"·"워크로드"·"별도 범주" 중 무엇으로 취급할지 제각각이라, CSA 설문에서도 응답자의 63%가 "부서마다 에이전트를 다르게 정의한다"고 답했다 — 기술 표준화 이전에 개념 정의부터 흔들리고 있다는 뜻이다.

## 자료 깊이 읽기

### Agentic AI Identity and Access Management: A New Approach (CSA 백서) — 영어/텍스트/중급
Cloud Security Alliance가 2025년 8월 18일 발표한 백서로, OAuth 2.1·SAML·OIDC가 왜 에이전트에 부적합한지를 조목조목 짚고 DID·VC·Zero Trust·ANS를 결합한 4계층 프레임워크를 제시한다. JIT 접근, 영지식증명 기반 프라이버시 보존 감사, 에이전트 네이밍 규칙(`protocol://AgentID.Capability.Provider.Version`)까지 구체적으로 다뤄, 이 주제의 기술적 뼈대를 잡는 데 가장 좋은 1차 자료다.

### The role of AI in IAM: Securing the agentic frontier (Okta) — 영어/텍스트/입문
Okta가 2026년 3월 2일 게시한 글로, 비인간 신원이 이미 사람 수를 넘어선 현실을 짚고 위임된 권한 강제·세밀한 권한부여(FGA)·CAEP 기반 실시간 접근 취소 등 5가지 실무 통제를 제안한다. 벤더 관점이지만 실무자가 당장 점검할 체크리스트로 읽기 좋다.

### Identity and access management for Agentic AI: securing non-human identities at scale (YouTube) — 영어/영상/입문
OpenText NetIQ가 2026년 5월 공개한 7분 55초짜리 설명 영상으로, 고유 신원 부여 → 연속 인증 → 세밀한 접근 제어 → 행동 기반 이상탐지 → 거버넌스 → 감사까지 에이전틱 IAM의 전체 구성요소를 순서대로 짚는다. 자막을 직접 확인해 정리했다 — **[상세 요약 보기](videos/agentic-iam.md)**.

### AI Agents and the Limits of Traditional Identity & Access Models (Agentic AI Summit, YouTube) — 영어/영상/중급
CSA와 Aembit이 2026년 4월 공동 진행한 22분 33초짜리 웨비나로, 200여 개 조직 설문 결과(에이전트-인간 행동 구분 불가 68%, 과도한 권한 부여 동의 74%, 자격증명 지속 순환 20%)와 함께 Claude 기반 에이전트를 도입한 금융 서비스 기업의 실제 전환 사례를 다룬다. 자막을 직접 확인해 정리했다 — **[상세 요약 보기](videos/agentic-iam.md)**.

**그 외 참고**
- [Aembit IAM for Agentic AI Is Now Generally Available](https://securityboulevard.com/2026/04/aembit-iam-for-agentic-ai-is-now-generally-available/) — 영어, 텍스트, 입문
- [Coalition for Secure AI — Agentic Identity and Access Control](https://www.coalitionforsecureai.org/wp-content/uploads/2026/04/agentic-identity-and-access-control.pdf) — 영어, PDF, 중급

## 자가 점검 질문

1. 전통적 IAM(OAuth 2.1·SAML·OIDC)이 AI 에이전트에 구조적으로 부적합한 이유 세 가지를 설명할 수 있는가?
2. 감사 실무에서 "위임 체인 추적"이 왜 새로운 ITGC 통제 항목이 되는지, 구체적 시나리오로 설명할 수 있는가?
3. JIT 접근과 블렌디드 아이덴티티가 실제로 막아주는 리스크는 무엇이고, 이 통제가 없을 때 감사증적이 어떻게 무너지는지 말할 수 있는가?
