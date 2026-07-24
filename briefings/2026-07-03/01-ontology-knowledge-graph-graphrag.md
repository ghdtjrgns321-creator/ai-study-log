# 오늘의 AI 개념: 온톨로지 · 지식그래프 · GraphRAG

## 한 줄 정의
데이터를 표가 아니라 개체와 개체 사이의 관계망으로 저장하고, 그 관계망을 검색해 AI 답변의 근거로 삼는 방식이다.

## 쉬운 설명
지식그래프(Knowledge Graph)는 정보를 "개체 — 관계 — 개체" 형태로 연결해 저장하는 구조다. 예를 들어 "삼성전자 — 공급받는다 → TSMC", "K-IFRS 1115호 — 적용된다 → 수익인식"처럼 점(개체)과 선(관계)으로 세상을 그린다.

온톨로지(Ontology)는 그 그래프를 그리기 위한 설계도다. "회사라는 개체는 어떤 속성을 가지며 어떤 관계를 맺을 수 있는가"를 미리 규정한 스키마에 해당한다. 관계형 데이터베이스로 비유하면 온톨로지는 테이블 설계(스키마)이고, 지식그래프는 그 설계에 따라 실제로 채워진 데이터다.

GraphRAG는 이 지식그래프를 검색 기반 생성(RAG, Retrieval-Augmented Generation)에 결합한 기법이다. 일반 RAG가 문서를 잘게 쪼갠 조각을 벡터로 검색한다면, GraphRAG는 개체와 관계, 경로까지 함께 검색한다. 그 덕분에 "A와 B를 거쳐 C에 도달하는" 다단계 추론 질문에서 더 정확하고 근거를 추적하기 쉬운 답을 낸다.

회계·감사 영역에서 특히 주목받는 이유는 거래처·계열사·전표 사이의 관계 자체가 분석 대상이기 때문이다.

## 왜 지금 중요한가
Gartner는 2026년 에이전틱 AI 하이프사이클에서 지식그래프를 핵심 구성요소로 다루고 있다. 기업용 지식그래프 시장이 빠르게 성장 중이며, 다단계 질문에서 지식그래프 기반 검색이 일반 벡터 검색보다 정확도가 크게 높다는 결과가 보고되고 있다.
- 출처: https://www.gartner.com/en/articles/hype-cycle-for-agentic-ai
- 출처: https://promethium.ai/guides/enterprise-knowledge-graph-buyers-guide-2026/
- 출처: https://www.ibm.com/think/news/ai-tech-trends-predictions-2026

## 회계법인 AI 직무 연결 포인트
- 특수관계자 거래 탐지: 회사·거래처·계열사·임원을 그래프로 연결하면 표 형태로는 드러나지 않는 순환 거래나 우회 거래 경로를 관계 탐색으로 찾아낼 수 있다.
- 전표 흐름 추적: 계정·전표·증빙을 개체로 연결하면 입력부터 재무제표 반영까지의 경로를 따라가며 이상 지점을 짚을 수 있다.
- 감사 문서 질의: 계약서·공시·내부규정을 지식그래프로 묶고 GraphRAG로 검색하면 "이 거래에 적용되는 기준서와 근거 문서는 무엇인가" 같은 다단계 질문에 근거를 붙여 답할 수 있다.

## 학습 자료
- [온톨로지: 데이터가 '지식'이 되는 순간](https://www.youtube.com/watch?v=d6VPiX-Hyr8) — 한국어 · 입문
- [지식 그래프(Knowledge Graph)의 의미와 가치](https://www.youtube.com/watch?v=N3_F9DzNQx4) — 한국어 · 입문
- [RAG 한계를 온톨로지로 극복 가능? 팔란티어 온톨로지 vs RAG](https://www.youtube.com/watch?v=wyClwnOPuj8) (23:38부터) — 한국어 · 중급
- [GraphRAG 실무 적용 고려요소 심층탐구 (테디노트)](https://www.youtube.com/watch?v=zHN2jDZHvI0) — 한국어 · 중급
- [IBM: GraphRAG Explained](https://www.youtube.com/watch?v=Za7aG-ooGLQ) — 영어 · 입문(14분)
- [SK Devocean: 지식그래프·GraphRAG 구조화된 지식의 발견](https://devocean.sk.com/blog/techBoardDetail.do?ID=166632&boardType=techBlog) — 한국어 · 텍스트 정리
- 실습: [파이썬으로 GraphRAG Agent 만들기](https://www.youtube.com/watch?v=H2OMM6GOP3g) / [파이썬과 AI로 지식그래프 만들기](https://www.youtube.com/watch?v=_sc5kXcI0l4) — 한국어 · 실습

## 자가 점검 질문 3개
1. 일반 RAG와 GraphRAG의 차이를 면접관에게 1분 안에 설명한다면 어떻게 하겠는가.
2. 온톨로지와 본인 KIFRS1115 프로젝트의 DB 스키마(ERD)는 무엇이 같고 무엇이 다른가.
3. 감사 업무에서 지식그래프로 풀 수 있는 문제를 하나 제시한다면 무엇인가.
