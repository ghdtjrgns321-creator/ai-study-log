# 오늘의 AI 개념: 잉클링(Inkling)

> 작성일: 2026-07-21 · 분류: trend

## 한 줄 정의

잉클링(Inkling)은 전 OpenAI CTO 미라 무라티(Mira Murati)가 세운 Thinking Machines Lab이 2026년 7월 15일 공개한 9750억 파라미터급 오픈웨이트 MoE 멀티모달 모델로, 추론 시 약 410억 파라미터만 활성화하며 자사 파인튜닝 플랫폼 Tinker에서 곧바로 기업 맞춤화가 가능하다.

## 쉬운 설명

Thinking Machines Lab은 미라 무라티가 OpenAI를 떠난 뒤 세운 회사로, 설립 약 1년 5개월 만에 처음으로 대중에 공개하는 모델이 잉클링이다. 잉클링은 텍스트·이미지·오디오·비디오를 함께 학습한 45조 토큰 데이터로 훈련됐고, 가중치 전체가 허깅페이스(Hugging Face)에 공개돼 있어 누구나 내려받아 자체 데이터로 재학습할 수 있다.

잉클링의 MoE 구조는 대형 종합병원에 비유할 수 있다. 병원 전체에는 256명의 전문의(라우팅 전문가)와 늘 대기하는 2명의 당직의(공유 전문가)가 있지만, 환자 한 명(입력 토큰)이 오면 증상에 맞는 전문의 6명만 호출돼 진료에 참여한다. 병원 규모(9750억 파라미터)는 크지만 환자 한 명을 볼 때 실제로 움직이는 인력(410억 파라미터)은 그보다 훨씬 적은 것과 같은 구조다.

이 모델은 답변만 하는 것이 아니라 텍스트·이미지·오디오 입력을 함께 이해하고, 최대 100만 토큰 분량의 문맥을 한 번에 처리할 수 있다. Thinking Machines Lab은 잉클링을 "오늘날 가장 강력한 모델은 아니다"라고 스스로 인정하면서도, 벤치마크 1위 대신 기업이 직접 소유하고 개조할 수 있는 기반 모델이라는 점을 핵심 전략으로 내세운다.

기존 폐쇄형 프론티어 모델인 GPT·Claude·Gemini는 가중치가 공개되지 않고 API 호출로만 사용할 수 있어, 모델 내부를 들여다보거나 자사 서버에 직접 올려 운영할 수 없다. 반면 잉클링은 가중치 자체를 내려받아 온프레미스에 배포하거나 자체 데이터로 파인튜닝할 수 있다는 점에서, "성능은 벤더에 맡기고 쓰는 모델"과 "직접 소유하고 개조하는 모델"이라는 전략의 축이 갈린다.

## 동작 원리

잉클링의 동작은 다음 순서로 이해할 수 있다.

1. MoE 레이어마다 256개의 라우팅 전문가와 2개의 공유 전문가가 존재하고, 시그모이드(sigmoid) 기반 라우터가 토큰마다 라우팅 전문가 6개를 선택해 활성화한다. 활성화 방식은 추가 손실 함수 없이 부하를 균형 잡는(auxiliary-loss-free) 방식이다.
2. 텍스트·이미지·오디오·비디오가 섞인 45조 토큰으로 사전학습됐고, 최대 100만 토큰의 컨텍스트 윈도우를 지원한다.
3. 추론 속도를 높이기 위해 스펙큘레이티브 MTP(multi-token prediction) 레이어를 두고, 저정밀도 NVFP4와 표준 BF16 두 버전으로 배포된다.
4. 가중치는 허깅페이스에 공개되며, transformers·SGLang·llama.cpp 등 주요 추론 프레임워크에서 공개 당일부터 바로 사용할 수 있다.
5. 기업은 공개된 가중치를 그대로 쓰거나, Thinking Machines Lab의 파인튜닝 플랫폼 Tinker에 올려 자사 데이터로 학습을 이어갈 수 있다. Tinker에는 잉클링과 바로 대화해볼 수 있는 "Inkling Playground"도 함께 제공된다.

## 구체 예시·사례

회계법인이 이 모델을 도입하는 상황을 가정하면 다음과 같은 흐름이 된다. 먼저 감사·세무 상담 기록, 내부 감사 조서 같은 기밀 데이터를 외부로 내보내지 않고, 사내 서버나 사설 클라우드에 잉클링 가중치를 내려받아 배치한다.

이후 Tinker 플랫폼을 통해 회계법인 고유의 세무 질의응답 로그나 감사 절차 문서로 모델을 추가 학습시켜, 일반 대화형 AI보다 해당 법인의 용어와 판단 기준에 맞는 사내 전용 보조 모델을 만든다. 이 과정에서 학습 데이터가 외부 벤더의 서버로 전송되지 않기 때문에, 고객 정보 유출이나 벤더 측 모델 정책 변경에 따른 리스크를 줄일 수 있다.

## 비슷한 것과 비교

| 항목 | 잉클링(Inkling) | 라마(Llama) 계열 | GPT·Claude·Gemini |
|---|---|---|---|
| 가중치 공개 여부 | 공개(오픈웨이트) | 공개(오픈웨이트) | 비공개 |
| 총 파라미터/활성 파라미터 | 975B / 41B(MoE) | 모델별 상이, 대개 dense 구조 | 비공개 |
| 멀티모달 입력 | 텍스트·이미지·오디오 네이티브 | 버전별로 상이 | 네이티브 멀티모달 |
| 파인튜닝 방식 | 자사 플랫폼 Tinker에서 즉시 지원 | 별도 인프라·프레임워크 구축 필요 | API 기반 제한적 파인튜닝 |
| 전략 초점 | 벤치마크 1위보다 기업 커스터마이징 | 오픈 생태계 확산 | 최고 성능과 통합 서비스 |

## 왜 지금 중요한가

잉클링은 2026년 7월 15일 발표됐고, 이는 이번 브리핑 작성일(2026-07-21) 기준 일주일이 채 지나지 않은 최신 뉴스다. Thinking Machines Lab은 발표와 동시에 가중치를 허깅페이스에 공개하고 Tinker에서 바로 파인튜닝을 지원한다고 밝혀, "발표"에 그치지 않고 즉시 사용 가능한 상태로 시장에 내놓았다.

- [Inkling: Our open-weights model - Thinking Machines Lab](https://thinkingmachines.ai/news/introducing-inkling/)
- [Thinking Machines amps up its bet against one-size-fits-all AI with its first open model, Inkling - TechCrunch](https://techcrunch.com/2026/07/15/thinking-machines-amps-up-its-bet-against-one-size-fits-all-ai-with-its-first-open-model-inkling/)
- [씽킹머신스 첫 모델 잉클링, 9750억 파라미터 중 410억만 작동 - 위키트리](https://www.wikitree.co.kr/articles/1146714)
- [Thinking Machines Lab offers enterprises a US alternative in open-weight AI - Computerworld](https://www.computerworld.com/article/4197755/thinking-machines-lab-offers-enterprises-a-us-alternative-in-open-weight-ai.html)

## 회계법인 AI 직무 연결 포인트

회계법인은 감사 조서, 고객 재무 정보, 세무 상담 내역처럼 외부 유출이 금지된 기밀 데이터를 다량으로 다룬다. 폐쇄형 API 모델을 쓰면 이런 데이터를 벤더 서버로 전송해야 하는 경우가 많아, 계약상 안전장치가 있어도 데이터 주권과 컴플라이언스 우려가 남는다.

잉클링처럼 가중치를 직접 소유하고 사내에서 파인튜닝할 수 있는 오픈웨이트 모델은, 데이터를 외부로 내보내지 않고도 업무에 특화된 모델을 만들 수 있다는 대안을 제공한다. 이는 특정 벤더의 가격 정책이나 모델 단종에 종속되지 않는 벤더 종속 회피 전략과도 직결된다.

동시에 오픈웨이트 모델을 직접 운영하려면 GPU 인프라, 파인튜닝 파이프라인, 모델 검증 체계를 회계법인이 스스로 갖춰야 한다는 부담도 따른다. 면접에서는 "오픈웨이트 모델 도입이 데이터 보안과 벤더 종속 문제를 해결해 주지만, 그만큼 내부 운영·검증 역량이 새로 요구된다"는 양면을 함께 설명하는 것이 중요하다.

## 핵심 용어·논쟁

- MoE(Mixture of Experts, 전문가 혼합) — 여러 전문가 서브네트워크 중 입력마다 일부만 선택적으로 활성화하는 구조.
- 오픈웨이트(Open-weight) — 모델 가중치 파일 자체를 공개해 누구나 내려받아 실행·재학습할 수 있게 하는 배포 방식.
- 활성 파라미터(Active Parameters) — 추론 한 번에 실제로 연산에 관여하는 파라미터 수로, 총 파라미터보다 훨씬 적다.
- 파인튜닝(Fine-tuning) — 사전학습된 모델을 특정 조직·업무의 데이터로 추가 학습시켜 맞춤화하는 과정.
- 컨텍스트 윈도우(Context Window) — 모델이 한 번에 참고할 수 있는 입력 토큰의 최대 길이.

논쟁으로는 9750억 파라미터급 대형 모델의 가중치를 통째로 공개하는 데 따른 안전성 우려가 있다. 오픈웨이트 모델은 폐쇄형 API 모델과 달리 배포 이후 사용처를 통제할 수 없어, 안전장치를 우회한 악용 가능성이 폐쇄형 모델보다 크다는 지적이 꾸준히 제기된다.

## 자료 깊이 읽기

### Inkling: Our open-weights model — 영어, 공식 발표 블로그, 중급
Thinking Machines Lab이 직접 공개한 발표문으로, 975억이 아닌 9750억 총 파라미터와 410억 활성 파라미터, 256개 라우팅 전문가·2개 공유 전문가·토큰당 6개 전문가 활성화 구조를 명시한다. 45조 토큰의 텍스트·이미지·오디오·비디오 학습 데이터, 최대 100만 토큰 컨텍스트, NVFP4·BF16 두 정밀도 버전, transformers·SGLang·llama.cpp day-0 지원, Tinker 연동과 Inkling Playground까지 이 문서 하나로 모델의 기술적 전모를 확인할 수 있다.

### 씽킹머신스 첫 모델 잉클링, 9750억 파라미터 중 410억만 작동 — 한국어, 뉴스 기사, 초급
위키트리가 국내 독자 대상으로 정리한 기사로, 오픈웨이트의 의미와 9750억/410억이라는 핵심 수치를 한국어로 쉽게 풀어 설명한다. 기업이 자체 데이터를 입력해 가중치를 조정하는 커스터마이징 개념을 초심자 눈높이에서 설명해, 처음 접하는 사람이 읽기에 적합하다.

### Thinking Machines amps up its bet against one-size-fits-all AI with its first open model, Inkling — 영어, 전문매체 기사, 중급
TechCrunch가 발표 당일 보도한 기사로, 잉클링을 "하나의 모델이 모든 기업에 맞는다"는 기존 프론티어 랩 전략에 대한 반박으로 위치시킨다. 벤치마크 최고 성능이 아니라 기업이 소유·개조할 수 있는 기반 모델이라는 회사의 전략적 메시지와, Tinker를 통한 즉시 파인튜닝 지원이 이 전략의 실행 수단이라는 점을 함께 짚는다.

**그 외 참고**
- [Welcome Inkling by Thinking Machines - Hugging Face Blog](https://huggingface.co/blog/thinkingmachines-inkling) — 영어, 공식 블로그, 중급
- [Thinking Machines' first model bets big on customization - Axios](https://www.axios.com/2026/07/15/mira-murati-thinking-machines-open-weight-model-inkling) — 영어, 전문매체 기사, 중급
- [Murati's Thinking Machines Releases First AI Model for Broad Use - Bloomberg](https://www.bloomberg.com/news/articles/2026-07-15/murati-s-thinking-machines-releases-first-ai-model-for-broad-use) — 영어, 전문매체 기사, 중급
- [Thinking Machine's Inkling explained in 8min.. - YouTube](https://www.youtube.com/watch?v=zmfofxWG_3I) — 영어, 영상, 초급
- [Inkling 975B: Thinking Machines' Massive New Open Weight AI - YouTube](https://www.youtube.com/watch?v=zLeYsNIz2SM) — 영어, 영상, 초급
- ["오픈AI·앤트로픽 독점 깨야"… 오픈AI 출신 무라티, '가성비 AI'로 승부수 - 한국일보](https://www.hankookilbo.com/news/article/A2026071609300005844) — 한국어, 뉴스 기사, 초급

## 자가 점검 질문

1. 잉클링의 총 파라미터 수와 활성 파라미터 수가 다른 이유를 MoE 구조로 설명할 수 있는가?
2. 회계법인이 잉클링 같은 오픈웨이트 모델을 도입해 사내 전용 AI를 구축하려면, 기술적으로 어떤 준비(인프라·데이터·검증 체계)가 필요한가?
3. 가중치를 통째로 공개하는 오픈웨이트 전략이 갖는 안전성·오용 리스크는 폐쇄형 API 모델과 비교했을 때 어떤 지점에서 더 커지는가?
