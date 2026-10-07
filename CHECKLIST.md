---
name: checklist
scope: figma-design
status: stable
---

# Figma 디자인 체크리스트

Figma 화면을 만들거나 고친 뒤, 완료 보고 전에 확인합니다.

## A. 작업 범위

| ID | 확인 내용 |
|---|---|
| CHK-01 | Figma 디자인 작업만 했다. 코드, 토큰 JSON, CSS, 빌드 파일은 만들거나 고치지 않았다. |
| CHK-02 | `DESIGN.md`에 없는 중요한 디자인 결정은 먼저 제안하고 승인받았다. |

## B. 변수와 스타일

| ID | 확인 내용 |
|---|---|
| CHK-10 | 색, 글꼴, 간격, 모서리, 그림자는 가능한 한 Figma 변수나 스타일을 썼다. |
| CHK-11 | 변수나 스타일이 없는 값은 임의로 확정하지 않고 필요한 이름을 제안했다. |
| CHK-12 | 텍스트, 아이콘, 테두리는 배경과 충분히 구분된다. |
| CHK-13 | Focus, Error, Disabled, Selected 상태가 시각적으로 구분된다. |
| CHK-14 | 토큰은 Foundation → Semantic → Component → 화면 순서로 연결했다. |
| CHK-15 | 화면 레이어에서 Foundation Token을 직접 쓰지 않았다. |

## C. 화면 구조

| ID | 확인 내용 |
|---|---|
| CHK-20 | 화면은 Frame과 Auto layout 중심으로 구성되어 있다. |
| CHK-21 | Group, 불필요한 Mask, 기본 이름 그대로 남은 레이어가 없다. |
| CHK-22 | 간격과 정렬을 빈 레이어나 눈대중으로 만들지 않았다. |
| CHK-23 | Hug, Fill, Fixed가 의도에 맞게 설정되어 있다. |
| CHK-24 | 화면 폭을 바꿔도 주요 콘텐츠가 깨지지 않는다. |

## D. 텍스트

| ID | 확인 내용 |
|---|---|
| CHK-30 | 텍스트는 Text Style을 우선 사용했다. |
| CHK-31 | 여러 줄 텍스트는 Auto height 또는 의도한 줄 수 제한을 썼다. |
| CHK-32 | 긴 문구를 넣어도 버튼, 카드, 내비게이션이 깨지지 않는다. |

## E. 컴포넌트

| ID | 확인 내용 |
|---|---|
| CHK-40 | 반복되는 UI는 컴포넌트나 인스턴스로 다뤘다. |
| CHK-41 | 인스턴스를 불필요하게 Detach하지 않았다. |
| CHK-42 | 버튼, 입력, 카드, 내비게이션의 상태와 배리언트가 구분된다. |
| CHK-43 | 컴포넌트 안의 레이어 이름은 역할을 알 수 있게 적었다. |
| CHK-44 | 새 컴포넌트의 기본 규칙은 `design-system/component-guidelines/rules.md`의 SH·LA·PR 항목을 확인했다. |
| CHK-45 | 새 컴포넌트의 모범 수치와 구조는 필요할 때 `design-system/component-patterns.md`의 레시피를 확인했다. |

## F. 모드와 접근성

| ID | 확인 내용 |
|---|---|
| CHK-50 | Light/Dark 같은 테마가 있으면 둘 다 확인했다. |
| CHK-51 | Mobile/Desktop 같은 폭 모드가 있으면 주요 화면에서 확인했다. |
| CHK-52 | 터치 대상은 너무 작지 않다. |
| CHK-53 | 중요한 정보가 색 하나에만 의존하지 않는다. |

## 보고 형식

```
검증 결과
- 범위: CHK-01~02 Pass
- 변수와 스타일: CHK-10 Pass · CHK-11 미확인 · CHK-14~15 Pass
- 화면 구조: CHK-20~24 Pass
- 텍스트: CHK-30~32 Pass
- 컴포넌트: CHK-40 Pass · CHK-41 해당 없음 · CHK-44~45 Pass
- 모드와 접근성: CHK-50 미확인 · CHK-51 Pass
- 수정 제안: 필요한 다음 수정 사항
```

<!-- CUSTOMIZE: 팀에서 반복되는 실수가 생기면 항목을 뒤에 추가한다. 기존 번호는 다시 매기지 않는다 -->
