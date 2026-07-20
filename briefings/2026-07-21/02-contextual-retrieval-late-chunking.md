# 오늘의 AI 개념: Contextual Retrieval과 Late Chunking(Contextual Retrieval & Late Chunking)

> 작성일: 2026-07-21 · 분류: ai-concept

## 한 줄 정의

Contextual Retrieval과 Late Chunking은 문서를 청크로 쪼갤 때 사라지는 문맥 정보를 되살려 검색 정밀도를 높이는 두 가지 RAG 청킹 고도화 기법이다.

## 쉬운 설명

기존 RAG는 문서를 일정 길이(예: 500토큰)로 잘라 각 조각을 독립적으로 임베딩한다. 이 방식은 구현이 쉽지만, 잘린 조각만 보면 "이 회사"나 "해당 분기" 같은 표현이 무엇을 가리키는지 알 수 없는 경우가 흔하다. 문서 전체를 봐야 알 수 있는 맥락이 청크 경계에서 끊기기 때문이다.

Contextual Retrieval은 이 문제를 사후 보완 방식으로 푼다. 청크를 만든 다음, LLM에게 전체 문서와 해당 청크를 함께 보여주고 "이 청크가 전체 문서에서 어떤 위치인지" 설명하는 짧은 문장을 생성시켜 청크 앞에 붙인다. 비유하자면 책의 한 페이지를 복사해서 나눠줄 때, 페이지 위쪽 여백에 "이 페이지는 3장 재무제표 주석 중 재고자산 평가 부분입니다"라는 메모를 손으로 적어주는 것과 같다.

Late Chunking은 반대로 사전 보완 방식이다. 청크를 나누기 전에 장문맥 임베딩 모델이 문서 전체를 먼저 통째로 인코딩해, 모든 토큰이 앞뒤 문맥을 반영한 벡터를 갖게 만든다. 그런 다음에야 청크 경계를 적용해 각 구간의 토큰 벡터를 평균 내 청크 임베딩을 만든다. 두 기법 모두 목표는 같지만, Contextual Retrieval은 LLM이 생성한 텍스트를 추가하는 방식이고 Late Chunking은 임베딩 계산 순서 자체를 바꾸는 방식이라는 점에서 접근이 다르다.

## 동작 원리

**Contextual Retrieval 단계**

1. 문서를 기존 방식대로 고정 길이 청크로 분할한다.
2. 각 청크와 문서 전체를 LLM(Anthropic은 Claude, 프롬프트 캐싱 활용)에 함께 입력해, 50~100토큰 분량의 문맥 설명을 생성한다.
3. 이 설명을 청크 앞에 붙여 임베딩하고, 동시에 BM25(키워드 검색) 색인에도 반영한다(Contextual BM25).
4. 검색 시 벡터 검색과 BM25 결과를 결합(rank fusion)하고, 상위 후보를 리랭커에 다시 통과시켜 최종 순위를 매긴다.

**Late Chunking 단계**

1. jina-embeddings-v2/v3처럼 8192토큰 이상을 처리하는 장문맥 임베딩 모델에 문서 전체(또는 가능한 최대 길이)를 입력한다.
2. 트랜스포머가 각 토큰에 대해 문서 전체 문맥을 반영한 벡터를 출력한다.
3. 이 토큰 벡터 시퀀스에 청크 경계를 나중에 적용하고, 경계 안의 토큰 벡터들을 평균 풀링해 청크별 임베딩을 만든다.
4. 별도의 LLM 호출이나 재색인 없이, 임베딩 모델 한 번의 순전파로 문맥이 반영된 청크 벡터 전체를 얻는다.

## 구체 예시·사례

재무제표 주석 중 "재고자산" 항목을 예로 들 수 있다. 원문은 "당사는 선입선출법을 적용하며, 상기 표의 순실현가능가치는..."처럼 앞 문단의 표(재고자산 구성 내역)를 가리키는 대명사와 생략된 주어로 이어져 있고, 이 문단만 따로 청크로 잘리면 "상기 표"가 무엇인지, "당사"가 어느 회사인지 임베딩만으로는 알기 어렵다.

Contextual Retrieval을 적용하면 이 청크 앞에 "이 내용은 A사 2025사업연도 감사보고서 주석 7번 재고자산 중 순실현가능가치 평가 방법을 설명하는 문단이며, 바로 앞 표는 제품·원재료별 장부금액 내역이다"라는 문장이 LLM에 의해 생성되어 삽입된 뒤 임베딩된다. Late Chunking을 적용하면 감사보고서 전체를 장문맥 모델에 먼저 입력해, "상기 표"라는 표현의 벡터 자체가 이미 앞 문단의 표 내용을 반영한 상태로 청크 임베딩이 만들어진다. 두 경우 모두 "재고자산 평가방법이 무엇인가"라는 질의에 대해 이 청크가 상위로 검색될 가능성이 기존 고정청킹보다 높아진다.

## 비슷한 것과 비교

| 구분 | 기존 고정 청킹 | Contextual Retrieval | Late Chunking |
|------|------|------|------|
| 문맥 보존 시점 | 보존하지 않음(청크 독립 처리) | 청크 분할 후, LLM이 문맥 설명을 추가 | 청크 분할 전, 문서 전체를 먼저 인코딩 |
| 추가 비용 | 없음 | 청크마다 LLM 호출 필요(프롬프트 캐싱으로 완화) | 장문맥 임베딩 모델 1회 순전파, LLM 불필요 |
| 필요 조건 | 없음 | LLM API, BM25 색인, 리랭커 | 8192토큰 이상 장문맥 임베딩 모델 |
| 강점 | 구현이 가장 단순 | 키워드·의미 검색 모두 강화, 의미적 정합성 우수 | 계산 비용이 낮고 재색인이 간단 |
| 약점(보고된 트레이드오프) | 대명사·생략 주어에서 검색 실패 빈발 | 청크 수만큼 LLM 비용·지연 발생 | 관련성·완결성 면에서 다소 손해를 본다는 평가 존재 |

두 기법은 상호 배타적이지 않고 함께 적용할 수 있다는 점도 확인된다.

## 왜 지금 중요한가

두 기법을 실제로 비교 평가한 논문 "Reconstructing Context: Evaluating Advanced Chunking Strategies for Retrieval-Augmented Generation"(Carlo Merola, Jaspinder Singh)이 ECIR 2025 워크숍에서 발표됐고, Contextual Retrieval은 의미적 정합성이 더 우수하지만 계산 비용이 크고 Late Chunking은 효율적이지만 관련성·완결성에서 다소 손해를 본다는 트레이드오프를 확인했다.

이 주제를 확장한 후속 연구도 2026년 들어 계속 나오고 있다. 예를 들어 문서 간 주제 정렬 청킹을 다룬 논문(2026년 1월), 청킹 방식을 상황별로 자동 선택하는 적응형 청킹 연구(2026년 3월), 멀티모달 문서 검색에 문맥 청킹을 적용한 연구(2026년 7월)가 arXiv에 잇달아 게재됐다.

벡터DB 업계에서도 관련 논의가 이어지고 있는데, 2026년 기준 신규 GenAI 엔터프라이즈 애플리케이션의 30% 이상이 벡터DB를 활용한다는 전망과 함께, Weaviate·Elasticsearch 등 주요 벤더가 Late Chunking을 하이브리드 검색 기능의 일부로 다루고 있다.

- [Reconstructing Context: Evaluating Advanced Chunking Strategies for RAG](https://arxiv.org/abs/2504.19754)
- [Cross-Document Topic-Aligned Chunking for Retrieval-Augmented Generation](https://arxiv.org/pdf/2601.05265)
- [CMDR: Contextual Multimodal Document Retrieval](https://arxiv.org/pdf/2607.05927)
- [RAG Is Not Dead: Advanced Retrieval Patterns That Actually Work in 2026 - DEV Community](https://dev.to/young_gao/rag-is-not-dead-advanced-retrieval-patterns-that-actually-work-in-2026-2gbo)

## 회계법인 AI 직무 연결 포인트

감사조서·재무제표 주석·세무 신고서류는 표와 서술이 번갈아 나오고, 앞 문단의 수치나 계정과목을 대명사로 받는 문장이 많아 고정 길이 청킹으로는 검색 정밀도가 떨어지기 쉬운 문서군이다. Contextual Retrieval이나 Late Chunking을 적용하면 "재고자산 평가방법", "특수관계자 거래 내역" 같은 질의에 대해 표 경계를 넘나드는 문맥까지 반영된 청크가 검색되어, 감사인이 관련 근거를 찾는 시간을 줄일 수 있다.

특히 다년도 감사조서를 누적해 사내 지식베이스로 구축하는 경우, 문서량이 많아질수록 청크 단위 검색 실패가 감사 품질에 직접 영향을 준다. 이런 환경에서는 청킹 방식 자체가 RAG 시스템의 신뢰도를 좌우하는 핵심 설계 요소가 되며, 면접에서 "RAG를 어떻게 설계하겠는가"라는 질문에 청킹 전략을 구체적으로 언급하면 실무 이해도를 보여줄 수 있다.

다만 Contextual Retrieval은 청크마다 LLM 호출 비용이 들고, Late Chunking은 특정 장문맥 임베딩 모델에 의존한다는 제약이 있으므로, 문서 특성과 예산에 맞춰 두 기법 중 하나 또는 혼합 방식을 선택하는 판단력이 요구된다.

## 핵심 용어·논쟁

- **Contextual Embeddings** — 청크 앞에 LLM이 생성한 문맥 설명을 붙여 임베딩하는 기법으로, Contextual Retrieval의 절반을 구성한다.
- **Contextual BM25** — 같은 문맥 설명을 BM25 키워드 색인에도 반영해 희소 검색 성능까지 높이는 기법.
- **평균 풀링(Mean Pooling)** — Late Chunking에서 토큰 벡터들을 청크 경계 안에서 평균 내 하나의 청크 벡터로 만드는 연산.
- **장문맥 임베딩 모델** — jina-embeddings-v2/v3처럼 수천 토큰 이상을 한 번에 처리할 수 있는 임베딩 모델로, Late Chunking의 전제 조건이다.
- **프롬프트 캐싱(Prompt Caching)** — 같은 문서를 여러 청크에 반복 입력할 때 문서 본문을 캐시해 Contextual Retrieval의 LLM 호출 비용을 낮추는 기법.

두 기법 중 어느 쪽이 우월한지는 아직 합의되지 않았다. 비교 연구에 따르면 Contextual Retrieval은 의미적 정합성에서, Late Chunking은 계산 효율성에서 각각 우위를 보여 문서 특성과 비용 제약에 따라 선택이 갈리는 트레이드오프 관계로 보는 것이 타당하다.

## 자료 깊이 읽기

### Introducing Contextual Retrieval — Anthropic 공식 엔지니어링 블로그 — 영어, 블로그, 중급
Anthropic이 2024년 하반기 공개한 기술 글로, RAG에서 청크가 문맥을 잃어 검색이 실패하는 문제를 Contextual Embeddings와 Contextual BM25 두 기법으로 해결한다고 소개한다. Contextual Embeddings만 적용하면 검색 실패율이 35% 줄고, Contextual BM25까지 결합하면 49%, 여기에 리랭킹까지 더하면 67% 줄어든다는 실험 수치를 제시한다. 청크마다 문서 전체를 반복 입력하는 비용 문제는 프롬프트 캐싱으로 낮출 수 있다고 설명하며, 리랭커가 상위 후보만 다시 채점해 최종 정확도를 높이는 구조도 함께 다룬다. 여러 검색 경로를 통해 위 수치와 기법 구성이 일관되게 확인됐다.

### Reconstructing Context: Evaluating Advanced Chunking Strategies for RAG — arXiv 논문 — 영어, 논문, 고급
Carlo Merola와 Jaspinder Singh이 2025년 4월 발표하고 ECIR 2025 워크숍(지식 강화 정보 검색 제2워크숍)에서 채택된 논문으로, Late Chunking과 Contextual Retrieval을 정면으로 비교 평가한다. 두 연구질문을 설정해 조기·후기 청킹 전략이 검색 정확도와 RAG 다운스트림 성능에 미치는 영향을 다양한 텍스트 분할기·임베딩 모델 조합으로 실험했다. 결론으로 Contextual Retrieval은 의미적 정합성을 더 잘 보존하지만 LLM 호출과 재랭킹 비용이 크고, Late Chunking은 임베딩 모델의 자연스러운 능력을 활용해 계산 효율은 높지만 관련성과 완결성 면에서 다소 손해를 본다는 트레이드오프를 제시한다. 원문 전체 수치표는 이번 조사에서 직접 열람하지 못해 결론 요지만 반영했다.

### Late Chunking vs Contextual Retrieval: The Math Behind RAG's Context Problem — Michael Ryaboy, KX Systems(Medium) — 영어, 블로그, 중급
청크로 문서를 쪼갤 때 문맥이 끊겨 관련성·완결성이 떨어지는 문제를 수학적 관점에서 짚고, 이를 해결하는 두 접근으로 Late Chunking과 Contextual Retrieval을 나란히 설명하는 글이다. Contextual Retrieval은 의미적 정합성 보존에서, Late Chunking은 계산 효율성에서 각각 강점을 갖는다는 트레이드오프를 핵심 메시지로 제시한다. 두 기법이 문맥 보존이라는 같은 목표를 서로 다른 시점(청크 이후 vs 청크 이전)에서 달성한다는 구조적 차이를 강조한다. 본문 전체 수식 전개까지는 이번 조사에서 직접 확인하지 못했다.

**그 외 참고**
- [Introducing Contextual Retrieval — Anthropic 공식 엔지니어링 블로그](https://www.anthropic.com/engineering/contextual-retrieval) — 영어, 공식 블로그, 중급
- [Late Chunking vs Contextual Retrieval: The Math Behind RAG's Context Problem — Medium(KX Systems)](https://medium.com/kx-systems/late-chunking-vs-contextual-retrieval-the-math-behind-rags-context-problem-d5a26b9bbd38) — 영어, 블로그, 중급
- [Late Chunking in Long-Context Embedding Models — Jina AI (한국어)](https://jina.ai/ko/news/late-chunking-in-long-context-embedding-models/) — 한국어, 블로그, 중급
- [What Late Chunking Really Is & What It's Not: Part II — Jina AI (한국어)](https://jina.ai/ko/news/what-late-chunking-really-is-and-what-its-not-part-ii/) — 한국어, 블로그, 중상급
- [Late Chunking: Contextual Chunk Embeddings Using Long-Context Embedding Models (arXiv:2409.04701)](https://arxiv.org/abs/2409.04701) — 영어, 논문, 고급
- [Introducing Contextual Retrieval — velog(@chris40461)](https://velog.io/@chris40461/Introducing-Contextual-Retrieval) — 한국어, 블로그, 중급
- [[AI] Anthropic의 Contextual Retrieval 요약 & 정리 — Steemit](https://steemit.com/kr-dev/@anpigon/ai-anthropic-contextual-retrieval-and) — 한국어, 블로그, 중급
- [Amazon Bedrock으로 구현하는 Contextual Retrieval — AWS 한국 기술 블로그](https://aws.amazon.com/ko/blogs/tech/amazon-bedrock-contextual-retrieval) — 한국어, 블로그, 중급
- [Stop Losing Context! How Late Chunking Can Enhance Your Retrieval Systems - YouTube](https://www.youtube.com/watch?v=Hj7PuK1bMZU) — 영어, 유튜브, 중급
- [Understanding late chunking in RAG systems (for beginners!) - YouTube](https://www.youtube.com/watch?v=1VaZWDxxWiw) — 영어, 유튜브, 초급

## 자가 점검 질문

1. Contextual Retrieval과 Late Chunking이 각각 "문맥 보존"이라는 같은 목표를 어느 시점에, 어떤 방식으로 달성하는가?
2. 감사조서나 재무제표 주석처럼 표와 서술이 섞인 문서에 두 기법 중 하나를 도입한다면, 어떤 기준으로 선택하겠는가?
3. Contextual Retrieval의 LLM 호출 비용, Late Chunking의 장문맥 임베딩 모델 의존성은 각각 어떤 상황에서 실무 도입의 걸림돌이 될 수 있는가?
