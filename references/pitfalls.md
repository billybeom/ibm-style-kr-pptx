# QA 프로세스 및 일반적인 함정

## IBM QA Checklist (Run Before Declaring Success) {#ibm-qa-checklist-run-before-declaring-success}

- [ ] **슬라이드 1은 표지** — 페이지 번호 없음, 대형 제목 좌측, 선택적 이미지 우측
- [ ] **마지막 슬라이드는 엔딩** — 페이지 번호 없음, IBM 브랜드 마무리
- [ ] **표지·엔딩 외 모든 슬라이드에 페이지 번호** (x=25.75" y=14.16")
- [ ] **모든 본문/레이블 텍스트는 28pt 이상** (표 내부만 20pt 허용)
- [ ] **폰트 패밀리는 전체 IBM Plex Sans KR** — Arial, Helvetica, Calibri 등 없음
- [ ] **이탤릭체 없음** — IBM Plex는 프레젠테이션에서 로만체만 사용
- [ ] **캔버스는 26.67" × 15.00"** — 표준 LAYOUT_16x9 아님
- [ ] **IBM Carbon 팔레트 색상만 사용** — IBM 이외 색상 없음
- [ ] **그라디언트·애니메이션 없음**
- [ ] **제목 왼쪽 정렬** — 가운데 정렬 아님
- [ ] **콘텐츠는 x=0.63"에서 시작** — 일관된 왼쪽 여백
- [ ] **y=13.5" 아래에 콘텐츠 없음** — 푸터 영역 예약됨

---

## QA Process {#qa-process}

**문제가 있다고 가정하십시오. 당신의 역할은 그것을 찾아내는 것입니다.**

첫 번째 렌더링이 올바를 가능성은 거의 없습니다. QA를 확인 단계가 아닌 버그 사냥으로 접근하십시오. 첫 번째 검사에서 문제를 발견하지 못했다면 충분히 꼼꼼히 보지 않은 것입니다.

### node compile.js 실행 후 검증

```bash
cd slides && node compile.js
```

- 오류 없이 실행 완료되는지 확인
- PowerPoint로 직접 열어 **복구 팝업이 없는지** 확인
- 각 슬라이드 육안 검토

### 콘텐츠 QA

```bash
python -m markitdown output.pptx
```

누락된 콘텐츠, 오타, 잘못된 순서를 확인하십시오.

**남은 플레이스홀더 텍스트 확인:**

```bash
python -m markitdown output.pptx | grep -iE "xxxx|lorem|ipsum|placeholder|this.*(page|slide).*layout"
```

grep 결과가 있으면 완료 선언 전에 수정하십시오.

### 검증 루프

1. 슬라이드 생성 → `python -m markitdown output.pptx`로 텍스트 추출 → 콘텐츠 검토
2. 위의 **IBM QA 체크리스트 실행** — 모든 항목 확인
3. **발견된 문제 목록 작성** (없다면 더 비판적으로 다시 확인)
4. 문제 수정
5. **영향받은 슬라이드 재검증** — 하나의 수정이 종종 다른 문제를 만듦
6. 새로운 문제 없이 전체 검사를 통과할 때까지 반복

**수정 및 재검증 사이클을 최소 한 번 완료하기 전까지 완료를 선언하지 마십시오.**

### 슬라이드별 QA (처음부터 생성 시)

```bash
python -m markitdown slide-XX-preview.pptx
```

누락된 콘텐츠, 플레이스홀더 텍스트, 누락된 페이지 번호를 확인하십시오.

---

## IBM 특화 실수 방지

- **표지 슬라이드를 빠뜨리지 마십시오** — 모든 IBM 덱은 표지 슬라이드로 시작 (페이지 번호 없음)
- **엔딩 슬라이드를 빠뜨리지 마십시오** — 모든 IBM 덱은 엔딩 슬라이드로 종료 (페이지 번호 없음)
- **페이지 번호를 잊지 마십시오** — 표지·엔딩 외 모든 슬라이드에 x=25.75" y=14.16" 위치에 필요
- **IBM Plex Sans KR 이외 폰트 사용 금지** — Arial, Helvetica, Calibri 또는 다른 패밀리 금지
- **이탤릭체 사용 금지** — IBM Plex는 IBM 프레젠테이션에서 로만체만 사용
- **28pt 이하 사용 금지** — 표 본문 행에만 20pt 허용
- **일반 색상 팔레트 사용 금지** — IBM Carbon Design System 색상만 사용
- **제목 가운데 정렬 금지** — IBM은 왼쪽 정렬 제목 사용
- **y=13.5" 아래에 콘텐츠 배치 금지** — 푸터 및 페이지 번호 영역
- **그라디언트 사용 금지** — IBM은 Carbon 단색만 사용
- **연속 슬라이드에 같은 IBM 템플릿 카테고리 반복 금지**

---

## PptxGenJS 주요 함정

### ❌ writeFile() 사용 금지 — write(nodebuffer) 사용

`pres.writeFile()`은 내부 재처리 과정에서 whitespace를 재삽입할 수 있습니다.  
반드시 `pres.write({ outputType: "nodebuffer" })`로 버퍼를 받아 `fs.writeFileSync()`로 저장할 것.

```javascript
// ❌ 잘못된 예
pres.writeFile({ fileName: './output/presentation.pptx' });

// ✅ 올바른 예
const fs = require('fs');
const buffer = await pres.write({ outputType: "nodebuffer" });
fs.writeFileSync('./output/presentation.pptx', buffer);
```

### ❌ width: 26.67 사용 금지 — 26.67013888888889 사용

`26.67`은 pptxgenjs가 `24387048 EMU`로 반올림 → PowerPoint 정밀값 `24387175`와 불일치.  
반드시 `width: 26.67013888888889` (= 24387175 / 914400) 사용.

```javascript
// ❌ 잘못된 예 — EMU 불일치 발생
pres.defineLayout({ name: 'IBM', width: 26.67, height: 15.00 });

// ✅ 올바른 예
pres.defineLayout({ name: 'IBM', width: 26.67013888888889, height: 15.00 });
```

### ❌ createSlide()에서 async/await 절대 사용 금지

```javascript
// ❌ 잘못된 예 — compile.js가 await하지 않음
async function createSlide(pres, theme) { ... }

// ✅ 올바른 예
function createSlide(pres, theme) { ... }
```

### ❌ hex 색상에 "#" 절대 사용 금지

```javascript
color: "FF0000"      // ✅ 올바른 예
color: "#FF0000"     // ❌ 파일 손상
```

### ❌ hex 문자열에 불투명도 인코딩 절대 금지

```javascript
shadow: { color: "00000020" }              // ❌ 파일 손상
shadow: { color: "000000", opacity: 0.12 } // ✅ 올바른 예
```

### ❌ 호출 간 옵션 오브젝트 재사용 절대 금지

PptxGenJS가 오브젝트를 제자리에서 변경하므로 반드시 새 오브젝트를 생성해야 합니다.

```javascript
// ❌ 잘못된 예
const shadow = { type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 };
slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });
slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });

// ✅ 올바른 예 — 팩토리 함수 사용
const makeShadow = () => ({ type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 });
slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });
slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });
```

---

## PowerPoint 복구 팝업 디버깅 가이드

pptxgenjs로 생성한 PPTX를 PowerPoint로 열 때 복구 팝업이 뜨는 경우 아래 절차를 따르십시오.

### 핵심 원칙

- **추가한 fix가 오히려 복구 팝업을 유발할 수 있다** — fix를 추가할수록 오히려 나빠지는 경우가 있음
- **XSD 스펙 순서 ≠ PowerPoint 실제 동작** — 스펙보다 실제 동작이 기준
- **pptxgenjs가 생성하는 "비표준" 순서가 오히려 PowerPoint에서 더 안전한 경우도 있다**

### 이진탐색 디버깅 절차

1. **슬라이드 범위 격리**: 전체를 반씩 나눠 팝업 유발 범위 확정
2. **각 슬라이드 단독 테스트**: 모두 정상이면 → fix 충돌 문제
3. **fix 격리**: 최소 fix(빈 a:ln 제거, whitespace 제거, notesSlide 빈런 제거)만 적용한 버전이 정상인지 확인 → fix를 두 그룹으로 나눠 이진탐색

### ✅ 안전한 fix 목록 (적용해도 복구 팝업 없음)

- 빈 `<a:ln></a:ln>` 제거
- 태그 사이 whitespace 제거 (`>\s+<` → `><`)
- notesSlide 빈 런 제거
- bgPr에 effectLst 추가 (`</a:solidFill></p:bgPr>` → `</a:solidFill><a:effectLst/></p:bgPr>`)
- 자기닫기 태그 정규화 (`<p:nvPr></p:nvPr>` → `<p:nvPr/>` 등)
- txBody 누락 sp 보정
- `<a:pPr>` 속성 순서 정규화 (`marL` → `indent` → `algn`)
- XML 엔티티 역변환 (`&apos;` → `'`, `&quot;` → `"`, `&#x2022;` → `•`)
- 선 도형 음수 ext 교정 (`cy="-숫자"` → `cy="0"`)
- `_rels/.rels` officeDocument를 rId1으로 교정
- `presentation.xml` EMU 교정 (`24387048` → `24387175`)
- `presentation.xml` extLst(sldGuideLst) 블록 추가
- `presProps.xml` extLst(discardImageEditData, defaultImageDpi) 블록 추가
- `slideMaster1.xml` `<p:bg>` 블록 추가
- `notesMaster1.xml` `<p:sp>` 블록 제거
- `[Content_Types].xml` 유령 Override 제거, 미사용 Default 제거, 순서 재정렬

### ❌ 위험한 fix (복구 팝업 유발 확인됨)

- **`presentation.xml`의 `notesMasterIdLst`를 `sldMasterIdLst` 직후로 이동하는 순서 교정**
  - pptxgenjs가 생성하는 순서(`sldIdLst` 뒤)가 PowerPoint에서 더 안전함
  - XSD 스펙(`sldMasterIdLst` 직후)과 PowerPoint 실제 동작이 다름 — 스펙을 따르면 오히려 팝업 발생
