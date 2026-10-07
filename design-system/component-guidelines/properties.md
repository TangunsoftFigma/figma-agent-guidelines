# 컴포넌트 프로퍼티

규칙: `rules.md` PR-01 ~ PR-09

## 유형별 용도

| 유형 | 용도 | 쓰지 않는 경우 | 예 |
|---|---|---|---|
| Boolean | 레이어 보이기/숨기기 | 색·크기 변경 | `Show icon`, `Show helper text`, `Show divider` |
| Text | 사용자에게 보이는 문구 | 바뀌지 않는 장식 문자 | `Label`, `Placeholder`, `Helper text` |
| Instance swap | 아이콘·아바타 교체 | 레이아웃이 달라지는 교체 | `Icon`, `Leading icon`, `Trailing icon` |
| Nested instance 노출 | 하위 컴포넌트 속성을 상위에서 편집 | 노출할 필요 없는 내부 부품 | 리스트 아이템 안의 Checkbox |
| Slot | 내용이 자유로운 영역 | 아이콘·정해진 요소 | `Content`, `Actions` |

## 규칙 설명

- **PR-01 Boolean 이름**: `Show X`(디자이너가 읽기 쉬움)와 `hasX`(코드 prop과 같음) 중 하나로 라이브러리 전체를 통일한다. 코드와 연결할 계획이면 `hasX`가 유리하다.
- **PR-02 아이콘 쌍**: 선택형 아이콘은 Boolean(`Show icon`)과 Instance swap(`Icon`)을 함께 만든다. Boolean은 표시 여부, Instance swap은 어떤 아이콘인지를 맡는다.
- **PR-03 Preferred values**: Instance swap마다 교체 후보를 지정한다. 지정하지 않으면 아무 컴포넌트나 들어갈 수 있다.
- **PR-04 Text 연결**: 화면에 보이는 문구는 모두 Text 프로퍼티에 연결한다. 연결하지 않으면 레이어를 찾아 들어가 직접 고쳐야 한다.
- **PR-05 중첩 노출**: 하위 컴포넌트(체크박스, 버튼, 아바타)는 Expose nested instances로 노출한다. 상위 인스턴스에서 바로 상태를 바꿀 수 있다.
- **PR-06 Slot**: 카드 본문, 다이얼로그 내용, 메뉴 리스트처럼 무엇이 들어갈지 정해지지 않은 영역에만 쓴다. 아이콘은 Instance swap으로 처리한다.
- **PR-07 비공개 빌딩 블록**: 다른 컴포넌트를 만들기 위한 부품은 이름 앞에 `.` 또는 `_`를 붙여 라이브러리에 공개되지 않게 한다.
- **PR-08 이름 확인**: 인스턴스를 수정하기 전에 컴포넌트의 프로퍼티 정의를 먼저 읽는다. 이름을 추측하지 않는다.
- **PR-09 수정 순서**: Text → Instance swap → Slot → Override 순으로 시도한다. Detach는 하지 않는다.

## 이름 규칙

| 대상 | 규칙 | 예 |
|---|---|---|
| Boolean | `Show X` 또는 `hasX` (하나로 통일) | `Show icon` / `hasLeadingIcon` |
| Text | 역할 이름 | `Label`, `Helper text` |
| Instance swap | 위치 이름 | `Leading icon`, `Trailing icon` |
| Slot | 영역 이름 | `Content`, `Actions`, `Header` |

- 영어로 쓰고, 이모지나 기호 접두어는 쓰지 않는다.
- 오타가 없는지 확인한다. 오타는 코드 연결과 Agent 검색을 깨뜨린다.
