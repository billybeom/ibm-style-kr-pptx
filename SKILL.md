---
name: ibm-kr-pptx
description: "IBM Carbon Design System 표준과 IBM Plex Sans KR 타이포그래피를 따르는 파워포인트 프레젠테이션을 생성, 편집, 읽어주는 스킬입니다. PptxGenJS로 IBM 규격 덱(IBM 표지, TOC, 섹션 구분자, 13개 IBM 콘텐츠 템플릿 카테고리, 엔딩 슬라이드)을 처음부터 만들거나, XML 워크플로로 기존 PPTX를 편집하거나, markitdown으로 텍스트를 추출합니다. IBM 일반 템플릿 스타일과 webMethods Hybrid Integration 셀러 덱 스타일을 모두 지원합니다. IBM Plex Sans KR 타이포그래피, IBM Blue 액센트, IBM 템플릿 레이아웃을 따릅니다. 트리거: PPT, PPTX, PowerPoint, 프레젠테이션, 발표자료, 슬라이드, 덱, IBM 프레젠테이션, IBM 덱, webMethods 프레젠테이션, 셀러 덱."
license: MIT
metadata:
  version: "2.0"
  category: productivity
---

# PPTX 생성기 & 편집기 (IBM / webMethods)

## 개요

이 스킬은 모든 파워포인트 작업을 처리합니다: 기존 프레젠테이션 읽기/분석, XML 조작을 통한 템플릿 기반 덱 편집, PptxGenJS를 사용한 처음부터 프레젠테이션 생성. **IBM Carbon Design System**과 **IBM Plex Sans KR** 타이포그래피를 엄격히 따릅니다.

두 가지 프레젠테이션 스타일을 지원합니다 — 상황에 맞게 선택하세요:

| 스타일 | 사용 시기 | 참조 |
|-------|-----------|------|
| **IBM 일반** | 표준 IBM 고객 프레젠테이션, 내부 덱 | [slide-types.md](references/slide-types.md), [design-system.md](references/design-system.md) |
| **webMethods Seller Deck** | IBM webMethods Hybrid Integration 셀러/제품 프레젠테이션 | [webmethods-template.md](references/webmethods-template.md) |

사용자가 webMethods, Hybrid Integration, 또는 셀러 프레젠테이션을 요청하거나 `webMethods_powerpoint_template.pptx` 스타일을 원한다고 명시하면 — [webMethods 템플릿 가이드](references/webmethods-template.md)를 사용하세요.

---

## IBM 프레젠테이션 요구사항

모든 IBM 덱은 다음 구조 규칙을 **반드시** 따라야 합니다 — 예외 없음:

1. **첫 번째 슬라이드 = 표지(Cover)** — 항상 IBM 브랜드 표지 슬라이드로 시작
2. **마지막 슬라이드 = 엔딩(Ending)** — 항상 IBM 브랜드 엔딩 슬라이드로 마무리
3. **표지와 엔딩에는 페이지 번호 없음**
4. **그 사이의 모든 슬라이드에 페이지 번호** x=25.75" y=14.16" 위치에 표시
5. **모든 본문/레이블 텍스트는 최소 28pt** (IBM Plex Sans KR 사용 시; 표 내부는 20pt 허용)
6. **폰트 패밀리 = IBM Plex Sans KR** (다양한 굵기) — 다른 폰트 패밀리와 절대 혼용 금지

```
[표지] → [셀러 가이던스 / TOC (선택)] → [섹션 구분자 + 콘텐츠 슬라이드] → [엔딩]
```

## 빠른 참조

| 작업 | 접근 방법 |
|------|----------|
| 콘텐츠 읽기/분석 | `python -m markitdown presentation.pptx` |
| 템플릿 편집 또는 생성 | [프레젠테이션 편집](references/editing.md) 참조 |
| 처음부터 생성 (IBM 일반) | 아래 [처음부터 생성 워크플로](#처음부터-생성--워크플로) 참조 |
| webMethods 셀러 덱 생성 | [webMethods 템플릿 가이드](references/webmethods-template.md) 참조 |

| 항목 | IBM 값 |
|------|--------|
| **캔버스** | 26.67" × 15.00" (`LAYOUT_CUSTOM`) |
| **색상** | 6자리 HEX (# 없이, 예: `"0F62FE"`) |
| **기본 폰트** | IBM Plex Sans KR (다양한 굵기) |
| **한국어/CJK 폰트** | IBM Plex Sans KR (모든 굵기) |
| **최소 폰트 크기** | 본문/레이블 **28pt** (표 내부만 20pt 허용) |
| **페이지 번호 위치** | x=25.75" y=14.16" w=0.30" h=0.27" |
| **왼쪽 콘텐츠 여백** | 0.63" |
| **IBM Blue 액센트** | `#0F62FE` |
| **테마 키** | `primary`, `secondary`, `accent`, `light`, `bg` |
| **도형** | RECTANGLE, OVAL, LINE, ROUNDED_RECTANGLE |
| **차트** | BAR, LINE, PIE, DOUGHNUT, SCATTER, BUBBLE, RADAR |

## 참조 파일

| 파일 | 내용 |
|------|------|
| [slide-types.md](references/slide-types.md) | IBM 슬라이드 구조: 표지, TOC, 섹션 구분자, 13개 IBM 콘텐츠 템플릿 카테고리, 엔딩 — IBM 좌표, 폰트 크기, JS 예제 포함 |
| [design-system.md](references/design-system.md) | IBM Carbon 색상, IBM Plex KR 타이포그래피, IBM 레이아웃 그리드, IBM 디자인 규칙 |
| [editing.md](references/editing.md) | 템플릿 기반 편집 워크플로, IBM 규격 점검, XML 조작, 서식 규칙 |
| [pitfalls.md](references/pitfalls.md) | IBM QA 체크리스트, IBM 특화 실수 유형, PptxGenJS 주요 함정 |
| [pptxgenjs.md](references/pptxgenjs.md) | PptxGenJS 전체 API 레퍼런스 |
| [webmethods-template.md](references/webmethods-template.md) | **webMethods Hybrid Integration 셀러 덱 스타일** — 레이아웃, 색상 사용법, 폰트 크기, 섹션 패턴, JS 예제 |

---

## 콘텐츠 읽기

```bash
# 텍스트 추출
python -m markitdown presentation.pptx
```

---

## 처음부터 생성 — 워크플로

**템플릿이나 참조 프레젠테이션이 없을 때 사용합니다.**

### 1단계: 조사 및 요구사항 파악

사용자 요구사항(주제, 대상, 목적, 톤, 콘텐츠 깊이)을 파악합니다.
**IBM 일반** 또는 **webMethods 셀러 덱** 스타일 중 무엇을 사용할지 결정합니다.

### 2단계: IBM 캔버스 및 테마 설정

IBM 커스텀 캔버스와 Carbon 테마를 정의합니다:

```javascript
pres.defineLayout({ name: 'IBM', width: 26.67, height: 15.00 });
pres.layout = 'IBM';
```

IBM 테마 객체 사용:

```javascript
const theme = {
  primary:   "000000",   // 검정 — 흰 배경의 본문 텍스트, 제목
  secondary: "414141",   // 진한 회색 — 보조 텍스트, 표 본문
  accent:    "0F62FE",   // IBM Blue — 액센트, 페이지 번호, 하이라이트
  light:     "BAE6FF",   // 연한 파란색 — 레이블 띠, 은은한 채우기
  bg:        "FFFFFF"    // 흰색 — 기본 슬라이드 배경
};
```

전체 내용은 [IBM Design System](references/design-system.md)을 참고하세요.

### 3단계: 덱 구조 계획

코드 생성 전 모든 슬라이드를 계획합니다:

1. **슬라이드 1**: 표지 — 필수, 페이지 번호 없음
2. **슬라이드 2** (선택): 셀러 가이던스 / 법적 고지 — 셀러/제품 덱용
3. **슬라이드 3** (선택): TOC — 섹션이 3개 이상일 때 추가
4. **중간 슬라이드**: 섹션 구분자 + 콘텐츠 슬라이드 — 각각 IBM 템플릿 카테고리 하나씩
5. **마지막 슬라이드**: 엔딩 — 필수, 페이지 번호 없음

콘텐츠 슬라이드마다 [slide-types.md](references/slide-types.md)에서 IBM 템플릿 카테고리를 하나 선택합니다. [템플릿 선택 가이드](references/slide-types.md#template-selection-guide)로 콘텐츠 유형에 맞는 카테고리를 고릅니다. **시각적 다양성**을 유지하세요 — 연속된 슬라이드에 같은 카테고리를 반복하지 마세요.

webMethods 스타일 덱은 [webmethods-template.md](references/webmethods-template.md)의 섹션 및 레이아웃 패턴을 따르세요.

### 4단계: 슬라이드 JS 파일 생성

`slides/` 디렉터리에 슬라이드별 JS 파일을 각각 생성합니다. 각 파일은 동기(synchronous) `createSlide(pres, theme)` 함수를 내보내야 합니다. [슬라이드 출력 형식](#슬라이드-출력-형식)과 [slide-types.md](references/slide-types.md)의 타입별 가이드를 따릅니다. 가능하면 서브에이전트를 활용해 슬라이드 최대 5개를 동시에 생성합니다.

**각 서브에이전트에 전달할 내용:**
1. 파일 명명: `slides/slide-01.js`, `slides/slide-02.js` 등
2. 이미지 저장 경로: `slides/imgs/`
3. 최종 PPTX 저장 경로: `slides/output/`
4. **IBM 캔버스: 26.67" × 15.00"** — `pres.defineLayout({ name:'IBM', width:26.67, height:15.00 })` 사용
5. **IBM 폰트: IBM Plex Sans KR** (굵기: Light, Regular, Medm, SmBld, ExtLt)
6. **최소 폰트 크기: 28pt** (모든 IBM Plex Sans KR 텍스트, 표 내부만 20pt 허용)
7. 색상: # 없이 6자리 HEX (예: `"0F62FE"`)
8. IBM 테마 객체 규약을 반드시 사용 ([테마 객체 규약](#테마-객체-규약-필수) 참조)
9. [PptxGenJS API 레퍼런스](references/pptxgenjs.md)를 반드시 따를 것
10. **슬라이드 1 = 표지 (페이지 번호 없음)**, **마지막 슬라이드 = 엔딩 (페이지 번호 없음)**, 나머지는 x=25.75" y=14.16"에 페이지 번호 포함

### 5단계: 최종 PPTX로 컴파일

모든 슬라이드 모듈을 합치는 `slides/compile.js`를 생성합니다:

```javascript
// slides/compile.js
const pptxgen = require('pptxgenjs');
const pres = new pptxgen();

// IBM 커스텀 캔버스 — 26.67" × 15.00"
pres.defineLayout({ name: 'IBM', width: 26.67, height: 15.00 });
pres.layout = 'IBM';

// IBM Carbon 테마
const theme = {
  primary:   "000000",   // 검정 — 본문 텍스트, 제목
  secondary: "414141",   // 진한 회색 — 보조 텍스트
  accent:    "0F62FE",   // IBM Blue — 액센트, 페이지 번호
  light:     "BAE6FF",   // 연한 파란색 — 레이블 띠
  bg:        "FFFFFF"    // 흰색 — 기본 배경
};

for (let i = 1; i <= 12; i++) {  // 슬라이드 수에 맞게 조정
  const num = String(i).padStart(2, '0');
  const slideModule = require(`./slide-${num}.js`);
  slideModule.createSlide(pres, theme);
}

pres.writeFile({ fileName: './output/presentation.pptx' });
```

실행: `cd slides && node compile.js`

### 6단계: QA (필수)

[QA 프로세스](references/pitfalls.md#qa-process)와 [IBM QA 체크리스트](references/pitfalls.md#ibm-qa-checklist-run-before-declaring-success)를 참고하세요.

**IBM QA 체크리스트:**
- [ ] 슬라이드 1이 페이지 번호 없는 표지 슬라이드인지 확인
- [ ] 마지막 슬라이드가 페이지 번호 없는 엔딩 슬라이드인지 확인
- [ ] 표지·엔딩을 제외한 모든 슬라이드에 x=25.75" y=14.16" 위치의 페이지 번호 있는지 확인
- [ ] 모든 본문/레이블 텍스트가 28pt 이상인지 확인 (표 내부만 20pt 허용)
- [ ] 폰트 패밀리가 전체적으로 IBM Plex Sans KR인지 확인 — 다른 폰트 없음
- [ ] 이탤릭체 텍스트 없는지 확인
- [ ] 캔버스가 26.67" × 15.00"인지 확인
- [ ] IBM Carbon 팔레트 색상만 사용됐는지 확인
- [ ] 그라디언트나 애니메이션 없는지 확인
- [ ] 제목이 왼쪽 정렬인지 확인

### 출력 구조

```
slides/
├── slide-01.js          # 표지 슬라이드 (페이지 번호 없음)
├── slide-02.js          # 셀러 가이던스 / 법적 고지 (선택)
├── slide-03.js          # TOC (선택)
├── slide-04.js          # 섹션 구분자
├── ...
├── slide-NN.js          # 엔딩 슬라이드 (페이지 번호 없음)
├── imgs/                # 슬라이드에 사용하는 이미지
└── output/              # 최종 결과물
    └── presentation.pptx
```

---

## 슬라이드 출력 형식

각 슬라이드는 **완전히 실행 가능한 JS 파일**입니다:

```javascript
// slide-01.js — IBM 표지 슬라이드
const pptxgen = require("pptxgenjs");

const slideConfig = {
  type: 'cover',
  index: 1,
  title: '프레젠테이션 제목'
};

// 반드시 동기(synchronous) 함수여야 함 (async 금지)
function createSlide(pres, theme) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // IBM 표지: 상단 눈썹(eyebrow) 레이블
  slide.addText("IBM Client Presentation", {
    x: 0.63, y: 0.42, w: 11.05, h: 0.63,
    fontSize: 28, fontFace: "IBM Plex Sans KR Medm",
    color: theme.primary, bold: false, align: "left"
  });

  // IBM 표지: 왼쪽 큰 제목 (IBM Plex Sans KR Light)
  slide.addText(slideConfig.title, {
    x: 0.63, y: 1.25, w: 11.05, h: 10,
    fontSize: 64, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left"
  });

  // 오른쪽 절반: 이미지 플레이스홀더
  // slide.addImage({ path: "imgs/cover.jpg", x: 13.96, y: 0.63, w: 12.08, h: 13.76 });

  // 표지 슬라이드에는 페이지 번호 없음

  return slide;
}

// 단독 미리보기
if (require.main === module) {
  const pres = new pptxgen();
  pres.defineLayout({ name: 'IBM', width: 26.67, height: 15.00 });
  pres.layout = 'IBM';
  const theme = {
    primary:   "000000",
    secondary: "414141",
    accent:    "0F62FE",
    light:     "BAE6FF",
    bg:        "FFFFFF"
  };
  createSlide(pres, theme);
  pres.writeFile({ fileName: "slide-01-preview.pptx" });
}

module.exports = { createSlide, slideConfig };
```

---

## 테마 객체 규약 (필수)

컴파일 스크립트는 다음 **정확한 키**를 가진 테마 객체를 전달합니다:

| 키 | IBM 값 | 목적 |
|----|--------|------|
| `theme.primary` | `"000000"` | 검정 — 흰 배경의 본문 텍스트, 제목 |
| `theme.secondary` | `"414141"` | 진한 회색 — 보조 텍스트, 표 본문 |
| `theme.accent` | `"0F62FE"` | IBM Blue — 액센트, 하이라이트, 페이지 번호 |
| `theme.light` | `"BAE6FF"` | 연한 파란색 — 레이블 띠, 은은한 채우기 |
| `theme.bg` | `"FFFFFF"` | 흰색 — 기본 슬라이드 배경 |

`background`, `text`, `muted`, `darkest`, `lightest` 같은 **다른 키 이름은 절대 사용하지 마세요**.

---

## IBM 페이지 번호 (표지·엔딩 외 모든 슬라이드에 필수)

IBM 페이지 번호는 오른쪽 하단 고정 위치에 표시됩니다.

- **위치**: x=25.75" y=14.16" w=0.30" h=0.27"
- **폰트**: `IBM Plex Sans KR Light`, 약 12pt
- 현재 번호만 표시 (예: `3`), "3/12" 형식 금지
- **표지 슬라이드 (슬라이드 1)**: 페이지 번호 없음
- **엔딩 슬라이드 (마지막 슬라이드)**: 페이지 번호 없음

```javascript
// IBM 페이지 번호 — 표지·엔딩을 제외한 모든 슬라이드에 추가
slide.addText(String(slideIndex), {
  x: 25.75, y: 14.16, w: 0.30, h: 0.27,
  fontSize: 12, fontFace: "IBM Plex Sans KR Light",
  color: "000000", align: "center", valign: "middle"
});
```

또는 IBM Blue 원형 변형 사용:

```javascript
// IBM Blue 원형 페이지 번호
slide.addShape(pres.shapes.OVAL, {
  x: 25.7, y: 14.1, w: 0.4, h: 0.4,
  fill: { color: theme.accent }
});
slide.addText(String(slideIndex), {
  x: 25.7, y: 14.1, w: 0.4, h: 0.4,
  fontSize: 12, fontFace: "IBM Plex Sans KR Light",
  color: "FFFFFF", bold: false,
  align: "center", valign: "middle"
});
```

---

## 의존성

- `pip install "markitdown[pptx]"` — 텍스트 추출
- `npm install -g pptxgenjs` — 처음부터 생성
- `npm install -g react-icons react react-dom sharp` — 아이콘 (선택)
