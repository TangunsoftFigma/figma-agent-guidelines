---
name: semantic-token
scope: figma-design
status: stable
---

# Semantic Token

Semantic Token은 화면에서 실제로 사용하는 의미 단위입니다. Foundation Token의 원재료를 받아서 "어디에 쓰는 값인지"를 정합니다.

Figma 화면 레이어는 가능한 한 Semantic Token을 사용합니다.

## 역할

- 화면 배경, 텍스트, 아이콘, 선, 버튼 채움 같은 역할을 이름으로 표현한다.
- Light/Dark 같은 테마 차이를 같은 토큰의 모드로 관리한다.
- Mobile/Desktop 같은 폭 차이를 같은 토큰의 모드로 관리한다.
- 화면을 만들 때 디자이너와 에이전트가 같은 이름으로 판단하게 한다.

## 기본 규칙

1. Semantic Token은 Foundation Token을 참조한다.
2. 이름에는 색상값보다 역할을 적는다.
3. 화면에서 직접 쓰는 토큰이므로 너무 추상적으로 만들지 않는다.
4. 같은 역할은 모드로 관리하고, 이름을 나눠 중복 생성하지 않는다.
5. 텍스트, 아이콘, 테두리는 어떤 배경 위에서 쓰는지 함께 정한다.

## 권장 그룹

| 그룹 | 역할 | 예시 이름 |
|---|---|---|
| Surface | 화면과 카드 같은 면 | `Surface/Default` |
| Fill | 버튼, 선택 상태, 상태 배경 | `Fill/Accent/Default` |
| Text | 텍스트 색 | `Text/Primary` |
| Icon | 아이콘 색 | `Icon/Secondary` |
| Border | 외곽선과 구분선 | `Border/Default` |
| Overlay | Dim, Scrim 같은 덮개 | `Overlay/Scrim` |
| Typography | Text Style을 구성하는 크기와 줄 높이 | `Font Size/Body` |
| Spacing | 화면 여백과 간격 | `Gap/Section` |
| Radius | 용도별 모서리 | `Corner/Container` |

## 색상 토큰 템플릿

| 이름 | 참조할 Foundation | 쓰는 곳 | 짝 또는 조건 |
|---|---|---|---|
| `Surface/Default` |  | 화면 기본 배경 |  |
| `Surface/Raised` |  | 카드, 시트 |  |
| `Text/Primary` |  | 핵심 텍스트 | `Surface/Default`, `Surface/Raised` 위 |
| `Text/Secondary` |  | 보조 텍스트 |  |
| `Fill/Primary/Default` |  | 가장 중요한 행동 |  |
| `Fill/Accent/Default` |  | 브랜드 강조 행동 |  |
| `Border/Default` |  | 기본 외곽선 |  |
| `Border/Focus` |  | 포커스 링 |  |

<!-- CUSTOMIZE: 서비스에 필요한 Semantic Color Token을 위 표에 추가한다 -->

## 반응형 토큰 템플릿

| 이름 | Mobile | Desktop | 쓰는 곳 |
|---|---|---|---|
| `Margin/Page` |  |  | 화면 좌우 여백 |
| `Gap/Section` |  |  | 큰 섹션 사이 |
| `Gap/Stack` |  |  | 세로 요소 사이 |
| `Inset/Container` |  |  | 카드 안쪽 여백 |
| `Font Size/Body` |  |  | 본문 |
| `Line Height/Body` |  |  | 본문 줄 높이 |

<!-- CUSTOMIZE: 서비스에 필요한 Semantic Responsive Token을 위 표에 추가한다 -->

## 모드 작성 기준

| 모드 | 기준 |
|---|---|
| Light | 밝은 배경에서 기본 사용 |
| Dark | 어두운 배경에서 기본 사용 |
| Mobile | 0~767px 화면 |
| Desktop | 768px 이상 화면 |

수업에서 Tablet이 필요하지 않다면 만들지 않아도 됩니다. 필요한 모드만 작게 시작합니다.

## 짝 규칙

전경 토큰은 어떤 배경 위에서 쓰는지 함께 정합니다.

```text
Text/Primary → Surface/Default, Surface/Raised 위에서 사용
Text/On Accent → Fill/Accent/Default 위에서 사용
Icon/Disabled → Surface/Default 위에서 사용
```

## 하지 말 것

- `Blue Text`, `White Background`처럼 외형만 적은 이름을 만들지 않는다.
- Light와 Dark를 이름으로 나눠 만들지 않는다.
- 배경과 전경의 짝을 정하지 않은 채 텍스트 색을 추가하지 않는다.
- 실제 화면에서 쓰지 않는 의미 토큰을 미리 많이 만들지 않는다.
