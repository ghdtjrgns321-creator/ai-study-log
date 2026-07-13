# 오늘의 AI 개념: Claude Code 인앱 브라우저(In-app Browser)

> 작성일: 2026-07-14 · 분류: claude-code

## 한 줄 정의

에이전트가 코드 편집기·터미널을 다루듯, 별도의 안전한 브라우저 창을 직접 열어 웹페이지를 읽고 클릭하고 입력하게 해주는 기능이다.

## 쉬운 설명

개발자가 화면을 나눠 터미널·에디터·브라우저를 동시에 켜놓고 작업하는 방식을, 이제 에이전트도 그대로 쓸 수 있게 되었다고 이해하면 된다. Claude Code 데스크톱 앱 안에 전용 브라우저 창이 추가되어, 채팅·터미널·파일 편집기·코드 diff 화면 옆에 나란히 띄울 수 있다.

기존에는 에이전트가 웹을 보려면 별도 MCP 브라우저 도구나 헤드리스 스크립트를 거쳐 간접적으로 접근해야 했다. 이번 기능은 사람이 직접 브라우저를 조작하듯 페이지 콘텐츠를 읽고, DOM(문서 객체 모델)을 검사하고, 버튼을 클릭하고, 양식을 입력하고, 스크린샷을 찍는 것을 에이전트 스스로 수행한다.

비슷한 기존 기능인 'Claude in Chrome'과는 목적이 다르다. Claude in Chrome은 사용자의 개인 브라우저 확장 프로그램으로 실제 로그인 정보와 방문 기록을 공유하지만, 이번 인앱 브라우저는 개인 정보가 전혀 없는 깨끗한 프로필을 사용하는 별도 창이다. 즉 하나는 '내 계정으로 실제 작업을 시키는 용도', 다른 하나는 '내 것과 분리된 환경에서 빌드·테스트하는 용도'로 구분된다.

## 동작 원리

1. 사용자가 단축키(macOS: Cmd+Shift+B, Windows: Ctrl+Shift+B)로 브라우저 창을 열거나, 필요 시 Claude가 자동으로 연다.
2. Claude가 로컬 개발 서버 미리보기 또는 외부 URL(문서, 이슈 트래커, 디자인 파일 등)을 불러온다.
3. 페이지의 DOM을 검사하고, 인터페이스 요소를 클릭하거나 양식을 채우고, 필요하면 스크린샷을 캡처한다.
4. 외부 사이트에서의 위험한 행동(로그인, 결제, 양식 제출 등)은 세이프티 classifier가 사전에 검토한다.
5. 확인된 결과(오류 메시지, 화면 상태)를 코드 수정 루프에 반영한다.

## 구체 예시·사례

개발자가 "회원가입 폼을 만들어 달라"고 요청하면, Claude Code는 관련 파일을 수정하고 로컬 개발 서버를 실행한 뒤, 브라우저 창에서 실제로 그 폼을 열어 샘플 정보를 입력하고 제출 버튼을 누른다. 이 과정에서 발생한 에러 메시지나 레이아웃 깨짐을 화면으로 직접 확인해 코드를 다시 고치는 것까지 한 번의 작업 흐름 안에서 이뤄진다.

## 비슷한 것과 비교

| 기능 | 성격 | 사용 프로필 | 주 용도 |
|------|------|------------|---------|
| 인앱 브라우저(이번 기능) | 샌드박스 창 | 깨끗한 별도 프로필 | 빌드·테스트, 인증 필요 없는 사이트 확인 |
| Claude in Chrome | 브라우저 확장 | 사용자 개인 프로필(로그인·기록 공유) | 실제 계정으로 대신 작업 수행 |
| Computer Use(컴퓨터 사용 에이전트) | OS 전체 제어 | 시스템 전체 | 네이티브 앱까지 포함한 광범위한 GUI 조작 |

브라우저 안에서만 끝나는 웹 UI 검증이 목적이면 인앱 브라우저, 실제 내 계정으로 처리해야 하는 작업이면 Claude in Chrome, 앱 전체를 다뤄야 하면 Computer Use를 고르면 된다.

## 왜 지금 중요한가

Claude Code 공식 변경 이력에 따르면 이 기능은 2026년 7월 6일~10일(버전 v2.1.202~v2.1.206) 주간 업데이트로 배포되었다. 데스크톱 앱의 패널 기반 레이아웃을 활용해 채팅·터미널과 나란히 배치되는 방식이다.

- [What's new - Claude Code Docs](https://code.claude.com/docs/en/whats-new)
- [Claude Code now has a built-in browser that lets the AI read, click, and type on external websites](https://the-decoder.com/claude-code-now-has-a-built-in-browser-that-lets-the-ai-read-click-and-type-on-external-websites/)

## 회계법인 AI 직무 연결 포인트

감사 대상 회사가 웹 기반 ERP나 회계 시스템을 쓰는 경우, 에이전트가 해당 화면을 직접 열어 데이터를 확인하고 스크린샷 증적을 남기는 절차에 활용할 수 있다.

사내에서 개발 중인 감사 자동화 툴의 웹 화면(UI)을 사람이 매번 클릭해 확인하는 대신, 에이전트가 회원가입·데이터 입력 같은 시나리오를 반복 테스트하게 맡길 수 있다.

회계기준 개정 공지나 규제 기관 공시 페이지처럼 로그인이 필요 없는 외부 웹 자료를 직접 열람해 최신 내용을 코드나 문서 작업에 반영하는 용도로도 쓸 수 있다.

## 핵심 용어·논쟁

- 샌드박스(Sandbox) — 외부 영향을 차단한 격리된 실행 환경.
- DOM(문서 객체 모델, Document Object Model) — 웹페이지 구조를 트리 형태로 표현한 것.
- 세이프티 classifier — 위험한 행동을 사전에 걸러내는 분류 모델.
- MCP(Model Context Protocol, 모델 컨텍스트 프로토콜) — 에이전트가 외부 도구·데이터에 접근하는 표준 규격.

## 자료 깊이 읽기

### What's new - Claude Code Docs — 영어, 공식 문서, 중급
Anthropic 공식 변경 이력 페이지로, 주차별로 업데이트를 정리한다. 2026년 7월 6일~10일(Week 28) 항목에 인앱 브라우저 도입이 명시되어 있으며, 같은 주에 `/doctor` 자동 진단·수정 기능과 auto mode의 안전장치 강화도 함께 발표되었다. 이전 주차(Week 27)의 Claude Sonnet 5 기본 모델 전환, Week 26의 서브에이전트 권한 처리 개선 등 최근 몇 주간의 맥락도 함께 파악할 수 있다. 실제 페이지를 열어 확인한 내용으로, 버전 번호와 날짜가 구체적으로 명시되어 신뢰도가 높다.

### Claude Code now has a built-in browser... (the-decoder.com) — 영어, 뉴스 기사, 입문
(요약 불가 — 본문 확인 실패. 검색 결과에는 제목과 개요만 노출되어 본문 전체를 확인하지 못했다.)

**그 외 참고**
- [Claude Code Desktop Adds a Sandboxed Browser for Agents](https://www.digitalapplied.com/blog/claude-code-desktop-sandboxed-browser-agents-2026) — 영어, 뉴스 기사, 입문
- [Claude Code Just Got Its Own Browser—and Chrome Can Take a Coffee Break](https://kingy.ai/news/claude-code-built-in-browser-web-app-testing/) — 영어, 뉴스 기사, 입문
- [Claude Code can now browse the web without opening Chrome](https://www.digitaltrends.com/cool-tech/claude-code-can-now-browse-the-web-without-opening-chrome/) — 영어, 뉴스 기사, 입문

## 자가 점검 질문

1. 인앱 브라우저와 Claude in Chrome, Computer Use는 각각 어떤 상황에서 선택해야 하는가?
2. 이 기능이 감사 증적(스크린샷, 로그) 수집 자동화에 활용될 때 어떤 신뢰성 검증 절차가 추가로 필요한가?
3. 에이전트가 외부 웹사이트에서 자동으로 로그인·양식 제출까지 하게 될 경우, 어떤 통제(승인 절차, 로그 기록)가 선행되어야 하는가?
