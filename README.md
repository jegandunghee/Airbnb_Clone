# StayNest — 숙소 예약 서비스 클론 프로젝트

> 유명 숙소 예약 서비스를 참고하여 제작한 반응형 웹 클론 코딩 프로젝트입니다.  
> CSS Grid 시스템과 SCSS를 핵심 기술로 사용하며, 실제 서비스와 유사한 수준의 UI/UX를 구현하는 것에 중점을 두었습니다.

<br/>

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | StayNest |
| **유형** | 반응형 웹 클론 코딩 포트폴리오 |
| **제작 기간** | 2026년 4월 |
| **핵심 기술** | HTML5, CSS3 (CSS Grid), SCSS, Vanilla JavaScript |
| **반응형 기준** | 모바일 `< 768px` / 태블릿 `768px~` / 데스크탑 `1200px~` |

<br/>

## 🔍 학습 목표 및 포인트

이 프로젝트는 다음 기술들을 실전에서 익히는 것을 목표로 합니다.

- **CSS Grid 시스템** 기반의 반응형 레이아웃 구성
- **SCSS** 문법 활용 (변수, Mixin, @use, @forward, 중첩 등)
- **Mobile First** 방식의 반응형 웹 설계
- **Vanilla JavaScript**로 인터랙티브 UI 구현
- 실제 서비스 수준의 헤더, 검색창, 카드 컴포넌트, 푸터 구현

<br/>

## 🛠️ 기술 스택

### Core
- **HTML5** — 시맨틱 마크업, 웹 접근성 고려
- **CSS3** — CSS Grid, Flexbox, 미디어 쿼리, CSS 변수, CSS Animation
- **SCSS** — 변수, Mixin, 함수, 파일 모듈화 (`@use`, `@forward`)
- **Vanilla JavaScript** — 탭 인터랙션, 카드 슬라이더, 하트 토글

### 폰트
- **Michroma** (Google Fonts) — 브랜드 로고 서체
- **Noto Sans KR** (Google Fonts) — 본문 한국어 서체

<br/>

## 📁 프로젝트 구조

```
Airbnb_Clone/
│
├── index.html              # 메인 HTML 파일
│
├── CSS/
│   ├── reset.css           # CSS 초기화 (box-sizing, margin, padding 등)
│   └── style.css           # SCSS에서 컴파일된 메인 스타일시트
│
├── SCSS/
│   ├── _font.scss          # 구글 폰트 import
│   ├── _variables.scss     # 색상, 여백, 그림자 등 디자인 토큰 변수
│   ├── _mixin.scss         # Flexbox 레이아웃 Mixin, 반응형 Mixin
│   └── style.scss          # 메인 SCSS 파일 (모든 파일 통합)
│
└── IMG/
    ├── favicon.ico         # 파비콘
    ├── contents/           # 카드 컨텐츠 이미지 (content01~05.jpg)
    └── icon/               # 아이콘 파일 (SVG, PNG)
        ├── icon01.png      # 숙소 탭 아이콘
        ├── icon02.png      # 체험 탭 아이콘
        ├── icon03.png      # 서비스 탭 아이콘
        ├── icon_search.svg # 검색 아이콘 (모바일)
        ├── icon_lang.svg   # 언어 변경 아이콘
        ├── icon_menu.svg   # 햄버거 메뉴 아이콘
        ├── figma_icon_search.png     # 검색 버튼 아이콘 (PC)
        ├── figma_heart_icon.png      # 하트 아이콘 (기본)
        └── figma_heart_pink_icon.png # 하트 아이콘 (찜 활성화)
```

<br/>

## 🎨 SCSS 구조 및 디자인 토큰

### `_variables.scss` — 디자인 변수

```scss
$main_color:    #dc1e52;  // 브랜드 메인 컬러 (레드핑크)
$font_main:     #222;     // 기본 텍스트 컬러
$font_sub:      #888;     // 서브 텍스트 컬러
$bg_color:      #fff;     // 배경 컬러
$base_padding:  0.5rem 2rem;
$base_shadow:   0 0 10px rgba(0, 0, 0, 0.3);
$card_radius:   2rem;
```

### `_mixin.scss` — 재사용 Mixin

```scss
// Flexbox 레이아웃 Mixin (매개변수 기본값 설정)
@mixin flex_layout($just: center, $dire: row, $align: center, $gap: 1rem) {
  display: flex;
  flex-direction: $dire;
  justify-content: $just;
  align-items: $align;
  gap: $gap;
}

// 반응형 브레이크포인트 Mixin
@mixin tablet {
  @media all and (min-width: 768px) { @content; }
}

@mixin desktop {
  @media all and (min-width: 1200px) { @content; }
}
```

<br/>

## 📐 반응형 레이아웃 설계 (CSS Grid 핵심)

이 프로젝트의 핵심은 **CSS Grid 시스템**을 활용한 반응형 레이아웃입니다.

### 반응형 브레이크포인트

| 구간 | 기준 폭 | 기준 font-size |
|------|---------|---------------|
| 모바일 | `< 768px` | `12px` |
| 태블릿 | `768px ~` | `14px` |
| 데스크탑 | `1200px ~` | `16px` |

> 모든 `rem` 단위는 `html { font-size }` 를 기준으로 계산되므로,  
> font-size 변경만으로 전체 요소 크기가 비례하여 조정됩니다.

### 카드 리스트 — CSS Grid 슬라이더

가장 핵심적인 반응형 기술이 적용된 부분입니다.  
`grid-auto-flow: column` 방식으로 카드를 가로 배치하고,  
`grid-auto-columns`로 화면 크기에 따라 표시 개수를 제어합니다.

```css
/* === 모바일: 2열 기준 === */
ul.card-list {
  display: grid;
  grid-auto-flow: column;         /* 가로 방향으로 카드 배치 */
  grid-template-rows: 1fr;        /* 단일 행 */
  grid-auto-columns: calc((100% - 1rem) / 2);   /* 2장 표시 */
  gap: 1rem;
  transition: transform 0.35s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

/* === 태블릿: 3열 기준 === */
@media (min-width: 768px) {
  ul.card-list {
    grid-auto-columns: calc((100% - 2.4rem) / 3); /* 3장 표시 */
    gap: 1.2rem;
  }
}

/* === 데스크탑: 6열 전체 === */
@media (min-width: 1200px) {
  ul.card-list {
    grid-auto-columns: calc((100% - 7rem) / 6);  /* 6장 전체 표시 */
    gap: 1.4rem;
  }
}
```

### 푸터 — CSS Grid 4열 고정

```css
.footer_grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 항상 4열 유지 */
  gap: 1.2rem;
}
```

<br/>

## 🖥️ 구현 화면

### 데스크탑 뷰 (1200px 이상)
- StayNest 로고 + 카테고리 탭 + "내 숙소 등록하기" 버튼 + 아이콘 버튼 노출
- PC 검색창: 여행지 / 체크인 / 체크아웃 / 여행자 + 빨간 검색 버튼
- 카드: 6열 그리드로 모든 카드 한 줄에 표시
- 네비게이션 버튼(< >) 숨김

### 태블릿 뷰 (768px ~ 1199px)
- 로고 + 카테고리 탭 노출, 모바일 검색창 숨김
- PC 검색창 노출
- 카드: 3열 그리드로 표시 + `< >` 버튼으로 슬라이드 이동
- "내 숙소 등록하기" 버튼 숨김 (태블릿에서는 공간 절약)

### 모바일 뷰 (768px 미만)
- 모바일 전용 심플 검색창 노출 (원형 pill 스타일)
- 카테고리 탭 아이콘만 세로 배열
- 카드: 2열 그리드 + `< >` 버튼으로 슬라이드 이동
- 로고 · PC 검색창 · 헬프 메뉴 숨김

<br/>

## ⚙️ 주요 기능

### 1. 카테고리 탭 (숙소 / 체험 / 서비스)
- 클릭한 탭에만 밑줄 활성화 표시
- 기본 선택: 숙소 탭
- "체험", "서비스" 탭에는 `New` 뱃지 표시

```javascript
document.querySelectorAll('nav ul.icon li').forEach(function(tab) {
  tab.addEventListener('click', function() {
    // 모든 탭에서 active 제거
    document.querySelectorAll('nav ul.icon li').forEach(function(t) {
      t.classList.remove('active');
    });
    // 클릭한 탭에만 active 추가
    this.classList.add('active');
  });
});
```

### 2. 카드 슬라이더 (< > 버튼)
- 섹션별 독립 슬라이더 동작
- 현재 `window.innerWidth`에 따라 보이는 카드 수 동적 계산
- 첫 번째 / 마지막 위치에서 버튼 비활성화 (`disabled`)
- 창 크기 변경 시 슬라이더 위치 자동 초기화

```javascript
function getVisibleCount() {
  if (window.innerWidth >= 1200) return 6; // 데스크탑: 전체
  if (window.innerWidth >= 768)  return 3; // 태블릿: 3장
  return 2;                                // 모바일: 2장
}
```

### 3. 하트 (찜하기) 토글
- 하트 클릭 시 일반 하트 ↔ 핑크 하트 전환
- 카드 이미지 오른쪽 상단에 `position: absolute`로 고정
- `e.stopPropagation()`으로 카드 클릭 이벤트와 분리

### 4. 검색창
- **모바일**: 심플한 원형 pill 스타일 검색창
- **PC**: 여행지 / 체크인 / 체크아웃 / 여행자 4개 항목 + 검색 버튼
- hover 시 배경색 전환 효과

<br/>

## 💡 주요 CSS 기법

| 기법 | 적용 위치 | 설명 |
|------|-----------|------|
| `CSS Grid (grid-auto-flow: column)` | 카드 리스트 | 가로 배치 + JS transform 슬라이더 |
| `CSS Grid (repeat(4, 1fr))` | 푸터 | 4열 고정 그리드 |
| `Flexbox` | 헤더, 탭, 검색창 | 가로 정렬 레이아웃 |
| `position: sticky` | 헤더 | 스크롤 시 상단 고정 |
| `position: absolute` | 하트 아이콘, New 뱃지 | 카드 위 절대 위치 고정 |
| `aspect-ratio: 1/1` | 카드 이미지 | 정사각형 비율 유지 |
| `will-change: transform` | 카드 리스트 | 슬라이드 애니메이션 GPU 가속 |
| `cubic-bezier` | 카드 슬라이드 | 자연스러운 슬라이드 이징 |
| `filter: drop-shadow()` | 하트 아이콘 | 이미지 그림자 효과 |
| `overflow: hidden` | 슬라이더 래퍼 | 넘치는 카드 숨김 |

<br/>

## 📦 카드 컴포넌트 구조

총 3개의 카드 섹션(ul)으로 구성됩니다.

```
main > section (x3)
  ├── .title
  │   ├── .sub (h2 + 화살표)
  │   └── .sub_icon (< > 네비게이션 버튼)
  │
  └── .card-list-wrapper (overflow: hidden)
      └── ul.card-list.list-{1|2|3} (CSS Grid 슬라이더)
          └── li.card (x6)
              ├── .image (배경이미지 + 뱃지 + 하트)
              │   ├── .badge_guest
              │   └── .heart (img)
              └── .info
                  ├── h4 (숙소명)
                  ├── .date
                  └── .price (.star 포함)
```

| 섹션 | 제목 | 내용 |
|------|------|------|
| `ul.list-1` | 서울의 인기 스테이 | 서울 숙소 6곳 |
| `ul.list-2` | 이번 주 추천 체험 | 서울 체험 프로그램 6개 |
| `ul.list-3` | 스페셜 Pick 🔥 | 전국 특가 숙소 6곳 |

<br/>

## 🚀 실행 방법

별도의 빌드 과정 없이 브라우저에서 바로 실행 가능합니다.

### 방법 1 — Python 내장 서버

```bash
# 프로젝트 루트 디렉토리에서 실행
python -m http.server 8080

# 브라우저에서 접속
# http://localhost:8080
```

### 방법 2 — VS Code Live Server 확장

1. VS Code에서 `index.html` 열기
2. 우측 하단 `Go Live` 버튼 클릭
3. 자동으로 브라우저 실행

### 방법 3 — 파일 직접 열기

`index.html` 파일을 브라우저에 드래그 앤 드롭하여 실행

> ⚠️ **주의**: SCSS 파일을 수정할 경우 별도의 SCSS 컴파일러(node-sass, sass CLI 등)를 사용하여  
> `SCSS/style.scss` → `CSS/style.css` 로 컴파일해야 브라우저에 반영됩니다.

<br/>

## 📝 참고 사항

- 이 프로젝트는 **학습 및 포트폴리오 목적**으로만 제작되었습니다.
- 실제 예약 서비스를 참고하여 레이아웃과 UI를 클론한 것으로, 상업적 이용을 목적으로 하지 않습니다.
- 브랜드명, 문구, 이미지 등은 모두 자체 제작 또는 변경된 내용을 사용합니다.

<br/>

---

**© 2024 StayNest Portfolio Project**
