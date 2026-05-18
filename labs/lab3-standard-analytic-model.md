# Lab 3: 표준 Analytic Model로 데이터 확인

## 목표

BCT_SD 패키지에서 제공하는 **표준 Analytic Model**을 활용하여 S/4HANA SD 데이터를 분석합니다.
Analytic Model의 구조(측정값, 차원)를 이해하고 데이터를 조회해봅니다.

**소요 시간**: 약 20분

---

## 개념 설명

```mermaid
graph TB
    subgraph LAYERS["SAP Datasphere 레이어"]
        direction TB
        L1["Local Tables\n(Raw Data)"]
        L2["Views\n(Harmonization)"]
        L3["Analytic Model\n(Consumption)"]
        L1 --> L2 --> L3
    end

    subgraph AM["Analytic Model 구성"]
        MEASURE["Measures (측정값)\n- 금액\n- 수량\n- 건수"]
        DIM["Dimensions (차원)\n- 고객\n- 자재\n- 판매 조직\n- 날짜"]
    end

    L3 -.-> AM

    style L3 fill:#E8A000,color:#fff
```

**Analytic Model이란?**
- SAP Datasphere의 데이터 소비(Consumption) 레이어
- 비즈니스 측정값(Measures)과 분석 차원(Dimensions) 정의
- SAP Analytics Cloud 및 Excel 등 BI 도구와 연결

---

## 단계별 가이드

### Step 1. Analytic Model 찾기

1. Data Builder → 왼쪽 상단 오브젝트 타입 필터
2. **Analytic Models** 선택
3. BCT_SD 패키지에서 Import된 표준 AM 클릭 (이름은 패키지 버전에 따라 상이)

```mermaid
flowchart LR
    A["Data Builder"] --> B["오브젝트 타입 필터\n→ Analytic Models"]
    B --> C["BCT_SD 표준 AM\n클릭하여 열기"]
```

> Tip: BCT_SD 패키지에 포함된 Analytic Model 이름은 패키지 버전에 따라 다를 수 있습니다. `SAP_SD_` 접두어로 시작하는 AM을 선택하세요.

---

### Step 2. Analytic Model 구조 파악

편집 화면에서 다음 패널을 확인합니다:

```mermaid
graph LR
    subgraph AM_UI["Analytic Model 편집 화면"]
        CANVAS["중앙 Canvas\n소스 오브젝트 표시"]
        MEASURES["우측 패널\nMeasures (측정값)"]
        DIMS["우측 패널\nDimensions (차원)"]
        ASSOC["연결된 Dimension Views\n(마스터 데이터)"]
    end
    CANVAS --- MEASURES
    CANVAS --- DIMS
    DIMS --- ASSOC
```

**확인 항목:**

| 패널 | 확인 내용 |
|------|---------|
| Source | 연결된 Fact View 이름 |
| Measures | 금액, 수량 등 측정값 목록 |
| Dimensions | 고객, 자재, 날짜 등 차원 목록 |
| Associations | 마스터 데이터 연결 확인 |

---

### Step 3. 측정값(Measures) 확인

Measures 패널에서 각 측정값의 속성 확인:

| 측정값 | 타입 | 집계 방식 |
|--------|------|---------|
| 청구 금액 | BASE | SUM |
| 청구 수량 | BASE | SUM |
| 건수 | CALCULATED | COUNT |

**측정값 타입 설명:**
- **BASE**: 소스 필드를 직접 집계
- **CALCULATED**: 다른 측정값을 조합하여 계산
- **RESTRICTED**: 특정 조건으로 필터링된 측정값

---

### Step 4. 차원(Dimensions) 확인

Dimensions 패널에서 각 차원의 속성 확인:

| 차원 | 연결 오브젝트 | 설명 |
|------|------------|------|
| 고객 | 고객 Dimension View | 고객 마스터 (이름, 지역 등) |
| 자재 | 자재 Dimension View | 자재 마스터 (자재명, 자재그룹) |
| 판매 조직 | - | 판매 조직 코드 |
| 날짜 | 날짜 Dimension | 연/분기/월/일 계층 |

---

### Step 5. Data Preview로 데이터 확인

1. Analytic Model 화면 상단 **Preview** 버튼 클릭
2. 데이터 조회 화면 열림

```mermaid
flowchart TD
    A["Preview 버튼 클릭"] --> B["데이터 조회 화면"]
    B --> C["측정값 선택\n(Rows)"]
    B --> D["차원 선택\n(Columns/Filters)"]
    C & D --> E["데이터 테이블 확인"]
```

**Preview 조작 방법:**

| 작업 | 방법 |
|------|------|
| 차원 추가 | 좌측 차원 목록에서 드래그 또는 클릭 |
| 측정값 추가 | 좌측 측정값 목록에서 드래그 또는 클릭 |
| 필터 적용 | 차원 옆 필터 아이콘 클릭 |
| 데이터 정렬 | 컬럼 헤더 클릭 |

---

### Step 6. 기본 분석 실습

다음 분석을 차례로 실습합니다:

#### 분석 1: 판매 조직별 청구 금액 합계

- 행(Row): 판매 조직
- 측정값: 청구 금액
- 결과 확인: 판매 조직별 금액 비교

#### 분석 2: 월별 청구 건수 트렌드

- 행(Row): 청구 날짜 (월 레벨)
- 측정값: 청구 건수
- 결과 확인: 월별 청구 추이 확인

#### 분석 3: 고객별 Top 10 분석

- 행(Row): 고객
- 측정값: 청구 금액
- 정렬: 청구 금액 내림차순
- 결과 확인: 상위 고객 식별

```mermaid
flowchart LR
    subgraph ANALYSIS["실습 분석 시나리오"]
        A1["분석 1\n판매 조직별 금액"]
        A2["분석 2\n월별 건수 트렌드"]
        A3["분석 3\n고객별 Top 10"]
    end
    A1 --> A2 --> A3
```

---

### Step 7. 마스터 데이터 연결 확인 (텍스트 표시)

Analytic Model에서 차원에 마스터 데이터가 연결되면 코드 대신 텍스트로 표시됩니다.

- 고객 코드 `0000001000` → 고객명 표시 여부 확인
- 자재 코드 → 자재명 표시 여부 확인

> 마스터 데이터가 연결되지 않은 경우 코드만 표시됩니다.

---

## 확인 포인트

```mermaid
graph TD
    A["Lab 3 완료 체크리스트"] --> B["Analytic Model 구조 이해"]
    A --> C["측정값 목록 확인"]
    A --> D["차원 목록 확인"]
    A --> E["Data Preview 데이터 조회"]
    A --> F["기본 분석 3가지 실습"]
```

---

## 표준 컨텐츠 vs 커스텀 개발 비교

```mermaid
graph LR
    STD["표준 컨텐츠 (BCT_SD)\n- 빠른 구현\n- SAP 검증 모델\n- 요건 변경 시 제약"]
    CUSTOM["커스텀 개발 (Lab 4)\n- 요건에 맞게 유연 개발\n- 필요한 필드만 선택\n- 개발 시간 필요"]

    STD -.->|"기반으로 확장"| CUSTOM
```

---

## 다음 단계

Lab 3 완료 후 → 점심 식사 후 → **[Lab 4-A: ODP 기반 커스텀 모델 개발](./lab4a-odp-fact-view-am.md)** 진행
