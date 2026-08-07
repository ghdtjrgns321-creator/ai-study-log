# 영상 상세 요약: Terminal-Bench: Pushing Claude Code, OpenAI Codex, Factory Droid, et al to the limits

- 원본 링크: https://www.youtube.com/watch?v=rTuU8FUlIvY
- 채널/형식: Latent Space 팟캐스트(진행자 Alessio·Swyx) — 터미널벤치 공동 개발자 Alex Shaw, Mike Merrill 게스트 출연
- 연결된 브리핑: `briefings/2026-08-08/01-terminal-bench-2-1.md`
- 출처 확인: yt-dlp로 영어 자막(auto-sub)을 직접 내려받아 전체 내용을 확인했다.

## 다루는 하위 주제·흐름

```
[1] 게스트 소개 및 배경
     ├─ Alex Shaw: 구글 퇴사 → K프라이즈(SWE-bench $100만 상금 대회) 참여 → Laude Institute 합류
     └─ Mike Merrill: 스탠퍼드 Ludwig Schmidt 연구실 포닥, 코드로 과학·개인 데이터 다루는 연구 이력
        │
[2] 터미널벤치 탄생 배경
     ├─ SWE-bench의 "깃허브 저장소/PR 특화" 틀을 넘어서려는 시도
     ├─ Andy Konwinski(데이터브릭스·Perplexity 공동창업자)의 "터미널 = 만능 도구" 아이디어
     └─ 클로드4 모델카드에 앤트로픽이 비공지로 인용하며 급부상
        │
[3] 태스크 설계 철학
     ├─ 태스크 = 지시문 + 컨테이너 환경 + 테스트 스크립트
     ├─ 코딩이 다수지만 DNA 서열 조립 등 비(非)코딩 태스크도 포함
     └─ "어렵되 부당하게 어렵지 않고, 실제로 돈을 받고 하는 일이며, 검증 가능한" 문제가 좋은 태스크
        │
[4] 대표 태스크 사례: Train Fast Text
     ├─ 스탠퍼드 DCLM 논문 실무에서 나온 실제 엔지니어링 난제
     ├─ 크기 제한 안에서 목표 정확도 달성 — 제약 하 모델 학습
     └─ 실행 시간 약 10분, 최근 모델들은 안정적으로 통과하기 시작
        │
[5] 벤치마크 확장 전략
     ├─ 오픈소스 공개 + 기여자 인센티브 시스템으로 태스크 다양성 확보
     ├─ 다른 유명 벤치마크(SWE-bench Verified 등)를 터미널벤치 형식으로 이식하는 "어댑터" 개발 중(약 30개 진행)
     └─ 장기 비전: 기업이 사내 전용 평가셋을 만들거나 RL 환경으로 활용
        │
[6] 모델 vs 하네스 분리 평가
     ├─ 자체 개발한 최소 구성 에이전트 "Terminus" — 배시 명령만 허용, 특수 도구 없음
     ├─ 이유: 클로드 코드·코덱스 CLI 등 상용 에이전트는 모델-하네스가 함께 튜닝돼 순수 모델 실력과 구분 안 됨
     └─ 같은 모델이라도 에이전트 프레임워크에 따라 최대 15%p 점수 차이 관찰 (다만 모델 간 차이가 더 크다는 게 공동 결론)
        │
[7] 향후 평가지표 논의
     ├─ 현재는 "정확도" 1차원 지표뿐
     ├─ 제안: 비용·시간(2차원), 나아가 "실제로 돈을 얼마나 벌어줬는가"까지 반영한 경제적 가치 평가
     └─ 타임아웃을 늘릴수록 정확도가 어디까지 오르는지 실험 예정(무한정 시간을 주는 게 정답은 아니라는 우려도 논의)
        │
[8] 로드맵
     ├─ 인터랙티브 벤치마킹 + RL 포스트트레이닝 프레임워크로 확장
     ├─ 클라우드 호스팅 버전 준비 중
     └─ 커뮤니티(디스코드) 기여자 모집
```

## 실무 팁·인용 원문 보존

- "a terminal bench task literally is an instruction, a container environment, and then a test script" — 태스크의 최소 구성요소 정의.
- Terminus 설계 이유: "if you're really interested in studying the ability of the model, it becomes very important to separate it from its harness."
- 평가 철학: "a good terminal bench task is one that's hard, but not adversarially hard, just hard on its own merits and valuable... and verifiable."
- 향후 지표 제안: "there's no more one-dimensional charts... second dimension should be something like a cost, something like a latency."
- SWE-bench Verified의 한계 지적: "if you go look at Sweetbench verified I think like 60~70% of the tasks in there are from Django" — 특정 프레임워크 편중 문제.

## 불확실 표시

- "최대 15%p 차이" 등 하네스별 점수 차이 수치는 발화자의 구두 추정치로, 정확한 그래프·수치표는 영상 내 화면 공유로만 제시돼 자막만으로는 확인 불가. 직접 재확인 필요.
- Terminus의 정확한 버전(Terminus 2 등) 및 e2b 샌드박스 연동 세부사항은 이 팟캐스트 녹화 시점 이후 갱신되었을 수 있어, 최신 사양은 공식 GitHub 저장소로 교차 확인 필요.
