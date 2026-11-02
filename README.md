# IBM 파워포인트 AI 스킬 (`ibm-pptx`)

IBM Carbon Design System과 **IBM Plex Sans KR** 폰트를 완벽히 준수하는 IBM 스타일 파워포인트 자료를 AI로 생성·편집·분석하는 스킬입니다.

---

## 지원하는 스타일

| 스타일 | 설명 | 참고 파일 |
|--------|------|-----------|
| **IBM 일반 템플릿** | 표준 IBM 클라이언트/내부 발표 자료 | [`PPTX-STYLE.md`](PPTX-STYLE.md), [`references/design-system.md`](references/design-system.md) |
| **webMethods 셀러 덱** | IBM webMethods Hybrid Integration 판매/제품 발표 자료 | [`references/webmethods-template.md`](references/webmethods-template.md) |

> **webMethods 스타일 요청 시**: "webMethods", "Hybrid Integration", "셀러 발표", 또는 `webMethods_powerpoint_template.pptx` 스타일로 만들어달라고 하면 자동으로 webMethods 전용 가이드를 사용합니다.

---

## 파일 구성

```
ibm-pptx/
├── SKILL.md                          # 스킬 정의 (AI가 읽는 핵심 파일)
├── PPTX-STYLE.md                     # IBM 슬라이드 스타일 전체 가이드 (80개 슬라이드, 15개 섹션 분석)
├── README.md                         # 이 파일
├── powerpoint-templates/
│   └── webMethods_powerpoint_template.PPTX  # webMethods 실제 템플릿 (48슬라이드)
├── references/
│   ├── design-system.md              # IBM Carbon 색상·폰트·그리드 규칙
│   ├── slide-types.md                # 슬라이드 유형별 레이아웃 + JS 예시
│   ├── editing.md                    # 기존 PPTX 편집 워크플로우
│   ├── pitfalls.md                   # IBM QA 체크리스트·실수 방지 가이드
│   ├── pptxgenjs.md                  # PptxGenJS API 전체 레퍼런스
│   └── webmethods-template.md        # webMethods 셀러 덱 전용 스타일 가이드
└── templates/
    ├── Templates-Cover/              # 커버 슬라이드 XML 템플릿 (12종)
    ├── Templates-Big-Trending/       # 대형 스탯/임팩트 슬라이드 (6종)
    ├── Templates-1-Column/           # 1단 레이아웃 (4종)
    ├── Templates-2-Columns/          # 2단 레이아웃 (16종)
    ├── Templates-3-Columns/          # 3단 레이아웃 (15종)
    ├── Templates-4-Columns/          # 4단 레이아웃 (7종)
    ├── Templates-2-Rows/             # 2행 레이아웃 (1종)
    ├── Templates-3-Rows/             # 3행 레이아웃 (4종)
    ├── Templates-2-Rows-2-Columns/   # 2행×2열 그리드 (4종)
    ├── Templates-2-Rows-3-Columns/   # 2행×3열 그리드 (1종)
    ├── Templates-2-Rows-4-Columns/   # 2행×4열 그리드 (2종)
    ├── Templates-3-Rows-3-Columns/   # 3행×3열 그리드 (1종)
    ├── Templates-Project-Plan/       # 프로젝트 플랜/간트 (2종)
    ├── Templates-Table/              # 표 레이아웃 (4종)
    └── Templates-Ending/             # 엔딩 슬라이드 (1종)
```

---

## 사전 준비

### 1. Node.js + PptxGenJS (필수 — 처음부터 생성 시)

```bash
npm install -g pptxgenjs
```

> 누락된 경우 스킬이 자동으로 설치를 시도합니다.

### 2. Python + markitdown (선택 — 기존 PPTX 텍스트 추출 시)

```bash
pip install "markitdown[pptx]"
```

---

## 설치 방법

### 글로벌 설치 (모든 프로젝트에서 사용)

```
~/.bob/skills/ibm-pptx/
```

### 프로젝트별 설치

```
./.bob/skills/ibm-pptx/
```

설치 후 폴더 구조:

```
.bob/skills/ibm-pptx/
├── SKILL.md
├── PPTX-STYLE.md
├── README.md
├── powerpoint-templates/
├── references/
└── templates/
```

IBM Bob이 자동으로 인식하며, 명시적으로 `/ibm-pptx`를 붙여 호출할 수도 있습니다.

---

## 사용 방법

### IBM 일반 스타일 덱 생성

```
/ibm-pptx IBM 스타일로 파워포인트 자료를 만들어 주세요.

IBM Instana를 소개하는 자료로, 엔드투엔드 풀스택 옵저버빌리티 플랫폼임을 강조하고
300개 이상의 기술을 즉시 지원하는 점을 부각해 주세요.

주요 차별점:
1. 자동 발견·자동 계측으로 제로 구성 시작 가능
2. 인프라·미들웨어·앱·EUM·신세틱 모니터링을 아우르는 풀스택 지원
3. MVS 기반 단순·예측 가능한 라이선스 모델
4. 모든 비즈니스 트랜잭션을 샘플링 없이 추적하는 고충실도 데이터

마지막 슬라이드는 Next Steps로, 고객과의 디스커버리 세션 제안으로 마무리해 주세요.
```

### webMethods 셀러 덱 생성

```
/ibm-pptx webMethods_powerpoint_template.pptx 스타일로
IBM webMethods Hybrid Integration 셀러 발표 자료를 만들어 주세요.

주제: API 관리 및 하이브리드 통합 플랫폼의 가치 제안
대상: 엔터프라이즈 IT 의사결정자 (CTO, IT 아키텍트)
섹션 구성:
1. 시장 현황 및 고객 과제
2. IBM webMethods 솔루션 소개
3. 주요 사용 사례 3가지
4. 가격 및 라이선스 안내
5. 경쟁사 비교
```

### 기존 PPTX 텍스트 추출

```
/ibm-pptx 이 파일의 내용을 요약해 주세요: presentation.pptx
```

생성된 덱은 `slides/output/` 폴더에 저장됩니다.

---

## IBM 스타일 핵심 규칙

| 항목 | 값 |
|------|----|
| **캔버스 크기** | 26.67" × 15.00" (16:9) |
| **기본 폰트** | IBM Plex Sans KR (Light / Regular / Medm / SmBld / ExtLt) |
| **최소 본문 폰트 크기** | 28pt (표 내부는 20pt 허용) |
| **IBM 블루** | `#0F62FE` |
| **기본 배경** | 흰색 `#FFFFFF` |
| **좌측 여백** | 0.63" |
| **페이지 번호 위치** | x=25.75" y=14.16" |
| **커버 슬라이드** | 페이지 번호 없음 |
| **엔딩 슬라이드** | 페이지 번호 없음 |
| **이탤릭체** | 금지 |
| **그라디언트·애니메이션** | 금지 |

---

## 슬라이드 구조

모든 IBM 덱은 아래 순서를 반드시 따릅니다:

```
[슬라이드 1: 커버]
  ↓
[슬라이드 2: 셀러 가이던스/법적 고지 — 선택, 셀러 덱 전용]
  ↓
[목차(TOC) — 선택, 섹션 3개 이상 시 권장]
  ↓
[섹션 구분자 + 콘텐츠 슬라이드 반복]
  ↓
[마지막 슬라이드: 엔딩]
```

---

## IBM 일반 템플릿 카탈로그 (80개 슬라이드, 15개 카테고리)

| 카테고리 | 슬라이드 수 | 주요 용도 |
|----------|------------|-----------|
| Cover | 12종 | 표지 — 이미지/텍스트/레이블 조합 |
| Big Trending | 6종 | 임팩트 스탯, 대형 인용구 |
| 1-Column | 4종 | 단일 내러티브, 이미지+텍스트 |
| 2-Columns | 16종 | 비교, 도전+해결책, 사례 연구 |
| 3-Columns | 15종 | 3가지 주제·프레임워크·역할 카드 |
| 4-Columns | 7종 | 4분면, 4가지 기둥·성과 |
| 2-Rows | 1종 | 상하 2행 구조 |
| 3-Rows | 4종 | 3행 수평 데이터 콜아웃 |
| 2-Rows × 2-Columns | 4종 | 2×2 그리드 |
| 2-Rows × 3-Columns | 1종 | 2×3 그리드 (6항목) |
| 2-Rows × 4-Columns | 2종 | 2×4 그리드 (8항목) |
| 3-Rows × 3-Columns | 1종 | 3×3 그리드 (9항목) |
| Project Plan | 2종 | 간트 차트, 단계별 일정 |
| Table | 4종 | 정형 데이터 표 |
| Ending | 1종 | IBM 브랜드 마무리 슬라이드 |

---

## webMethods 템플릿 전용 특징

`powerpoint-templates/webMethods_powerpoint_template.PPTX`를 직접 분석(48개 슬라이드)하여 도출한 스타일 규칙입니다.

### 주요 차이점

| 요소 | IBM 일반 | webMethods 셀러 덱 |
|------|----------|--------------------|
| **섹션 구분자 배너** | 없음 | 상단 ~3cm 연한 IBM 블루(`#D0E2FF`) 띠 |
| **카테고리 레이블** | 28pt, 검정 | 27–28pt bold, IBM 블루(`#0F62FE`) |
| **컬럼 헤더** | 일반 텍스트 | IBM 블루 Medium 체 (`IBM Plex Sans KR Medm`) |
| **세로 구분선** | 없음 | 회색(`#929292`) 선 ~0.75pt |
| **사용 사례 패널** | 없음 | 우측 하단 연한 블루 박스(`#D0E2FF`) |
| **셀러 가이던스 슬라이드** | 없음 | 슬라이드 2번에 고정 |
| **본문 폰트 크기** | 28pt 이상 | 22–24pt (실제 템플릿 기준) |
| **법적 고지 폰트** | — | 18pt |

### 슬라이드 패턴 (12종)

1. 커버 — 우측 반 이미지 + 좌측 제목
2. 셀러 가이던스 & 법적 고지 — 2단 법적 텍스트
3. 섹션 구분자 — 연한 블루 배너 + 제목
4. 스테이크홀더/페르소나 맵 — 4개 역할 그리드
5. 대형 스탯 — 중심 숫자 + 설명
6. 2단 콘텐츠 — 좌우 동등 컬럼
7. 3단 콘텐츠 — 3등분 컬럼
8. 4단/아이콘 그리드 — 4개 항목
9. 사용 사례/케이스 스터디 — 내러티브 + 과제 목록 + 이미지
10. 이미지+텍스트 — 반쪽 이미지
11. 표/비교 — 정형 데이터
12. 엔딩 — IBM 브랜드 마무리

자세한 레이아웃 좌표와 JS 코드 예시는 [`references/webmethods-template.md`](references/webmethods-template.md)를 참고하세요.

---

## 참고 문서

| 파일 | 설명 |
|------|------|
| [`PPTX-STYLE.md`](PPTX-STYLE.md) | IBM 슬라이드 전체 스타일 가이드 (80개 슬라이드 분석) |
| [`references/design-system.md`](references/design-system.md) | IBM Carbon 색상, IBM Plex Sans KR 타이포그래피, 4단 그리드 |
| [`references/slide-types.md`](references/slide-types.md) | 슬라이드 유형별 레이아웃 좌표 및 PptxGenJS 코드 예시 |
| [`references/editing.md`](references/editing.md) | 기존 PPTX 편집 워크플로우 및 XML 조작 방법 |
| [`references/pitfalls.md`](references/pitfalls.md) | IBM QA 체크리스트 및 자주 발생하는 실수 방지 |
| [`references/pptxgenjs.md`](references/pptxgenjs.md) | PptxGenJS 전체 API 레퍼런스 |
| [`references/webmethods-template.md`](references/webmethods-template.md) | webMethods 셀러 덱 전용 스타일 가이드 |
