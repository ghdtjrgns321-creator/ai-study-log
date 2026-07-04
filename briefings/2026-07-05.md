# 오늘의 AI 개념: 컨텍스트 엔지니어링(Context Engineering)

## 한 줄 정의

AI에게 질문 문구만 잘 다듬어 주는 대신, 좋은 답을 내는 데 필요한 배경 정보 전체를 체계적으로 준비해서 넣어 주는 작업이다.

## 쉬운 설명

컨텍스트 엔지니어링은 거대언어모델(LLM, Large Language Model)이 특정 작업을 수행할 때 참고할 지식, 이전 대화 기록, 회사 규정, 외부 문서, 도구 사용 결과 등 필요한 정보 전체를 설계하고 관리하는 작업을 말한다. 단발성 질문 하나를 잘 쓰는 프롬프트 엔지니어링과 달리, 여러 단계와 여러 세션에 걸쳐 어떤 정보를 언제 모델에 넣어 줄지 시스템 차원에서 설계한다.

비유하자면 프롬프트 엔지니어링이 신입사원에게 오늘 할 업무 지시를 명확하게 전달하는 일이라면, 컨텍스트 엔지니어링은 그 신입사원이 일을 제대로 하도록 사규집, 이전 업무 이력, 관련 부서 연락처, 참고 서식을 미리 책상 위에 챙겨 놓아 주는 일에 가깝다. 질문을 잘 만드는 기술이 아니라, 질문에 답하는 데 필요한 재료를 빠짐없이 갖춰 주는 기술이다.

프롬프트 엔지니어링과 완전히 대체 관계는 아니다. 프롬프트 엔지니어링은 단일 지시문의 표현을 다듬는 좁은 범위의 작업이고, 컨텍스트 엔지니어링은 검색증강생성(RAG, Retrieval-Augmented Generation), 장단기 기억, 도구 연결까지 포함하는 더 넓은 범위의 시스템 설계 작업이다.

## 왜 지금 중요한가

에이전트형 AI가 여러 단계를 스스로 계획하고 실행하는 구조로 발전하면서, 단일 프롬프트만으로는 일관된 결과를 내기 어려워졌다. 이 때문에 정보를 어떻게 모으고 어떤 순서로 모델에 제공할지를 다루는 컨텍스트 엔지니어링이 최근 논의의 중심으로 떠올랐다.

세무·회계 분야에서도 관련 논의가 나오고 있다. Thomson Reuters는 세무·회계 업무에서 신뢰할 수 있고 감사 가능한 결과를 얻으려면, 단순히 질문을 잘 던지는 것을 넘어 조직 구조·업무 절차·업무 로직 같은 맥락 정보를 AI에 체계적으로 제공하는 방식이 중요해지고 있다고 설명한다.

- [What context engineering means for tax and accounting](https://tax.thomsonreuters.com/blog/context-engineering-in-tax-and-accounting-the-next-level-of-ai-workflows/)

## 회계법인 AI 직무 연결 포인트

감사 업무에서는 회사별 조직 구조, 계정과목 정의, 표준운영절차(SOP, Standard Operating Procedure)를 컨텍스트로 미리 구성해 두면, AI가 여러 회사·여러 기간의 감사 업무에서 일관된 판단 기준을 적용하도록 만들 수 있다.

검색증강생성과 결합하면 회계기준서, 과거 감사조서, 재무제표 주석을 컨텍스트로 관리해, AI가 답변마다 근거 문서를 함께 제시하도록 만들 수 있다. 이는 감사 결과의 출처 추적이 요구되는 업무 특성과 맞닿아 있다.

모델 컨텍스트 프로토콜(MCP, Model Context Protocol) 같은 표준을 활용하면 ERP(Enterprise Resource Planning, 전사적 자원관리)나 회계 시스템의 실시간 데이터를 컨텍스트로 연결할 수 있어, 분개 내역이나 잔액 조회 같은 최신 데이터를 반영한 분석이 가능해진다.

## 학습 자료

- [\[프롬프트 강의\] 프롬프트 엔지니어링과 컨텍스트 엔지니어링](https://www.youtube.com/watch?v=CeZPsKo1nXw) — 한국어, 유튜브, 입문
- [\[강수진 X 테디노트\] 2025 프롬프트 엔지니어링, Context Engineering & Agent Orchestration](https://www.youtube.com/watch?v=b8GfaOVRqH8) — 한국어, 유튜브, 중급
- [Context Engineering Clearly Explained](https://www.youtube.com/watch?v=jLuwLJBQkIs) — 영어, 유튜브, 입문
- [Context Engineering: AI 시대의 새로운 핵심 역량](https://devocean.sk.com/blog/techBoardDetail.do?ID=167772&boardType=techBlog) — 한국어, 텍스트(SK DevOcean 기술 블로그), 중급
- [What context engineering means for tax and accounting](https://tax.thomsonreuters.com/blog/context-engineering-in-tax-and-accounting-the-next-level-of-ai-workflows/) — 영어, 텍스트, 중급

## 자가 점검 질문

1. 프롬프트 엔지니어링과 컨텍스트 엔지니어링의 차이를 한 문장으로 설명한다면 무엇인가?
2. 감사 업무에 컨텍스트 엔지니어링을 적용할 때, 어떤 사내 문서나 데이터를 컨텍스트로 우선 구성해야 하는가?
3. 컨텍스트를 과도하게 많이 제공했을 때 발생할 수 있는 문제는 무엇이며, 이를 어떻게 관리할 수 있는가?
