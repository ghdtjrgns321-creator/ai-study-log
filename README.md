# AI 학습 로그

**AI 개념 매일 학습 저장소**. 매일 아침 7시, 클라우드 예약 에이전트가 선정한 주제 3~5개를 검색, 가공하여 브리핑을 작성하고 자동 커밋한다.

## 구조

```
ai-study-log/
├─ README.md                  이 문서
├─ covered.md                 다룬 주제 (중복 방지 겸 학습 이력 인덱스)
├─ agent/
│  ├─ instructions.md         에이전트 지시서(선정 규칙·형식·커밋)
│  └─ template.md             브리핑 출력 형식
└─ briefings/
   └─ YYYY-MM-DD/
      ├─ NN-슬러그.md              (그날 주제별 브리핑, 01부터 번호)
      └─ videos/{슬러그}.md        (그날 브리핑에 인용된 유튜브 영상의 상세 요약)
```

## 매일 어떻게 채워지나

1. 에이전트가 저장소를 클론한다.
2. `agent/instructions.md`를 읽고 그대로 수행한다 — `covered.md`로 중복을 피하고, 웹 검색으로 후보를
   모아 품질순 3~5개를 고른 뒤 `agent/template.md` 형식으로 작성한다.
3. `covered.md`를 갱신하고 커밋·푸시한다.