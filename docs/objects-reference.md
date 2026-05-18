# 개발 오브젝트 참조 목록

## 표준 컨텐츠 패키지 (BCT_SD)

| 오브젝트 타입 | 오브젝트 ID | 설명 |
|-------------|------------|------|
| Replication Flow | `SAP_SD_REPLICATION` | SD 표준 복제 플로우 |
| Local Table | `SAP_SD_VBAK` | 판매 오더 헤더 |
| Local Table | `SAP_SD_VBAP` | 판매 오더 항목 |
| Local Table | `SAP_SD_VBEP` | 납품 일정 |
| Local Table | `SAP_SD_KNA1` | 고객 마스터 |
| Local Table | `SAP_SD_MARA` | 자재 마스터 |
| Graphical View | `SAP_SD_V_SALES_ORDER` | 판매 오더 통합 뷰 |
| Analytic Model | `SAP_SD_C_BILLING` | 청구 분석 모델 |

> ⚠️ 실제 BCT_SD 패키지 오브젝트 ID는 Import 후 확인 필요

---

## 커스텀 개발 오브젝트 (Lab 4)

### Lab 4-A: ODP 기반

| 오브젝트 타입 | 오브젝트 ID | 소스 | 설명 |
|-------------|------------|------|------|
| SQL View (Fact View) | `WS_HL_SQLV_OPEN_ORDER_ODP` | Local Tables (ODP 복제) | ODP 기반 미결 오더 Fact View |
| Analytic Model | `WS_RL_OPEN_ORDER_ODP` | `WS_HL_SQLV_OPEN_ORDER_ODP` | ODP 기반 미결 오더 분석 모델 |

### Lab 4-B: CDS View 기반

| 오브젝트 타입 | 오브젝트 ID | 소스 | 설명 |
|-------------|------------|------|------|
| SQL View (Fact View) | `WS_HL_SQLV_OPEN_ORDER_CDSV` | Remote Tables (CDS View) | CDS View 기반 미결 오더 Fact View |
| Analytic Model | `WS_RL_OPEN_ORDER_CDSV` | `WS_HL_SQLV_OPEN_ORDER_CDSV` | CDS View 기반 미결 오더 분석 모델 |

---

## 커넥션 정보

| 커넥션 ID | 타입 | 대상 시스템 | 용도 |
|----------|------|-----------|------|
| `HE4_S4H` | ABAP | S/4HANA HE4 | ODP DataSource, Remote Table |
| `HE4_S4HANAOP` | S/4HANA OP | S/4HANA HE4 | S/4HANA 전용 커넥션 |

---

## 오브젝트 네이밍 규칙

```
WS_  : Workshop 커스텀 오브젝트 접두어
HL_  : Harmonization Layer (정합 레이어)
RL_  : Reporting/Consumption Layer (소비 레이어)
SQLV : SQL View 타입
GRPV : Graphical View 타입
_ODP : ODP 소스 기반
_CDSV: CDS View 소스 기반
```
