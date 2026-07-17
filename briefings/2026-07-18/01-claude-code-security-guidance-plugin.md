# 오늘의 AI 개념: 보안 가이던스 플러그인(Security-Guidance Plugin)

> 작성일: 2026-07-18 · 분류: claude-code

## 한 줄 정의

Claude Code가 스스로 작성한 코드를 취약점 관점에서 다시 검토하고, 문제를 찾으면 같은 세션 안에서 바로 고치게 해주는 공식 플러그인이다.

## 쉬운 설명

개발자가 Claude Code에 기능 구현을 맡기면, 코드는 빠르게 만들어지지만 보안 검토는 대개 뒤로 밀려 풀리퀘스트(PR) 단계나 코드 리뷰어의 몫으로 남는다. 보안 가이던스 플러그인은 이 순서를 앞당긴다. Claude가 파일을 고칠 때, 한 턴의 작업을 마칠 때, 커밋·푸시를 실행할 때마다 별도의 검토 절차가 자동으로 끼어들어 인젝션, XSS, SSRF, 하드코딩된 시크릿 같은 문제를 코드가 저장소에 올라가기 전에 잡아낸다.

비유하면 회계법인 신입 심사역이 전표를 입력할 때마다 옆자리 선임이 즉시 훑어보고, 하루 작업이 끝나면 별도 담당자가 그날 처리분 전체를 다시 검토하며, 결산 마감 시점에는 관련 계정을 함께 들여다보는 시니어가 한 번 더 확인하는 3중 체계와 비슷하다. 각 단계는 깊이가 다르고, 뒷단으로 갈수록 더 넓은 맥락을 본다.

설치하면 별도로 호출할 명령어나 슬래시 커맨드 없이 백그라운드에서 자동으로 동작한다는 점이 특징이다. 기존에 알려진 `/security-review`가 요청 시점에 한 번 도는 온디맨드 점검이라면, 이 플러그인은 코드가 만들어지는 매 순간 상시로 붙는다는 점에서 다르다.

## 동작 원리

플러그인은 Claude Code의 훅(hooks) 메커니즘 위에 구축되어 있으며, 서로 다른 시점에 3개 층으로 작동한다.

| 층 | 훅 이벤트 | 방식 | 탐지 예시 |
| --- | --- | --- | --- |
| 1. 편집 시점 패턴 매칭 | `PostToolUse`(Edit/Write/NotebookEdit) | 모델 호출 없는 정규식·문자열 매칭 | `eval(`, `os.system`, `pickle`, `dangerouslySetInnerHTML`, `.github/workflows/` 수정 |
| 2. 턴 종료 시점 diff 리뷰 | `Stop` | 별도 Claude 인스턴스(기본 Opus 4.7)가 백그라운드에서 해당 턴의 git diff 전체 검토 | 인증 우회, IDOR, 인젝션, SSRF, 취약한 암호화 |
| 3. 커밋·푸시 시점 에이전틱 리뷰 | `PostToolUse`(Bash의 `git commit`/`git push`) | Claude Agent SDK 기반 리뷰어가 호출자·새니타이저 등 관련 파일까지 함께 읽음 | 여러 파일에 걸친 취약점, 오탐 억제 |

1층은 비용이 들지 않고 파일당 패턴당 세션 1회만 경고한다. 2층은 최대 30개 변경 파일까지 검토하며 한 턴에서 최대 3회까지 반복된다. 3층은 시간당 20회로 제한되며, 2층이 이미 지적한 내용과 중복되면 다시 Claude를 호출하지 않는다. 세 층 모두 쓰기나 커밋을 막지는 않으며, 발견 사항을 Claude에게 지시로 전달해 같은 대화 안에서 고치게 하는 방식으로 작동한다.

```json
// .claude/settings.json — 프로젝트 전체·클라우드 세션에 강제 적용
{
  "enabledPlugins": {
    "security-guidance@claude-plugins-official": true
  }
}
```

```yaml
# .claude/security-patterns.yaml — 자체 규칙 추가 예시
patterns:
  - rule_name: tenant_unfiltered_query
    regex: "\\.objects\\.all\\(\\)"
    paths: ["**/src/tenants/**"]
    reminder: "멀티테넌트 코드는 org_id로 필터링해야 한다."
```

## 구체 예시·사례

멀티테넌트 SaaS 저장소에서 Claude에게 관리자용 조회 API를 추가해 달라고 요청한 상황을 가정한다. Claude가 `Organization.objects.all()`로 전체 조직 데이터를 필터 없이 반환하는 라우트를 작성하면, 1층 패턴 매칭은 사전 정의된 위험 함수 목록에 없어 통과할 수 있다. 턴이 끝나면 2층 diff 리뷰가 이 라우트에 역할 검사가 없다는 점을 IDOR로 지적하고, Claude는 같은 턴에서 `require_role("admin")` 호출을 추가한다. 이후 Claude가 `git commit`을 실행하면 3층 에이전틱 리뷰가 이 라우트를 호출하는 다른 파일과 인증 미들웨어까지 함께 읽어, 정말로 조직 경계가 지켜지는지 재확인한다. 팀이 `.claude/security-patterns.yaml`에 `tenant_unfiltered_query` 같은 정규식 규칙을 추가해 두면, 다음번에는 1층에서부터 이 패턴이 즉시 걸린다.

## 비슷한 것과 비교

| 구분 | 보안 가이던스 플러그인 | `/security-review` | PR 단계 Code Review |
| --- | --- | --- | --- |
| 시점 | 코드 작성 중 상시 | 사용자가 요청할 때 1회 | PR 생성 시점 |
| 대상 | 해당 세션에서 Claude가 만든 변경분 | 현재 브랜치 전체 | 브랜치 전체, 여러 에이전트 |
| 이용 조건 | 모든 플랜 무료 | 모든 플랜 | Team·Enterprise 플랜 |
| 대체 여부 | 사람 리뷰·SAST/DAST·의존성 스캔 대체 아님 | 위와 동일 | CI 정적분석·모의해킹 대체 아님 |

선택 기준은 단순하다. 작성 중 즉시 되돌리려면 이 플러그인, 특정 시점에 한 번 깊게 훑으려면 `/security-review`, PR 게이트가 필요하면 Code Review를 쓴다. 세 가지는 배타적이지 않고 방어 계층으로 함께 쓰도록 설계되어 있다.

## 왜 지금 중요한가

- [Week 22 · May 25–29, 2026 - Claude Code Docs](https://code.claude.com/docs/ko/whats-new/2026-w22) — Claude Opus 4.8(2026-05-28) 출시와 같은 주(v2.1.150→v2.1.157)에 정식 배포되었다고 명시한다.
- [Catch security issues as Claude writes code - Claude Code Docs](https://code.claude.com/docs/en/security-guidance) — 모든 플랜에서 무료이며, 편집·턴 종료·커밋의 3층 구조와 훅 기반 구현을 공식 문서로 확인할 수 있다.
- [Claude now reviews and fixes vulnerabilities as you write code - Help Net Security](https://www.helpnetsecurity.com/2026/05/27/anthropic-claude-code-security-guidance-plugin/) — Anthropic 내부 롤아웃·벤치마크에서 이 플러그인을 쓴 PR의 보안 관련 코멘트가 30~40% 줄었다고 보도했다. 이 수치는 공식 문서 페이지 자체에는 없어, Anthropic 발표를 인용한 외부 보도로 교차 확인했다.

## 회계법인 AI 직무 연결 포인트

회계법인이 자체적으로 감사 도구·RAG 챗봇·업무 자동화 스크립트를 Claude Code로 개발하는 경우, 이 플러그인은 개발 과정에서 발생하는 보안 부채를 코드 작성 즉시 줄여주는 안전판 역할을 한다. 특히 감사 증거나 고객 재무 데이터를 다루는 내부 도구에서 하드코딩된 API 키나 IDOR 같은 취약점이 남으면 정보보안뿐 아니라 감사 독립성·기밀유지 의무 위반으로도 번질 수 있어, 코드가 저장소에 올라가기 전에 걸러내는 장치의 가치가 크다.

`.claude/claude-security-guidance.md`로 조직 고유의 보안 규칙(예: 고객 계좌번호를 로그에 남기지 않는다, 관리자 라우트는 반드시 역할 검사를 거친다)을 프로젝트에 박아 넣을 수 있다는 점도 눈여겨볼 만하다. 이는 회계법인이 내부 개발 표준·정보보안 정책을 코드 수준의 가드레일로 강제하는 수단이 될 수 있으며, ITGC(IT 일반통제) 실사에서 "AI가 작성한 코드에 대한 보안 검토 절차가 존재하는가"라는 질문에 구체적으로 답할 근거가 된다.

다만 공식 문서 스스로 이 플러그인이 "보증이 아닌 보조 도구"이며 사람의 코드 리뷰, SAST/DAST, 의존성 스캐닝, 모의해킹을 대체하지 않는다고 명시하고 있다. 회계법인이 AI 개발 도구 도입을 벤더 평가나 내부통제 문서에 반영할 때, 이 플러그인의 존재를 "보안 검토를 마쳤다"는 근거로 과대 해석하지 않도록 주의해야 한다.

## 핵심 용어·논쟁

- 패턴 매칭(Pattern Rules) — 모델 호출 없이 정규식·문자열로 위험 함수 호출을 즉시 탐지하는 1층 검사.
- LLM diff review — 턴이 끝날 때 별도 Claude 인스턴스가 해당 턴의 git diff 전체를 검토하는 2층 검사.
- 에이전틱 커밋 리뷰(Agentic Commit Review) — 커밋·푸시 시점에 관련 파일까지 추적해 다중 파일 취약점을 찾는 3층 검사.
- IDOR(Insecure Direct Object Reference) — 권한 검사 없이 식별자만으로 다른 사용자의 리소스에 접근할 수 있는 취약점.
- 논쟁: 같은 모델 계열이 코드를 작성하고 그 코드를 검토도 한다는 점에서 "자기 검증의 독립성" 문제가 제기될 수 있다. 공식 문서는 리뷰어를 프레시 컨텍스트의 별도 호출로 분리해 작성자의 판단에 영향받지 않도록 설계했다고 설명하지만, 근본적으로 동일 모델 패밀리가 작성·검토를 모두 수행한다는 구조적 한계는 남는다.

## 자료 깊이 읽기

### Catch security issues as Claude writes code — 영어, 공식 문서, 중급
Claude Code 공식 문서로, 3층 검토 구조 각각의 훅 이벤트(`PostToolUse`, `Stop`, `Bash` 필터링)와 사용 모델(`SECURITY_REVIEW_MODEL`, `SG_AGENTIC_MODEL`), 층별 비활성화 환경변수, 커스텀 규칙 작성법(`.claude/security-patterns.yaml`)까지 필드 단위로 정리되어 있다. 커밋 리뷰가 시간당 20회로 제한되고 편집 검사는 세션당 파일·패턴 조합에 1회만 경고한다는 실제 운영 제약도 명시해, 도입 전 검토용으로 가장 신뢰할 만하다.

### Week 22 · May 25–29, 2026 — 한국어, 공식 릴리즈노트, 초급
Claude Code 주간 업데이트 다이제스트로, 보안 가이던스 플러그인이 Opus 4.8·다이나믹 워크플로우·패스트 모드 가격 조정과 같은 주(v2.1.150~v2.1.157)에 함께 발표되었음을 보여준다. 설치 명령과 활성화 명령을 화면 그대로 제공해 짧게 훑기에 적합하다.

**그 외 참고**
- [Claude Code's Security-Guidance Plugin: Shift-Left Security That Fixes Code as You Write It](https://inventivehq.com/blog/claude-code-security-guidance-plugin) — 영어, 기술 블로그, 초급 (이번 조사에서 실시간 접속 확인 실패, 검색 스니펫으로만 교차 확인)
- [Getting Started with the Claude Code Security Plugin](https://apito.ai/en/blog/dev-guides/claude-code-security-guidance-plugin-2026/) — 영어, 튜토리얼 블로그, 초중급 (접속 확인 실패, 검색 스니펫만 확인)
- [Claude Code 보안 가이던스 플러그인 완벽 정리 — 설치부터 실전 활용까지](https://www.gpters.org/nocode/post/claude-code-boan-gaideonseu-peulreogeuin-wanbyeog-jeongri----seolcibuteo-ETIduV9ETu3sZkm) — 한국어, 커뮤니티 블로그, 초급 (접속 확인 실패, 검색 스니펫만 확인)
- [Claude Code Security Guidance Plugin Explained](https://www.youtube.com/watch?v=gfUJUIbQ-hs) — 영어, 유튜브 영상 (접속 확인 실패, 검색 결과 목록에만 노출)

※ 위 4건은 이번 조사 시점에 사내 프록시 정책으로 anthropic.com·github.com 외 외부 도메인 접속이 전반적으로 차단되어 있어(example.com 등 무관한 도메인도 동일하게 403) WebFetch로 생존 여부를 직접 검증하지 못했다. 실제 검색 결과에 노출된 URL만 옮겨 적었으며, 다음 학습 시 재확인이 필요하다.

## 자가 점검 질문

1. 편집 시점 패턴 매칭, 턴 종료 diff 리뷰, 커밋 시점 에이전틱 리뷰는 각각 어떤 종류의 취약점을 잘 잡고 어떤 것을 놓치는가?
2. 회계법인 내부 개발팀이 이 플러그인을 도입한다면, `.claude/claude-security-guidance.md`에 가장 먼저 넣어야 할 규칙은 무엇일까?
3. "보증이 아닌 보조 도구"라는 공식 입장에도 불구하고, 실무에서 이 플러그인의 존재가 보안 검토를 소홀히 하는 근거로 오용될 위험은 어떻게 통제할 수 있을까?
