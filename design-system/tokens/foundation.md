---
name: foundation
layer: foundation
collection: Foundation
modes: [Default]
values_source: tokens/foundation.tokens.json
status: stable
---

# Foundation 토큰

디자인에 쓸 수 있는 재료의 전체 목록입니다. 이 레이어의 토큰은 의미를 갖지 않으며 "어디에 쓰는가"를 결정하지 않습니다. 결정은 [Semantic Color](semantic-color.md)와 [Semantic Responsive](semantic-responsive.md)에서 합니다.

## 규칙

- **[FND-01] MUST NOT** Foundation 토큰을 레이어나 컴포넌트 속성에 직접 바인딩하지 않는다.
  - 이유: 모드 전환은 Semantic에서 일어난다. 직접 바인딩한 값은 다크 모드나 다른 브레이크포인트에서 바뀌지 않는다.
- **[FND-02] MUST** 모든 Foundation 변수는 발행 숨김(Hide from publishing)을 켜고 스코프를 모두 끈다.
  - 이유: 피커에 나타나지 않아야 사람과 에이전트 모두 실수로 고를 수 없다. 스코프를 꺼도 배리어블 편집기에서 alias 대상으로는 계속 쓸 수 있다.
- **[FND-03] MUST NOT** 스케일 사이 값을 추가하지 않는다. 새 값이 필요하면 `design-system/decisions/`에 ADR을 먼저 쓴다.
  - 이유: 스케일 밖 값이 하나 생기면 "가장 가까운 값"을 고르는 기준이 무너진다.
- **[FND-04] MUST** Foundation 토큰은 원시값만 가진다. 다른 토큰을 참조하지 않는다.
  - 이유: 참조 사슬의 끝이 항상 Foundation이어야 값의 출처를 한 번에 찾을 수 있다.
- **[FND-05] MUST** 숫자 이름은 값 자체다 (`Space/16` = 16px). 색 스케일만 단계 번호(1–12)를 쓴다.
  - 이유: AI가 이름에서 값을 계산할 필요가 없다. 값이 바뀌면 이름도 바뀌므로(새 토큰) 이름이 거짓말을 하지 않는다. 소수점 단계(0.5)가 경로에 들어가지 않아 DTCG 별칭 문법과도 충돌하지 않는다.

## 그룹 구성

| 그룹 | 토큰 경로 | Figma 타입 | 단위 |
|---|---|---|---|
| Color | `Color/{Scale}/{1–12}`, `Color/White`, `Color/Black`, `Color/Black Alpha/{1–12}` | Color | sRGB hex |
| Layout | `Space/*`, `Size/*`, `Breakpoint/*` | Number | px |
| Shape | `Radius/*`, `Stroke/*` | Number | px |
| Typography | `Type/Family/*`, `Type/Size/*`, `Type/Line Height/*`, `Type/Weight/*` | String / Number | px, 굵기 수치 |
| Motion | 확장 슬롯 (이 키트에서는 비워 둠) | — | — |

- 타이포 조합(글꼴·크기·줄 높이·굵기)은 배리어블이 아니라 **Text Style**이 묶는다. → [Text Style 바인딩](semantic-responsive.md#text-style-바인딩)
- 그림자는 **Effect Style**로 관리하고, 그림자 색만 `Shadow/*` Semantic 토큰에 바인딩한다.
- `Breakpoint/*`는 Figma에서 바인딩하지 않는다. 코드의 미디어 쿼리 기준이자 Semantic Responsive 모드 이름의 기준이다.

<!-- CUSTOMIZE: 모션을 다루려면 Duration·Easing 그룹을 추가하고 tokens/README.md의 Variable/Style 구분도 함께 고친다 -->

## 스케일 생성 규칙

### Color

- 단계는 12개다. 단계마다 OKLCH 명도(L)를 정하고, 색상(h)은 스케일마다 고정하며, 채도(C)는 9단계를 정점(C 정점)으로 두고 단계별 비율을 곱한다.
- 라이트 스케일(`Gray`)과 다크 스케일(`Gray Dark`)은 **같은 번호가 같은 용도**를 갖는다. 그래서 다크 모드 alias는 대부분 "같은 번호의 Dark 스케일"로 정해진다.
- sRGB 범위를 벗어나는 값은 명도를 유지한 채 채도만 줄여 맞춘다.
- `Black Alpha`는 겹침 전용이다 (딤, 그림자 색). 불투명한 면에는 쓰지 않는다.

생성 파라미터 (이 키트의 샘플 팔레트가 이 값으로 만들어졌다):

| 스케일 | h | C 정점 | 단계별 L (1 → 12) |
|---|---|---|---|
| Gray | 260 | 0.006 | 0.993 0.982 0.962 0.943 0.922 0.896 0.861 0.8 0.56 0.52 0.44 0.22 |
| Gray Dark | 260 | 0.006 | 0.18 0.205 0.245 0.275 0.305 0.345 0.405 0.49 0.6 0.66 0.79 0.95 |
| Blue | 258 | 0.19 | 0.993 0.982 0.962 0.943 0.922 0.896 0.861 0.8 0.55 0.5 0.46 0.3 |
| Blue Dark | 258 | 0.19 | 0.18 0.205 0.245 0.275 0.305 0.345 0.405 0.49 0.5 0.54 0.8 0.94 |
| Red | 27 | 0.2 | 0.993 0.982 0.962 0.943 0.922 0.896 0.861 0.8 0.56 0.51 0.47 0.31 |
| Red Dark | 27 | 0.2 | 0.18 0.205 0.245 0.275 0.305 0.345 0.405 0.49 0.51 0.55 0.78 0.93 |
| Green | 150 | 0.16 | 0.993 0.982 0.962 0.943 0.922 0.896 0.861 0.8 0.62 0.57 0.48 0.31 |
| Green Dark | 150 | 0.16 | 0.18 0.205 0.245 0.275 0.305 0.345 0.405 0.49 0.58 0.62 0.8 0.94 |
| Amber | 75 | 0.165 | 0.993 0.982 0.962 0.943 0.922 0.896 0.861 0.8 0.8 0.76 0.5 0.33 |
| Amber Dark | 75 | 0.165 | 0.18 0.205 0.245 0.275 0.305 0.345 0.405 0.49 0.78 0.82 0.86 0.96 |

- 단계별 채도 비율 (라이트): 0.015 0.035 0.08 0.12 0.17 0.22 0.3 0.45 1.0 1.0 0.85 0.45
- 단계별 채도 비율 (다크): 0.1 0.13 0.22 0.28 0.33 0.38 0.45 0.6 1.0 1.0 0.7 0.25

<!-- CUSTOMIZE: 브랜드 색을 바꾸려면 Blue 행의 h와 C 정점만 바꿔 다시 생성한다. L 열은 대비 보장의 근거이므로 바꿨다면 npm run tokens:check로 짝 대비를 다시 확인한다 -->

### Layout · Shape · Typography

- `Space`는 4px 단위로 늘어나고, 2px은 아이콘과 텍스트 미세 조정 전용이다.
- `Size`는 컨트롤과 아이콘 크기다. 44는 최소 터치 영역이다.
- `Radius/Full`은 양끝이 완전히 둥근 형태(알약형)를 위한 값이다.
- 타이포 크기와 줄 높이는 짝으로 쓰도록 Semantic에서 묶는다. Foundation에서는 짝을 정하지 않는다.
- 실제 값 목록은 아래 [값 표](#값-표)에 자동으로 만들어진다.

<!-- CUSTOMIZE: 브랜드 글꼴은 Type/Family/Sans 값을, 서비스의 분기점은 Breakpoint/Tablet·Desktop 값을 Figma에서 바꾼다 -->

## 단계 용도 가이드 (Semantic 작성용)

| 단계 | 용도 |
|---|---|
| 1 | 앱 기본 바탕 |
| 2 | 은은한 구역 바탕 |
| 3 | UI 요소 바탕 (기본) |
| 4 | UI 요소 바탕 (호버) |
| 5 | UI 요소 바탕 (눌림·선택) |
| 6 | 구분선 |
| 7 | 장식 외곽선 |
| 8 | 비활성 전경 (텍스트·아이콘) |
| 9 | 솔리드 채움, 식별이 필요한 외곽선 (3:1) |
| 10 | 솔리드 채움 호버, 회색에서는 가장 낮은 위계의 텍스트 |
| 11 | 보조 텍스트, 유채색 텍스트·아이콘 |
| 12 | 기본 텍스트, 고대비 채움 |

이 표는 Semantic 토큰의 alias 대상을 고를 때만 쓴다. 화면 작업의 근거로 쓰지 않는다 (FND-01). 표와 다르게 고른 경우는 Semantic 문서 해당 항목의 `비고`에 이유를 적는다.

## 값 표

### 색 스케일

<!-- GENERATED:START id=foundation-colors — tokens/*.tokens.json에서 생성됨. 직접 수정하지 말고 npm run tokens:sync -->
| 스케일 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Gray | #fdfdfd | #f9f9f9 | #f2f2f3 | #ececec | #e5e5e6 | #dcdddd | #d0d1d2 | #bdbebf | #727578 | #67696c | #515355 | #1a1b1c |
| Gray Dark | #111212 | #171717 | #202021 | #272828 | #2e2f30 | #38393a | #48494a | #5f6062 | #7e8084 | #909296 | #b9bbbd | #eeeeef |
| Blue | #fcfdff | #f6f9fe | #ecf3fd | #e3edfc | #d8e6fb | #ccdef9 | #bbd3f7 | #9cc0f5 | #156cdd | #005dca | #0b53b0 | #0f2d58 |
| Blue Dark | #0c121a | #101722 | #142134 | #162841 | #1a2f4e | #20395e | #2a4977 | #3460a0 | #005dca | #1069da | #95c0ff | #e0ecff |
| Red | #fffcfc | #fef7f6 | #fdefed | #fce7e4 | #fbddd9 | #f9d2cd | #f6c3bc | #f2a89e | #d02c2a | #be1219 | #a51f1e | #551915 |
| Red Dark | #1a0e0d | #221211 | #331815 | #3f1c18 | #4b201c | #5a2823 | #72332e | #994139 | #be1219 | #cc2827 | #ff968a | #ffe0db |
| Green | #fcfdfc | #f7faf7 | #edf5ee | #e4f0e5 | #d9ebdc | #cde4d1 | #bcdbc1 | #9dcba6 | #20a04e | #009041 | #007131 | #0e3a1c |
| Green Dark | #0d140e | #101a12 | #142517 | #162e1c | #1a3621 | #204228 | #295434 | #326f42 | #009342 | #20a04e | #87d297 | #d9f3dd |
| Amber | #fefcfb | #fbf9f5 | #f8f1e9 | #f4ebde | #f1e3d1 | #ebdac3 | #e5cdae | #dab788 | #fbac16 | #eba000 | #865900 | #4a2f00 |
| Amber Dark | #161109 | #1d160c | #2b1e0b | #35240b | #3f2b0b | #4c340d | #604213 | #81570c | #f4a500 | #ffb334 | #fdc677 | #ffefdb |
| Black Alpha | #000000 1.2% | #000000 2.7% | #000000 4.7% | #000000 7.1% | #000000 9% | #000000 11.4% | #000000 14.1% | #000000 22% | #000000 44% | #000000 48% | #000000 56% | #000000 90% |

| 토큰 | 값 |
|---|---|
| `Color/White` | #ffffff |
| `Color/Black` | #000000 |
<!-- GENERATED:END -->

### 치수·타이포

<!-- GENERATED:START id=foundation-dimensions — tokens/*.tokens.json에서 생성됨. 직접 수정하지 말고 npm run tokens:sync -->
| 그룹 | 토큰 (이름이 곧 px 값, 다른 경우만 = 표기) |
|---|---|
| `Space` | 0, 2, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64 |
| `Size` | 16, 20, 24, 32, 40, 44, 48, 64, 80, 96 |
| `Radius` | 0, 4, 8, 12, 16, 24, Full = 9999px |
| `Stroke` | 1, 2 |
| `Type/Size` | 12, 13, 14, 16, 18, 20, 24, 28, 32, 40 |
| `Type/Line Height` | 16, 18, 20, 24, 28, 32, 36, 40, 48 |
| `Type/Family` | Sans = Pretendard |
| `Type/Weight` | Regular = 400, Medium = 500, Semibold = 600, Bold = 700 |
| `Breakpoint` | Tablet = 768px, Desktop = 1280px |
<!-- GENERATED:END -->

## 역조회 (하드코딩 정리용)

화면이나 코드에서 원시값을 발견했을 때 쓰는 표다. 세 번째 열의 Semantic 토큰으로 바꾼다. Foundation 토큰으로 바꾸지 않는다 (FND-01). 같은 값에 Semantic이 여러 개면 [Semantic Color의 토큰 선택 순서](semantic-color.md#토큰-선택-순서)로 역할을 정한다.

<!-- GENERATED:START id=foundation-reverse — tokens/*.tokens.json에서 생성됨. 직접 수정하지 말고 npm run tokens:sync -->
| 원시값 | Foundation | 이 값을 쓰는 Semantic (모드) |
|---|---|---|
| #fdfdfd | `Color/Gray/1` | `Surface/Default` (Light), `Text/Inverse` (Light), `Icon/Inverse` (Light) |
| #f9f9f9 | `Color/Gray/2` | `Surface/Subtle` (Light) |
| #f2f2f3 | `Color/Gray/3` | `Fill/Primary Subtle/Default` (Light), `Fill/Disabled` (Light) |
| #ececec | `Color/Gray/4` | `Fill/Primary Subtle/Hover` (Light) |
| #e5e5e6 | `Color/Gray/5` | `Fill/Primary Subtle/Selected` (Light) |
| #dcdddd | `Color/Gray/6` | `Border/Subtle` (Light) |
| #d0d1d2 | `Color/Gray/7` | `Border/Default` (Light) |
| #bdbebf | `Color/Gray/8` | `Text/Disabled` (Light), `Icon/Disabled` (Light) |
| #727578 | `Color/Gray/9` | `Border/Strong` (Light) |
| #67696c | `Color/Gray/10` | `Fill/Primary/Pressed` (Light), `Text/Tertiary` (Light) |
| #515355 | `Color/Gray/11` | `Fill/Primary/Hover` (Light), `Text/Secondary` (Light), `Icon/Secondary` (Light) |
| #1a1b1c | `Color/Gray/12` | `Surface/Inverse` (Light), `Fill/Primary/Default` (Light), `Text/Primary` (Light), `Icon/Primary` (Light) |
| #111212 | `Color/Gray Dark/1` | `Surface/Default` (Dark), `Text/Inverse` (Dark), `Text/On Primary` (Dark), `Icon/Inverse` (Dark), `Icon/On Primary` (Dark) |
| #171717 | `Color/Gray Dark/2` | `Surface/Subtle` (Dark), `Surface/Raised` (Dark) |
| #202021 | `Color/Gray Dark/3` | `Surface/Overlay` (Dark), `Fill/Primary Subtle/Default` (Dark), `Fill/Disabled` (Dark) |
| #272828 | `Color/Gray Dark/4` | `Fill/Primary Subtle/Hover` (Dark) |
| #2e2f30 | `Color/Gray Dark/5` | `Fill/Primary Subtle/Selected` (Dark) |
| #38393a | `Color/Gray Dark/6` | `Border/Subtle` (Dark) |
| #48494a | `Color/Gray Dark/7` | `Border/Default` (Dark) |
| #5f6062 | `Color/Gray Dark/8` | `Text/Disabled` (Dark), `Icon/Disabled` (Dark) |
| #7e8084 | `Color/Gray Dark/9` | `Border/Strong` (Dark) |
| #909296 | `Color/Gray Dark/10` | `Fill/Primary/Pressed` (Dark), `Text/Tertiary` (Dark) |
| #b9bbbd | `Color/Gray Dark/11` | `Fill/Primary/Hover` (Dark), `Text/Secondary` (Dark), `Icon/Secondary` (Dark) |
| #eeeeef | `Color/Gray Dark/12` | `Surface/Inverse` (Dark), `Fill/Primary/Default` (Dark), `Text/Primary` (Dark), `Icon/Primary` (Dark) |
| #ecf3fd | `Color/Blue/3` | `Fill/Accent Subtle/Default` (Light) |
| #e3edfc | `Color/Blue/4` | `Fill/Accent Subtle/Hover` (Light) |
| #d8e6fb | `Color/Blue/5` | `Fill/Accent Subtle/Selected` (Light) |
| #156cdd | `Color/Blue/9` | `Fill/Accent/Default` (Light), `Border/Focus` (Light), `Border/Accent` (Light) |
| #005dca | `Color/Blue/10` | `Fill/Accent/Hover` (Light) |
| #0b53b0 | `Color/Blue/11` | `Fill/Accent/Pressed` (Light), `Text/Accent` (Light), `Text/Link` (Light), `Icon/Accent` (Light) |
| #142134 | `Color/Blue Dark/3` | `Fill/Accent Subtle/Default` (Dark) |
| #162841 | `Color/Blue Dark/4` | `Fill/Accent Subtle/Hover` (Dark) |
| #1a2f4e | `Color/Blue Dark/5` | `Fill/Accent Subtle/Selected` (Dark) |
| #3460a0 | `Color/Blue Dark/8` | `Fill/Accent/Pressed` (Dark) |
| #005dca | `Color/Blue Dark/9` | `Fill/Accent/Default` (Dark) |
| #1069da | `Color/Blue Dark/10` | `Fill/Accent/Hover` (Dark) |
| #95c0ff | `Color/Blue Dark/11` | `Text/Accent` (Dark), `Text/Link` (Dark), `Icon/Accent` (Dark), `Border/Focus` (Dark), `Border/Accent` (Dark) |
| #fdefed | `Color/Red/3` | `Fill/Danger Subtle/Default` (Light) |
| #d02c2a | `Color/Red/9` | `Fill/Danger/Default` (Light), `Border/Danger` (Light) |
| #be1219 | `Color/Red/10` | `Fill/Danger/Hover` (Light) |
| #a51f1e | `Color/Red/11` | `Fill/Danger/Pressed` (Light), `Text/Danger` (Light), `Icon/Danger` (Light) |
| #331815 | `Color/Red Dark/3` | `Fill/Danger Subtle/Default` (Dark) |
| #994139 | `Color/Red Dark/8` | `Fill/Danger/Pressed` (Dark) |
| #be1219 | `Color/Red Dark/9` | `Fill/Danger/Default` (Dark) |
| #cc2827 | `Color/Red Dark/10` | `Fill/Danger/Hover` (Dark) |
| #ff968a | `Color/Red Dark/11` | `Text/Danger` (Dark), `Icon/Danger` (Dark), `Border/Danger` (Dark) |
| #edf5ee | `Color/Green/3` | `Fill/Success Subtle/Default` (Light) |
| #007131 | `Color/Green/11` | `Text/Success` (Light), `Icon/Success` (Light) |
| #142517 | `Color/Green Dark/3` | `Fill/Success Subtle/Default` (Dark) |
| #87d297 | `Color/Green Dark/11` | `Text/Success` (Dark), `Icon/Success` (Dark) |
| #f8f1e9 | `Color/Amber/3` | `Fill/Warning Subtle/Default` (Light) |
| #865900 | `Color/Amber/11` | `Text/Warning` (Light), `Icon/Warning` (Light) |
| #2b1e0b | `Color/Amber Dark/3` | `Fill/Warning Subtle/Default` (Dark) |
| #fdc677 | `Color/Amber Dark/11` | `Text/Warning` (Dark), `Icon/Warning` (Dark) |
| #ffffff | `Color/White` | `Surface/Raised` (Light), `Surface/Overlay` (Light), `Text/On Primary` (Light), `Text/On Accent` (Dark), `Text/On Accent` (Light), `Text/On Danger` (Dark), `Text/On Danger` (Light), `Icon/On Primary` (Light), `Icon/On Accent` (Dark), `Icon/On Accent` (Light), `Icon/On Danger` (Dark), `Icon/On Danger` (Light) |
| #000000 4.7% | `Color/Black Alpha/3` | `Shadow/Raised` (Light) |
| #000000 11.4% | `Color/Black Alpha/6` | `Shadow/Overlay` (Light) |
| #000000 14.1% | `Color/Black Alpha/7` | `Shadow/Raised` (Dark) |
| #000000 44% | `Color/Black Alpha/9` | `Overlay/Scrim` (Light), `Shadow/Overlay` (Dark) |
| #000000 48% | `Color/Black Alpha/10` | `Overlay/Scrim` (Dark) |
| 4px | `Space/4` | `Gap/Inline Tight` (Desktop), `Gap/Inline Tight` (Mobile), `Gap/Inline Tight` (Tablet) |
| 8px | `Space/8` | `Gap/Inline` (Desktop), `Gap/Inline` (Mobile), `Gap/Inline` (Tablet) |
| 12px | `Space/12` | `Gap/Stack` (Mobile), `Gap/Stack` (Tablet), `Inset/Sm` (Desktop), `Inset/Sm` (Mobile), `Inset/Sm` (Tablet) |
| 16px | `Space/16` | `Margin/Page` (Mobile), `Gap/Stack` (Desktop), `Inset/Md` (Desktop), `Inset/Md` (Mobile), `Inset/Md` (Tablet), `Inset/Container` (Mobile) |
| 20px | `Space/20` | `Inset/Lg` (Desktop), `Inset/Lg` (Mobile), `Inset/Lg` (Tablet), `Inset/Container` (Tablet) |
| 24px | `Space/24` | `Margin/Page` (Tablet), `Inset/Container` (Desktop) |
| 32px | `Space/32` | `Margin/Page` (Desktop), `Gap/Section` (Mobile) |
| 40px | `Space/40` | `Gap/Section` (Tablet) |
| 48px | `Space/48` | `Gap/Section` (Desktop) |
| 16px | `Size/16` | `Icon Size/Sm` (Desktop), `Icon Size/Sm` (Mobile), `Icon Size/Sm` (Tablet) |
| 20px | `Size/20` | `Icon Size/Md` (Desktop), `Icon Size/Md` (Mobile), `Icon Size/Md` (Tablet) |
| 24px | `Size/24` | `Icon Size/Lg` (Desktop), `Icon Size/Lg` (Mobile), `Icon Size/Lg` (Tablet) |
| 32px | `Size/32` | `Control Height/Sm` (Desktop), `Control Height/Sm` (Mobile), `Control Height/Sm` (Tablet) |
| 40px | `Size/40` | `Control Height/Md` (Desktop), `Control Height/Md` (Mobile), `Control Height/Md` (Tablet) |
| 44px | `Size/44` | `Hit Area/Min` (Desktop), `Hit Area/Min` (Mobile), `Hit Area/Min` (Tablet) |
| 48px | `Size/48` | `Control Height/Lg` (Desktop), `Control Height/Lg` (Mobile), `Control Height/Lg` (Tablet) |
| 64px | `Size/64` | `Control Min Width/Sm` (Desktop), `Control Min Width/Sm` (Mobile), `Control Min Width/Sm` (Tablet) |
| 80px | `Size/80` | `Control Min Width/Md` (Desktop), `Control Min Width/Md` (Mobile), `Control Min Width/Md` (Tablet) |
| 96px | `Size/96` | `Control Min Width/Lg` (Desktop), `Control Min Width/Lg` (Mobile), `Control Min Width/Lg` (Tablet) |
| 8px | `Radius/8` | `Corner/Control` (Desktop), `Corner/Control` (Mobile), `Corner/Control` (Tablet) |
| 12px | `Radius/12` | `Corner/Container` (Desktop), `Corner/Container` (Mobile), `Corner/Container` (Tablet) |
| 16px | `Radius/16` | `Corner/Sheet` (Desktop), `Corner/Sheet` (Tablet) |
| 24px | `Radius/24` | `Corner/Sheet` (Mobile) |
| 9999px | `Radius/Full` | `Corner/Pill` (Desktop), `Corner/Pill` (Mobile), `Corner/Pill` (Tablet) |
| 1px | `Stroke/1` | `Border Width/Default` (Desktop), `Border Width/Default` (Mobile), `Border Width/Default` (Tablet) |
| 2px | `Stroke/2` | `Border Width/Focus Ring` (Desktop), `Border Width/Focus Ring` (Mobile), `Border Width/Focus Ring` (Tablet) |
| 12px | `Type/Size/12` | `Font Size/Caption` (Desktop), `Font Size/Caption` (Mobile), `Font Size/Caption` (Tablet) |
| 13px | `Type/Size/13` | `Font Size/Label Sm` (Desktop), `Font Size/Label Sm` (Mobile), `Font Size/Label Sm` (Tablet) |
| 14px | `Type/Size/14` | `Font Size/Body Sm` (Desktop), `Font Size/Body Sm` (Mobile), `Font Size/Body Sm` (Tablet), `Font Size/Label Md` (Desktop), `Font Size/Label Md` (Mobile), `Font Size/Label Md` (Tablet) |
| 16px | `Type/Size/16` | `Font Size/Body` (Desktop), `Font Size/Body` (Mobile), `Font Size/Body` (Tablet), `Font Size/Label Lg` (Desktop), `Font Size/Label Lg` (Mobile), `Font Size/Label Lg` (Tablet) |
| 18px | `Type/Size/18` | `Font Size/Heading Sm` (Desktop), `Font Size/Heading Sm` (Mobile), `Font Size/Heading Sm` (Tablet) |
| 20px | `Type/Size/20` | `Font Size/Heading Md` (Mobile), `Font Size/Heading Md` (Tablet) |
| 24px | `Type/Size/24` | `Font Size/Heading Lg` (Mobile), `Font Size/Heading Lg` (Tablet), `Font Size/Heading Md` (Desktop) |
| 28px | `Type/Size/28` | `Font Size/Display` (Mobile), `Font Size/Heading Lg` (Desktop) |
| 32px | `Type/Size/32` | `Font Size/Display` (Tablet) |
| 40px | `Type/Size/40` | `Font Size/Display` (Desktop) |
| 16px | `Type/Line Height/16` | `Line Height/Caption` (Desktop), `Line Height/Caption` (Mobile), `Line Height/Caption` (Tablet) |
| 18px | `Type/Line Height/18` | `Line Height/Label Sm` (Desktop), `Line Height/Label Sm` (Mobile), `Line Height/Label Sm` (Tablet) |
| 20px | `Type/Line Height/20` | `Line Height/Body Sm` (Desktop), `Line Height/Body Sm` (Mobile), `Line Height/Body Sm` (Tablet), `Line Height/Label Lg` (Desktop), `Line Height/Label Lg` (Mobile), `Line Height/Label Lg` (Tablet), `Line Height/Label Md` (Desktop), `Line Height/Label Md` (Mobile), `Line Height/Label Md` (Tablet) |
| 24px | `Type/Line Height/24` | `Line Height/Heading Sm` (Desktop), `Line Height/Heading Sm` (Mobile), `Line Height/Heading Sm` (Tablet), `Line Height/Body` (Desktop), `Line Height/Body` (Mobile), `Line Height/Body` (Tablet) |
| 28px | `Type/Line Height/28` | `Line Height/Heading Md` (Mobile), `Line Height/Heading Md` (Tablet) |
| 32px | `Type/Line Height/32` | `Line Height/Heading Lg` (Mobile), `Line Height/Heading Lg` (Tablet), `Line Height/Heading Md` (Desktop) |
| 36px | `Type/Line Height/36` | `Line Height/Display` (Mobile), `Line Height/Heading Lg` (Desktop) |
| 40px | `Type/Line Height/40` | `Line Height/Display` (Tablet) |
| 48px | `Type/Line Height/48` | `Line Height/Display` (Desktop) |
| Pretendard | `Type/Family/Sans` | `Font Family/Base` (Desktop), `Font Family/Base` (Mobile), `Font Family/Base` (Tablet) |
| 400 | `Type/Weight/Regular` | `Font Weight/Body` (Desktop), `Font Weight/Body` (Mobile), `Font Weight/Body` (Tablet) |
| 500 | `Type/Weight/Medium` | `Font Weight/Label` (Desktop), `Font Weight/Label` (Mobile), `Font Weight/Label` (Tablet) |
| 600 | `Type/Weight/Semibold` | `Font Weight/Heading` (Desktop), `Font Weight/Heading` (Mobile), `Font Weight/Heading` (Tablet), `Font Weight/Strong` (Desktop), `Font Weight/Strong` (Mobile), `Font Weight/Strong` (Tablet) |
| 700 | `Type/Weight/Bold` | `Font Weight/Display` (Desktop), `Font Weight/Display` (Mobile), `Font Weight/Display` (Tablet) |
<!-- GENERATED:END -->
