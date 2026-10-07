# Figma 컴포넌트 가이드라인

Figma에서 컴포넌트를 만들고 수정할 때 따르는 규칙이다.

## 파일 구성

| 파일 | 대상 | 내용 |
|---|---|---|
| `rules.md` | Agent 필수 · 사람 | 규칙 원문 (ID 부여). 규칙은 여기에만 쓴다 |
| `shape.md` | 사람 · Agent(필요 시) | 크기·패딩·radius·터치 영역 |
| `layout.md` | 사람 · Agent(필요 시) | Fixed / Hug / Fill, 레이어 구조 |
| `properties.md` | 사람 · Agent(필요 시) | Boolean · Text · Instance swap · Nested · Slot |

## 읽는 순서

- **Agent**: 컴포넌트를 만들거나 수정할 때 `rules.md`를 먼저 읽는다. 설명이 필요할 때만 주제 파일을 연다.
- **수강생**: shape → layout → properties 순으로 읽고 `rules.md`로 정리한다.

## 새 컴포넌트 리뷰 체크리스트

- [ ] 높이가 8px 스케일이고 같은 크기의 다른 컨트롤과 높이가 같다 (SH-01, SH-02)
- [ ] 가로 패딩 ≈ 높이 × 0.35, 세로 패딩 0 (SH-03, SH-04)
- [ ] 터치 영역 44 이상 (SH-07)
- [ ] 패딩·간격·radius·색이 변수에 바인딩되어 있다 (SH-09)
- [ ] 모든 컨테이너가 Auto Layout이고 사이징이 규칙과 일치한다 (LA-01 ~ LA-10)
- [ ] 여러 줄 텍스트는 Auto height + 가로 Fill (LA-11)
- [ ] 아이콘은 Boolean + Instance swap 쌍, Preferred values 지정 (PR-02, PR-03)
- [ ] 보이는 문구가 모두 Text 프로퍼티에 연결되어 있다 (PR-04)
- [ ] 하위 컴포넌트가 노출되어 있다 (PR-05)
- [ ] 빌딩 블록은 비공개 접두어 (PR-07)

## 수정 규칙

- 규칙을 바꿀 때는 `rules.md`를 먼저 고치고, 다른 파일은 ID로만 참조한다. 같은 규칙 문장을 두 곳에 쓰지 않는다.
- 규칙 ID는 재사용하지 않는다. 폐기한 규칙은 `~~SH-04~~ (폐기: 사유)`로 남긴다.
