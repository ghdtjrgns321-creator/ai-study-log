# 오늘의 AI 개념: FLUX 3(Black Forest Labs) 멀티모달 프론티어 모델 공개

> 작성일: 2026-07-26 · 분류: trend

## 한 줄 정의

독일 스타트업 Black Forest Labs가 이미지·비디오·오디오·로봇 동작 예측을 하나의 모델로 함께 학습한 멀티모달 프론티어 모델 FLUX 3를 공개했다.

## 쉬운 설명

Black Forest Labs는 2026년 7월 23일 FLUX 3를 발표했다. 기존 FLUX 시리즈가 이미지 생성에 집중했다면, FLUX 3는 이미지·비디오·오디오를 하나의 통합 아키텍처로 동시에 학습한 첫 모델이며, 같은 아키텍처를 로봇의 다음 동작을 예측하는 데까지 확장했다.

비유하자면, 기존 이미지 생성 모델이 "그림만 그릴 줄 아는 화가"였다면, FLUX 3는 "그림도 그리고, 그 장면에 맞는 소리도 만들고, 로봇의 다음 동작까지 예측하는 다재다능한 감독"에 가깝다. 세 가지(이미지·비디오·오디오)를 따로 이어붙인 게 아니라, 처음부터 하나의 모델이 함께 배웠다는 점이 핵심이다.

기존에는 이미지 모델·비디오 모델·오디오 모델·로봇 제어 모델이 각각 따로 존재했다. FLUX 3는 이들을 "Self-Flow"라는 학습 방식으로 하나의 네트워크에 통합해, 모달리티(정보 형태) 간 상호 제약이 오히려 각 영역의 이해도를 높인다고 회사 측은 설명한다.

## 동작 원리

1. 이미지·비디오·오디오 데이터를 하나의 통합 아키텍처로 동시에 학습한다(Self-Flow 방식) — 각 모달리티가 서로를 보완하는 제약 조건으로 작동한다.
2. 텍스트-투-비디오, 이미지-투-비디오, 비디오-투-비디오 편집, 키프레임 기반 전환, 다국어 대사 생성, 개별 클립을 이어붙이는 에이전틱 체이닝 등 다양한 워크플로를 지원한다.
3. 같은 아키텍처를 로봇 조작 영역으로 확장해, 미믹 로보틱스(mimic robotics)와 협력한 파트너 시스템을 통해 "다음 동작 예측"을 수행한다.
4. 현재 FLUX 3 Video·이미지는 제한적 얼리 액세스로 제공되며, 오픈웨이트 버전(FLUX 3 Dev)은 추후 공개될 계획이다.

## 구체 예시·사례

아우디 공장에서는 FLUX 3 기반 시스템(FLUX-mimic)이 실험실이 아닌 실제 생산 라인에서 유연한 도어 실(seal)을 장착하는 작업에 쓰이고 있다. 이는 기존 자동화 로봇이 다루기 어려워하던 부드러운 재질의 조작(soft-body manipulation) 작업으로, 로봇이 다음 순간 부품이 어떻게 휘어지고 어디에 들어맞을지를 FLUX 3의 예측 능력을 빌려 처리하는 사례다.

## 비슷한 것과 비교

| 구분 | 기존 FLUX(이미지 전용) | Runway·Luma 등 비디오 전용 모델 | FLUX 3 |
|------|------|------|------|
| 학습 모달리티 | 이미지만 | 비디오(제한적 오디오) | 이미지·비디오·오디오·로봇 동작 통합 |
| 로봇 적용 | 없음 | 없음 | 미믹 로보틱스 협력으로 실적용 시작 |
| 공개 방식 | 오픈웨이트 일부 공개 | 대부분 폐쇄형 API | 얼리 액세스 → 추후 오픈웨이트 백본 예정 |

회사 자체 선호도 테스트(사전 공개 체크포인트 기준이라는 단서가 붙음)에서는 FLUX 3가 Runway Gen-4.5·Luma Ray 3.2 대비 선호도가 높았다고 밝혔으나, 이는 벤더 자체 발표이며 독립 검증은 아직 이뤄지지 않았다.

## 왜 지금 중요한가

Black Forest Labs는 2026년 7월 23일 공식 블로그와 GlobeNewswire 보도자료를 통해 FLUX 3를 발표했다. 이미지 생성 모델 하나가 오디오·비디오·로봇 제어까지 아우르는 통합 모델로 확장된 사례는, "생성형 AI 모델"과 "물리적 행동을 예측하는 모델(오늘 다룬 세계모델 계열)"의 경계가 점점 흐려지고 있음을 보여준다.

- [Black Forest Labs Unveils FLUX 3, A New Multimodal Frontier Model For Visual Intelligence — GlobeNewswire 공식 보도자료](https://www.globenewswire.com/news-release/2026/07/23/3332364/0/en/black-forest-labs-unveils-flux-3-a-new-multimodal-frontier-model-for-visual-intelligence.html)
- [FLUX 3 - Real World Models — Black Forest Labs 공식 블로그](https://bfl.ai/blog/flux-3)
- [Black Forest Labs launches FLUX 3 capable of generating images and 20-second video with audio — VentureBeat](https://venturebeat.com/technology/black-forest-labs-launches-flux-3-capable-of-generating-images-and-20-second-video-with-audio-but-in-limited-release-to-start)

## 회계법인 AI 직무 연결 포인트

FLUX 3 자체는 회계·감사 실무 도구는 아니지만, 이런 멀티모달 생성 모델의 확산은 회계법인의 부정 탐지·문서 진위 검증 업무와 직접 연결된다. 생성 AI가 이미지·비디오·오디오를 실사에 가깝게 동시에 만들어낼 수 있다는 것은, 위조 증빙서류·딥페이크 화상회의·조작된 음성 지시 같은 감사 리스크가 더 정교해진다는 뜻이기도 하다.

동시에 이런 모델이 산업 현장(로봇 조작 등)에 실제로 투입되면서 발생하는 새로운 자산·비용 항목(로봇 자동화 투자, AI 모델 라이선스 비용)은 회계 처리·자산 인식 기준에서 새로운 판단이 필요한 영역이기도 하다. 감사인은 이런 신종 기술 자산을 어떻게 자본화·상각할지에 대한 회계기준 적용 논의에 대비할 필요가 있다.

## 핵심 용어·논쟁

- **멀티모달(Multimodal)** — 텍스트·이미지·비디오·오디오 등 여러 형태의 데이터를 함께 다루는 AI 방식.
- **Self-Flow** — FLUX 3가 이미지·비디오·오디오를 하나의 네트워크로 동시에 학습하는 데 쓴 학습 방식.
- **오픈웨이트(Open-weight)** — 모델 가중치가 공개돼 누구나 내려받아 실행·검증할 수 있는 배포 방식.

벤더가 자체적으로 발표한 "경쟁 모델 대비 선호도" 수치는 사전 공개 체크포인트를 기준으로 한 내부 테스트 결과라는 단서가 붙어 있어, 실제 얼리 액세스 이후 공개될 모델의 성능과는 차이가 있을 수 있다는 점이 독립 검증 전의 한계로 남아 있다.

## 자료 깊이 읽기

### Black Forest Labs Unveils FLUX 3, A New Multimodal Frontier Model For Visual Intelligence — GlobeNewswire 공식 보도자료 — 영어, 보도자료, 초급
2026년 7월 23일 배포된 공식 보도자료다. FLUX 3가 이미지·비디오·오디오를 통합 아키텍처로 학습하고, 로봇 액션 예측까지 확장했다는 핵심 내용을 전한다. FLUX 3 Video는 20초 길이의 영상을 오디오와 함께 한 번에 생성하며, 현재 제한된 얼리 액세스로 제공되고 이미지 생성은 향후 몇 주 내 얼리 액세스가 시작된다고 밝힌다. 로봇 액션 예측은 미믹 로보틱스 등 파트너를 통해 우선 제공되며, 아우디 공장에서 이미 테스트가 진행 중이라고 설명한다.

### FLUX 3 - Real World Models — Black Forest Labs 공식 블로그 — 영어, 공식 기술 블로그, 중급
회사가 직접 게시한 기술 블로그로, FLUX 3가 이미지·비디오·오디오를 "Self-Flow" 방식으로 동시에 학습해 단일 모달리티가 아닌 통합된 세계 표현을 학습했다고 설명한다. 콘텐츠 제작용과 행동 예측용으로 나뉘는 오픈웨이트 버전(FLUX 3 Dev)을 추후 공개할 계획이라는 로드맵도 함께 제시한다.

**그 외 참고**
- [Black Forest Labs launches FLUX 3 capable of generating images and 20-second video with audio — VentureBeat](https://venturebeat.com/technology/black-forest-labs-launches-flux-3-capable-of-generating-images-and-20-second-video-with-audio-but-in-limited-release-to-start) — 영어, 뉴스 기사, 초급
- [FLUX 3 - Incredible AI Video Model - Demo Reel — YouTube](https://www.youtube.com/watch?v=LSP8s2Q2KfY) — 영어, 유튜브, 초급

유튜브 자료는 이번 환경에서 유튜브 접속 자체가 차단돼(yt-dlp 자막 다운로드 시도 시 429 오류) 자막을 직접 확인하지 못했다. 상세 요약 파일 없이 제목·링크만 남긴다(검색 결과에 실제로 등장한 URL).

## 자가 점검 질문

1. FLUX 3가 이미지·비디오·오디오·로봇 동작을 하나의 아키텍처로 통합 학습한 것이 왜 중요한 기술적 진전인가?
2. 멀티모달 생성 모델의 발전이 회계법인의 부정 탐지·증빙 검증 업무에 어떤 새로운 위험을 만드는가?
3. 벤더가 발표한 자체 성능 비교 수치를 검토할 때 어떤 점을 비판적으로 봐야 하는가?
