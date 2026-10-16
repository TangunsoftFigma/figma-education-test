# Base — Foundation Token 사양



## 1. 문서 기준과 범위

이 문서는 Ihwa(이화) 디자인 시스템의 Foundation Token 컬렉션인 **Base**를 정의한다. 적용 환경은 **PC/모바일 겸용**이다.

- 정의 기준: 선택된 Foundation Token 네이밍 설계 보드.
- 구현 기준: 작성 시점의 Base 컬렉션, Default 모드, 총 **306개 변수**.
- 보드의 확정된 상세 표와 메모를 규칙의 근거로 삼는다. 현재 변수에서 확인한 값은 구현 현황으로 구분해 기재한다.
- 문서 작성은 변수 추가·삭제·이름 변경·값 변경을 포함하지 않는다.
- Semantic/Intent 및 Component의 역할별 매핑 사양은 이 문서의 범위가 아니다.

## 2. Base의 역할과 참조 구조

Foundation Token은 자연값(raw value) 전체가 아니라, 그중 시스템에서 사용하기로 선택한 원재료 값의 집합이다. 브랜드 색상 팔레트, 글꼴, 글자 크기, 간격, 크기, 곡률 및 효과의 기초 수치를 보관한다.

**값의 공급 방향: Base(Foundation) → Intent(Semantic) → Component**

| **계층** | **책임** | **참조 기준** |
|---|---|---|
| Foundation / Base | 사용할 원시 값을 정의한다. | 색상·수치·문자열 원본을 보관한다. |
| Semantic / Intent | 원시 값에 역할과 맥락을 부여한다. | Base 변수를 참조한다. |
| Component | 특정 컴포넌트의 속성과 상태를 정의한다. | Semantic/Intent를 참조한다. |

Base의 값에는 Primary, Danger, Button Background 같은 역할을 새로 부여하지 않는다. 보드의 대분류 설명에 나온 예시는 후보의 설명이며, 현재 허용 Set은 아래 상세 사양을 따른다.

## 3. 컬렉션 구성

| **항목** | **사양** |
|---|---|
| 디자인 시스템 | Ihwa (이화) |
| 컬렉션 이름 | Base |
| 계층 | Foundation |
| 적용 환경 | PC/모바일 겸용 |
| 현재 모드 | Default 단일 모드 |
| 현재 총 변수 수 | 306 |
| 명명 구조 | Category/Set/Option |

Base는 원시 값의 집합이며 현재 테마·기기별 모드를 나누지 않는다. 원시 값을 어떻게 선택해 쓸지는 상위 계층에서 결정한다.

| **Category** | **현재 변수 수** | **하위 Set** |
|---|---:|---|
| Color | 52 | Blue, Red, Green, Purple, Gray |
| Typography | 167 | Font Family, Font Size, Font Weight, Line Height, Letter Spacing |
| Layout | 36 | Space, Size |
| Shape | 19 | Radius, Stroke |
| Effect | 32 | Opacity, Offset, Blur, Spread |

### 3.1 데이터 타입과 단위

| **종류** | **Figma 변수 타입** | **해당 Set 및 단위** |
|---|---|---|
| 색상 | COLOR | Color 전체; 현재 모두 alpha 1 |
| 서체명 | STRING | Typography/Font Family |
| 글꼴 굵기 | FLOAT | Typography/Font Weight; 300~700의 숫자 값 |
| 크기·간격·곡률·선·효과 길이 | FLOAT | Font Size, Line Height, Letter Spacing, Space, Size, Radius, Stroke, Offset, Blur, Spread; px 기준 |
| 불투명도 | FLOAT | Effect/Opacity; 0~100 퍼센트 기준 |

보드 도입부는 Color/Number/Text/Boolean이라는 일반적인 변수 종류를 소개한다. 이 목록이 모두 Base에 구현되어야 한다는 뜻은 아니다. 현재 Boolean 변수는 없으며 Font Weight는 문자열이 아닌 숫자형이다.

## 4. 네이밍 규칙

### 4.1 기본 구조

**Category/Set/Option**의 3단계로 구성한다. 슬래시 앞뒤에 공백을 넣지 않는다.

| **단계** | **의미** | **예** |
|---|---|---|
| Category | 디자인 속성의 최상위 분류 | Color, Typography, Layout, Shape, Effect |
| Set | Category 안의 하위 그룹 | Blue, Font Size, Space, Radius, Opacity |
| Option | 허용된 값 또는 단계 | 05, 16, Sans, 24-110, 24-i1 |

### 4.2 단어 표기

- 단어 사이는 띄어쓰기로 구분한다.
- 각 단어의 첫 글자는 대문자, 나머지는 소문자로 표기한다.
- FontSize, FontFamily, LineHeight 같은 붙여쓰기 대신 **Font Size, Font Family, Line Height**를 사용한다.
- 숫자와 약속된 기호 표기는 별도의 Option 규칙을 따른다.
- 서체 실제 값인 SUIT Variable, Noto Serif KR는 이름 규칙에 맞춰 변경하지 않는다.

| **올바른 이름** | **설명** |
|---|---|
| Color/Blue/05 | 색상 단계는 앞자리 0을 유지한다. |
| Typography/Font Family/Sans | 서체명 자체가 아닌 분류명을 Option으로 사용한다. |
| Typography/Font Size/16 | 실제 글자 크기 값을 사용한다. |
| Typography/Font Weight/600 | 실제 굵기 값을 사용한다. |
| Typography/Line Height/24-110 | 24px 글자의 행간 110%를 뜻한다. |
| Typography/Letter Spacing/24-i1 | 24px 글자의 자간 -1%를 뜻한다. |
| Layout/Space/16 | 일반 수치는 실제 값을 사용한다. |
| Effect/Spread/i4 | 보드에 별도로 정의된 음수 Spread 표기를 따른다. |

### 4.3 하이픈과 음수 Option

Option 안의 하이픈은 **Line Height와 Letter Spacing에서 글자 크기와 비율을 구분하는 용도**로 제한한다. 음수 부호는 Option에서 소문자 **i**로 표기한다.

- 24-i1: 글자 크기 24px, 자간 -1%.
- i4: Spread 실제 값 -4px. 비율이 아니다.
- Base 이름 자체에 단위를 덧붙이지 않는다. 단위는 Set과 변수 설명으로 구분한다.

## 5. Color

### 5.1 Set과 단계

| **Set** | **허용 Option** | **수** |
|---|---|---:|
| Blue | 05, 10, 20, 30, 40, 50, 60, 70, 80, 90 | 10 |
| Red | 05, 10, 20, 30, 40, 50, 60, 70, 80, 90 | 10 |
| Green | 05, 10, 20, 30, 40, 50, 60, 70, 80, 90 | 10 |
| Purple | 05, 10, 20, 30, 40, 50, 60, 70, 80, 90 | 10 |
| Gray | 00, 05, 10, 20, 30, 40, 50, 60, 70, 80, 90, 99 | 12 |

- 유채색은 10단계, 무채색은 양 끝 2단계를 더한 12단계다.
- 단계는 명도·채도 기준으로 균일하게 구성되어야 한다.
- 유채색의 가장 어두운 값도 무채색과 분명하게 구별되어야 한다.
- **DIM은 Foundation에서 정의하지 않는다.**
- 단계 번호는 색상 스케일의 식별자다. 50이 명도 50%, 불투명도 50% 또는 특정 대비를 뜻하지는 않는다.

### 5.2 현재 구현 색상

다음 표는 현재 Base 변수의 sRGB 값을 8비트 HEX로 반올림해 표시한 것이다. 실제 저장값은 Figma의 COLOR 변수 값을 따른다. —는 해당 Option을 만들지 않는다는 뜻이다.

| **Option** | **Blue** | **Red** | **Green** | **Purple** | **Gray** |
|---|---|---|---|---|---|
| 00 | — | — | — | — | #FFFFFF |
| 05 | #F7FAFF | #FFF8F8 | #F4FDF6 | #FDF8FF | #FAFAFA |
| 10 | #CCE2FF | #FFDADB | #D0F8D8 | #F5D8FF | #DBDBDB |
| 20 | #A0C8FF | #FFBBBC | #AFF0BD | #ECB7FF | #BCBCBC |
| 30 | #72AEFF | #FF989E | #8DE8A3 | #E494FF | #9E9E9E |
| 40 | #4693F7 | #FF717E | #66DF89 | #D871F9 | #818181 |
| 50 | #0077ED | #FF385C | #30D66E | #CA4AF1 | #666666 |
| 60 | #165CB0 | #BE3549 | #33A057 | #973FB3 | #4F4F4F |
| 70 | #14427B | #842834 | #276F3D | #6A2E7D | #383838 |
| 80 | #0E294B | #50191F | #174124 | #401D4B | #242424 |
| 90 | #071221 | #220A0C | #08190C | #1B0B20 | #101010 |
| 99 | — | — | — | — | #000000 |

이전 구성에서 합의한 기준 색상 위치는 **50**이다. 나머지 단계는 OKLCH 기반으로 생성되었다. 이는 현재 구현 경위이며, 보드의 지각적 균일성 요구를 모두 검증했다는 의미는 아니다. 색상 쌍의 접근성 대비는 실제 역할과 배경이 정해지는 Intent/Component 적용 단계에서 별도로 확인한다.

## 6. Typography

### 6.1 Font Family

| **토큰** | **타입** | **값** |
|---|---|---|
| Typography/Font Family/Sans | STRING | SUIT Variable |
| Typography/Font Family/Serif | STRING | Noto Serif KR |

Font Family 값은 폰트의 이름이다. 실제 사용 환경에서 해당 서체와 필요한 굵기를 사용할 수 있는지는 별도로 확인한다.

### 6.2 Font Size

총 **20개**, 타입 FLOAT, 단위 px.

**10, 11, 12, 14, 16, 18, 20, 22, 24, 28, 32, 36, 40, 44, 48, 56, 64, 72, 80, 96**

| **범위** | **확장 규칙 / 사용 범위** |
|---|---|
| 10, 11, 12 | 특히 작게 사용해야 하는 일부 케이스 |
| 12~24 | 2px 단위 |
| 24~48 | 4px 단위 |
| 48~80 | 8px 단위 |
| 80, 96 | 특히 크게 사용해야 하는 일부 케이스 |

범위가 겹치는 경계값은 중복 생성하지 않는다. Base에 큰 값이 있다고 해서 모든 환경에서 사용을 허용하는 것은 아니다. 모바일의 큰 글자 크기는 장식 등 용도를 검토해 상위 계층에서 선택한다.

### 6.3 Font Weight

총 **5개**, 타입 FLOAT, 값은 **300, 400, 500, 600, 700**이다.

이름과 값은 숫자로 일치시킨다. 예: Typography/Font Weight/600 → 600. 보드의 Font Weight 메모에 있는 Font Size/16 예시는 해당 항목의 취지에 맞게 이 사양에서는 Font Weight 예시로 바로잡았다.

### 6.4 Line Height

모든 Font Size와 허용 비율 **110, 120, 130, 140, 150%**를 조합한다. 총 **20 × 5 = 100개**다.

- 이름: Typography/Line Height/{Font Size}-{Percent}
- 실제 값(px) = Font Size × Percent ÷ 100
- 예: Typography/Line Height/24-110 → 26.4px
- 예: Typography/Line Height/16-150 → 24px

변수 값에는 110 같은 퍼센트 숫자가 아니라 계산한 px 값을 저장한다. 상위 계층에서 Font Size를 선택할 때 대응하는 크기 접두사의 Line Height를 사용한다.

### 6.5 Letter Spacing

모든 Font Size와 허용 비율 **-1%, -3%**를 조합한다. 총 **20 × 2 = 40개**다.

- 이름: Typography/Letter Spacing/{Font Size}-i{Percent의 절댓값}
- 실제 값(px) = Font Size × 음수 Percent ÷ 100
- 예: Typography/Letter Spacing/24-i1 → -0.24px
- 예: Typography/Letter Spacing/24-i3 → -0.72px

이름의 i는 음수 부호를 대신한다. 실제 값은 음수 숫자로 저장한다. 양수 자간이나 0 자간은 현재 허용 목록에 없다.

### 6.6 숫자 정밀도

Line Height와 Letter Spacing은 소수 값을 허용한다. Figma 저장 과정에서 생기는 부동소수점 표현 오차(예: 26.3999996)는 계산식과 구분한다. 문서에는 수학적 계산값을 표시하며, 이를 이유로 임의 정수 반올림을 적용하지 않는다.

## 7. Layout

타입은 FLOAT, 단위는 px다. **Space는 공간, Size는 요소의 크기**에 사용한다.

| **Set** | **용도** | **허용 값** | **수** |
|---|---|---|---:|
| Space | Padding, Gap 등 공간 속성 | 1, 2, 4, 6, 8, 12, 16, 20, 24, 32, 40, 48, 56, 64, 72, 80, 96, 112, 128 | 19 |
| Size | Width, Height 등 크기 속성 | 1, 2, 4, 8, 12, 16, 20, 24, 32, 40, 48, 56, 64, 80, 96, 112, 128 | 17 |

### 7.1 Space 확장 규칙

- 1: 특히 좁은 간격이 필요한 일부 케이스.
- 2~8: 2px 단위.
- 8~24: 4px 단위.
- 24~80: 8px 단위.
- 80~128: 16px 단위.

### 7.2 Size 확장 규칙

- 1, 2: 특히 작은 크기가 필요한 일부 케이스.
- 4~24: 4px 단위.
- 24~64: 8px 단위.
- 64~128: 16px 단위.

현재 두 Set 모두 0이 없으며 Size의 최댓값은 128이다. 컨테이너 최대 너비 등 더 큰 값이 필요하더라도 별도 승인 없이 Base에 추가하지 않는다. Space에 있는 값이 Size에 자동으로 포함되는 것은 아니다.

## 8. Shape

타입은 FLOAT, 단위는 px다.

| **Set** | **허용 값** | **수** |
|---|---|---:|
| Radius | 1, 2, 4, 6, 8, 10, 12, 16, 20, 24, 32, 40, 9999 | 13 |
| Stroke | 1, 2, 3, 4, 6, 8 | 6 |

### 8.1 Radius

- 1, 2: 미세한 곡률이 필요한 케이스.
- 4~12: 2px 단위.
- 12~24: 4px 단위.
- 24~40: 8px 단위.
- 9999: 최대 곡률이 필요한 케이스.

9999는 최대 곡률을 얻기 위한 큰 숫자 원시 값이다. Full 같은 용도명은 상위 계층에서 부여한다.

### 8.2 Stroke

- 1~4: 1px 단위.
- 6, 8: 아주 두꺼운 윤곽선이 필요한 일부 케이스.

## 9. Effect

효과를 구성하는 기초 수치를 정의한다. Shadow처럼 여러 속성이 합쳐진 완성 프리셋을 Base 토큰 하나로 정의하지 않는다.

| **Set** | **허용 Option** | **실제 값 / 단위** | **수** |
|---|---|---|---:|
| Opacity | 0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100 | 같은 숫자, % | 11 |
| Offset | 0, 1, 2, 4, 6, 8 | 같은 숫자, px | 6 |
| Blur | 1, 2, 4, 6, 8, 12, 16, 24 | 같은 숫자, px | 8 |
| Spread | i4, i2, i1, 0, 1, 2, 4 | -4, -2, -1, 0, 1, 2, 4px | 7 |

### 9.1 Opacity 단위

0은 완전 투명, 100은 완전 불투명이다. **0~1 비율이 아닌 0~100 값**을 저장한다. 다른 환경으로 전달할 때 그 환경이 0~1을 요구하면 변환 경계에서 100으로 나눈다. Base 원본 값을 0~1로 바꾸지 않는다.

### 9.2 음수 Spread 표기와 규칙의 적용 범위

보드는 하이픈 구분 규칙을 Line Height·Letter Spacing에 한정하면서, Spread에도 i4/i2/i1이라는 음수 표기를 별도로 명시한다. 따라서 이 사양은 **하이픈 구분은 Typography의 두 Set에만 허용하고, i 음수 접두사는 Letter Spacing과 명시된 Spread Option에 적용**하는 것으로 상세 표를 우선해 정리한다. 임의의 다른 Set에 i 표기를 확대하지 않는다.

## 10. 검수 기준

- Category/Set/Option의 3단계 구조인지 확인한다.
- 허용된 Category·Set·Option 목록과 정확히 일치하는지 확인한다.
- 여러 단어의 Set 이름이 띄어쓰기와 첫 글자 대문자 규칙을 지키는지 확인한다.
- 색상 단계의 00/05 표기와 유채색 10단계·Gray 12단계를 확인한다.
- Line Height 100개, Letter Spacing 40개가 각 Font Size에 빠짐없이 대응하는지 확인한다.
- px 계산값과 퍼센트 값, 특히 Opacity의 0~100 저장 기준을 혼동하지 않는지 확인한다.
- Space/Size와 Font Size/Font Weight를 목적에 맞게 구분했는지 확인한다.
- 변경 시 기존 별칭 참조와 바인딩의 영향을 점검한다.
- 현재 인벤토리 기준 총 306개(Color 52, Typography 167, Layout 36, Shape 19, Effect 32)인지 확인한다. 추후 승인된 변경이 생기면 목록과 수를 함께 갱신한다.

## 11. 변경 관리

**상위 계층을 만들다가 필요한 값이 없다는 이유만으로 Base를 임의로 확장하지 않는다.**

추가·수정·삭제가 필요하면 다음 정보를 먼저 제시하고 사용자의 승인을 받는다.

1. 필요한 값과 해당 Category/Set/Option.
2. 기존 Base 값으로 충족할 수 없는 이유.
3. 추가·수정·삭제가 Intent 및 Component 참조에 미치는 영향.
4. 승인 후 변경한 이름·이전 값·새 값·변경 이유와 문서 반영 내역.

현재 Base에는 Amber와 320px 이상의 컨테이너 크기 토큰이 없다. 과거 임의로 추가되었다가 제거된 항목을 현재 사양으로 취급하거나 이 문서를 근거로 재생성하지 않는다.

문서와 실제 변수가 다르면 차이를 보고하고, 문서 작성만 요청받은 상태에서는 변수를 자동으로 변경하지 않는다.