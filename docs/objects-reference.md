# 개발 오브젝트 참조 목록

## 표준 컨텐츠 패키지 (BCT_SD)

Lab 1에서 Content Network에서 import하는 SAP 표준 패키지입니다.
실제 오브젝트 ID는 import 후 Data Builder에서 확인하세요.

---

## Lab 4 커스텀 개발 오브젝트

### Lab 4-A: ODP 기반

| 오브젝트 타입 | Technical Name | Business Name | 소스 |
|-------------|----------------|---------------|------|
| SQL View (Fact View) | `WS_HL_SQLV_OPEN_ORDER_ODP` | Open Order ODP Fact View | Local Tables (ODP 복제) |
| Analytic Model | `WS_RL_OPEN_ORDER_ODP` | Open Order ODP AM | `WS_HL_SQLV_OPEN_ORDER_ODP` |

#### ODP Fact View 소스 테이블

| Local Table | ODP DataSource | 설명 |
|-------------|----------------|------|
| `SAP_SD_IL_2LIS_11_VAHDR` | `2LIS_11_VAHDR` | 수주 헤더 |
| `SAP_SD_IL_2LIS_11_VAITM` | `2LIS_11_VAITM` | 수주 아이템 |
| `SAP_SD_IL_2LIS_11_VASCL` | `2LIS_11_VASCL` | 납품일정행 (확정수량) |
| `SAP_SD_IL_2LIS_12_VCITM` | `2LIS_12_VCITM` | 납품 아이템 (출고수량/일자) |
| `SAP_SD_IL_2LIS_13_VDITM` | `2LIS_13_VDITM` | 청구 아이템 |
| `SAP_SD_IL_2LIS_13_VDHDR` | `2LIS_13_VDHDR` | 청구 헤더 |

#### ODP Fact View 주요 필드

| 필드명 | 타입 | 설명 |
|--------|------|------|
| `VBELN` | String(10) | 영업전표번호 (KEY) |
| `POSNR` | String(6) | 항목번호 (KEY) |
| `ERDAT` | Date | 생성일 |
| `CalendarYearMonth` | String | 생성년월 (YYYYMM) |
| `VDATU` | Date | 납품요청일 (RDD) |
| `VKORG` | String(4) | 판매조직 |
| `BUKRS` | String(4) | 회사코드 |
| `VTWEG` | String(2) | 유통채널 |
| `AUART` | String(4) | 판매전표유형 |
| `KUNNR` | String(10) | 주문자 (Sold-to) |
| `MATNR` | String(18) | 자재번호 |
| `MATKL` | String(9) | 자재그룹 |
| `SPART` | String(2) | 제품군 |
| `WERKS` | String(4) | 플랜트 |
| `KWMENG` | Decimal | 주문수량 |
| `CONFIRMED_QTY` | Integer | 확정수량 |
| `GI_QTY` | Integer | 출고수량 |
| `GI_DATE` | Date | 출고일자 |
| `BILL_QTY` | Integer | 청구수량 |
| `BILL_AMT` | Integer | 청구금액 |
| `OPEN_DLV_QTY` | Decimal | 미납품수량 (KWMENG - GI_QTY) |
| `UNBILLED_QTY` | Integer | 미청구수량 (GI_QTY - BILL_QTY) |
| `DELIVERY_STATUS` | String | 납품진행상태 (Not Started / In Progress / Completed) |
| `COMPARISON_DATE` | Date | 비교기준일 |
| `RDD_LEADTIME_DAYS` | Integer | 납품요청일 리드타임(일) |
| `RDD_COMPLIANCE` | String | 납품요청일 준수여부 (On-Time / Delay) |

#### ODP Analytic Model 구조

| 구성 요소 | 상세 |
|----------|------|
| Fact Source | `WS_HL_SQLV_OPEN_ORDER_ODP` |
| BASE Measures | `KWMENG`(주문수량), `CONFIRMED_QTY`(확정수량), `GI_QTY`(출고수량), `BILL_QTY`(청구수량), `BILL_AMT`(청구금액), `OPEN_DLV_QTY`(미납품수량), `UNBILLED_QTY`(미청구수량) |
| RESTRICTION Measures | `Measure_Value`, `01_CURR_MONTH`(당월), `02_PRE_MONTH`(전월), `03_CURRENT_YEAR_CUMUL`(당년누계), `04_PRE_YEAR_CUM`(전년누계), `05_PRE_SAME_MONTH`(전년동기) |
| Variables (params) | `P_MONTH`(기준월), `RV_PREVIOUS_MONTH`, `RV_CURR_MONTH`, `RV_CURR_YEAR_JAN`, `RV_PREVIOUS_YEAR_SAME_MONTH`, `RV_PREVIOUS_YEAR_JAN` |
| Dimension Association | `_MATNR` → `SAP_LO_Product_V2` (자재 마스터) |

---

### Lab 4-B: CDS View 기반

| 오브젝트 타입 | Technical Name | Business Name | 소스 |
|-------------|----------------|---------------|------|
| SQL View (Fact View) | `WS_HL_SQLV_OPEN_ORDER_CDSV` | Open Order CDSV Fact View | Remote Tables (CDS View) |
| Analytic Model | `WS_RL_OPEN_ORDER_CDSV` | Open Order CDSV AM | `WS_HL_SQLV_OPEN_ORDER_CDSV` |

#### CDS View Fact View 소스 테이블 (Remote Table)

| Remote Table | S/4HANA CDS View | 설명 |
|-------------|-------------------|------|
| `SAP_SD_IL_C_SALESDOCUMENTITEMDEX_1` | `C_SalesDocumentItemDEX_1` | 수주 헤더+아이템 통합 |
| `SAP_SD_IL_C_SALESDOCUMENTSCHEDLINEDEX_1` | `C_SalesDocumentSchedLineDEX_1` | 납품일정행 (확정수량) |
| `SAP_SD_IL_I_DELIVERYDOCUMENTITEM` | `I_DeliveryDocumentItem` | 납품 아이템 |
| `SAP_SD_IL_I_DELIVERYDOCUMENT` | `I_DeliveryDocument` | 납품 헤더 (출고일자) |
| `SAP_SD_IL_C_BILLINGDOCITEMBASICDEX_1` | `C_BillingDocItemBasicDEX_1` | 청구 아이템 |

#### CDS View Fact View 주요 필드

ODP 방식과 동일한 비즈니스 의미, 필드명은 CDS View 표준명 사용:

| 필드명 | 타입 | ODP 대응 | 설명 |
|--------|------|----------|------|
| `SalesDocument` | String(10) | `VBELN` | 영업전표번호 (KEY) |
| `SalesDocumentItem` | String(6) | `POSNR` | 항목번호 (KEY) |
| `ERDAT` | Date | `ERDAT` | 생성일 (SalesDocumentDate에서 변환) |
| `CalendarYearMonth` | String(6) | `CalendarYearMonth` | 생성년월 |
| `VDATU` | Date | `VDATU` | 납품요청일 |
| `SalesOrganization` | String(4) | `VKORG` | 판매조직 |
| `BillingCompanyCode` | String(4) | `BUKRS` | 회사코드 |
| `DistributionChannel` | String(2) | `VTWEG` | 유통채널 |
| `SalesDocumentType` | String(4) | `AUART` | 판매전표유형 |
| `SoldToParty` | String(10) | `KUNNR` | 주문자 |
| `Material` | String(40) | `MATNR` | 자재번호 |
| `Division` | String(2) | `SPART` | 제품군 |
| `Plant` | String(4) | `WERKS` | 플랜트 |
| `KWMENG` | Decimal | `KWMENG` | 주문수량 (OrderQuantity에서 변환) |
| `CONFIRMED_QTY` | Integer | `CONFIRMED_QTY` | 확정수량 |
| `GI_QTY` | Integer | `GI_QTY` | 출고수량 |
| `BILL_QTY` | Integer | `BILL_QTY` | 청구수량 |
| `BILL_AMT` | Integer | `BILL_AMT` | 청구금액 |
| `OPEN_DLV_QTY` | Decimal | `OPEN_DLV_QTY` | 미납품수량 |
| `UNBILLED_QTY` | Integer | `UNBILLED_QTY` | 미청구수량 |
| `DELIVERY_STATUS` | String | `DELIVERY_STATUS` | 납품진행상태 |
| `RDD_LEADTIME_DAYS` | Integer | `RDD_LEADTIME_DAYS` | 리드타임(일) |
| `RDD_COMPLIANCE` | String | `RDD_COMPLIANCE` | RDD 준수여부 |

---

## 커넥션 정보

| 커넥션 ID | 타입 | 대상 시스템 | 용도 |
|----------|------|-----------|------|
| `HE4_S4H` | ABAP | S/4HANA HE4 | ODP DataSource, Remote Table (CDS View) |

---

## 오브젝트 네이밍 규칙

```
WS_   : Workshop 커스텀 오브젝트 접두어
HL_   : Harmonization Layer (데이터 정합 레이어)
RL_   : Reporting/Consumption Layer (소비/분석 레이어)
SQLV  : SQL View 타입
_ODP  : ODP DataSource 소스 기반
_CDSV : CDS View 소스 기반
```
