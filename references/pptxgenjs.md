# PptxGenJS 튜토리얼

## 설정 & 기본 구조

```javascript
const pptxgen = require("pptxgenjs");

let pres = new pptxgen();
pres.layout = 'LAYOUT_16x9';  // 또는 'LAYOUT_16x10', 'LAYOUT_4x3', 'LAYOUT_WIDE'
pres.author = '작성자 이름';
pres.title = '프레젠테이션 제목';

let slide = pres.addSlide();
slide.addText("안녕하세요!", { x: 0.5, y: 0.5, fontSize: 36, color: "363636" });

pres.writeFile({ fileName: "Presentation.pptx" });
```

## 레이아웃 치수

슬라이드 치수 (좌표 단위: 인치):
- `LAYOUT_16x9`: 10" x 5.625" (기본값)
- `LAYOUT_16x10`: 10" x 6.25"
- `LAYOUT_4x3`: 10" x 7.5"
- `LAYOUT_WIDE`: 13.3" x 7.5"

---

## 텍스트 & 서식

```javascript
// 기본 텍스트
slide.addText("단순 텍스트", {
  x: 1, y: 1, w: 8, h: 2, fontSize: 24, fontFace: "IBM Plex Sans KR",
  color: "363636", bold: true, align: "center", valign: "middle"
});

// 자간 (charSpacing 사용; letterSpacing은 무시됨)
slide.addText("간격이 넓은 텍스트", { x: 1, y: 1, w: 8, h: 1, charSpacing: 6 });

// 리치 텍스트 배열
slide.addText([
  { text: "볼드 ", options: { bold: true } },
  { text: "이탤릭 ", options: { italic: true } }
], { x: 1, y: 3, w: 8, h: 1 });

// 여러 줄 텍스트 (breakLine: true 필요)
slide.addText([
  { text: "1번째 줄", options: { breakLine: true } },
  { text: "2번째 줄", options: { breakLine: true } },
  { text: "3번째 줄" }  // 마지막 항목은 breakLine 불필요
], { x: 0.5, y: 0.5, w: 8, h: 2 });

// 텍스트 박스 여백 (내부 패딩)
slide.addText("제목", {
  x: 0.5, y: 0.3, w: 9, h: 0.6,
  margin: 0  // 도형이나 아이콘 등 다른 요소와 x 위치를 맞출 때 0으로 설정
});
```

**참고:** 텍스트 박스는 기본적으로 내부 여백이 있습니다. 도형, 선, 아이콘 등 다른 요소와 x 위치를 정밀하게 맞출 때는 `margin: 0`으로 설정하세요.

---

## 목록 & 불릿

```javascript
// 올바른 방법: 여러 개의 불릿
slide.addText([
  { text: "첫 번째 항목", options: { bullet: true, breakLine: true } },
  { text: "두 번째 항목", options: { bullet: true, breakLine: true } },
  { text: "세 번째 항목", options: { bullet: true } }
], { x: 0.5, y: 0.5, w: 8, h: 3 });

// 잘못된 방법: 유니코드 불릿 절대 사용 금지
slide.addText("* 첫 번째 항목", { ... });  // 이중 불릿 생성됨

// 하위 항목 및 번호 목록
{ text: "하위 항목", options: { bullet: true, indentLevel: 1 } }
{ text: "첫 번째", options: { bullet: { type: "number" }, breakLine: true } }
```

---

## 도형

```javascript
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0.5, y: 0.8, w: 1.5, h: 3.0,
  fill: { color: "FF0000" }, line: { color: "000000", width: 2 }
});

slide.addShape(pres.shapes.OVAL, { x: 4, y: 1, w: 2, h: 2, fill: { color: "0000FF" } });

slide.addShape(pres.shapes.LINE, {
  x: 1, y: 3, w: 5, h: 0, line: { color: "FF0000", width: 3, dashType: "dash" }
});

// 투명도 적용
slide.addShape(pres.shapes.RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "0088CC", transparency: 50 }
});

// 둥근 모서리 직사각형 (rectRadius는 ROUNDED_RECTANGLE에만 작동, RECTANGLE에는 안 됨)
// 직사각형 액센트 오버레이와 함께 사용하지 말 것 — 둥근 모서리를 덮지 못함. 대신 RECTANGLE 사용.
slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "FFFFFF" }, rectRadius: 0.1
});

// 그림자 적용
slide.addShape(pres.shapes.RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "FFFFFF" },
  shadow: { type: "outer", color: "000000", blur: 6, offset: 2, angle: 135, opacity: 0.15 }
});
```

그림자 옵션:

| 속성      | 타입   | 범위          | 비고                                                      |
|-----------|--------|---------------|-----------------------------------------------------------|
| `type`    | string | `"outer"`, `"inner"` | |
| `color`   | string | 6자리 HEX (예: `"000000"`) | `#` 접두사 없이; 8자리 HEX 금지 — 주의사항 참조 |
| `blur`    | number | 0–100 pt      | |
| `offset`  | number | 0–200 pt      | **반드시 양수 값** — 음수 값은 파일 손상 유발 |
| `angle`   | number | 0–359 도      | 그림자가 떨어지는 방향 (135 = 오른쪽 하단, 270 = 위쪽)  |
| `opacity` | number | 0.0–1.0       | 투명도에 이 속성 사용; 색상 문자열에 인코딩 금지          |

위쪽으로 그림자를 드리우려면 (예: 푸터 바 위에), `angle: 270`과 양수 offset을 사용하세요 — 음수 offset 절대 사용 금지.

**참고**: 그라디언트 채우기는 기본적으로 지원되지 않습니다. 대신 그라디언트 이미지를 배경으로 사용하세요.

---

## 이미지

### 이미지 소스

```javascript
// 파일 경로에서
slide.addImage({ path: "images/chart.png", x: 1, y: 1, w: 5, h: 3 });

// URL에서
slide.addImage({ path: "https://example.com/image.jpg", x: 1, y: 1, w: 5, h: 3 });

// Base64에서 (빠름, 파일 I/O 없음)
slide.addImage({ data: "image/png;base64,iVBORw0KGgo...", x: 1, y: 1, w: 5, h: 3 });
```

### 이미지 옵션

```javascript
slide.addImage({
  path: "image.png",
  x: 1, y: 1, w: 5, h: 3,
  rotate: 45,              // 0–359 도
  rounding: true,          // 원형 크롭
  transparency: 50,        // 0–100
  flipH: true,             // 수평 반전
  flipV: false,            // 수직 반전
  altText: "설명",         // 접근성
  hyperlink: { url: "https://example.com" }
});
```

### 이미지 크기 조정 모드

```javascript
// Contain — 안에 맞게, 비율 유지
{ sizing: { type: 'contain', w: 4, h: 3 } }

// Cover — 영역 채우기, 비율 유지 (일부 잘릴 수 있음)
{ sizing: { type: 'cover', w: 4, h: 3 } }

// Crop — 특정 부분 잘라내기
{ sizing: { type: 'crop', x: 0.5, y: 0.5, w: 2, h: 2 } }
```

### 치수 계산 (가로세로 비율 유지)

```javascript
const origWidth = 1978, origHeight = 923, maxHeight = 3.0;
const calcWidth = maxHeight * (origWidth / origHeight);
const centerX = (10 - calcWidth) / 2;

slide.addImage({ path: "image.png", x: centerX, y: 1.2, w: calcWidth, h: maxHeight });
```

### 지원 형식

- **표준**: PNG, JPG, GIF (GIF 애니메이션은 Microsoft 365에서 작동)
- **SVG**: 최신 PowerPoint/Microsoft 365에서 작동

---

## 아이콘

react-icons를 사용해 SVG 아이콘을 생성한 뒤, 범용 호환성을 위해 PNG로 래스터화합니다.

### 설정

```javascript
const React = require("react");
const ReactDOMServer = require("react-dom/server");
const sharp = require("sharp");
const { FaCheckCircle, FaChartLine } = require("react-icons/fa");

function renderIconSvg(IconComponent, color = "#000000", size = 256) {
  return ReactDOMServer.renderToStaticMarkup(
    React.createElement(IconComponent, { color, size: String(size) })
  );
}

async function iconToBase64Png(IconComponent, color, size = 256) {
  const svg = renderIconSvg(IconComponent, color, size);
  const pngBuffer = await sharp(Buffer.from(svg)).png().toBuffer();
  return "image/png;base64," + pngBuffer.toString("base64");
}
```

### 슬라이드에 아이콘 추가

```javascript
const iconData = await iconToBase64Png(FaCheckCircle, "#4472C4", 256);

slide.addImage({
  data: iconData,
  x: 1, y: 1, w: 0.5, h: 0.5  // 크기 단위: 인치
});
```

**참고**: 선명한 아이콘을 위해 size를 256 이상으로 설정하세요. size 매개변수는 래스터화 해상도를 제어하며, 슬라이드에서의 표시 크기(인치 단위의 `w`와 `h`)와는 다릅니다.

### 아이콘 라이브러리

설치: `npm install -g react-icons react react-dom sharp`

react-icons의 주요 아이콘 세트:
- `react-icons/fa` - Font Awesome
- `react-icons/md` - Material Design
- `react-icons/hi` - Heroicons
- `react-icons/bi` - Bootstrap Icons

---

## 슬라이드 배경

```javascript
// 단색
slide.background = { color: "F1F1F1" };

// 투명도 있는 색상
slide.background = { color: "FF3399", transparency: 50 };

// URL에서 이미지
slide.background = { path: "https://example.com/bg.jpg" };

// Base64에서 이미지
slide.background = { data: "image/png;base64,iVBORw0KGgo..." };
```

---

## 표

```javascript
slide.addTable([
  ["헤더 1", "헤더 2"],
  ["셀 1", "셀 2"]
], {
  x: 1, y: 1, w: 8, h: 2,
  border: { pt: 1, color: "999999" }, fill: { color: "F1F1F1" }
});

// 셀 병합이 있는 고급 표
let tableData = [
  [{ text: "헤더", options: { fill: { color: "6699CC" }, color: "FFFFFF", bold: true } }, "셀"],
  [{ text: "병합됨", options: { colspan: 2 } }]
];
slide.addTable(tableData, { x: 1, y: 3.5, w: 8, colW: [4, 4] });
```

---

## 차트

```javascript
// 막대 차트
slide.addChart(pres.charts.BAR, [{
  name: "매출", labels: ["Q1", "Q2", "Q3", "Q4"], values: [4500, 5500, 6200, 7100]
}], {
  x: 0.5, y: 0.6, w: 6, h: 3, barDir: 'col',
  showTitle: true, title: '분기별 매출'
});

// 꺾은선 차트
slide.addChart(pres.charts.LINE, [{
  name: "기온", labels: ["1월", "2월", "3월"], values: [32, 35, 42]
}], { x: 0.5, y: 4, w: 6, h: 3, lineSize: 3, lineSmooth: true });

// 파이 차트
slide.addChart(pres.charts.PIE, [{
  name: "점유율", labels: ["A", "B", "기타"], values: [35, 45, 20]
}], { x: 7, y: 1, w: 5, h: 4, showPercent: true });
```

### 더 보기 좋은 차트 만들기

기본 차트는 구식으로 보입니다. 다음 옵션을 적용하면 모던하고 깔끔한 모습이 됩니다:

```javascript
slide.addChart(pres.charts.BAR, chartData, {
  x: 0.5, y: 1, w: 9, h: 4, barDir: "col",

  // 커스텀 색상 (프레젠테이션 팔레트에 맞춤)
  chartColors: ["0D9488", "14B8A6", "5EEAD4"],

  // 깔끔한 배경
  chartArea: { fill: { color: "FFFFFF" }, roundedCorners: true },

  // 차분한 축 레이블
  catAxisLabelColor: "64748B",
  valAxisLabelColor: "64748B",

  // 은은한 그리드 (값 축만)
  valGridLine: { color: "E2E8F0", size: 0.5 },
  catGridLine: { style: "none" },

  // 막대 위에 데이터 레이블
  showValue: true,
  dataLabelPosition: "outEnd",
  dataLabelColor: "1E293B",

  // 단일 시리즈에는 범례 숨기기
  showLegend: false,
});
```

**주요 스타일 옵션:**
- `chartColors: [...]` — 시리즈/세그먼트용 HEX 색상
- `chartArea: { fill, border, roundedCorners }` — 차트 배경
- `catGridLine/valGridLine: { color, style, size }` — 그리드 선 (`style: "none"`으로 숨기기)
- `lineSmooth: true` — 곡선 (꺾은선 차트)
- `legendPos: "r"` — 범례 위치: "b", "t", "l", "r", "tr"

---

## 슬라이드 마스터

```javascript
pres.defineSlideMaster({
  title: 'TITLE_SLIDE', background: { color: '283A5E' },
  objects: [{
    placeholder: { options: { name: 'title', type: 'title', x: 1, y: 2, w: 8, h: 2 } }
  }]
});

let titleSlide = pres.addSlide({ masterName: "TITLE_SLIDE" });
titleSlide.addText("내 제목", { placeholder: "title" });
```

---

## 주요 함정

이 문제들은 파일 손상, 시각적 버그, 잘못된 출력을 유발합니다. 반드시 피하세요.

1. **HEX 색상에 "#" 절대 사용 금지** — 파일 손상 유발
   ```javascript
   color: "FF0000"      // 올바름
   color: "#FF0000"     // 잘못됨
   ```

2. **HEX 색상 문자열에 불투명도 인코딩 절대 금지** — 8자리 색상 (예: `"00000020"`)은 파일 손상. 대신 `opacity` 속성 사용.
   ```javascript
   shadow: { type: "outer", blur: 6, offset: 2, color: "00000020" }          // 파일 손상
   shadow: { type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.12 }  // 올바름
   ```

3. **`bullet: true` 사용** — "o" 같은 유니코드 기호 절대 사용 금지 (이중 불릿 생성됨)

4. **배열 항목 또는 텍스트 런 사이에 `breakLine: true` 사용**

5. **불릿과 함께 `lineSpacing` 사용 금지** — 과도한 간격 유발; 대신 `paraSpaceAfter` 사용

6. **프레젠테이션마다 새 인스턴스 필요** — `pptxgen()` 객체 재사용 금지

7. **옵션 객체를 여러 호출에 재사용 절대 금지** — PptxGenJS는 객체를 in-place로 변환 (예: 그림자 값을 EMU로 변환). 하나의 객체를 여러 호출에 공유하면 두 번째 도형이 손상됩니다.
   ```javascript
   const shadow = { type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 };
   slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });  // 두 번째 호출에서 이미 변환된 값 전달
   slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });

   const makeShadow = () => ({ type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 });
   slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });  // 매번 새 객체 생성
   slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });
   ```

8. **`ROUNDED_RECTANGLE`을 액센트 테두리와 함께 사용 금지** — 직사각형 오버레이 바가 둥근 모서리를 덮지 못합니다. 대신 `RECTANGLE` 사용.
   ```javascript
   // 잘못된 방법: 액센트 바가 둥근 모서리를 덮지 못함
   slide.addShape(pres.shapes.ROUNDED_RECTANGLE, { x: 1, y: 1, w: 3, h: 1.5, fill: { color: "FFFFFF" } });
   slide.addShape(pres.shapes.RECTANGLE, { x: 1, y: 1, w: 0.08, h: 1.5, fill: { color: "0891B2" } });

   // 올바른 방법: RECTANGLE을 사용하여 깔끔한 정렬
   slide.addShape(pres.shapes.RECTANGLE, { x: 1, y: 1, w: 3, h: 1.5, fill: { color: "FFFFFF" } });
   slide.addShape(pres.shapes.RECTANGLE, { x: 1, y: 1, w: 0.08, h: 1.5, fill: { color: "0891B2" } });
   ```

---

## 빠른 참조

- **도형**: RECTANGLE, OVAL, LINE, ROUNDED_RECTANGLE
- **차트**: BAR, LINE, PIE, DOUGHNUT, SCATTER, BUBBLE, RADAR
- **레이아웃**: LAYOUT_16x9 (10"x5.625"), LAYOUT_16x10, LAYOUT_4x3, LAYOUT_WIDE
- **정렬**: "left", "center", "right"
- **차트 데이터 레이블**: "outEnd", "inEnd", "center"
