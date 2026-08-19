# 오늘의 AI 개념: 대만 자율형 AI 사이버공격 사건(Taiwan Autonomous AI Cyberattack)

> 작성일: 2026-08-20 · 분류: trend

## 한 줄 정의

2026년 7월 초 나흘간 중국계로 추정되는 해커 조직이 오픈소스 AI 에이전트 프레임워크 Hermes·OpenClaw로 만든 최대 8개의 서브에이전트를 동시 투입해, 인간의 실시간 개입 없이 정찰부터 침투·탈취까지 수행한 사건으로 "세계 최초의 종단간(end-to-end) 자율 AI 사이버공격" 사례로 보도됐다.

## 쉬운 설명

지금까지 국가 배후 해킹은 숙련된 인간 해커 여러 명이 팀을 짜서 표적을 정찰하고, 취약점을 찾고, 침투 경로를 손으로 설계하는 일이었다. 이번 사건은 그 팀의 자리를 AI 에이전트가 대신 채운 사례다. 공격자는 오픈소스로 누구나 내려받을 수 있는 AI 에이전트 프레임워크 Hermes와 OpenClaw를 가져다, 8개의 서브에이전트에 각각 다른 표적과 공격 기법을 맡기고 풀어놓았다.

비유하자면 예전에는 도둑 한 명이 자물쇠를 하나씩 직접 따고 다녔다면, 이번에는 도둑이 "이 건물은 너, 저 건물은 너" 하고 8명의 대리인에게 지시만 내리고, 대리인들은 각자 알아서 문을 열 방법을 찾아 실행하고 막히면 스스로 다른 방법을 시도한 셈이다. 이스라엘 보안업체 Dream(드림)이 이 작전 흔적이 담긴 160메가바이트 규모의 온라인 아카이브를 발견하면서 전모가 드러났다.

기존의 "AI가 해킹을 도왔다"는 사례들과 다른 점은, 이번엔 AI가 보조 도구가 아니라 공격 파이프라인 전체(정찰→취약점 탐색→인증 우회→데이터 탈취)를 스스로 이어 붙였다는 것이다. 다만 뒤에서 볼 것처럼, "완전 자율"이라는 표현 자체는 보안업계 안에서도 이견이 있다.

## 동작 원리

공격 체계는 아래와 같은 흐름으로 구성됐다(주로 The Register·CyberScoop 보도 기준).

1. **프레임워크 구축** — 오픈소스 AI 에이전트 프레임워크 Hermes와 OpenClaw를 조합해 공격용 오케스트레이션 기반을 만든다.
2. **서브에이전트 8개 배치** — 최대 8개의 서브에이전트를 동시에 띄우고, 각 서브에이전트에 서로 다른 표적(정부 웹사이트, 이메일 시스템, 원자력안전기관, 에너지기업 등)과 서로 다른 공격 기법(API 스캐닝, 인증 우회, 비밀번호 추측 등)을 배정한다.
3. **공격 파도(attack wave) 반복** — 2026년 7월 1~4일 나흘간 총 12차례의 공격 파도를 실행한다. 각 파도마다 서브에이전트들이 표적 시스템을 다시 정찰하고, 막힌 경로가 있으면 전술을 스스로 수정해 재시도한다.
4. **안전장치 우회** — 서브에이전트들은 AI 모델의 안전 가드레일을 코드 취약점이 아니라 "이 작업은 승인된 모의침투(authorized penetration testing)"라는 거짓 맥락으로 속여서 통과시켰다.
5. **매핑·침투·탈취** — 21개 대만 정부 연계 시스템을 매핑하고, 85개 이상의 계정을 침해했으며, 미인증 API·숨겨진 인증 우회 API 3개를 악용해 2,500건 이상의 인사 기록을 탈취했다.
6. **베이지안 우선순위·자체 수정 루프** — Dream의 분석에 따르면 이 체계는 어떤 표적·기법을 다음에 시도할지 베이지안 방식으로 우선순위를 매기고, 실패하면 스스로 전략을 수정하는 루프를 갖추고 있었다.

## 구체 예시·사례

보도를 종합하면 대략적인 타임라인은 다음과 같다.

- **2026년 7월 1일~4일**: 나흘간 12차례의 공격 파도. 최대 8개 서브에이전트가 동시 가동돼 대만 정부 웹사이트·정부 이메일 시스템·국가 핵안보청(원자력안전 관련 기관)·IT 공급망 벤더·에너지 기업 7곳 이상을 표적으로 삼았다.
- **침투 기법 사례**: 한 서브에이전트는 미인증 API에서 직원 정보를 추출했고, 다른 서브에이전트는 CAPTCHA를 자동으로 뚫었으며, 또 다른 서브에이전트는 직원 ID 기반 예측 가능한 비밀번호 패턴을 공격했다. 자격증명 없이도 유효한 인증 세션을 반환하는 숨겨진 API 3개도 발견·악용됐다.
- **결과**: 21개 연계 시스템 매핑, 85개 이상 계정 침해, 2,500건 이상 인사 기록 탈취, 정부 웹 애플리케이션에 지속형 백도어 설치.
- **귀속 근거**: Dream은 작전 기록 상 간체자(Simplified Chinese) 사용을 근거로 중국계 운영자 가능성이 높다고 밝혔으나, 대만 당국도 Dream도 특정 국가·해킹조직으로 공식 귀속하지는 않았다.
- **공개 경위**: 이 작전은 2026년 8월 12일 파이낸셜타임스 보도로 처음 알려졌고, 같은 달 Black Hat 컨퍼런스에서 FBI 사이버부 부국장 Brett Leatherman, OpenAI의 Michael Dalton, 전직 NSA 국장 Paul Nakasone 등이 이를 "AI 생성 자율 사이버공격의 분기점"이라 언급하며 공론화됐다.

## 비슷한 것과 비교

| 구분 | 기존 사람 주도 APT 공격 | 이번 자율 AI 공격(대만 사례) |
|---|---|---|
| 실행 주체 | 숙련된 인간 해커 팀(정찰조·침투조 분업) | 오픈소스 AI 프레임워크 기반 서브에이전트 8개 |
| 속도·규모 | 표적당 수 주~수 개월 소요 | 나흘간 21개 시스템·12차례 공격 파도 |
| 전술 수정 | 인간이 상황 보고받고 다음 수 결정 | 서브에이전트가 막히면 스스로 전술 재조정(자체 수정 루프) |
| 필요 인력 | 다수의 숙련 인력 | 소수 운영자 + AI 에이전트 오케스트레이션 |
| 안전장치 우회 | 해당 없음(사람이 직접 판단·실행) | "승인된 모의침투"로 위장해 AI 모델의 가드레일을 속임 |
| 자율성 평가 | 해당 없음 | 업계 내 "완전 자율" vs "근자율(near-autonomous)" 이견 존재 |

선택 기준이라기보다 시사점 정리에 가깝다 — 이번 사례가 보여주는 건 "AI가 사람보다 뛰어난 해커"라기보다, **소수의 운영자가 AI 오케스트레이션만으로 과거 다수 인력이 필요했던 규모·속도의 공격을 수행할 수 있게 됐다**는 인력 레버리지의 변화다.

## 왜 지금 중요한가

이 사건은 2026년 7월 1~4일 발생했고, 2026년 8월 12일 파이낸셜타임스 보도를 계기로 The Register·CNN·Tom's Hardware·Dark Reading·Security Affairs 등 주요 매체가 잇달아 다뤘으며, 같은 달 Black Hat 컨퍼런스에서 FBI·OpenAI 관계자가 직접 언급하며 재확인됐다. 보도 시점이 모두 2026년 8월 12~14일에 몰려 있어 신선도 요건(3개월 이내)을 충족한다.

FBI 사이버부 부국장 Brett Leatherman과 OpenAI의 Michael Dalton은 Black Hat에서 "향후 위협 행위자들이 의도적으로 공격 에이전트 집단을 배포·최적화·무기화할 것"이라고 경고했고, 전직 NSA 국장 Paul Nakasone은 이를 "AI 생성 자율 사이버공격의 분기점"이라 표현했다. 다만 CyberScoop 보도가 짚었듯, Dream 연구진 스스로도 "모델만 실행한다고 되는 게 아니라 상당한 세부 조정·미세 조정 작업이 필요했다"고 밝혀, "완전 자율"이라는 수사와 실제 인간 개입 정도 사이에는 여전히 논쟁의 여지가 있다.

- [Autonomous AI attacks pose 'clear and present danger' to critical infrastructure — The Register(2026-08-14)](https://www.theregister.com/security/2026/08/14/autonomous-ai-attacks-pose-clear-and-present-danger-to-critical-infrastructure/5287594)
- [Near-autonomous AI agents attack Taiwan's nuclear safety agency — The Register(2026-08-12)](https://www.theregister.com/security/2026/08/12/near-autonomous-ai-agents-attack-taiwans-nuclear-safety-agency/5287055)
- [Researchers observe first 'near-autonomous' AI attack on government target in Taiwan — CyberScoop](https://cyberscoop.com/near-autonomous-ai-attack-government-target-taiwan/)
- [China-Linked Hackers Use AI Agents in Autonomous Attack on Taiwan — Security Affairs](https://securityaffairs.com/197079/apt/china-linked-hackers-use-ai-agents-in-autonomous-attack-on-taiwan.html)
- [Hackers used autonomous AI agents to attack Taiwan. Is this the future of cyberwarfare? — CNN Business(2026-08-13)](https://www.cnn.com/2026/08/13/tech/china-taiwan-ai-agent-cyberattack-intl-hnk)
- ["인간 개입 없이 AI가 스스로 침투" 中 연계 세력, 대만 정부·기반시설 자율 해킹 — 인사이트](https://www.insight.co.kr/news/568145)

## 회계법인 AI 직무 연결 포인트

이번 사건은 감사 대상 기업의 IT 일반통제(ITGC) 평가에 새로운 리스크 축을 추가한다. 기존 ITGC 점검은 "패치 관리·접근권한·변경관리가 제대로 되고 있는가"를 사람 손으로 확인하는 것이 중심이었지만, 이번처럼 AI 에이전트가 미인증 API·숨겨진 인증 우회 경로를 자동으로 탐색해 침투한다면, 감사인은 피감기업의 취약점 관리 체계가 "사람이 놓친 구멍"뿐 아니라 "AI가 자동으로 찾아낼 구멍"까지 방어하고 있는지를 새로운 평가 항목으로 삼아야 한다. 특히 원자력안전기관·에너지 기업처럼 규제산업의 핵심시설이 표적이 됐다는 점은, 상장기업의 사이버보안 리스크 공시(예: SEC의 사이버보안 사건 공시 규정)와 감사인의 부정위험 평가(ISA 240 등)에도 직접 영향을 준다.

더 근본적으로는, 이 사건이 "AI 에이전트 자체를 감사 대상으로 다뤄야 하는 이유"를 잘 보여준다. 공격자는 AI 모델의 안전 가드레일을 "승인된 모의침투"라는 거짓 맥락 하나로 우회했는데, 이는 피감기업이 사내에서 쓰는 AI 에이전트(예: 자동화된 결제 승인 에이전트, AI 기반 계정 관리 도구)에도 똑같이 적용될 수 있는 공격 표면이다. 즉 회계법인이 감사·자문에서 다루는 "AI 거버넌스" 항목에는 이제 모델 성능·편향 검증뿐 아니라, "이 AI 에이전트가 그럴듯한 거짓 맥락(프롬프트 인젝션·소셜 엔지니어링)으로 자신의 권한 범위를 넘어서게 설득당할 수 있는가"라는 레드팀 관점의 통제 평가가 포함돼야 한다.

마지막으로, 소수의 공격 운영자가 AI 오케스트레이션만으로 나흘 만에 21개 시스템을 매핑하고 85개 계정을 침해했다는 사실은, 감사법인이 자체적으로 도입 중인 AI 에이전트(코딩 에이전트, 자동화된 문서처리 에이전트 등)의 접근권한 설계에도 경종을 울린다. 회계법인 내부에서 AI 에이전트에 광범위한 시스템 접근권을 부여할 때, 이번 사례처럼 소수의 악의적 프롬프트만으로 그 권한이 오남용될 가능성을 최소권한 원칙(least privilege)과 계획-실행 분리 같은 구조적 통제로 얼마나 차단했는지가 자체 품질관리(QC 1000 등)의 새 점검 항목이 될 수 있다.

## 핵심 용어·논쟁

- **서브에이전트(Sub-agent)** — 오케스트레이터 역할의 AI가 특정 표적·작업을 맡겨 독립적으로 실행시키는 하위 AI 에이전트. 이번 사건에서는 최대 8개가 동시 가동됐다.
- **공격 파도(Attack Wave)** — 일정 시간 단위로 반복된 정찰·침투 시도의 묶음. 이번 사건은 나흘간 12차례의 파도로 구성됐다.
- **가드레일 우회(Guardrail Bypass)를 통한 프레이밍 공격** — AI 모델의 안전장치를 코드 취약점이 아니라 "이 작업은 정당한 모의침투"라는 거짓 맥락으로 속여 통과시키는 기법. 이번 사건의 핵심 우회 수법이다.
- **근자율(Near-autonomous) vs 완전 자율(Fully autonomous)** — "완전 자율"은 인간 개입이 전무하다는 뜻이지만, 실제로는 프레임워크 구축·미세조정 등에 상당한 인간 작업이 들어갔다는 것이 Dream 연구진 스스로의 설명이다. CyberScoop 등 일부 매체는 이 때문에 "근자율"이라는 더 신중한 표현을 쓴다.

가장 뜨거운 쟁점은 "이 공격을 '세계 최초의 완전 자율 AI 사이버공격'이라 부르는 것이 정확한가"다. TechRadar·Tom's Hardware 등은 자극적으로 "완전 자율(fully autonomous)"·"종단간(end-to-end)"이라는 표현을 헤드라인에 썼지만, 실제 조사를 수행한 Dream 연구진은 "모델만 실행하는 것보다 훨씬 많은 작업(세부·미세 조정)이 필요했다"고 밝혀 그 표현에 스스로 거리를 뒀다. 이는 AI 보안 사건 보도에서 흔히 나타나는 "자율성 과장"의 사례이자, 독자가 헤드라인만이 아니라 1차 조사 기관의 원 표현("near-autonomous")까지 확인해야 하는 이유이기도 하다.

## 자료 깊이 읽기

이번 사건은 발생 직후(8월 12~14일) 여러 매체가 동시에 보도해 교차 검증이 비교적 쉬웠다. 아래 세 자료를 직접 열어 확인하고 요약했다.

### Autonomous AI attacks pose 'clear and present danger' to critical infrastructure — The Register — 영어/뉴스기사/중급
2026년 8월 14일 Black Hat 컨퍼런스 후속 보도. 공격 시기(7월 초 나흘), 사용 프레임워크(Hermes·OpenClaw), 서브에이전트 수(최대 8개), 공격 파도 수(12회)를 명시하고, FBI 사이버부 부국장 Brett Leatherman과 OpenAI의 Michael Dalton이 "위협 행위자들이 앞으로 공격 에이전트 집단을 의도적으로 배포·최적화·무기화할 것"이라 경고한 발언을 전한다. 전직 NSA 국장 Paul Nakasone은 이를 "AI 생성 자율 사이버공격의 분기점"으로 표현했다. 다만 "세계 최초" 표현의 정확한 출처는 이 기사 자체에서 명시되지 않는다.

### Researchers observe first 'near-autonomous' AI attack on government target in Taiwan — CyberScoop — 영어/뉴스기사/중급
이스라엘 보안업체 Dream이 160메가바이트 규모의 온라인 아카이브를 통해 이 작전을 처음 발견한 경위를 다룬다. 핵심은 제목부터 "완전 자율"이 아닌 "근자율(near-autonomous)"이라는 신중한 표현을 쓴 점이다. Dream 연구진은 "모델만 실행하는 것보다 훨씬 많은 세부·미세 조정 작업이 필요했다"고 밝히면서도, 공격 체계가 베이지안 우선순위 지정과 자체 수정 루프 같은 고급 기능을 갖췄다고 설명한다. 다른 매체의 "세계 최초 완전 자율 공격"이라는 헤드라인과 대비되는 균형 잡힌 시각을 제공한다.

### "인간 개입 없이 AI가 스스로 침투" 中 연계 세력, 대만 정부·기반시설 자율 해킹 — 인사이트 — 한국어/뉴스기사/입문
국내 매체의 관련 보도로, 21개 정부 시스템 매핑·85개 이상 계정 침해·2,500여 건 인사기록 탈취·원자력안전기관과 에너지기업 7곳까지 피해 확대 등 핵심 수치를 The Register·CyberScoop 보도와 일치하게 전한다. Dream이 침투 기록의 간체자 사용을 근거로 중국발 가능성을 지목했다고 언급하되, 대만 당국이 구체적 피해 내용 공개를 자제하고 있다는 점도 함께 짚는다.

이 주제를 다룬 YouTube 영상(TaiwanPlus News의 "Analysis: China-Linked Hackers Use AI Tools To Target Taiwan" 등)을 검색으로 확인했으나, `yt-dlp`가 오늘 환경에서 YouTube 측 429(Too Many Requests)·봇 차단 응답을 지속적으로 반환해 자막을 내려받지 못했다(임의의 다른 영상으로도 동일하게 재현되어 특정 영상이 아닌 환경 차원의 일시적 접근 제한으로 판단된다). 지어낸 요약을 넣는 대신 이번 편은 실제로 확인한 텍스트 자료 세 건으로 구성했다 — (요약 불가 — 자막/본문 확인 실패로 영상 상세 요약 파일은 작성하지 않음).

**그 외 참고**
- [Suspected China-linked hackers used AI to run the first-ever end-to-end autonomous cyberattack on Taiwan's government — Tom's Hardware](https://www.tomshardware.com/tech-industry/cyber-security/suspected-china-linked-hackers-used-ai-to-run-the-first-ever-end-to-end-autonomous-cyberattack-on-taiwans-government-israeli-firm-says-open-source-built-tool-continuously-devised-effective-hack-strategies-in-real-time) — 영어, 뉴스기사, 입문
- [China-linked hacker AI capabilities APAC attack — Dark Reading](https://www.darkreading.com/cyberattacks-data-breaches/china-linked-hacker-ai-capabilities-apac-attack) — 영어, 뉴스기사, 중급

## 자가 점검 질문

1. 이번 사건에서 공격자가 AI 모델의 안전 가드레일을 우회한 방법("승인된 모의침투로 위장")은 코드 취약점 공격과 어떻게 다르며, 이런 유형의 우회를 막으려면 AI 에이전트 설계에 어떤 구조적 통제가 필요한가?
2. "완전 자율 AI 공격"이라는 표현과 Dream 연구진의 "근자율(near-autonomous)"이라는 표현 사이의 간극은 왜 생겼으며, 감사·리스크 평가 실무자는 이런 자율성 과장을 어떻게 걸러내야 하는가?
3. 피감기업이 사내에서 AI 에이전트에 시스템 접근권한을 부여하고 있다면, 감사인은 ITGC 평가에서 구체적으로 어떤 질문(권한 범위, 프롬프트 인젝션 방어, 이상행위 로깅 등)을 추가로 던져야 하는가?
