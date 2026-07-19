# 오늘의 AI 개념: DeepSeek V4 정식 출시(DeepSeek V4 Release)

> 작성일: 2026-07-20 · 분류: trend

## 한 줄 정의

DeepSeek V4는 중국 딥시크가 2026년 7월 15일 정식 출시한 오픈 웨이트 대형 언어모델로, 100만 토큰급 문맥을 실용적인 비용으로 처리하는 새 어텐션 구조와 전력 요금처럼 시간대별로 값이 달라지는 API 가격제를 함께 선보였다.

## 쉬운 설명

DeepSeek V4는 MoE(Mixture-of-Experts, 전문가 혼합) 구조를 쓰는 V4-Pro와 경량판 V4-Flash 두 변형으로 나온다. MoE란 입력마다 전체 파라미터 중 일부 "전문가" 부분만 골라 쓰는 구조로, 전체 규모는 크지만 실제 연산량은 그보다 훨씬 적게 유지하는 방식이다.

비유하자면 대형 백화점 전체 직원(전체 파라미터) 중, 손님 한 명이 올 때마다 그 손님에게 필요한 매장 직원 몇 명(활성 파라미터)만 응대에 나서는 것과 비슷하다. V4-Pro는 총 1.6조 개 파라미터 중 토큰 하나를 처리할 때 약 490억 개만 실제로 쓰인다.

기존 V3.2 세대와 다른 점은 CSA(Compressed Sparse Attention, 압축 희소 어텐션)와 HCA(Heavily Compressed Attention, 고압축 어텐션)를 섞은 하이브리드 어텐션 구조다. CSA는 토큰 여러 개를 압축기로 뭉쳐 저장한 뒤 그중 중요한 부분에만 집중하고, HCA는 훨씬 더 많은 토큰을 하나로 압축해 전체를 훑어보는 방식이다. 이 조합 덕분에 100만 토큰 문맥에서 단일 토큰 추론에 드는 연산량(FLOPs)이 V3.2 대비 약 27%, 어텐션 계산에 필요한 메모리(KV 캐시)는 약 10% 수준으로 줄었다고 소개된다.

## 동작 원리 / 핵심 스펙

| 항목 | V4-Pro | V4-Flash |
|------|------|------|
| 총 파라미터 | 1.6조 | 2,840억 |
| 활성 파라미터 | 490억 | 130억 |
| 문맥 윈도우 | 100만 토큰 | 100만 토큰 |
| 최대 출력 토큰 | 38만 4천 | 38만 4천 |

두 모델 모두 사고형(thinking)·비사고형 모드를 지원하고, 도구 호출(tool calling)과 JSON 출력을 기본 지원한다. 다만 라이선스 표기는 출처마다 Apache 2.0과 MIT로 엇갈려 나와, 실제 도입 전에는 공식 라이선스 파일을 직접 확인할 필요가 있다.

## 구체 예시·사례

DeepSeek는 V4를 완전한 코드베이스를 한 번에 읽고, 여러 턴에 걸친 장기 자율 에이전트 작업을 KV 캐시 절감 덕분에 낮은 비용으로 지속하는 에이전틱 코딩·기업 자동화용 모델로 마케팅한다. 클로드 코드를 비롯한 주요 에이전트 프레임워크와 곧바로 연동되도록 지원하며, V4-Pro는 자율적인 코드 리팩터링·디버깅 후보로, V4-Flash는 대량 프로덕션 워크로드용 저비용 변형으로 자리매김하고 있다.

## 비슷한 것과 비교

| 모델 | 총/활성 파라미터 | 문맥 | 가격(입력/출력, 달러/백만 토큰) | 개방성 |
|------|------|------|------|------|
| DeepSeek V4-Pro | 1.6조 / 490억 | 100만 | 오프피크 0.435/0.87, 피크 시 약 2배 | 오픈 웨이트 |
| DeepSeek V4-Flash | 2,840억 / 130억 | 100만 | 0.14/0.28 | 오픈 웨이트 |
| Claude Sonnet 5 | 비공개 | 100만(기본=최대) | 표준 3/15 | 비공개 |
| GPT-5.6 계열 | 비공개 | 100만 | 라인업별 1~5 / 6~30 | 비공개 |
| Kimi K3 | 2.8조 / 활성 전문가 16개 | 100만 | 3/15(캐시 히트 0.30) | 오픈 웨이트 |

가격 대비로 보면 1달러로 V4-Pro는 약 115만 출력 토큰을, Kimi K3는 약 6만 7천 토큰을 살 수 있어, DeepSeek 쪽이 압도적으로 저렴하다는 비교가 나온다. 다만 코딩 벤치마크(Terminal-Bench 2.1)에서는 Kimi K3가 88.3%, DeepSeek V4-Pro가 62.1%를 기록해, 가격과 성능이 반비례하는 모습을 보인다.

## 왜 지금 중요한가

DeepSeek는 이번 출시와 함께 피크/오프피크 시간대별 API 요금제를 도입했다. 매일 오전 9시~정오, 오후 2시~6시가 피크 시간대이며, 이 시간대 요금은 평소의 2배로 책정된다. V4-Pro 출력 기준으로 오프피크 100만 토큰당 6위안이던 요금이 피크 시간에는 12위안(약 1.77달러)까지 오른다.

DeepSeek는 2025년 V3·R1으로 업계 가격 경쟁을 촉발했던 회사인데, 2026년 7월 처음으로 시간대별 할증 요금을 도입하며 노선을 일부 되돌린 셈이다. 이는 초저가 경쟁이 무한정 지속되기 어렵다는 방증이자, 반도체 수출 규제 속에서 실제 연산 용량 제약이 존재한다는 신호로 해석된다.

- [DeepSeek to launch V4 in mid-July with new peak-time API pricing - TechNode](https://technode.com/2026/06/30/deepseek-to-launch-v4-in-mid-july-with-new-peak-time-api-pricing/)
- [After triggering price war, DeepSeek reverses course, adds surcharge for peak-hour API use - SCMP](https://www.scmp.com/tech/big-tech/article/3358868/after-triggering-price-war-deepseek-reverses-course-surcharge-peak-hour-api-use)

## 회계법인 AI 직무 연결 포인트

100만 토큰 문맥과 낮은 출력 요금 덕분에 재무제표 전체 세트나 여러 해치 원장 데이터를 하나의 문맥에 통째로 넣어 낮은 비용으로 분석하는 것이 이론적으로 가능해졌다는 평가가 나온다. 오픈 웨이트이므로 자체 서버에 직접 구동해 데이터를 외부로 보내지 않는 선택지도 있다.

다만 부정회계 판단 벤치마크(AuditFraudBench)에서 DeepSeek V4-Flash를 시험한 결과, 수익 인식 시점 조작 탐지 재현율은 72.6%로 준수했지만 다른 유형의 부정(서술적 왜곡, 비용 이연 등)도 대부분 같은 유형으로 오분류하는 등 세부 판단의 정밀도는 낮았다는 평가가 있다. 정교한 회계 판단을 전적으로 맡기기에는 아직 이르다는 근거로 볼 수 있다.

민감한 재무 정보를 다룰 때는 데이터 처리 방식에 대한 우려도 짚어야 한다. DeepSeek의 공식 웹·API를 그대로 쓸 경우 데이터가 중국 내에 저장되고 향후 모델 학습에 재사용될 가능성이 있다는 지적이 있어, 민감한 재무 데이터를 공개 API에 그대로 넣는 것은 권장되지 않는다. 오픈 웨이트를 자체 호스팅하면 이 우려는 피할 수 있지만, 대신 모델 가중치 관리와 컴플라이언스 문서화를 회사가 처음부터 직접 구축해야 하는 부담이 새로 생긴다.

## 핵심 용어·논쟁

- **MoE(Mixture-of-Experts, 전문가 혼합)** — 전체 파라미터 중 입력마다 일부 전문가 서브네트워크만 활성화해 연산량을 줄이는 구조.
- **활성 파라미터(Active Parameters)** — 추론 1회당 실제로 연산에 관여하는 파라미터 수로, 총 파라미터보다 훨씬 작아 비용과 속도를 좌우한다.
- **문맥 윈도우(Context Window)** — 모델이 한 번에 참조할 수 있는 입력·출력 토큰의 최대 길이.
- **KV 캐시(KV Cache)** — 어텐션 계산 시 이전 토큰들의 키·값을 저장해두는 메모리로, 문맥이 길어질수록 커진다.
- **피크/오프피크 과금** — 전력 요금제처럼 수요가 몰리는 특정 시간대에 API 단가를 높게 매기는 방식.

라이선스 표기(Apache 2.0 대 MIT)가 출처마다 다르게 보도되는 점, 그리고 "칩 설계 자동화" 같은 일부 마케팅 사례가 이번 조사에서 원출처로 직접 확인되지 않은 점은 실제 도입 전 반드시 재확인이 필요한 부분이다.

## 자료 깊이 읽기

DeepSeek 공식 발표문(api-docs.deepseek.com)과 기술 전문지(marktechpost.com)의 원문은 이번 세션의 접속 제한으로 직접 열람하지 못했다(요약 불가 — 본문 확인 실패). 아래는 검색 결과에 실제로 나타난 자료만 링크로 남긴다.

- [DeepSeek AI Releases DeepSeek-V4 - MarkTechPost](https://www.marktechpost.com/2026/04/24/deepseek-ai-releases-deepseek-v4-compressed-sparse-attention-and-heavily-compressed-attention-enable-one-million-token-contexts/) — 영어, 전문지 기사, 중급
- [Kimi K3 vs DeepSeek V4-Pro vs GLM-5.2 비교 - MarkTechPost](https://www.marktechpost.com/2026/07/18/kimi-k3-vs-deepseek-v4-pro-vs-glm-5-2-open-trillion-scale-moe-models-compared-on-benchmarks-license-and-serving-cost/) — 영어, 전문지 기사, 중상급
- [DeepSeek-V4 Explained: How Million-Token Context LLMs Become Practical - YouTube](https://www.youtube.com/watch?v=DvG4E-nYHvI) — 영어, 유튜브, 중급
- [DeepSeek v4 in 4 Minutes - YouTube](https://www.youtube.com/watch?v=Oi6pQmGjH7Y) — 영어, 유튜브, 입문
- [DeepSeek 나무위키](https://namu.wiki/w/DeepSeek) — 한국어, 위키 문서, 입문

## 자가 점검 질문

1. MoE 구조에서 총 파라미터 수와 활성 파라미터 수의 차이가 실제 서비스 비용과 속도에 어떤 영향을 미치는가?
2. 100만 토큰 문맥과 저렴한 요금이 재무 데이터 분석에 주는 이점과, 동시에 짚어야 할 데이터 보안·거버넌스 우려는 각각 무엇인가?
3. 오픈 웨이트 모델을 자체 호스팅하는 방식과 벤더의 API를 그대로 쓰는 방식은 회계법인 입장에서 어떤 책임 소재의 차이를 만드는가?
