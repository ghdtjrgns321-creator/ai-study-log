- 원본 링크: https://www.youtube.com/watch?v=Psa8mLikdag
- 제목: `Managed Agents in the Gemini API`
- 채널: Google for Developers · 게시일 2026-06-03 · 재생시간 9:35
- 연결된 브리핑: `briefings/2026-07-31/02-managed-agents.md`
- 확인 방법: yt-dlp로 영어 자동 자막(auto-generated captions)을 실제로 내려받아 전문을 읽고 정리했다(`--write-auto-sub --sub-lang en`).

## 영상 개요

Google for Developers 공식 채널이 올린 9분 35초짜리 인터뷰 겸 데모 영상이다. 진행자와 Gemini API 팀의 Ali Çevik, Philipp Schmid 두 명이 Gemini API의 신규 기능인 "매니지드 에이전트(Managed Agents)"와 그 기반이 되는 "Interactions API"를 설명하고 실제 데모를 시연한다.

## 다루는 내용 순서

1. **매니지드 에이전트란 무엇인가 — 한 줄 정의**
   Ali는 매니지드 에이전트를 "API 호출 한 번으로 자율적으로 문제를 창의적으로 해결하는 에이전트를 얻는 것"이라고 정의한다. 핵심은 이 에이전트가 원격 리눅스 환경의 샌드박스 안에서 실행된다는 점이다. 이 덕분에 코드를 실행하고 bash 명령을 쓰는 등 무엇이든 할 수 있으면서도, 개발자가 자신의 프로덕션 서버에 직접 AI가 짠 코드를 실행시키는 위험을 지지 않아도 된다.

2. **Antigravity 하네스가 기반**
   초기 출시는 Gemini 3.5 Flash와 새로운 "Antigravity 에이전트"가 함께 구동한다. Philipp은 이 프리뷰 에이전트가 Antigravity IDE도 구동하는 동일한 "Antigravity agent harness" 위에서 돌아간다고 설명한다. API 호출 한 번으로 격리된 리눅스 환경을 받아 코드 실행, 파일 생성, 스킬 실행, 로컬 머신에서 쓰던 도구 사용이 모두 가능하며, 이 기본 에이전트 위에 자체 시스템 지침과 스킬을 얹어 커스텀 매니지드 에이전트를 만들고 고객·내부팀·개인 프로젝트에 배포할 수 있다.

3. **역사적 맥락 — Interactions API의 탄생**
   Ali는 이번이 Gemini API의 첫 에이전트 기능이 아니라고 설명한다. 이전에 출시한 "Interactions API"에서 첫 매니지드 에이전트인 "Deep Research"를 이미 선보였다. Gemini API는 원래 콘텐츠 생성이 프론티어 AI의 핵심 능력이던 시절 설계된 "generate content API"였지만, 이후 함수 호출·도구·추론 모델·서브에이전트·장시간 실행 에이전트 등으로 능력이 복잡해지면서, 이런 프론티어 능력을 대표하는 새 API로 Interactions API를 설계했다고 밝힌다. 이 API는 모델과 에이전트 모두를 하나의 인터페이스로 호출할 수 있게 한다.

4. **선택권 강조 — 매니지드 에이전트는 선택 사항**
   Philipp은 개발자가 반드시 에이전트 기능을 써야 하는 것은 아니라고 강조한다. 여전히 많은 고객이 Interactions API나 generate content로 순수 모델 호출만 쓰고 있으며, 호스팅된 환경이 필요하면 매니지드 에이전트를, 자체 프레임워크를 쓰고 싶으면 같은 API로 모델만 호출하는 선택지도 유지된다.

5. **데모 — "Daily Hacker Bites" 라디오쇼 앱**
   AI Studio Build로 만든 미니 앱을 시연한다. 매니지드 에이전트가 Hacker News의 그날 인기 댓글·주제를 읽고, 서로 반대되는 두 관점을 골라, 서로 다른 지역에서 전화 연결하는 형식의 라디오쇼 대본으로 바꾼다. 이 과정에서 Interactions API를 통해 Gemini TTS(음성 합성)를 호출하고, Lyria(음악 생성 모델)로 배경음악을 만들고, Gemini 모델로 대본을 작성한다. 이 예시 하나가 18개 안팎의 출처를 참고했다고 언급되며, 완성된 결과물은 약 3분짜리 라디오쇼다. 실제로 "vibe coding으로 하루 200줄 쓰던 걸 2,000줄 쓰게 됐다고 더 나은 엔지니어인가"라는 주제로 두 화자가 대립하는 각본이 재생된다.

6. **데이터 모델 변화 — "에이전트 우선(agent-first)" 설계**
   Philipp은 generate content에서 Interactions API로 넘어가며 가장 크게 바꾼 것이 데이터 모델이라고 설명한다. 기존에는 사용자 메시지 → 모델 응답이라는 단순한 턴제(turn-based) 구조였지만, 에이전트는 사용자 입력 → 툴 호출 → 서브에이전트 호출 등 여러 단계가 연속으로 이어지는 "스텝(step)의 스트림" 구조를 가진다. 사용자 턴이 항상 모델 턴 다음에 오지 않을 수도 있다. Interactions API는 이런 모든 단계(도구·환경 포함)를 모델과 동등한 일급 시민(first-party)으로 API에 통합했다.

7. **에이전트를 위한 개발자 경험 — 마크다운 중심 설계**
   Gemini API 팀은 모델의 지식 컷오프상 Interactions API 자체를 모를 수 있다는 점을 고려해, 문서 전체를 마크다운으로 접근 가능하게 재구성하고, 에이전트가 검색할 수 있는 링크와 전용 MCP 서버를 제공한다. 개발자는 이 스킬들을 코딩 에이전트(Antigravity)에 연결해 "이 스킬을 써서 이런 매니지드 에이전트를 만들어줘"라고 지시하고 함께 반복 개선한 뒤 배포할 수 있다. 에이전트 정의 자체도 `agents.md`와 스킬 마크다운 파일들로 이루어지며, 두 발표자는 이를 두고 "소프트웨어의 미래는 결국 마크다운 파일 뭉치일 수도 있다"고 농담 삞인 소감을 밝힌다.

8. **마무리 — 시작 방법**
   매니지드 에이전트를 써보고 싶다면 Gemini API 문서, AI Studio, 또는 `agent.new`에서 첫 에이전트를 만들어볼 수 있다고 안내하며 영상을 마친다. 발표자들은 이번이 "매니지드 에이전트라는 새 이야기의 1장"이며 로드맵이 길다고 언급한다.

## 참고 — 직접 재확인 필요 사항

- 자동 생성 자막을 기반으로 정리했으므로, 제품명(Interactions API, Antigravity agent harness 등)의 정확한 공식 표기는 Google 공식 문서(`ai.google.dev/gemini-api/docs/agents`)에서 재확인이 필요하다.
- 영상 시점(2026-06-03)의 "프리뷰" 상태 설명이 이후 정식 출시 여부·요금제로 바뀌었을 수 있으므로, 실제 이용 전 최신 공식 문서 확인이 필요하다.
