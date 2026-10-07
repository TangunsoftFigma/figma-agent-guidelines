# Figma Agent Guidelines (디자인 전용 실습판)

Figma에서 화면과 컴포넌트를 디자인할 때 AI 에이전트가 읽을 최소 가이드입니다.

이 버전은 수강생 실습용으로 범위를 줄였습니다. 코드 작성, 토큰 JSON 동기화, CSS 빌드, 자동 검사, 배포는 다루지 않습니다. 수강생은 `DESIGN.md`를 채우고, 에이전트는 그 내용을 기준으로 Figma 디자인 작업만 돕습니다.

## 가장 먼저 할 일

`DESIGN.md`를 열고 아래 5개 항목을 먼저 작성합니다.

1. 서비스 한 줄 정의와 대상 사용자
2. 무드 키워드 3~5개와 피하고 싶은 무드
3. 컬러 방향
4. 형태와 깊이
5. Key Characteristics 초안 3개

## 들어 있는 것

```
AGENTS.md      에이전트가 먼저 읽는 공통 규칙
DESIGN.md      수강생이 직접 채우는 디자인 브리프
Token.md       토큰의 전체 구조와 상속 규칙
Foundation-token.md   원재료 토큰 작성 규칙
Semantic-token.md     화면에서 쓰는 의미 토큰 작성 규칙
Component-token.md    컴포넌트 토큰 작성 규칙
design-system/component-guidelines/README.md   컴포넌트 제작·수정 가이드 묶음
design-system/component-guidelines/rules.md    컴포넌트 제작·수정 시 Agent 필수 규칙
design-system/component-guidelines/shape.md    크기·패딩·radius·터치 영역
design-system/component-guidelines/layout.md   Fixed / Hug / Fill, 레이어 구조
design-system/component-guidelines/properties.md   Boolean · Text · Instance swap · Nested · Slot
design-system/component-patterns.md   공개 디자인 시스템 기반 컴포넌트 레시피
design-system/research/component-benchmark.json   레시피 원자료
CHECKLIST.md   Figma 작업 완료 전 점검표
LICENSE        오픈소스 라이선스
```

## 사용 방법

1. `DESIGN.md`의 빈 칸을 내 서비스에 맞게 채웁니다.
2. 토큰을 만들 때는 `Token.md` → `Foundation-token.md` → `Semantic-token.md` → `Component-token.md` 순서로 봅니다.
3. 컴포넌트를 만들거나 고칠 때는 `design-system/component-guidelines/rules.md`를 먼저 읽습니다.
4. 컴포넌트의 모범 수치와 구조가 필요하면 `design-system/component-patterns.md`를 참고합니다.
5. Figma에서 필요한 변수, 스타일, 컴포넌트를 만듭니다.
6. 에이전트에게 아래처럼 요청합니다.

   > AGENTS.md와 DESIGN.md를 먼저 읽고, 이 기준으로 Figma 화면을 만들어 줘. 컴포넌트를 만들거나 고칠 때는 component-guidelines/rules.md를 먼저 보고, 필요한 주제 파일만 추가로 읽어 줘. 끝나면 CHECKLIST.md 기준으로 점검 결과를 보고해 줘.

7. 작업 후 `CHECKLIST.md`로 화면을 확인합니다.

## 이 레포가 하지 않는 것

- 코드 생성이나 코드 품질 검사
- Figma 토큰 JSON 내보내기·동기화
- CSS 변수 빌드
- npm 명령 실행
- GitHub Actions 자동 검사
- Figma 배리어블의 무단 생성, 삭제, 이름 변경

## 수강생이 주로 바꿀 곳

| 파일 | 바꿀 내용 |
|---|---|
| `DESIGN.md` | 서비스 분위기, 색, 타이포그래피, 컴포넌트, 레이아웃 원칙 |
| `Foundation-token.md` | 브랜드 색, 글꼴, 간격, 모서리 같은 원재료 |
| `Semantic-token.md` | 화면에서 직접 쓰는 색, 간격, 글자 의미 |
| `Component-token.md` | 버튼, 카드, 입력 같은 컴포넌트별 값 |
| `design-system/component-guidelines/` | 컴포넌트 제작·수정 규칙, 크기, 레이아웃, 프로퍼티 |
| `design-system/component-patterns.md` | 공개 디자인 시스템 기반 컴포넌트 수치와 구조 |
| `CHECKLIST.md` | 팀이나 과제에서 반복되는 실수 |
| `AGENTS.md` | 수업 운영 방식에 맞춘 에이전트 작업 규칙 |

`LICENSE`는 오픈소스 배포에 필요한 파일이므로 그대로 둡니다.
