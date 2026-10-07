# 레이아웃 (Fixed / Hug / Fill)

규칙: `rules.md` LA-01 ~ LA-13

## 기본 원칙

- 모든 컨테이너는 Auto Layout 프레임이다 (LA-01).
- **가로는 Fill, 세로는 Hug가 기본이다.** 폭은 부모를 따르고 높이는 내용이 정한다 (LA-02, LA-03).
- Fixed는 크기가 정해져 있어야 하는 요소에만 쓴다: 아이콘, 컨트롤, 바의 높이, 다이얼로그 폭.
- 세로 Fill은 상태 레이어·오버레이처럼 부모를 덮어야 하는 레이어에만 쓴다.

## 요소별 설정

| 요소 | 가로 | 세로 | 규칙 |
|---|---|---|---|
| 버튼 루트 | Hug | Fixed (사이즈별 높이) | LA-04 |
| 버튼 (전체 폭으로 쓸 때) | 인스턴스에서 Fill로 변경 | Fixed | LA-04 |
| 버튼 라벨 | Hug (늘렸을 때 가운데 정렬을 유지하려면 Fill + 가운데 정렬) | Hug | – |
| 아이콘 · 아이콘 버튼 | Fixed | Fixed | LA-05 |
| Checkbox · Radio · Switch 컨트롤 | Fixed | Fixed | LA-05 |
| 도형 · 구분선 | Fixed (가로 구분선은 Fill × 1) | Fixed | LA-05 |
| Tag · Chip · Badge | Hug | Fixed | LA-06 |
| Tooltip | Hug | Hug | LA-06 |
| 입력 · Select 트리거 | Fill | Hug | LA-07 |
| 입력 안의 텍스트 | Fill | Hug | LA-07 |
| 리스트 아이템 · 메뉴 아이템 | Fill | Hug | LA-07 |
| 카드 | Fill (그리드 안) / Fixed (단독) | Hug | LA-08 |
| Dialog | Fixed | Hug | LA-09 |
| Dialog 본문 텍스트 | Fill | Hug | LA-09 |
| 앱 바 · 내비 바 · 탭 바 | Fill | Fixed | LA-10 |

## 텍스트 리사이즈 (LA-11)

| 설정 | 언제 |
|---|---|
| Auto width | 한 줄 텍스트: 버튼 라벨, 태그, 짧은 라벨 |
| Auto height + 가로 Fill | 여러 줄 텍스트: 본문, 설명, 도움말 |
| Fixed + Truncate | 폭이 정해진 곳의 말줄임: 메뉴, 리스트 |

## 레이어 구조 (LA-12)

배경, 상태, 내용을 레이어로 분리한다.

```
Button (루트, 터치 영역)
└─ Container (배경 · radius · stroke)
   ├─ State layer (Absolute 또는 Fill/Fill, hover·pressed 오버레이)
   └─ Content (패딩 · 간격)
      ├─ Icon
      └─ Label
```

## Absolute position (LA-13)

- 쓰는 곳: 상태 레이어, 포커스 링, 배지 점, 툴팁 화살표.
- 콘텐츠 배치에는 쓰지 않는다. 내용이 바뀌면 겹치거나 어긋난다.
