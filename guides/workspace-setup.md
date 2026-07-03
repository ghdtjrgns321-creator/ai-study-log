# Day 1-2: 작업환경 설정 (VS Code + 터미널 + Claude Code)

이 문서는 개념 학습이 아니라 실전 환경 개선 가이드다. 현재 상태를 기준으로 무엇을 바꾸는지 순서대로 정리한다.

## 지금 상태 진단
- VS Code를 파일 탐색기 용도로만 사용(편집·Git·터미널 기능 미사용).
- PowerShell 기본 창에서 Claude Code(`claude`)와 Codex CLI만 실행.
- 결과적으로 코드 변경 내역(diff)·Git 상태·에러를 눈으로 확인하는 경로가 없다.

아래 9개 액션을 위에서부터 적용하면 "탐색기+CLI" 환경이 "통합 개발 환경"으로 바뀐다. 1~4번만 해도 체감이 크다.

---

## 액션 1. VS Code에 Claude Code 확장 설치
- 지금: PowerShell 창에서 `claude`만 실행. 변경된 코드를 텍스트로만 본다.
- 바꿀 것: VS Code 안에서 Claude Code를 실행해 변경 사항을 좌우 비교(inline diff)로 확인.
- 방법: VS Code 확장 탭(`Ctrl+Shift+X`)에서 "Claude Code" 검색 후 설치. VS Code 1.98.0 이상 필요.

확장을 쓰면 CLI 대비 세 가지가 편해진다. 변경 코드를 side-by-side diff로 검토할 수 있고, 특정 파일의 특정 라인 범위를 컨텍스트로 지정할 수 있으며, 에디터에서 선택한 영역이 자동으로 대화에 포함된다.

- 공식 문서: https://code.claude.com/docs/en/vs-code

## 액션 2. VS Code 통합 터미널로 이동
- 지금: PowerShell을 별도 창으로 띄워 사용.
- 바꿀 것: VS Code 안의 통합 터미널에서 `claude`, `codex`를 실행해 편집기와 터미널을 한 화면에서 본다.
- 방법: VS Code에서 ``Ctrl+` ``(백틱)으로 터미널을 열고 그 안에서 CLI 실행.

## 액션 3. Git 변경 내역을 눈으로 보기 (Source Control + GitLens)
- 지금: 어떤 파일이 언제 왜 바뀌었는지 추적 경로가 없다.
- 바꿀 것: VS Code 좌측 Source Control 패널로 변경 파일·diff·커밋을 GUI로 다룬다.
- 방법: VS Code 좌측 아이콘 바의 Source Control(브랜치 모양) 사용. 추가로 확장 탭에서 "GitLens" 설치 시 코드 각 줄 옆에 마지막 수정자·커밋이 표시된다.

## 액션 4. 인라인 에러 표시 확장 설치
- 지금: 문법 오류를 실행해야 안다.
- 바꿀 것: 에러를 코드 줄 위에 즉시 표시.
- 방법: 확장 탭에서 "Error Lens" 설치. 언어에 맞는 확장도 함께 설치(Python이면 "Python", 포매팅은 "Prettier" 또는 언어별 포매터).

참고: 확장은 많이 깔수록 좋은 게 아니다. VS Code가 무거워지므로 실제로 쓰는 것만 남긴다.

- 확장 참고 글: https://nestloghub.com/blog/coding/vscode-essential-extensions-2026

---

## 액션 5. 프로젝트별 CLAUDE.md 만들기
- 지금: Claude Code가 프로젝트 구조를 매번 처음부터 파악.
- 바꿀 것: 프로젝트 루트에 CLAUDE.md를 두어 규칙·구조·컨벤션을 영구 저장.
- 방법: 프로젝트에서 `claude` 실행 후 `/init` 명령. 프로젝트를 분석해 CLAUDE.md 초안을 생성한다. 이후 직접 수정.

- 공식 문서: https://code.claude.com/docs/en/memory

## 액션 6. 권한(permissions) 설정으로 반복 승인 줄이기
- 지금: 명령 실행마다 승인 프롬프트.
- 바꿀 것: 자주 쓰는 안전한 명령을 허용 목록에 등록.
- 방법: 프로젝트의 `.claude/settings.json`(또는 사용자 전역 `~/.claude/settings.json`)에 permissions의 allow 목록을 정의.

- 공식 문서: https://code.claude.com/docs/en/permission-modes

## 액션 7. MCP로 외부 도구 연결
- 지금: Claude Code가 파일·터미널 밖 데이터에 접근 불가.
- 바꿀 것: MCP(Model Context Protocol) 서버를 연결해 외부 데이터·도구를 붙인다.
- 방법: `.mcp.json` 또는 사용자 설정에 MCP 서버를 등록. 세션 내 `/mcp`로 상태 확인.

- 공식 문서: https://code.claude.com/docs/en/mcp

---

## 액션 8. PowerShell 프롬프트 개선 (Git 상태 + 자동완성)
- 지금: 기본 프롬프트라 현재 브랜치·변경 여부가 안 보인다.
- 바꿀 것: 프롬프트에 Git 브랜치·상태를 표시하고 명령 자동완성을 강화.
- 방법: Oh My Posh(프롬프트 테마)와 posh-git(Git 상태 표시)을 설치하고 PowerShell 프로필에 등록. Nerd Font 계열 글꼴이 있어야 아이콘이 정상 표시된다.

- 공식 문서(Windows 설치): https://ohmyposh.dev/docs/installation/windows
- 프로젝트: https://github.com/JanDeDobbeleer/oh-my-posh

## 액션 9. Windows Terminal + 최신 PowerShell
- 지금: 기본 콘솔 창.
- 바꿀 것: 탭·글꼴·테마를 지원하는 Windows Terminal에서 최신 PowerShell 7 사용.
- 방법: Microsoft Store에서 Windows Terminal 설치. 최신 PowerShell은 아래 저장소에서 받는다.

- PowerShell 저장소: https://github.com/PowerShell/PowerShell

---

## Claude Code와 Codex 함께 쓰기
두 도구 모두 터미널 기반 코딩 에이전트이므로 같은 프로젝트 폴더에서 번갈아 실행할 수 있다. 한쪽이 작성한 변경을 다른 쪽에 검토시키는 교차 확인 용도로 쓰면 서로의 사각지대를 줄일 수 있다.

다만 두 도구가 동시에 같은 파일을 수정하면 충돌하므로, 한 번에 한 도구만 편집하도록 순서를 지킨다. 각 도구의 세부 워크플로우는 각자의 공식 문서를 기준으로 확인한다.

## 우선순위 요약
- 오늘(1일차): 액션 1~4 (VS Code 확장 + 통합 터미널 + Git 보기 + 에러 표시)
- 다음(2일차): 액션 5~7 (CLAUDE.md + 권한 + MCP)
- 여유 있을 때: 액션 8~9 (터미널 꾸미기)

## 자가 점검 질문 3개
1. 방금 Claude Code가 수정한 코드의 변경 전후를 어디서 어떻게 확인하는가.
2. 현재 작업 중인 Git 브랜치와 커밋되지 않은 변경을 프롬프트나 화면 어디에서 보는가.
3. CLAUDE.md에 무엇을 적어두면 Claude Code가 매번 다시 설명하지 않아도 되는가.
