---
name: component-token
scope: figma-design
status: stable
---

# Component Token

Component Token은 특정 컴포넌트 안에서 쓰는 값입니다. 버튼, 카드, 입력, 내비게이션처럼 반복되는 UI의 배경, 텍스트, 간격, 모서리, 상태를 안정적으로 관리합니다.

Component Token은 Semantic Token을 참조합니다.

## 역할

- 컴포넌트의 배리언트와 상태를 일관되게 만든다.
- 같은 컴포넌트를 여러 화면에서 반복해도 값이 흔들리지 않게 한다.
- 화면을 만드는 에이전트가 컴포넌트 안의 세부 값을 추측하지 않게 한다.

## 기본 규칙

1. Component Token은 Semantic Token을 참조한다.
2. 컴포넌트 이름을 가장 앞에 둔다.
3. 배리언트, 파트, 속성, 상태 순서로 이름을 만든다.
4. 컴포넌트 안에 원시값을 직접 넣지 않는다.
5. 배리언트가 많아지면 실제 화면에서 필요한 것만 남긴다.

## 이름 구조

```text
컴포넌트/배리언트/파트/속성/상태
```

예시:

```text
Button/Primary/Container/Fill/Default
Button/Primary/Container/Fill/Pressed
Button/Primary/Label/Text/Default
Card/Default/Container/Fill/Default
Input/Default/Container/Border/Focus
```

## 컴포넌트 파트

| 파트 | 의미 |
|---|---|
| Container | 컴포넌트의 바깥 면 |
| Label | 주요 텍스트 |
| Icon | 아이콘 |
| Border | 외곽선 |
| Indicator | 배지, 선택 표시, 알림점 |

필요한 파트만 사용합니다. 모든 컴포넌트에 같은 파트를 억지로 넣지 않습니다.

## 상태

| 상태 | 의미 |
|---|---|
| Default | 기본 |
| Hover | 마우스를 올림 |
| Pressed | 누름 |
| Focus | 키보드 포커스 |
| Disabled | 비활성 |
| Selected | 선택됨 |
| Error | 오류 |

Figma 과제에서 Hover가 필요 없다면 만들지 않아도 됩니다. 실제 시연할 상태만 만듭니다.

## 버튼 토큰 템플릿

| 이름 | 참조할 Semantic Token | 쓰는 곳 |
|---|---|---|
| `Button/Primary/Container/Fill/Default` |  | Primary 버튼 배경 |
| `Button/Primary/Container/Fill/Pressed` |  | Primary 버튼 누름 |
| `Button/Primary/Label/Text/Default` |  | Primary 버튼 텍스트 |
| `Button/Accent/Container/Fill/Default` |  | Accent 버튼 배경 |
| `Button/Disabled/Container/Fill/Default` |  | 비활성 버튼 배경 |
| `Button/Disabled/Label/Text/Default` |  | 비활성 버튼 텍스트 |

<!-- CUSTOMIZE: 서비스에 필요한 Button Token을 위 표에 추가한다 -->

## 카드 토큰 템플릿

| 이름 | 참조할 Semantic Token | 쓰는 곳 |
|---|---|---|
| `Card/Default/Container/Fill/Default` |  | 카드 배경 |
| `Card/Default/Container/Border/Default` |  | 카드 외곽선 |
| `Card/Default/Container/Radius/Default` |  | 카드 모서리 |
| `Card/Default/Container/Padding/Default` |  | 카드 안쪽 여백 |

<!-- CUSTOMIZE: 서비스에 필요한 Card Token을 위 표에 추가한다 -->

## 입력 토큰 템플릿

| 이름 | 참조할 Semantic Token | 쓰는 곳 |
|---|---|---|
| `Input/Default/Container/Fill/Default` |  | 입력 배경 |
| `Input/Default/Container/Border/Default` |  | 입력 기본 선 |
| `Input/Default/Container/Border/Focus` |  | 입력 포커스 선 |
| `Input/Error/Container/Border/Default` |  | 입력 오류 선 |
| `Input/Default/Label/Text/Default` |  | 입력 라벨 |
| `Input/Default/Placeholder/Text/Default` |  | 플레이스홀더 |

<!-- CUSTOMIZE: 서비스에 필요한 Input Token을 위 표에 추가한다 -->

## 만들기 순서

1. 컴포넌트가 실제로 반복되는지 확인한다.
2. `design-system/component-patterns.md`에서 같은 컴포넌트의 구조와 수치 범위를 확인한다.
3. 필요한 배리언트와 상태만 적는다.
4. 파트를 나눈다.
5. 각 파트가 어떤 Semantic Token을 참조할지 정한다.
6. Figma 컴포넌트에 연결한다.
7. 인스턴스에서 값이 덮어써지지 않는지 확인한다.

## 하지 말 것

- Component Token이 Foundation Token을 직접 참조하지 않는다.
- 컴포넌트마다 같은 의미의 색을 새로 만들지 않는다.
- 상태가 구분되지 않는 토큰을 여러 개 만들지 않는다.
- 인스턴스에서 토큰으로 연결된 속성을 임의로 덮어쓰지 않는다.
