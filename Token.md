---
name: token-overview
scope: figma-design
status: stable
---

# 토큰 구조

이 문서는 Figma 변수와 스타일을 어떤 순서로 만들고 상속할지 정리합니다. 이 레포의 토큰 문서는 코드 생성이나 JSON 동기화가 아니라, **Figma 디자인 작업에서 같은 결정을 반복하지 않기 위한 기준**입니다.

## 전체 구조

토큰은 아래 순서로만 이어집니다.

```text
Foundation Token → Semantic Token → Component Token → Figma 화면
```

| 단계 | 역할 | 화면에서 직접 사용 |
|---|---|---|
| Foundation | 색, 글꼴, 간격 같은 원재료 | 사용하지 않음 |
| Semantic | 화면에서 쓰는 의미 단위 | 사용함 |
| Component | 특정 컴포넌트의 속성 | 컴포넌트 안에서 사용함 |

## 상속 규칙

1. Foundation Token은 원시값을 가진다.
2. Semantic Token은 Foundation Token을 참조한다.
3. Component Token은 Semantic Token을 참조한다.
4. 화면 레이어는 Semantic Token 또는 Component Token만 사용한다.
5. 한 단계를 건너뛰지 않는다.
6. 토큰 이름에는 값의 생김새보다 역할을 적는다.

## 예시 흐름

```text
Foundation: Color/Brand/Primary
↓
Semantic: Fill/Accent/Default
↓
Component: Button/Accent/Container/Default
↓
Figma: Accent Button 인스턴스의 배경
```

## 컬렉션 나누기

| 컬렉션 | 담는 것 | 문서 |
|---|---|---|
| Foundation | 원재료 값 | `Foundation-token.md` |
| Semantic | 화면에서 쓰는 의미 | `Semantic-token.md` |
| Component | 컴포넌트별 결정 | `Component-token.md` |

## 이름 규칙

- `/`로 계층을 나눈다.
- 같은 계층에서는 단어 형식을 맞춘다.
- 토큰 이름은 짧게 쓰되, 역할을 알 수 있어야 한다.
- 색 이름보다 용도를 우선한다.
- 상태는 마지막에 둔다.

좋은 이름:

```text
Surface/Default
Text/Primary
Fill/Accent/Pressed
Button/Primary/Container/Default
```

피할 이름:

```text
Blue/500
Light Gray Background
Big Button Padding
Dark Mode Text
```

## 모드 규칙

Light, Dark, Mobile, Desktop처럼 상황에 따라 값이 달라지는 경우 새 토큰을 만들지 않고 같은 토큰의 모드로 관리합니다.

```text
좋음: Surface/Default 안에 Light 값과 Dark 값이 있음
피함: Surface/Default/Light, Surface/Default/Dark를 따로 만듦
```

## 새 토큰을 만들 때

1. 같은 역할의 토큰이 이미 있는지 먼저 찾는다.
2. 없으면 어느 단계의 토큰인지 정한다.
3. 이름을 역할 중심으로 짓는다.
4. 어떤 화면이나 컴포넌트에서 쓰는지 적는다.
5. Light/Dark, Mobile/Desktop 같은 모드가 필요한지 확인한다.
6. 연결 순서가 Foundation → Semantic → Component를 지키는지 확인한다.

## 제안 형식

새 토큰이 필요하면 아래 형식으로 먼저 제안합니다.

```text
제안 토큰
- 이름:
- 단계: Foundation / Semantic / Component
- 필요한 이유:
- 참조할 토큰:
- 쓰는 곳:
- 필요한 모드:
```

## 금지 사항

- 화면에서 Foundation Token을 직접 쓰지 않는다.
- 컴포넌트 안에 원시 색상이나 원시 간격을 직접 넣지 않는다.
- 같은 의미의 토큰을 이름만 다르게 중복 생성하지 않는다.
- Light/Dark를 토큰 이름으로 나누지 않는다.
- 수업 범위를 넘어 코드용 토큰, CSS 변수, JSON 파일을 만들지 않는다.
