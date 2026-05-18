# SAP BDC Datasphere Partner Workshop 2025

> **SAP Korea BDC (Business Data Cloud) 파트너 워크샵**
> SAP Datasphere 핸즈온 실습 교육 자료

---

## 📅 워크샵 개요

| 항목 | 내용 |
|------|------|
| **일시** | 2025년 5월 19일 (월) |
| **대상** | SAP Korea BDC 파트너 |
| **형태** | 1-Day 핸즈온 워크샵 |
| **주제** | SAP Datasphere 데이터 모델링 실습 (S/4HANA SD 시나리오) |

---

## 🌐 교육 환경

| 항목 | 정보 |
|------|------|
| **Datasphere 테넌트** | https://poc-dsp-1.ap12.hcs.cloud.sap/ |
| **연결 S/4HANA** | HE4 (S/4HANA On-Premise) |
| **커넥션 ID** | `HE4_S4H` |
| **표준 컨텐츠 패키지** | `BCT_SD` (SD 표준 분석 컨텐츠 한글화) |

---

## 👤 참가자 계정 정보

각 참가자는 개인 전용 Space와 계정이 할당됩니다.

| 계정 | Space | 비밀번호 |
|------|-------|---------|
| `dspuser01` | `DSPWS01` | `Welcome1!` |
| `dspuser02` | `DSPWS02` | `Welcome1!` |
| `dspuser03` | `DSPWS03` | `Welcome1!` |
| `dspuser04` | `DSPWS04` | `Welcome1!` |
| `dspuser05` | `DSPWS05` | `Welcome1!` |
| `dspuser06` | `DSPWS06` | `Welcome1!` |
| `dspuser07` | `DSPWS07` | `Welcome1!` |
| `dspuser08` | `DSPWS08` | `Welcome1!` |
| `dspuser09` | `DSPWS09` | `Welcome1!` |
| `dspuser10` | `DSPWS10` | `Welcome1!` |
| `dspuser11` | `DSPWS11` | `Welcome1!` |
| `dspuser12` | `DSPWS12` | `Welcome1!` |
| `dspuser13` | `DSPWS13` | `Welcome1!` |
| `dspuser14` | `DSPWS14` | `Welcome1!` |
| `dspuser15` | `DSPWS15` | `Welcome1!` |
| `dspuser16` | `DSPWS16` | `Welcome1!` |
| `dspuser17` | `DSPWS17` | `Welcome1!` |
| `dspuser18` | `DSPWS18` | `Welcome1!` |
| `dspuser19` | `DSPWS19` | `Welcome1!` |
| `dspuser20` | `DSPWS20` | `Welcome1!` |
| `dspuser21` | `DSPWS21` | `Welcome1!` |
| `dspuser22` | `DSPWS22` | `Welcome1!` |
| `dspuser23` | `DSPWS23` | `Welcome1!` |
| `dspuser24` | `DSPWS24` | `Welcome1!` |
| `dspuser25` | `DSPWS25` | `Welcome1!` |
| `dspuser26` | `DSPWS26` | `Welcome1!` |
| `dspuser27` | `DSPWS27` | `Welcome1!` |
| `dspuser28` | `DSPWS28` | `Welcome1!` |
| `dspuser29` | `DSPWS29` | `Welcome1!` |
| `dspuser30` | `DSPWS30` | `Welcome1!` |
| `dspuser31` | `DSPWS31` | `Welcome1!` |
| `dspuser32` | `DSPWS32` | `Welcome1!` |
| `dspuser33` | `DSPWS33` | `Welcome1!` |
| `dspuser34` | `DSPWS34` | `Welcome1!` |
| `dspuser35` | `DSPWS35` | `Welcome1!` |
| `dspuser36` | `DSPWS36` | `Welcome1!` |
| `dspuser37` | `DSPWS37` | `Welcome1!` |
| `dspuser38` | `DSPWS38` | `Welcome1!` |
| `dspuser39` | `DSPWS39` | `Welcome1!` |
| `dspuser40` | `DSPWS40` | `Welcome1!` |

> ⚠️ **첫 로그인 시 비밀번호를 변경하시기 바랍니다.**

---

## 📋 워크샵 어젠다

```
09:00 - 09:30  │ 등록 및 환경 확인
09:30 - 10:00  │ 오프닝: SAP BDC & Datasphere 개요
10:00 - 10:30  │ 전체 아키텍처 및 시나리오 설명
               │
10:30 - 12:00  │ [PART 1] 표준 컨텐츠 활용
               │   Lab 1. BCT_SD 패키지 Import
               │   Lab 2. Replication Flow로 S/4HANA 데이터 적재
               │   Lab 3. 표준 Analytic Model로 데이터 확인
               │
12:00 - 13:00  │ 점심
               │
13:00 - 13:30  │ [PART 2] 커스텀 데이터 모델링 시나리오 설명
               │   가상 고객 요건 Review
               │
13:30 - 16:30  │ [PART 2] 커스텀 모델 개발 실습
               │   Lab 4-A. ODP 기반 Fact View 및 Analytic Model
               │   Lab 4-B. CDS View 기반 Fact View 및 Analytic Model
               │
16:30 - 17:00  │ Q&A 및 클로징
```

---

## 📁 실습 가이드

| Lab | 제목 | 링크 |
|-----|------|------|
| Lab 1 | BCT_SD 표준 컨텐츠 패키지 Import | [→ 가이드](./labs/lab1-bct-sd-import.md) |
| Lab 2 | Replication Flow로 S/4HANA 데이터 적재 | [→ 가이드](./labs/lab2-replication-flow.md) |
| Lab 3 | 표준 Analytic Model 데이터 확인 | [→ 가이드](./labs/lab3-standard-analytic-model.md) |
| Lab 4-A | ODP 기반 Open Order Fact View & AM | [→ 가이드](./labs/lab4a-odp-fact-view-am.md) |
| Lab 4-B | CDS View 기반 Open Order Fact View & AM | [→ 가이드](./labs/lab4b-cdsv-fact-view-am.md) |

---

## 📖 참고 문서

| 문서 | 링크 |
|------|------|
| 전체 아키텍처 구성도 | [→ architecture.md](./docs/architecture.md) |
| 가상 고객 요건 (POC 시나리오) | [→ customer-requirements.md](./docs/customer-requirements.md) |
| 개발 오브젝트 목록 | [→ objects-reference.md](./docs/objects-reference.md) |

---

## 🔗 유용한 링크

- [SAP Datasphere 공식 문서](https://help.sap.com/docs/SAP_DATASPHERE)
- [SAP Datasphere Learning Journey](https://learning.sap.com/learning-journeys/store-and-model-data-with-sap-datasphere)
- [SAP BTP Cockpit](https://cockpit.btp.cloud.sap/)

---

> 문의사항: SAP Korea BDC 팀
