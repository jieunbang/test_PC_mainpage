# Card Section 인터랙션 스펙 문서

## 1. 개요

메인 페이지 첫 번째 섹션의 카드 영역 인터랙션 및 반응형 스펙 문서입니다.

---

## 2. 레이아웃 구조

```
┌─────────────────────────────────────────────────────────────┐
│ main-content-wrapper                                        │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ card-section (max-width: 1600px)                        │ │
│ │ ┌───────────────────────────┐ ┌───────────────────────┐ │ │
│ │ │ main-card (flex: 1)       │ │ side-cards (426px)    │ │ │
│ │ │ - 이미지 슬라이더         │ │ ┌───────────────────┐ │ │ │
│ │ │ - 타이틀/서브타이틀       │ │ │ side-card 1       │ │ │ │
│ │ │ - CTA 버튼               │ │ │ (인재영입)        │ │ │ │
│ │ │ - 인디케이터             │ │ └───────────────────┘ │ │ │
│ │ │                          │ │ ┌───────────────────┐ │ │ │
│ │ │                          │ │ │ side-card 2       │ │ │ │
│ │ │                          │ │ │ (기분좋은금융생활)│ │ │ │
│ │ └───────────────────────────┘ └───────────────────────┘ │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. 메인 카드 이미지 슬라이더

### 3.1 슬라이드 데이터

| 인덱스 | 이미지 파일 | 설명 |
|--------|-------------|------|
| 0 | `main-card.png` | 메인 이미지 1 |
| 1 | `main-card2.png` | 메인 이미지 2 |
| 2 | `main-card3.png` | 메인 이미지 3 |
| 3 | `main-card4.png` | 메인 이미지 4 |

### 3.2 타이밍 설정

| 항목 | 값 | 설명 |
|------|-----|------|
| `mainCardIntervalTime` | **4000ms (4초)** | 슬라이드 자동 전환 간격 |
| `transition` | **0.8s ease-in-out** | 페이드 전환 애니메이션 시간 |

### 3.3 상태 변수

```javascript
let mainCardCurrentSlide = 0;    // 현재 활성 슬라이드 인덱스
let mainCardAutoPlay = true;      // 자동 재생 여부
let mainCardInterval = null;      // setInterval 참조
const mainCardIntervalTime = 4000; // 전환 간격 (ms)
```

### 3.4 주요 함수

| 함수명 | 설명 |
|--------|------|
| `mainCardGoToSlide(index)` | 특정 인덱스 슬라이드로 이동 |
| `mainCardNextSlide()` | 다음 슬라이드로 이동 (순환) |
| `mainCardStartAutoPlay()` | 자동 재생 시작 |
| `mainCardStopAutoPlay()` | 자동 재생 중지 |
| `mainCardToggleAutoPlay()` | 자동 재생 토글 |
| `startMainCardSlider()` | 슬라이더 초기화 및 시작 |

### 3.5 인터랙션 동작

1. **자동 재생**: 4초마다 다음 슬라이드로 페이드 전환
2. **인디케이터 클릭**: 해당 슬라이드로 즉시 이동, 자동 재생 타이머 재시작
3. **재생/일시정지 버튼**: 자동 재생 토글
4. **섹션 진입 시**: 슬라이더 초기화 및 자동 재생 시작
5. **섹션 이탈 시**: 자동 재생 중지

---

## 4. 반응형 브레이크포인트

### 4.1 기본 스타일 (1920px 기준)

```css
.main-content-wrapper {
  padding: 0 160px;
}

.card-section {
  max-width: 1600px;
  gap: 20px;
  height: calc(100vh - 80px - 80px);
  max-height: 860px;
}

.main-card {
  flex: 1;
  max-width: 1154px;
  border-radius: 32px;
}

.side-cards {
  width: 426px;
  gap: 20px;
}
```

### 4.2 브레이크포인트별 스타일

#### max-width: 1600px

```css
.main-content-wrapper {
  padding: 30px 80px;
}

.card-section {
  max-width: 1440px;
  height: calc(100vh - 80px - 60px);
}

.side-cards {
  width: 360px;
}

.main-card-content {
  left: 60px;
  bottom: 60px;
  right: 60px;
}

.main-card-title {
  font-size: 44px;
}

.main-card-indicator {
  right: 60px;
  bottom: 80px;
}
```

#### max-width: 1280px

```css
.main-content-wrapper {
  padding: 24px 40px;
}

.card-section {
  height: calc(100vh - 80px - 48px);
  gap: 16px;
}

.side-cards {
  width: 320px;
  gap: 16px;
}

.main-card-content {
  left: 40px;
  bottom: 40px;
  right: 40px;
}

.main-card-title {
  font-size: 40px;
}

.side-card-content {
  left: 24px;
  bottom: 24px;
}

.side-card-title {
  font-size: 22px;
}

.main-card-indicator {
  right: 40px;
  bottom: 60px;
}
```

#### max-width: 1080px (최소)

```css
.main-content-wrapper {
  padding: 20px 24px;
}

.card-section {
  gap: 12px;
  height: calc(100vh - 80px - 40px);
  min-width: 1032px;
}

.side-cards {
  width: 280px;
  gap: 12px;
}

.main-card {
  min-width: 400px;
}

.main-card-title {
  font-size: 36px;
}

.main-card-subtitle {
  font-size: 16px;
}

.main-card-button {
  height: 48px;
  font-size: 16px;
}

.main-card-content {
  left: 32px;
  bottom: 32px;
  right: 32px;
}
```

---

## 5. 인디케이터 스펙

### 5.1 기본 스타일

```css
.main-card-indicator {
  position: absolute;
  right: 80px;
  bottom: 80px;
  display: flex;
  gap: 8px;
  align-items: center;
  z-index: 1;
}

.indicator-dot {
  width: 12px;
  height: 12px;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.indicator-dot:hover {
  transform: scale(1.2);
}

.indicator-control {
  width: 12px;
  height: 12px;
  cursor: pointer;
  transition: transform 0.2s ease;
}
```

### 5.2 인디케이터 이미지

| 상태 | 이미지 파일 |
|------|-------------|
| 비활성 | `indicator-dot.svg` |
| 활성 | `indicator-dot-active.svg` |
| 재생 중 | `indicator-pause.svg` |
| 일시정지 | `indicator-play.svg` |

---

## 6. 사이드 카드 호버 인터랙션

### 6.1 첫 번째 사이드 카드 (인재영입)

```css
/* 호버 시 오버레이 표시 */
.side-card:not(.text-card):hover .side-card-hover-overlay,
.side-card:not(.text-card):hover .side-card-hover-content {
  opacity: 1;
  pointer-events: auto;
}

/* 호버 시 기존 컨텐츠 숨김 */
.side-card:not(.text-card):hover .side-card-content {
  opacity: 0;
}
```

### 6.2 두 번째 사이드 카드 (기분좋은 금융생활)

```css
/* 호버 시 블랙 딤 오버레이 + QR 코드 표시 */
.text-card-hover-overlay {
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(7.5px);
  z-index: 2;
}

/* 호버해도 로고 유지 */
.side-card.text-card:hover .side-card-image {
  opacity: 1;
}
```

---

## 7. 애니메이션 타이밍

| 요소 | 속성 | 값 |
|------|------|-----|
| 슬라이드 전환 | opacity transition | 0.8s ease-in-out |
| 호버 오버레이 | opacity transition | 0.3s ease |
| 인디케이터 호버 | transform transition | 0.2s ease |
| 섹션 전환 | opacity transition | 0.6s cubic-bezier(0.4, 0, 0.2, 1) |

---

## 8. 이미지 파일 목록

### 메인 카드 슬라이더
- `images/main-card.png`
- `images/main-card2.png`
- `images/main-card3.png`
- `images/main-card4.png`

### 인디케이터
- `images/indicator-dot.svg`
- `images/indicator-dot-active.svg`
- `images/indicator-pause.svg`
- `images/indicator-play.svg`

### 사이드 카드
- `images/side-card-1.png` (인재영입 배경)
- `images/main_slogan.svg` (기분좋은 금융생활 로고)
- `images/QR.png` (QR 코드)

---

## 9. 접근성

- 인디케이터에 `aria-label` 속성 적용
- 재생/일시정지 버튼 상태에 따른 `aria-label` 동적 변경
- 키보드 네비게이션 지원 (좌/우 화살표 키)

---

*문서 작성일: 2024년 12월*

