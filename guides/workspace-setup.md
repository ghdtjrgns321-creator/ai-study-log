# Day 1-2: 요즘 쓰는 에이전틱 코딩 환경

기본 VS Code 설정 이야기가 아니다. 지금 개발자들이 "현란하게" 쓴다고 말하는 흐름, 즉 에이전트 여러 개를 동시에 굴리는 환경과 도구를 정리한다.

## 지금 상태와 지향점
- 현재: PowerShell 별도 창에서 Claude Code(`claude`)와 Codex CLI 실행. 모니터가 작아 VS Code 통합 터미널 대신 창을 분리해 쓰고, 변경 내역은 VS Code로 확인 중.
- 이 셋업은 "에이전트 1개에게 1개 작업을 시키는" 방식이다. 요즘 화제가 되는 흐름은 "에이전트 여러 개가 작업을 나눠 병렬로 처리하고, 사람은 관리자(supervisor)로 지켜보는" 방식이다.

아래는 그 흐름을 대표하는 도구들이다. 사용자가 언급한 Antigravity가 바로 이 방향의 대표 주자이며, 최근 CLI 중심으로 바뀌었다.

---

## 1. Google Antigravity — CLI 중심 멀티 에이전트 플랫폼
Antigravity는 구글이 2025년 11월 내놓은 에이전트 중심(agent-first) 개발 플랫폼이다. 처음에는 코드 편집이 되는 데스크톱 앱 형태였으나, 2026년 개편으로 무게중심이 터미널 도구인 Antigravity CLI(명령어 `agy`)로 옮겨갔다.

중요한 변화가 두 가지 있다. 첫째, 2026년 6월 18일 기존 Gemini CLI가 요청 처리를 멈추고 Antigravity CLI로 통합됐다. 둘째, 2.0 데스크톱 앱은 에이전트를 관리하는 용도로 남았지만 코드 편집 기능은 빠졌다. 따라서 "Antigravity로 직접 코드를 편집한다"는 기대는 지금 시점에 맞지 않는다.

Antigravity CLI는 Go 언어로 새로 쓴 단일 실행 파일이라 시작 속도와 메모리 효율이 좋고, 여러 에이전트를 나눠 돌리는 멀티 에이전트·백그라운드 작업을 터미널에서 처리한다. 이 CLI는 데스크톱 앱과 같은 실행 기반(harness)을 공유한다.

- CLI 중심이라 지금 PowerShell에서 `claude`·`codex`를 쓰는 방식과 결이 같다. 새 편집기를 배우는 게 아니라 터미널 에이전트를 하나 더 얹는 셈이다.
- 개편 발표(Gemini CLI → Antigravity CLI): https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/
- 플랫폼 소개: https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/
- 공식 사이트: https://antigravity.google/

## 2. Cursor — AI가 중심인 코드 에디터
Cursor는 VS Code를 기반으로 만든 AI 코드 에디터다. 채팅·자동완성·에이전트가 편집기 안에 녹아 있어, 별도 CLI 창을 오가지 않고 편집 흐름 안에서 AI를 쓴다.

작은 화면에서 창을 여러 개 띄우기 부담스러울 때, 편집과 AI 대화가 한 앱에 통합돼 있다는 점이 장점이다. 유료 요금제는 월 20달러 선에서 시작한다.

- 공식 사이트: https://cursor.com/

## 3. 이미 가진 Claude Code를 "현란하게" 쓰기
새 도구를 깔기 전에, 지금 쓰는 Claude Code에도 멀티 에이전트급 기능이 이미 있다. 지금은 기본 대화만 쓰고 있을 가능성이 높다.

- 플랜 모드: 바로 코드를 고치지 않고 계획을 먼저 세워 검토받게 한다. `Shift+Tab`으로 모드 전환. 근거: https://code.claude.com/docs/en/permission-modes
- 서브에이전트·워크플로우: 하나의 작업을 여러 에이전트로 쪼개 병렬 처리한다. Antigravity의 멀티 에이전트와 같은 개념을 터미널에서 구현한 것이다. 근거: https://code.claude.com/docs/en/common-workflows
- 브라우저 자동화: `@browser`로 Chrome을 붙여 웹앱을 직접 조작·디버깅한다. Antigravity의 브라우저 기능과 유사하다. 근거: https://code.claude.com/docs/en/chrome
- MCP 연결: 외부 데이터·도구를 붙여 에이전트 능력을 확장한다. 근거: https://code.claude.com/docs/en/mcp

## 참고: Windsurf는 사라졌다
과거 인기 있던 AI 에디터 Windsurf는 2026년 기준 독립 제품으로 존재하지 않는다. Devin을 만든 Cognition이 인수해 "Devin Desktop"으로 리브랜딩했다. 옛 자료에서 Windsurf를 보면 이 맥락을 기억한다.

- Devin: https://devin.ai/

---

## 트렌드 한 줄 요약
2026년의 공통 흐름은 "에이전트 1개 → 에이전트 여러 개를 관리"다. Antigravity는 이를 전면에 내세운 CLI 중심 플랫폼이고, Claude Code·Cursor·Codex도 같은 방향으로 기능을 넓히는 중이다.

성능은 도구 간 격차가 크게 좁혀졌다는 평가가 많으므로, 벤치마크 순위보다 본인 작업 흐름에 맞는지가 선택 기준이다.

## 추천 액션
- 먼저: Antigravity CLI(`agy`)를 설치해 멀티 에이전트를 터미널에서 굴려본다. 지금 `claude`·`codex` 쓰는 방식과 같은 결이라 진입장벽이 낮다.
- 동시에: 지금 쓰는 Claude Code에서 플랜 모드와 서브에이전트를 한 번씩 써본다. 이미 가진 도구의 활용도부터 올린다.
- 판단: 두 흐름을 겪은 뒤, CLI 여러 개를 병행할지, Cursor 같은 통합 편집기로 갈지 정한다.

## 자가 점검 질문 3개
1. "에이전트 1개에게 시키기"와 "에이전트 여러 개를 관리하기"의 차이를 한 문장으로 설명한다면.
2. Antigravity의 Artifact(산출물)가 사람의 검증에 어떤 도움을 주는가.
3. 지금 쓰는 Claude Code에서 아직 안 써본 기능(플랜 모드·서브에이전트·MCP) 중 내 작업에 가장 쓸모 있을 것은 무엇인가.
