# webMethods Hybrid Integration — 셀러 덱 스타일 가이드

> 출처: `powerpoint-templates/webMethods_powerpoint_template.PPTX`  
> 분석 슬라이드 수: **48개** — IBM webMethods 셀러 발표 자료  
> IBM webMethods, Hybrid Integration, 셀러 중심 발표 자료를 만들 때 이 가이드를 사용하십시오.

---

## 목차

1. [캔버스 및 크기](#1-캔버스-및-크기)
2. [색상 팔레트](#2-색상-팔레트)
3. [타이포그래피](#3-타이포그래피)
4. [덱 구조](#4-덱-구조)
5. [슬라이드 패턴 카탈로그](#5-슬라이드-패턴-카탈로그)
   - [커버](#51-커버-슬라이드)
   - [셀러 가이던스 & 법적 고지](#52-셀러-가이던스--법적-고지)
   - [섹션 구분자 / 챕터 인트로](#53-섹션-구분자--챕터-인트로)
   - [스테이크홀더 / 페르소나 맵](#54-스테이크홀더--페르소나-맵)
   - [대형 스탯 / 대형 텍스트](#55-대형-스탯--대형-텍스트)
   - [2단 콘텐츠](#56-2단-콘텐츠)
   - [3단 콘텐츠](#57-3단-콘텐츠)
   - [4단 / 아이콘 그리드](#58-4단--아이콘-그리드)
   - [사용 사례 / 케이스 스터디](#59-사용-사례--케이스-스터디)
   - [이미지 + 텍스트 (반쪽 이미지)](#510-이미지--텍스트-반쪽-이미지)
   - [표 / 비교](#511-표--비교)
   - [엔딩](#512-엔딩-슬라이드)
6. [푸터 & 페이지 번호](#6-푸터--페이지-번호)
7. [디자인 규칙](#7-디자인-규칙)
8. [JS 코드 예시](#8-js-코드-예시)

---

## 1. 캔버스 및 크기

표준 IBM 캔버스와 동일:

| 속성 | 값 |
|------|----|
| **너비** | 26.67" (33.877 cm) |
| **높이** | 15.00" (38.1 cm) |
| **화면 비율** | 16:9 |
| **PptxGenJS 레이아웃** | `pres.defineLayout({ name:'IBM', width:26.67, height:15.00 })` |
| **좌측 콘텐츠 여백** | 0.63" |
| **상단 콘텐츠 여백** | 0.42"–0.63" |
| **푸터 영역 y 좌표** | ~14.02" |
| **슬라이드 번호 영역** | x=25.75" y=14.16" w=0.30" h=0.27" |

---

## 2. 색상 팔레트

webMethods 덱은 표준 IBM Carbon 팔레트를 특정 방식으로 강조합니다:

| 색상 | Hex | webMethods 덱에서의 사용 |
|------|-----|--------------------------|
| **IBM 블루** | `#0F62FE` | 주요 강조색 — 섹션 레이블, 카테고리 태그, 콜아웃 헤더, 페이지 번호 점 |
| **검정** | `#000000` | 메인 본문 텍스트, 슬라이드 제목 |
| **흰색** | `#FFFFFF` | 배경, 어두운 채우기 위 텍스트 |
| **연한 IBM 블루** | `accent1+lumMod20+lumOff80` | 섹션 구분자 배너 채우기 (IBM 블루 틴트 ~20% 명도) |
| **진한 회색** | `#414141` | 보조 본문 텍스트, 표 본문 |
| **회색 선** | `#929292` | 컬럼 구분선, 구분자 규칙 |
| **초록색** | `#229338` | 성장 수치, 긍정적 지표 |

### 배경 패턴

- **표준 콘텐츠 슬라이드**: 흰색 (`#FFFFFF`)
- **섹션 구분자 배너** (상단 띠, ~3cm 높이): 연한 IBM 블루 틴트 (`accent1+lumMod20+lumOff80`)  
  PptxGenJS에서는 가장 가까운 근사치 `"D0E2FF"` (Carbon Blue-10) 사용
- **사용 사례 / 케이스 스터디 우측 패널**: 이미지 배경 박스에 동일한 연한 블루 틴트 사용

---

## 3. 타이포그래피

webMethods 덱은 모든 레벨에서 **IBM Plex Sans KR**만 사용합니다:

| 폰트 | 굵기 | 크기 | 사용처 |
|------|------|------|--------|
| `IBM Plex Sans KR Light` | 300 | 84pt | 커버 메인 제목 |
| `IBM Plex Sans KR Light` | 300 | 35–36pt | 섹션 부제목, 인트로 본문 |
| `IBM Plex Sans KR Light` | 300 | 27–28pt | 카테고리/아이브로 레이블 (커버 & 섹션 구분자) |
| `IBM Plex Sans KR Light` | 300 | 23–24pt | 본문, 불릿 텍스트, 설명 텍스트 |
| `IBM Plex Sans KR Light` | 300 | 18–20pt | 법적 고지 / 소형 본문 |
| `IBM Plex Sans KR Light` | 300 | 12–14pt | 푸터 / 페이지 번호 |
| `IBM Plex Sans KR Medm` | 500 | 24pt | 컬럼 헤더, 역할 제목 (볼드 스타일 레이블) |
| `IBM Plex Sans KR SmBld` | 600 | 20pt | 표 헤더 행, 스윔레인 레이블 |

### webMethods 덱 전용 타이포그래피 규칙

- **아이브로/카테고리 태그** (슬라이드 제목 위): 27–28pt, `IBM Plex Sans KR Light`, IBM 블루 (`#0F62FE`), 볼드
- **슬라이드 제목**: 35–44pt, `IBM Plex Sans KR Light`, 검정 (`#000000`)
- **컬럼 역할 제목** (스테이크홀더 맵, 페르소나 카드): 24pt, `IBM Plex Sans KR Medm`, IBM 블루
- **본문 / 불릿 텍스트**: 22–24pt, `IBM Plex Sans KR Light`, 검정
- **법적 고지 텍스트**: 18pt, `IBM Plex Sans KR Light`, 검정
- **이탤릭체 금지** — 전체에서 로만체만 사용
- 행간: 본문 텍스트 전체에서 1.1×

---

## 4. 덱 구조

webMethods 셀러 덱은 아래 필수 흐름을 따릅니다:

```
[슬라이드 1: 커버]
[슬라이드 2: 셀러 가이던스 & 법적 고지]
[슬라이드 N: 섹션 구분자] → [콘텐츠 슬라이드…]
[슬라이드 N: 섹션 구분자] → [콘텐츠 슬라이드…]
…
[마지막 슬라이드: 엔딩 (블랭크 End slide 레이아웃)]
```

### 섹션 구성 패턴

webMethods 덱은 **주제별 섹션**으로 구성되며, 각 섹션 앞에 아래 요소를 포함한 섹션 구분자 슬라이드가 있습니다:
- 소형 **IBM 블루 아이브로 레이블** (좌측 상단, 27pt 볼드)
- 대형 **섹션 제목** (35pt, 검정, 2행으로 줄 바꿈)
- 시각적 다양성을 위한 **우측 반쪽 이미지**
- 상단을 가로지르는 **연한 파란색 배너 띠**

### 콘텐츠 밀도 규칙

| 슬라이드 유형 | 최대 텍스트 요소 | 이미지 사용 |
|--------------|----------------|-------------|
| 커버 | 2개 (아이브로 + 제목) | 1개 대형 우측 반쪽 이미지 |
| 섹션 구분자 | 2–3개 (레이블 + 제목 + 선택적 부제목) | 1개 우측 반쪽 이미지 |
| 사용 사례 | 5–8개 텍스트 블록 | 1–2개 지원 이미지 |
| 스테이크홀더 맵 | 4–5개 역할 제목 + 4–5개 설명 블록 | 없음 (아이콘/픽토그램만) |
| 2단 콘텐츠 | 컬럼 본문 2개 + 제목 1개 | 0–2개 이미지 |
| 엔딩 | 0 | 0 (레이아웃 상속 IBM 브랜딩) |

---

## 5. 슬라이드 패턴 카탈로그

### 5.1 커버 슬라이드

**레이아웃**: `Cover, plain` (우측 반쪽 이미지가 있는 흰색 커버)

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 아이브로 레이블 | 0.63" | 0.42" | 11.05" | 0.63" | `IBM Plex Sans KR Medm` | 28pt | `#0F62FE` |
| 메인 제목 | 0.63" | 1.08" | 11.05" | 11.33" | `IBM Plex Sans KR Light` | 84pt | `#000000` |
| 서브 정보 (레벨, 날짜, 연락처) | 0.63" | 8.00" | 11.05" | 6.00" | `IBM Plex Sans KR Light` | 24–28pt | `#000000` |
| 우측 이미지 | 14.10" | 0.56" | 11.97" | 13.90" | — | — | — |

**규칙**:
- 제목은 84pt에서 세로 탭(`\v`) 줄 바꿈을 사용해 ~3–5개의 짧은 행으로 구성
- 서브 정보 블록에 발표 레벨, 발표자 이름, 이메일, 직책 목록 표시
- 우측 이미지는 슬라이드 절반을 채움 — 슬라이드 높이에 맞게 크롭
- **페이지 번호 없음**

---

### 5.2 셀러 가이던스 & 법적 고지

**레이아웃**: `Legal disclaimer, two columns`

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 제목 | 0.63" | 0.63" | 6.80" | 3.13" | `IBM Plex Sans KR Light` | 68pt | `#000000` |
| 좌측 본문 (고지 컬럼 1) | 0.63" | 5.54" | 5.44" | 1.14" | `IBM Plex Sans KR Light` | 28pt | `#000000` |
| 가운데 본문 (법적 텍스트) | 0.63" | 0.63" | 5.95" | 12.51" | `IBM Plex Sans KR Light` | 18pt | `#000000` |
| 우측 본문 (추가 법적 내용) | 6.98" | 0.63" | 6.68" | 12.51" | `IBM Plex Sans KR Light` | 18pt | `#000000` |
| 세로 구분선 | — | — | — | — | — | — | `#000000` 선, 1pt |

**규칙**:
- "셀러 가이던스 및 법적 고지" 제목을 68pt로 두 줄에 걸쳐 표시
- 소형 법적 텍스트 두 컬럼을 x≈13.35"와 x≈20.05"의 얇은 세로선으로 구분
- 좌측 하단에 IBM 기밀 고지 볼드 표시: "IBM and Business Partner Internal Use Only"

---

### 5.3 섹션 구분자 / 챕터 인트로

**레이아웃**: `Blank slide` (커스텀)

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 상단 배너 (사각형) | 0" | 0.10" | 26.67" | 3.03" | — | — | `D0E2FF` (IBM 블루 틴트) |
| 아이브로 레이블 | 0.49" | 0.59" | 11.87" | 0.99" | `IBM Plex Sans KR Light` | 27–28pt 볼드 | `#0F62FE` |
| 섹션 제목 | 0.49" | 1.08" | 11.38" | 1.98" | `IBM Plex Sans KR Light` | 35–36pt | `#000000` |
| 본문 텍스트 (선택) | 0.49" | 3.55" | 5.94" | 10.87" | `IBM Plex Sans KR Light` | 23–24pt | `#000000` |
| 우측 이미지 | 13.35" | 0.07" | 13.40" | 7.54" | — | — | — |
| 하단 우측 틴트 박스 | 13.35" | 7.53" | 13.40" | 7.50" | — | — | `D0E2FF` |

**규칙**:
- 연한 파란색 배너가 슬라이드 상단 ~3cm를 전체 너비로 가로질러 확장
- 아이브로 레이블은 볼드 IBM 블루 (챕터/모듈 식별)
- 섹션 제목은 더 크게 (35pt), 검정, 좌측 정렬
- 섹션 제목 아래에 선택적으로 23pt 설명 단락 배치
- 우측 반쪽 이미지 + 연한 파란색 하단 박스로 시각적 균형 형성

---

### 5.4 스테이크홀더 / 페르소나 맵

**레이아웃**: `Blank slide` (커스텀 그리드)

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 슬라이드 헤드라인 | 0.63" | 1.53" | 22.25" | 1.53" | `IBM Plex Sans KR Light` | 42pt | `#000000` (theme:text2) |
| 상단 배너 | 0" | 0.10" | 26.67" | 3.03" | — | — | `D0E2FF` |
| 세로 컬럼 구분선 (×3) | x 변동 | 3.57" | 0cm | 30.5cm | — | — | `#929292` 선 |
| 수평 행 구분선 (상단) | 0.63" | 6.60" | 71.25cm | 0cm | — | — | `#929292` 선 |
| 수평 행 구분선 (하단) | 0.63" | 10.88" | 71.25cm | 0cm | — | — | `#929292` 선 |
| 역할 제목 (컬럼별) | x 변동 | 4.96" | 3.62" | 0.67" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` (accent1) |
| 설명 레이블 | 0.57" | 6.62" | 2.51" | 0.74" | `IBM Plex Sans KR Light` | 24pt | `#0F62FE` |
| 설명 텍스트 | x 변동 | 6.81" | 3.96" | 3.65" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |
| 직책 레이블 | 0.60" | 10.89" | 1.93" | 1.22" | `IBM Plex Sans KR Light` 볼드 | 20pt | `#0F62FE` |
| 직책 텍스트 | x 변동 | 10.90" | 4.49" | 1.22" | `IBM Plex Sans KR Light` | 20–24pt | `#000000` |

**컬럼 x 위치 (4개 컬럼)**:
- 컬럼 1: x = 0.63" (x_emu ≈ 574,413)
- 컬럼 2: x = 2.78" (x_emu ≈ 2,535,014)
- 컬럼 3: x = 6.73" (x_emu ≈ 6,150,228)
- 컬럼 4: x = 17.57" (x_emu ≈ 16,059,440)

---

### 5.5 대형 스탯 / 대형 텍스트

**레이아웃**: `Large text` 또는 `Blank slide`

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 대형 수치 | 0.63" | 0.42" | 18.75" | 6.00" | `IBM Plex Sans KR Medm` | 130–168pt | `#0F62FE` 또는 `#229338` |
| 지원 레이블 | 0.63" | 6.00" | 18.75" | 2.00" | `IBM Plex Sans KR Light` | 36–44pt | `#000000` |
| 부제목 / 맥락 | 0.63" | 8.00" | 18.75" | 4.00" | `IBM Plex Sans KR Light` | 24–28pt | `#414141` |

**규칙**:
- 슬라이드당 지배적인 숫자/수치 하나
- 중립/제품 수치는 IBM 블루, 성장/긍정적 수치는 초록
- 지원 텍스트는 간결하게 (28pt에서 최대 2행)

---

### 5.6 2단 콘텐츠

**레이아웃**: `Text, 2 wide columns`

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 슬라이드 제목 | 0.63" | 0.63" | 25.41" | 2.09" | `IBM Plex Sans KR Light` | 35–44pt | `#000000` |
| 좌측 컬럼 헤더 | 0.63" | 3.33" | 11.05" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 좌측 컬럼 본문 | 0.63" | 4.33" | 11.05" | 9.01" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |
| 우측 컬럼 헤더 | 13.98" | 3.33" | 11.04" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 우측 컬럼 본문 | 13.98" | 4.33" | 11.04" | 9.01" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |

**규칙**:
- 컬럼 헤더는 IBM 블루 `#0F62FE`, Medium 굵기
- 본문 텍스트는 Light 굵기, 검정
- 불릿 목록: 불릿 문자 `•`, `IBM Plex Sans KR Light`, 들여쓰기 ~27pt
- 두 컬럼 모두 y=3.33"에서 시작 (표준 콘텐츠 영역 시작)

---

### 5.7 3단 콘텐츠

**레이아웃**: `Text, 4 columns` (4개 중 3개 컬럼 사용)

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 슬라이드 제목 | 0.63" | 0.63" | 5.40" | 1.67" | `IBM Plex Sans KR Light` | 35–44pt | `#000000` |
| 컬럼1 헤더 | 0.63" | 3.33" | 5.42" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 컬럼1 본문 | 0.63" | 4.33" | 5.42" | 9.01" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |
| 컬럼2 헤더 | 7.30" | 3.33" | 5.41" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 컬럼2 본문 | 7.30" | 4.33" | 5.41" | 9.01" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |
| 컬럼3 헤더 | 13.98" | 3.33" | 5.42" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 컬럼3 본문 | 13.98" | 4.33" | 5.42" | 9.01" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |

---

### 5.8 4단 / 아이콘 그리드

**레이아웃**: `Text, 4 columns` 또는 `Boxes, 4 horizontal, large title`

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 대형 제목 | 0.63" | 0.42" | 12.07" | 4.60" | `IBM Plex Sans KR Light` | 44pt | `#000000` |
| 아이콘 (컬럼별) | x 변동 | 7.30" | 0.80" | 0.80" | — | — | — |
| 컬럼 헤더 | x 변동 | 7.30" | 5.41" | 1.00" | `IBM Plex Sans KR Medm` | 24pt | `#0F62FE` |
| 컬럼 본문 | x 변동 | 8.30" | 5.41" | 5.04" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |

**컬럼 x 위치** (4개 동등한 컬럼):
- 컬럼 1: 0.63" | 컬럼 2: 7.29" | 컬럼 3: 13.96" | 컬럼 4: 20.63"

---

### 5.9 사용 사례 / 케이스 스터디

**레이아웃**: `Blank slide` (커스텀 — 좌측 내러티브 + 우측 과제/해결책)

이 패턴은 명명된 사용 사례에 사용됩니다 (예: "ZillaForge" 케이스 스터디 슬라이드):

| 요소 | x | y | w | h | 폰트 | 크기 | 색상 |
|------|---|---|---|---|------|------|------|
| 케이스 태그 (아이브로) | 0.49" | 0.59" | 11.87" | 0.99" | `IBM Plex Sans KR Light` 볼드 | 27–28pt | `#0F62FE` |
| 슬라이드 제목 | 0.49" | 1.08" | 11.38" | 1.98" | `IBM Plex Sans KR Light` | 35–36pt | `#000000` |
| 내러티브 본문 (좌측) | 0.49" | 3.56" | 5.93" | 10.89" | `IBM Plex Sans KR Light` | 23–24pt | `#000000` |
| 세로 구분선 | 6.65" | 3.56" | 0cm | 10.39" | — | — | `#000000` 선 0.5pt |
| 우측 컬럼 헤더 | 7.17" | 3.56" | 5.68" | 0.99" | `IBM Plex Sans KR Light` 볼드 | 23–28pt | `#000000` |
| 우측 컬럼 불릿 | 7.17" | 4.56" | 5.68" | 5.94" | `IBM Plex Sans KR Light` | 22–24pt | `#000000` |
| 우측 이미지 (상단) | 13.35" | -0.01" | 13.40" | 7.54" | — | — | — |
| 우측 틴트 박스 (하단) | 13.35" | 7.54" | 13.40" | 7.50" | — | — | `D0E2FF` |
| 우측 회사 설명 | 13.62" | 7.76" | 12.15" | 4.45" | `IBM Plex Sans KR Light` | 35–36pt | `#000000` |

**규칙**:
- 좌측 반쪽: 내러티브 맥락 + 단락 형식 글
- 우측 반쪽 (상단): 지원 이미지
- 우측 반쪽 (하단): 회사 설명 또는 핵심 데이터가 있는 연한 파란색 틴트 박스
- 불릿 목록은 `•` 문자 불릿 사용

---

### 5.10 이미지 + 텍스트 (반쪽 이미지)

**레이아웃**: `Video or imagery, half, inset`

| 요소 | x | y | w | h |
|------|---|---|---|---|
| 좌측 이미지 | 0.63" | 0.63" | 13.30" | 13.30" |
| 우측 본문 | 13.96" | 3.33" | 11.04" | 10.01" |

**규칙**: 이미지는 좌측, 텍스트는 우측. 시각 자료가 주요 증거일 때 사용.

---

### 5.11 표 / 비교

**레이아웃**: `Table`

| 요소 | x | y | w | h |
|------|---|---|---|---|
| 제목 (좌측) | 0.63" | 0.63" | 5.41" | 4.37" |
| 표 본문 | 7.29" | 0.63" | 18.75" | 12.71" |

**표 디자인 규칙**:
- 헤더 행: `IBM Plex Sans KR SmBld`, 20pt, **IBM 블루 위 흰색** (`#0F62FE`)
- 본문 행: `IBM Plex Sans KR Light`, 20pt, `#414141` 텍스트, 흰색/`#F4F4F4` 교차 배경
- 테두리: 얇은 `#E0E0E0` 수평선만 (본문 세로 테두리 없음)
- 첫 번째 컬럼은 행 헤더로 볼드 가능

---

### 5.12 엔딩 슬라이드

**레이아웃**: `End slide` (IBM 브랜드 레이아웃 — 커스텀 콘텐츠 불필요)

- IBM 마스터 "End slide" 또는 "1_End slide" 레이아웃 사용
- 본문 텍스트나 도형 불필요 — 레이아웃이 브랜딩 제공
- **페이지 번호 없음**

마스터가 없을 때 PptxGenJS로 근사치 구현:

```javascript
function createEndingSlide(pres, theme) {
  const slide = pres.addSlide();
  slide.background = { color: "003A6D" };  // IBM 진한 남색

  slide.addText("감사합니다", {
    x: 0.63, y: 5.5, w: 20, h: 3,
    fontSize: 84, fontFace: "IBM Plex Sans KR Light",
    color: "FFFFFF", bold: false, align: "left"
  });

  slide.addText("ibm.com/products/webmethods", {
    x: 0.63, y: 11.5, w: 15, h: 0.8,
    fontSize: 24, fontFace: "IBM Plex Sans KR Light",
    color: "BAE6FF", bold: false, align: "left"
  });

  // 엔딩 슬라이드에 페이지 번호 없음
  return slide;
}
```

---

## 6. 푸터 & 페이지 번호

### 푸터

| 속성 | 값 |
|------|----|
| 위치 | x=0.63" y=14.02" w=5.42" h=0.42" |
| 폰트 | `IBM Plex Sans KR Light` 12–14pt |
| 색상 | `#000000` 또는 `#414141` |
| 내용 | 기밀 등급, 날짜, IBM 저작권 고지 (선택) |

### 페이지 번호

| 속성 | 값 |
|------|----|
| 위치 | x=25.75" y=14.16" w=0.30" h=0.27" |
| 폰트 | `IBM Plex Sans KR Light` ~12pt |
| 색상 | `#000000` |
| 형식 | 현재 슬라이드 번호만 — "n / 전체" 형식 아님 |

> **규칙**: 커버 (슬라이드 1), 셀러 가이던스 (슬라이드 2), 엔딩 (마지막 슬라이드)에는 페이지 번호가 없습니다. 그 외 모든 슬라이드에는 페이지 번호가 있어야 합니다.

---

## 7. 디자인 규칙

### ✅ 해야 할 것

- 모든 굵기에서 `IBM Plex Sans KR` 패밀리 단독 사용
- 슬라이드 제목은 **35–44pt** 이상 유지
- 아이브로 레이블, 컬럼 헤더, 콜아웃 카테고리 태그, 페이지 번호에 **IBM 블루 `#0F62FE`** 사용
- 모든 텍스트 좌측 정렬 — 본문 단락 가운데 정렬 금지
- 섹션 배너 채우기 및 케이스 스터디 우측 패널 배경에 **연한 파란색 틴트 `D0E2FF`** 사용
- 얇은 `#929292` 세로선으로 컬럼 구분
- 커버·가이던스·엔딩 외 모든 슬라이드에 페이지 번호 포함 (x=25.75" y=14.16")
- `•` 문자 불릿과 `IBM Plex Sans KR Light` 폰트로 불릿 목록 구성
- 모든 콘텐츠 요소의 좌측 여백 0.63" 유지
- 복잡한 슬라이드에서 논리적 행 구분에 **수평 회색 구분선** (`#929292`, ~0.75pt) 사용
- 본문 텍스트 행간 **1.1×** 유지

### ❌ 하지 말아야 할 것

- 이탤릭체 사용 금지
- 그라디언트, 3D 효과, 그림자 사용 금지
- y=13.5" 아래에 콘텐츠 배치 금지
- 폰트 패밀리 혼용 금지
- 제목 또는 본문 가운데 정렬 금지
- 슬라이드당 강조색 2가지 초과 사용 금지
- 경고/오류 외에 빨간색 사용 금지
- 텍스트나 도형에 드롭 섀도우 추가 금지

---

## 8. JS 코드 예시

### 섹션 구분자 (webMethods 스타일)

```javascript
function createSectionDivider(pres, theme, sectionLabel, sectionTitle, slideIndex) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 상단 배너 (IBM 블루 틴트)
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0.10, w: 26.67, h: 3.03,
    fill: { color: "D0E2FF" }, line: { color: "D0E2FF" }
  });

  // 아이브로 레이블 — IBM 블루, 볼드
  slide.addText(sectionLabel, {
    x: 0.49, y: 0.59, w: 11.87, h: 0.99,
    fontSize: 28, fontFace: "IBM Plex Sans KR Light",
    color: "0F62FE", bold: true, align: "left"
  });

  // 섹션 제목 — 검정, Light 굵기
  slide.addText(sectionTitle, {
    x: 0.49, y: 1.08, w: 11.38, h: 1.98,
    fontSize: 36, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left"
  });

  // 페이지 번호
  slide.addText(String(slideIndex), {
    x: 25.75, y: 14.16, w: 0.30, h: 0.27,
    fontSize: 12, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, align: "center", valign: "middle"
  });

  return slide;
}
```

### 2단 콘텐츠 (webMethods 스타일)

```javascript
function createTwoColumnSlide(pres, theme, title, leftHeader, leftBody, rightHeader, rightBody, slideIndex) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 슬라이드 제목
  slide.addText(title, {
    x: 0.63, y: 0.63, w: 25.41, h: 2.09,
    fontSize: 36, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left"
  });

  // 좌측 컬럼 헤더 (IBM 블루)
  slide.addText(leftHeader, {
    x: 0.63, y: 3.33, w: 11.05, h: 0.80,
    fontSize: 24, fontFace: "IBM Plex Sans KR Medm",
    color: "0F62FE", bold: false, align: "left"
  });

  // 좌측 컬럼 본문
  slide.addText(leftBody, {
    x: 0.63, y: 4.20, w: 11.05, h: 9.14,
    fontSize: 22, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left", valign: "top"
  });

  // 우측 컬럼 헤더 (IBM 블루)
  slide.addText(rightHeader, {
    x: 13.98, y: 3.33, w: 11.04, h: 0.80,
    fontSize: 24, fontFace: "IBM Plex Sans KR Medm",
    color: "0F62FE", bold: false, align: "left"
  });

  // 우측 컬럼 본문
  slide.addText(rightBody, {
    x: 13.98, y: 4.20, w: 11.04, h: 9.14,
    fontSize: 22, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left", valign: "top"
  });

  // 페이지 번호
  slide.addText(String(slideIndex), {
    x: 25.75, y: 14.16, w: 0.30, h: 0.27,
    fontSize: 12, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, align: "center", valign: "middle"
  });

  return slide;
}
```

### 사용 사례 슬라이드 (webMethods 스타일)

```javascript
function createUseCaseSlide(pres, theme, caseTag, slideTitle, narrative, challengeItems, slideIndex) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 아이브로 / 케이스 태그
  slide.addText(caseTag, {
    x: 0.49, y: 0.59, w: 11.87, h: 0.99,
    fontSize: 28, fontFace: "IBM Plex Sans KR Light",
    color: "0F62FE", bold: true, align: "left"
  });

  // 슬라이드 제목
  slide.addText(slideTitle, {
    x: 0.49, y: 1.08, w: 11.38, h: 1.98,
    fontSize: 36, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left"
  });

  // 좌측 내러티브 본문
  slide.addText(narrative, {
    x: 0.49, y: 3.56, w: 5.93, h: 10.89,
    fontSize: 24, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left", valign: "top"
  });

  // 세로 구분선
  slide.addShape(pres.shapes.LINE, {
    x: 6.65, y: 3.56, w: 0, h: 10.39,
    line: { color: "000000", width: 0.5 }
  });

  // 우측 컬럼 헤더 "과제"
  slide.addText("과제", {
    x: 7.17, y: 3.56, w: 5.68, h: 0.99,
    fontSize: 28, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: true, align: "left"
  });

  // 과제 불릿 목록
  const bulletItems = challengeItems.map(item => ({
    text: item,
    options: { bullet: { code: '2022' }, fontSize: 22, fontFace: "IBM Plex Sans KR Light", color: theme.primary }
  }));
  slide.addText(bulletItems, {
    x: 7.17, y: 4.56, w: 5.68, h: 9.89,
    align: "left", valign: "top"
  });

  // 우측 틴트 박스 (하단 우측 — 회사 정보)
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 13.35, y: 7.54, w: 13.40, h: 7.50,
    fill: { color: "D0E2FF" }, line: { color: "D0E2FF" }
  });

  // 페이지 번호
  slide.addText(String(slideIndex), {
    x: 25.75, y: 14.16, w: 0.30, h: 0.27,
    fontSize: 12, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, align: "center", valign: "middle"
  });

  return slide;
}
```

### 커버 슬라이드 (webMethods 스타일)

```javascript
function createCoverSlide(pres, theme, productName, levelLabel, speakers) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 아이브로 레이블 (IBM 블루, 볼드)
  slide.addText(levelLabel, {
    x: 0.63, y: 0.42, w: 11.05, h: 0.69,
    fontSize: 28, fontFace: "IBM Plex Sans KR Light",
    color: "0F62FE", bold: true, align: "left"
  });

  // 메인 제목 (제품명, 대형)
  slide.addText(productName, {
    x: 0.63, y: 1.08, w: 11.05, h: 6.00,
    fontSize: 84, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left"
  });

  // 발표자 정보 블록
  const speakerText = speakers.map(s => `${s.name}\t${s.email}\n${s.title}`).join('\n\n');
  slide.addText(speakerText, {
    x: 0.63, y: 7.50, w: 11.05, h: 6.50,
    fontSize: 24, fontFace: "IBM Plex Sans KR Light",
    color: theme.primary, bold: false, align: "left", valign: "top"
  });

  // 우측 반쪽 이미지 (실제 경로 입력)
  // slide.addImage({ path: "imgs/cover-hero.jpg", x: 14.10, y: 0.56, w: 11.97, h: 13.90 });

  // 커버에 페이지 번호 없음
  return slide;
}
```

---

## QA 체크리스트 (webMethods 덱 전용)

- [ ] 슬라이드 1은 커버 슬라이드 — 페이지 번호 없음
- [ ] 슬라이드 2는 셀러 가이던스 & 법적 고지 슬라이드 — 페이지 번호 없음
- [ ] 마지막 슬라이드는 End slide 레이아웃 — 페이지 번호 없음
- [ ] 모든 섹션 구분자에 상단 연한 파란색 배너 띠 있음
- [ ] 모든 섹션 구분자에 볼드 IBM 블루 아이브로 레이블 있음
- [ ] 모든 콘텐츠 슬라이드에 페이지 번호 (x=25.75" y=14.16")
- [ ] 모든 본문/레이블 텍스트는 22pt 이상 (법적 텍스트에만 18pt 허용)
- [ ] 폰트 패밀리는 전체에서 IBM Plex Sans KR
- [ ] 이탤릭체 없음
- [ ] 컬럼 헤더는 IBM 블루 (`#0F62FE`), Medium 굵기
- [ ] 불릿 목록은 `•` 문자 불릿 사용
- [ ] 세로 컬럼 구분선은 회색 (`#929292`), ~0.75pt
- [ ] 그라디언트 또는 애니메이션 없음
- [ ] 캔버스는 26.67" × 15.00"
