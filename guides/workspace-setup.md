# Day 1-2: 요즘 쓰는 에이전틱 코딩 환경

기본 VS Code 설정 이야기가 아니다. 지금 개발자들이 "현란하게" 쓴다고 말하는 흐름, 즉 에이전트 여러 개를 동시에 굴리는 환경과 도구를 정리한다.

## 지금 상태와 지향점
- 현재: PowerShell 별도 창에서 Claude Code(`claude`)와 Codex CLI 실행. 모니터가 작아 VS Code 통합 터미널 대신 창을 분리해 쓰고, 변경 내역은 VS Code로 확인 중.
- 이 셋업은 "에이전트 1개에게 1개 작업을 시키는" 방식이다. 요즘 화제가 되는 흐름은 "에이전트 여러 개가 작업을 나눠 병렬로 처리하고, 사람은 관리자(supervisor)로 지켜보는" 방식이다.

아래는 그 흐름을 대표하는 도구들이다. 사용자가 언급한 Antigravity가 바로 이 방향의 대표 주자다.

---

## 1. Google Antigravity — 멀티 에이전트 IDE
Antigravity는 구글이 2025년 11월 내놓은 에이전트 중심(agent-first) 개발 플랫폼이다. 일반 편집기와 달리 "에이전트 매니저(Agent Manager)"라는 화면이 중심에 있다.

핵심은 에이전트를 최대 여러 개까지 동시에 띄워 각자 다른 작업(파일 수정, 명령 실행, 테스트 작성)을 시키고, 진행 상황을 한눈에 지켜보는 것이다. 각 에이전트는 작업 계획·스크린샷·브라우저 녹화 같은 산출물(Artifact)을 남겨서, 사람이 로직을 눈으로 검증할 수 있다.

특히 브라우저를 직접 띄워 자기가 만든 웹앱의 버튼을 눌러보고 안 되면 스스로 고치는 기능이 "현란하다"는 평의 핵심이다. 기본 모델은 Gemini 계열이지만 Claude(Sonnet·Opus)와 다른 모델도 선택할 수 있어 구글 전용이 아니다.

- 별도 데스크톱 앱이라 모니터가 작아도 창을 분리해 쓰는 지금 방식과 잘 맞는다. 개인은 공개 프리뷰로 무료 시작 가능.
- 공식 발표: https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/
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
2026년의 공통 흐름은 "에이전트 1개 → 에이전트 여러 개를 관리"다. Antigravity는 이를 전면에 내세운 전용 IDE이고, Claude Code·Cursor·Codex도 같은 방향으로 기능을 넓히는 중이다.

성능은 도구 간 격차가 크게 좁혀졌다는 평가가 많으므로, 벤치마크 순위보다 본인 작업 흐름에 맞는지가 선택 기준이다.

## 추천 액션
- 먼저: Antigravity를 무료로 설치해 에이전트 매니저 화면을 직접 본다. "현란한" 흐름이 무엇인지 체감하는 게 목적이다.
- 동시에: 지금 쓰는 Claude Code에서 플랜 모드와 서브에이전트를 한 번씩 써본다. 이미 가진 도구의 활용도부터 올린다.
- 판단: 두 흐름을 겪은 뒤, 별도 IDE(Antigravity·Cursor)로 갈지 CLI 중심을 유지할지 정한다.

## 자가 점검 질문 3개
1. "에이전트 1개에게 시키기"와 "에이전트 여러 개를 관리하기"의 차이를 한 문장으로 설명한다면.
2. Antigravity의 Artifact(산출물)가 사람의 검증에 어떤 도움을 주는가.
3. 지금 쓰는 Claude Code에서 아직 안 써본 기능(플랜 모드·서브에이전트·MCP) 중 내 작업에 가장 쓸모 있을 것은 무엇인가.
