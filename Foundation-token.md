---
name: foundation-token
scope: figma-design
status: stable
---

# Foundation Token

Foundation Token은 디자인 시스템의 원재료입니다. 색상값, 글꼴, 간격, 모서리, 그림자처럼 더 이상 쪼개기 어려운 값을 담습니다.

Foundation Token은 **화면에서 직접 쓰지 않습니다.** 화면과 컴포넌트는 Semantic Token이나 Component Token을 사용합니다.

## 역할

- 브랜드와 무채색 팔레트의 원본을 둔다.
- 글꼴, 간격, 크기, 모서리, 그림자의 기본 단위를 둔다.
- Semantic Token이 참조할 안정적인 재료를 제공한다.

## 기본 규칙

1. Foundation Token은 원시값을 가질 수 있다.
2. 이름은 의미보다 재료에 가깝게 짓는다.
3. 화면 레이어에 직접 연결하지 않는다.
4. 브랜드가 바뀌어도 Semantic Token 이름은 유지될 수 있게 만든다.
5. 너무 많은 단계를 만들지 않는다. 수업에서는 필요한 만큼만 만든다.

## 권장 그룹

| 그룹 | 담는 값 | 예시 이름 |
|---|---|---|
| Color | 브랜드, 무채색, 상태 색의 원본 | `Color/Brand/Primary` |
| Type | 글꼴 이름과 기본 굵기 | `Type/Family/Base` |
| Space | 간격 단위 | `Space/4`, `Space/8` |
| Size | 아이콘, 컨트롤 높이 같은 기본 크기 | `Size/44` |
| Radius | 모서리 반경 | `Radius/8` |
| Border | 선 굵기 | `Border/1` |
| Shadow | 그림자 값 | `Shadow/1` |
| Opacity | 투명도 | `Opacity/Disabled` |

## 작성 템플릿

| 이름 | 값 | 쓰임 | 비고 |
|---|---|---|---|
| `Color/Brand/Primary` |  | 브랜드 색 원본 |  |
| `Color/Neutral/0` |  | 가장 밝은 무채색 |  |
| `Color/Neutral/1000` |  | 가장 어두운 무채색 |  |
| `Type/Family/Base` |  | 기본 글꼴 |  |
| `Space/4` |  | 작은 간격 단위 |  |
| `Radius/8` |  | 기본 모서리 |  |

<!-- CUSTOMIZE: 서비스에 필요한 Foundation Token을 위 표에 추가한다 -->

## 색상 작성 기준

- 브랜드 색은 1개를 먼저 정하고, 필요할 때만 보조 색을 추가한다.
- 무채색은 배경, 선, 텍스트에 충분히 나눠 쓸 수 있을 정도로만 만든다.
- 성공, 경고, 오류 색은 실제 화면에서 필요할 때 추가한다.
- 색 이름에 버튼, 카드, 텍스트 같은 용도를 넣지 않는다. 그런 의미는 Semantic Token에서 정한다.

## 간격 작성 기준

- 기본 단위를 하나 정한다.
- 화면 여백, 섹션 간격, 요소 간격에 쓸 수 있는 단계만 둔다.
- 값이 많아지면 수강생이 선택하기 어려우므로 처음에는 작게 시작한다.

## 확인 질문

Foundation Token을 만들기 전에 아래 질문에 답합니다.

- 브랜드 색은 무엇인가?
- 기본 글꼴은 무엇인가?
- 간격의 기본 단위는 무엇인가?
- 모바일 화면에서 가장 자주 쓰는 좌우 여백은 무엇인가?
- 카드와 버튼의 모서리는 둥근 편인가, 각진 편인가?

## 하지 말 것

- 화면 레이어에 Foundation Token을 직접 쓰지 않는다.
- `Primary Button Color`처럼 용도를 이름에 넣지 않는다.
- 쓰이지 않는 팔레트 단계를 많이 만들지 않는다.
- 코드용 이름이나 CSS 변수 이름을 함께 설계하지 않는다.
