# 영상 정리: Windsurf Becomes Devin Desktop in 2026: What Changed

> 원본: [Windsurf Becomes Devin Desktop in 2026: What Changed](https://www.youtube.com/watch?v=dCcchCYJ5no) — 영어, 유튜브, 약 4분 40초, 채널 "Standarity" (2026-06-10 게시)
> 연결된 브리핑: [04-windsurf-devin-desktop.md](../04-windsurf-devin-desktop.md)
> 이 문서는 유튜브 자동 자막(영어)을 직접 내려받아 정리한 것이다. 채널 성격상 사람이 직접 진행하는 리뷰가 아니라 뉴스 요약을 기계 음성(TTS)으로 읽어주는 형태의 짧은 정리 영상으로 보이며, 별도의 심층 취재나 실사용 후기는 담겨 있지 않다. 다만 자막에 담긴 사실관계는 Cognition 공식 블로그(cognition.com/blog/introducing-devin-desktop, devin.ai/blog/windsurf-is-now-devin-desktop) 및 공식 FAQ(docs.devin.ai)와 대조해 일치함을 확인했다.

## 영상 내용 요약

영상은 "무엇이 바뀌었는가"를 4가지 핵심 포인트로 압축해 반복 설명하는 구조다(도입 - 본론 - 실행 체크리스트 - 재요약의 4단 반복).

1. **리브랜딩 방식**: 2026년 6월 2일, Cognition은 Windsurf를 Devin Desktop으로 바꾸는 업데이트를 오버 디 에어(OTA, 재설치 불필요) 방식으로 배포했다. 재설치 절차나 별도 마이그레이션 마법사 없이, 에디터를 재시작하면 계정·요금제·확장 프로그램·키 바인딩이 그대로 유지된 채 새 버전으로 전환됐다.

2. **기본 화면의 변화**: 기존에는 코드 에디터 화면이 기본 화면이었는데, 전환 후에는 "에이전트 커맨드 센터(Agent Command Center)"가 기본 화면이 됐다. 영상은 이를 "에이전트를 호출하는 코드 에디터"에서 "IDE를 품은 에이전트 관리 허브"로의 방향 전환이라고 설명한다.

3. **Cascade의 종료와 Devin Local**: Windsurf의 로컬 에이전트였던 Cascade는 2026년 7월 1일부로 종료(end of life)된다. 대체 에이전트인 Devin Local은 러스트(Rust)로 처음부터 새로 작성됐으며, Cognition 발표 기준 최대 30% 더 토큰 효율적이고, 서브에이전트(하나의 로컬 에이전트가 하위 작업을 위한 보조 에이전트를 여러 개 만들어 병렬 처리하는 기능)를 지원한다.

4. **개방형 프로토콜 지원**: Devin Desktop은 아파치 2.0 라이선스의 Agent Client Protocol(ACP)을 지원하며, 영상에 따르면 Codex·Claude Agent·Gemini CLI 같은 외부 에이전트도 하나의 에디터 안에서 동등한 자격으로 실행할 수 있다.

## 실행 체크리스트 (영상이 강조한 부분)

- Cascade를 명시적으로 호출하는 CI 파이프라인·스크립트·워크플로 규칙이 있다면, 7월 1일 이전에 Devin Local을 가리키도록 미리 바꿔둬야 한다.
- 계정·요금제·확장 프로그램이 자동 이관됐다고 안내되지만, 설정 화면에서 직접 플랜(Free/Pro/Max/Teams/Enterprise)이 정확히 이관됐는지 확인할 것을 권장한다.
- 기본 화면이 에이전트 커맨드 센터로 바뀌었으므로, 기존 에디터 중심 작업 흐름에 익숙한 사용자는 새 레이아웃 학습이 필요하다.

## 이 영상에서 주의할 점

- 채널이 뉴스 큐레이션·TTS 낭독 형식이라 심층 분석이나 실사용 스크린샷은 없다. 사실관계 확인용으로만 활용하고, 실제 마이그레이션 절차나 UI 세부사항은 공식 문서(docs.devin.ai/desktop/devin-desktop-faq)로 재확인해야 한다.
- 한국어 자막은 별도로 제공되지 않아 영어 자막 기준으로 정리했다.
