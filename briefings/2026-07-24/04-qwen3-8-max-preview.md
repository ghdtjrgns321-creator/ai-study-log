# 오늘의 AI 개념: 알리바바 Qwen3.8-Max-Preview 공개

> 작성일: 2026-07-24 · 분류: trend

## 한 줄 정의

알리바바가 2.4조 개 매개변수를 가진 새 대형 멀티모달 모델의 미리보기 버전을 공개했지만, 성능을 검증할 벤치마크 자료는 아직 내놓지 않았다.

## 쉬운 설명

알리바바 클라우드는 2026년 7월 19일 상하이에서 열린 세계인공지능대회(WAIC)에서 큐원(Qwen) 계열의 새 플래그십 모델 미리보기인 "Qwen3.8-Max-Preview"를 공개했다. 매개변수(모델이 학습한 값의 개수, Parameter) 규모가 2.4조 개로, 텍스트뿐 아니라 이미지·영상·문서까지 다루는 멀티모달(Multimodal) 모델이다.

이 모델은 희소 전문가 혼합(Sparse Mixture-of-Experts, MoE) 구조를 쓴다. 비유하자면 하나의 거대한 뇌가 모든 질문에 답하는 대신, 여러 전문가 팀을 두고 질문 유형에 맞는 일부 전문가만 골라 답하게 하는 방식이다. 그 결과 전체 매개변수는 많아도 한 번의 응답에 실제로 쓰이는 매개변수는 그보다 훨씬 적다.

알리바바는 이 모델이 코딩·풀스택 개발·데이터 분석·오피스 업무에서 이전 버전인 Qwen3.7-Max를 능가할 것이라고 밝혔고, 자체 트위터(X) 게시물에서 성능이 "앤트로픽의 Fable 5에 이어 2위"라고 주장했다. 다만 이 주장을 뒷받침할 벤치마크 표, 모델 카드, 활성화 매개변수 수 같은 기술 문서는 함께 공개되지 않았다.

## 동작 원리

1. Qwen3.8-Max-Preview는 희소 MoE 구조로, 입력 토큰마다 전체 전문가 네트워크 중 일부만 활성화해 연산량을 줄인다.
2. 텍스트·이미지·영상·문서를 함께 처리하는 멀티모달 입력을 지원하며, 컨텍스트 윈도는 최대 100만 토큰 수준으로 알려졌다.
3. 정식 버전이 아닌 미리보기(Preview) 단계로, 알리바바의 Token Plan 구독과 코딩 도구 Qoder·QoderWork를 통해 제한적으로 접근할 수 있다.
4. 프로모션 기간에는 기존 대비 대폭 할인된 가격(표준가의 약 10% 수준)으로 제공된다.
5. 알리바바는 정식 버전을 추후 오픈소스(가중치 공개)로 출시할 계획이라고 밝혔으나, 구체적인 출시 시점은 발표되지 않았다.

## 구체 예시·사례

같은 주 초 문슛AI(Moonshot AI)가 오픈 가중치 모델 키미 K3(Kimi K3)를 공개한 지 며칠 지나지 않아 알리바바가 이번 미리보기를 내놓았다. 중국 AI 기업들이 잇달아 대형 모델을 발표하며 경쟁하는 흐름 속에 이번 공개가 이어진 것으로 볼 수 있다.

다만 초기 사용 후기는 엇갈린다. 일부 사용자는 최상위권 모델에 근접할 만큼 우수하다고 평가한 반면, 다른 사용자는 모델 규모에 비해 기대에 못 미친다는 반응을 보였다. 제3자 평가기관(Artificial Analysis, LMArena 등)의 독립적인 채점 결과는 아직 나오지 않아, 현재로서는 알리바바 측 주장을 그대로 검증하기 어렵다.

## 비슷한 것과 비교

| 구분 | Qwen3.8-Max-Preview | Qwen3.7-Max(이전 버전) | Kimi K3(문슛AI) |
|------|------|------|------|
| 공개 형태 | 미리보기, 벤치마크 미공개 | 정식 버전 | 오픈 가중치로 정식 공개 |
| 매개변수 | 2.4조(활성화 규모 비공개) | 상대적으로 소규모 | 별도 공개 규모 |
| 검증 상태 | 제3자 벤치마크 없음 | 검증된 실적 존재 | 오픈 가중치라 직접 검증 가능 |

가중치가 공개되지 않고 자체 주장 외 근거가 없는 단계이므로, 이번 미리보기의 성능 우위 주장은 정식 출시와 독립 벤치마크가 나올 때까지 잠정적으로만 받아들이는 것이 합리적이다.

## 왜 지금 중요한가

이 발표는 2026년 7월 19일, 8일 전인 7월 22일 기사 게재 시점 기준으로도 최근 5일 이내의 소식이다. 알리바바가 자사 모델을 앤트로픽의 최신 모델과 직접 비교하며 "2위"라고 자평한 점은, 중국 빅테크가 서구 프런티어 모델과의 격차를 좁혔다고 주장하는 흐름을 보여주는 사례로 언급된다.

동시에 벤치마크·모델 카드 없이 성능 주장만 먼저 내놓은 공개 방식은, 검증되지 않은 수치를 그대로 인용하는 위험성을 보여주는 반면교사이기도 하다.

- [Alibaba Previews Qwen3.8-Max, a 2.4 Trillion-Parameter Multimodal Model — MarkTechPost](https://www.marktechpost.com/2026/07/19/alibaba-previews-qwen3-8-max-a-2-4-trillion-parameter-multimodal-model-days-after-moonshots-kimi-k3-open-weight-launch/)
- [Alibaba's Qwen3.8-Max Claims Second Place Behind Fable 5 With No Benchmarks Published — Tech Times](https://www.techtimes.com/articles/321158/20260721/alibabas-qwen38-max-claims-second-place-behind-fable-5-no-benchmarks-published.htm)
- [Alibaba's new generation large model Qwen 3.8 announced with performance "second only to Claude Fable 5" — GIGAZINE](https://gigazine.net/gsc_news/en/20260721-qwen3-8/)

## 회계법인 AI 직무 연결 포인트

빅4 회계법인이 사내 AI 도구에 어떤 모델을 쓸지 검토할 때, 벤더의 성능 주장을 곧이곧대로 채택하지 않고 독립 벤치마크·보안 검증·데이터 처리 정책까지 함께 확인하는 절차가 필요하다는 점을 이번 사례가 잘 보여준다. 특히 감사 데이터처럼 민감한 정보를 다루는 업무라면, 벤치마크 미공개 상태의 모델을 실무에 바로 투입하는 것은 위험 부담이 크다.

또한 중국계 모델을 포함해 다양한 지역의 대형 모델이 빠르게 등장하는 상황은, 국내 회계법인이 데이터 주권·규제 준수(예: 한국 AI기본법) 관점에서 모델 선택 기준을 미리 세워둬야 한다는 시사점을 준다.

면접에서는 "새로 나온 모델이 최고 성능이라고 홍보될 때 무엇을 먼저 확인해야 하는가"라는 질문에, 독립 벤치마크 유무, 모델 카드 공개 여부, 데이터 처리·보안 정책을 확인 기준으로 제시할 수 있다.

## 핵심 용어·논쟁

- **희소 전문가 혼합(Sparse Mixture-of-Experts, MoE)** — 입력마다 전체 매개변수 중 일부 전문가 네트워크만 선택적으로 활성화하는 모델 구조.
- **모델 카드(Model Card)** — 모델의 학습 데이터, 성능, 한계, 위험 요소를 정리해 공개하는 문서.
- **활성화 매개변수(Activated Parameters)** — MoE 구조에서 한 번의 추론에 실제로 계산에 관여하는 매개변수 수. 전체 매개변수 수와 다르다.
- **오픈 가중치(Open Weight)** — 모델의 학습된 가중치 파일을 공개해 누구나 내려받아 실행·검증할 수 있게 하는 배포 방식.

벤치마크 없이 자체 주장만으로 순위를 언급하는 공개 방식이 업계 관행으로 굳어지는 것이 바람직한지는 논쟁적이다. 독립 평가기관의 검증이 뒤따르지 않으면 마케팅 문구와 실제 성능을 구분하기 어렵다는 지적이 나온다.

## 자료 깊이 읽기

### Alibaba Previews Qwen3.8-Max, a 2.4 Trillion-Parameter Multimodal Model — MarkTechPost — 영어, 뉴스, 중급
AI 전문 매체 MarkTechPost의 기사로, Qwen3.8-Max-Preview 공개 소식을 비교적 상세히 다룬다. 상하이 WAIC에서 공개됐다는 발표 경위, 2.4조 매개변수·멀티모달 지원이라는 사양, 문슛AI의 키미 K3 오픈 가중치 공개 직후 나온 발표라는 시점상 맥락을 정리한다. 알리바바의 Token Plan을 통한 제한적 접근 방식과, 정식 버전은 추후 오픈소스로 공개될 예정이라는 알리바바 측 계획도 함께 전한다. 벤치마크 점수나 모델 카드가 발표에 포함되지 않았다는 점을 명확히 짚어, 성능 주장을 그대로 받아들이기보다 검증이 필요한 단계임을 시사한다.

### Alibaba's Qwen3.8-Max Claims Second Place Behind Fable 5 With No Benchmarks Published — Tech Times — 영어, 뉴스, 초중급
알리바바의 자체 성능 주장을 비판적으로 검토한 기사다. 알리바바 큐원 팀이 X(트위터)에서 "Fable 5에 이어 2위"라고 밝힌 문구를 인용하면서도, 이를 뒷받침할 벤치마크 점수·모델 카드·활성화 매개변수 수·상세 기술 문서가 전혀 공개되지 않았다는 점을 제목부터 강조한다. 독립적으로 성능을 검증하기 어려운 현재 상태에서 이 주장을 어떻게 받아들여야 하는지에 대한 신중한 관점을 제공한다.

**그 외 참고**
- [Alibaba's new generation large model Qwen 3.8 announced — GIGAZINE](https://gigazine.net/gsc_news/en/20260721-qwen3-8/) — 영어, 뉴스, 초중급
- [Qwen3.8 is Here in Preview - Thorough Hands-on Testing — YouTube](https://www.youtube.com/watch?v=FV-vzjVeao0) — 영어, 유튜브, 초중급
- [Alibaba Cloud Introduces Personal Token Plan with Qwen3.8-Max — Phemex News](https://phemex.com/news/article/alibaba-cloud-launches-personal-token-plan-with-qwen38max-preview-93744) — 영어, 뉴스, 초중급

## 자가 점검 질문

1. 벤치마크·모델 카드 없이 발표된 성능 주장을 뉴스에서 접했을 때, 이를 실무 도입 판단에 반영하기 전에 무엇을 먼저 확인해야 하는가?
2. 희소 전문가 혼합(MoE) 구조가 매개변수 총량과 실제 추론 비용의 관계를 어떻게 바꾸는가?
3. 회계법인이 사내 AI 도구용 모델을 검토할 때, 이번 사례처럼 검증되지 않은 신모델을 배제해야 할 기준은 무엇이라고 생각하는가?
