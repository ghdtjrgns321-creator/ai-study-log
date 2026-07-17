# 오늘의 AI 개념: 에이전틱 컨텍스트 엔지니어링(Agentic Context Engineering, ACE)

> 작성일: 2026-07-18 · 분류: ai-concept

## 한 줄 정의

AI에게 한 번 정해서 주는 지침서 대신, AI가 일을 해본 결과를 스스로 되짚어 지침서 내용을 조금씩 추가·수정해 나가게 만드는 기법이다.

## 쉬운 설명

에이전틱 컨텍스트 엔지니어링(ACE)은 AI 에이전트가 참고하는 컨텍스트를 한 번 작성하고 끝나는 고정 문서가 아니라, 실행할수록 점점 두꺼워지고 정교해지는 "플레이북(playbook)"으로 다루는 기법이다. Generator, Reflector, Curator라는 세 개의 역할이 협력해 이 플레이북을 지속적으로 갱신한다. 스탠퍼드대학교, SambaNova Systems, UC버클리 공동 연구진이 2025년 10월 공개한 논문 "Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models"(arXiv:2510.04618)에서 제안했으며, 2026년 ICLR(International Conference on Learning Representations) 포스터 논문으로 채택됐다.

비유하자면 요리사가 쓰는 레시피 수첩에 가깝다. 처음에는 기본 레시피만 적혀 있지만, 요리를 반복할 때마다 "이 재료는 이 온도에서 태우기 쉬움", "이 순서로 하면 시간이 단축됨" 같은 메모를 여백에 계속 덧붙인다. 다만 매번 수첩 전체를 새로 옮겨 적지는 않고, 필요한 줄만 추가하거나 고친다. 이렇게 하면 예전에 배운 요령이 지워지지 않고 그대로 쌓인다.

기존에 다룬 컨텍스트 엔지니어링(2026-07-05 브리핑)은 배포 시점에 사람이 문서·기록·도구 연결을 설계해 넣어 주는 정적인 시스템 설계 작업이었다. ACE는 그 컨텍스트를 배포 이후에도 실행 결과를 재료 삼아 자동으로 계속 고쳐 나가는 절차를 추가한다는 점이 다르다. 즉 컨텍스트 엔지니어링이 "무엇을 넣어 줄지"를 다룬다면, ACE는 "넣어 준 것을 어떻게 계속 더 낫게 만들지"를 다룬다. 모델 가중치를 재학습시키지 않고 컨텍스트만 갱신한다는 점에서 파인튜닝의 대안으로도 소개된다.

ACE의 핵심 장치는 델타 업데이트(delta update)다. 매번 전체 플레이북을 요약해서 다시 쓰면 짧고 일반적인 문장만 남고 구체적인 도메인 지식이 사라지는 현상(브레비티 편향, brevity bias)과, 반복적인 재작성으로 세부 정보가 점점 유실되는 현상(컨텍스트 붕괴, context collapse)이 발생한다. ACE는 전체를 다시 쓰지 않고 작고 구체적인 항목(불릿) 단위로만 추가·수정해 이 문제를 피한다.

## 동작 원리

Generator → Reflector → Curator 순서로 한 사이클이 돈다.

1. Generator가 현재 플레이북을 참고해 실제 작업(질의응답, 도구 호출 등)을 수행하고 추론 과정을 기록한다.
2. Reflector가 그 결과와 성공/실패 피드백을 되짚어, 어떤 전략이 도움이 됐고 어떤 함정이 있었는지 구체적인 통찰을 뽑아낸다. 각 항목에는 "도움이 됨/해로움" 카운터가 붙는다.
3. Curator가 Reflector의 제안을 작고 구체적인 델타(추가·수정 항목)로 변환해 플레이북에 결정론적으로 병합한다. 이때 중복 제거와 정리를 함께 수행하는데, 이를 "성장과 정제(grow-and-refine)" 원칙이라 부른다.
4. 갱신된 플레이북을 가지고 Generator가 다음 작업을 수행하며 사이클이 반복된다.

레이블이 달린 정답 데이터 없이도, 작업 실행 자체에서 나오는 자연스러운 피드백(성공/실패, 오류 메시지 등)만으로 이 사이클이 돌아간다는 점이 특징이다.

## 구체 예시·사례

논문은 AppWorld라는 에이전트 벤치마크(여러 앱을 오가며 사용자 요청을 처리하는 에이전트 과제)로 ACE를 평가했다. ACE는 평균 정확도 약 59.5%를 기록해 기존 베이스라인 대비 약 10.6퍼센트포인트 향상됐으며, 이는 공개 리더보드에서 상위권이던 IBM의 GPT-4.1 기반 에이전트와 맞먹는 수준으로 보고됐다. 금융 분야에서는 FiNER(재무 개체명 인식)와 Formula(재무제표 수식 추론) 같은 데이터셋에서 평균 8.6% 성능 향상을 보였다. 이와 함께 적응(플레이북 갱신) 지연시간이 강력한 베이스라인 대비 크게 줄었다고 보고됐다. 다만 이 수치들은 논문 원문을 직접 확인하지 못해(아래 참고) 여러 2차 해설 자료의 교차 확인으로 정리한 값이며, 정확한 소수점 단위는 원문 확인이 필요하다.

## 비슷한 것과 비교

| 구분 | 정적 컨텍스트 엔지니어링 | ACE |
|---|---|---|
| 컨텍스트 성격 | 배포 전 설계자가 고정 구성한 문서·프롬프트 | 사용하면서 계속 커지는 진화형 플레이북 |
| 갱신 주체 | 사람이 수동으로 개정 | Reflector가 제안하고 Curator가 자동 병합 |
| 갱신 방식 | 필요할 때 전체 재작성 | 작은 델타(불릿) 단위 추가·수정 |
| 갱신 트리거 | 요구사항 변경 시 비정기적 | 매 실행·피드백마다 지속적 |
| 대표 리스크 | 시간이 지나면 컨텍스트가 낡음 | 관리 없이는 플레이북이 무한히 커질 수 있음(정제 필요) |

선택 기준: 컨텍스트가 자주 반복 실행되고 실패 패턴이 누적되는 장기 운영 에이전트라면 ACE 방식이 유리하고, 일회성이거나 실행 빈도가 낮은 작업이면 정적 컨텍스트 엔지니어링으로 충분하다.

## 왜 지금 중요한가

ACE 논문은 2026년 ICLR 포스터 논문으로 채택됐으며, 이후 여러 해설 블로그와 유튜브 영상이 이어지면서 "컨텍스트 엔지니어링의 다음 단계"로 소개되고 있다.

- [Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models (arXiv:2510.04618)](https://arxiv.org/abs/2510.04618)
- [Agentic Context Engineering | OpenReview (ICLR 2026)](https://openreview.net/forum?id=eC4ygDs02R)
- [Your Agents Just Got a Memory Upgrade: ACE Open-Sourced on GitHub](https://sambanova.ai/blog/ace-open-sourced-on-github)
- [GitHub - ace-agent/ace](https://github.com/ace-agent/ace)

## 회계법인 AI 직무 연결 포인트

논문이 금융(finance) 벤치마크에서 8.6% 성능 향상을 보고했다는 점은 회계·감사 실무와 맞닿아 있다. FiNER류 재무 개체명 인식, Formula류 재무제표 수식 추론은 감사 과정에서 계정과목 분류나 재무제표 각주의 수치 검증 작업과 성격이 비슷하다. 정답 레이블 없이 실행 피드백만으로 학습이 가능하다는 점은, 감사조서마다 정답지가 따로 없는 실무 환경에서도 AI가 반복 수행을 통해 스스로 판단 기준을 다듬어 갈 가능성을 시사한다.

델타 업데이트 방식은 감사 품질 관리 관점에서도 유리하다. 매번 전체 지침을 새로 쓰는 대신 작은 항목 단위로 변경 이력이 남기 때문에, "언제 어떤 판단 기준이 왜 추가됐는지"를 추적하기 쉽다. 이는 감사 절차의 변경 사유를 문서화해야 하는 요구와 잘 맞는다.

다만 델타가 자동으로 누적되는 구조이므로, 회계법인이 실제 도입 시에는 플레이북에 잘못된 판단이 섞여 들어가지 않도록 Curator 단계에서 사람의 검토(휴먼 인 더 루프)를 추가하는 절차가 필요하다. 자동으로 축적된 컨텍스트가 감사 판단의 근거가 될 경우, 그 축적 과정 자체가 통제 대상이 되어야 한다.

## 핵심 용어·논쟁

- 플레이북(playbook) — 정적 프롬프트 대신 전략과 교훈을 누적하는 살아있는 컨텍스트 저장소
- 컨텍스트 붕괴(context collapse) — 컨텍스트를 반복적으로 재작성하면서 세부 정보가 유실되는 현상
- 브레비티 편향(brevity bias) — 요약을 반복하면 구체적 지식이 사라지고 일반적인 문장만 남는 경향
- 델타 업데이트(delta update) — 전체 재작성 대신 작고 구체적인 항목만 추가·수정하는 갱신 방식
- 성장과 정제(grow-and-refine) — 플레이북을 필요할 때만 정리(중복 제거·가지치기)하면서 성장시키는 원칙

진행 중인 쟁점으로는, 플레이북이 오래 운영될수록 델타가 계속 쌓이면서 컨텍스트 길이와 관리 비용이 늘어날 수 있다는 점, 그리고 Reflector가 잘못된 통찰을 뽑아낼 경우 오류가 플레이북에 그대로 누적될 위험이 있다는 점이 지적된다.

## 자료 깊이 읽기

논문 원문(arXiv, openreview)과 다수의 2차 해설 사이트는 이번 조사에서 접속이 차단되거나(사내 네트워크 정책상 arxiv.org 접속 거부) 사이트 측 봇 차단으로 본문을 가져오지 못했다. 실제로 본문을 확인한 자료는 아래 GitHub 저장소뿐이며, 나머지는 검색 스니펫으로 교차 확인한 내용을 위 본문에 반영했다.

### GitHub - ace-agent/ace — 영어, 텍스트(저장소 README), 중급
ACE 공식 구현 저장소로, README에서 세 역할 구조를 명확히 설명한다. Generator는 새 질의에 대해 추론 과정을 생성하며 효과적 전략과 반복되는 함정을 식별한다. Reflector는 평가와 통찰 추출을 분리해 맥락 품질을 개선하고, 각 항목을 도움됨/해로움 카운터로 태깅한다. Curator는 학습 내용을 구조화된 델타 업데이트로 변환하고, 중복 제거와 정리로 컨텍스트 붕괴를 방지한다. README는 이 구조로 에이전트 과제에서 평균 +10.6%, 도메인 특화 벤치마크에서 +8.6% 성능 향상, 적응 지연시간 약 86.9% 감소를 달성했다고 명시한다.

### 나머지 자료 — (요약 불가, 자막/본문 확인 실패)
아래는 검색 결과에서 확인됐으나 본문 확인 실패로 요약을 제공하지 못한 자료다. 링크만 제공한다.

**그 외 참고**
- [Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models (arXiv 원문)](https://arxiv.org/abs/2510.04618) — 영어, 텍스트(논문), 고급
- [Agentic Context Engineering | OpenReview (ICLR 2026)](https://openreview.net/forum?id=eC4ygDs02R) — 영어, 텍스트(리뷰 페이지), 고급
- [ACE Explained by the Creators: How Agentic Context Engineering Is Changing AI Forever](https://www.youtube.com/watch?v=w8C2d__ArIA) — 영어, 유튜브, 중급
- [Agentic Context Engineering (ACE) | Qizheng Zhang | Random Samples](https://www.youtube.com/watch?v=A3RKCKemnSg) — 영어, 유튜브(저자 본인 설명), 중급
- [ACE: Agentic Context Engineering for Scalable, Self-Improving LLM Systems](https://www.youtube.com/watch?v=y_dRsD-qVUs) — 영어, 유튜브, 입문
- [모델의 Agent 역량을 향상시키는 Agentic Context Engineering (velog)](https://velog.io/@mmodestaa/Agentic-Context-Engineering) — 한국어, 텍스트(블로그), 중급
- [컨텍스트 붕괴 해결! ACE 프레임워크로 AI 에이전트 성능 높이기 (ProB AI 연구소)](https://prob.co.kr/ace-framework-agentic-context-engineering/) — 한국어, 텍스트(블로그), 입문

## 자가 점검 질문

1. ACE에서 Generator, Reflector, Curator가 각각 맡는 역할을 한 문장씩으로 설명한다면 무엇인가?
2. 감사 업무에 ACE 방식을 적용한다면, 어떤 실행 결과를 "피드백"으로 삼아 플레이북을 갱신할 수 있는가?
3. 델타가 자동으로 계속 누적되는 구조에서, 잘못된 판단 기준이 플레이북에 섞여 들어가는 것을 막으려면 어떤 통제 절차가 필요한가?
