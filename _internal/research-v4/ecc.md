# DDR5 온다이 ECC와 시스템 ECC
> 조사일: 2026-07-29 / 상태: 완료

**중요 전제**: 로컬 `jesd79_5.txt`는 **"Proposed DDR5 Full spec (79-5)" 위원회 회람 초안(Rev0.1, JC42.3 ballot 회람본)**입니다. 본문 각 절에 "Q1'17 Ballot #NNNN.NN" 항목번호가 붙어 있고 페이지 머리글이 "Item No. xxxx.yyy"로 남아 있는 미확정 문서입니다. **최종 비준된 JESD79-5(및 5A/5B/5C) 사양과 다를 수 있으므로, 이 파일에서 인용한 JEDEC 수치는 모두 "초안 기준"으로 표기합니다.**

---

## 1. 확인된 사실

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR5 온다이 ECC 코드 종류 | **SEC (Single Error Correction)** — 단일 비트 정정만. DED(더블 비트 검출) 없음 | T0(초안) | jesd79_5.txt L17124 §4.29 "On-Die ECC - Q1'17 Ballot #1830.50" | 확인일 2026-07-29 |
| 온다이 ECC 코드워드 구성 | **데이터 128비트 + 체크비트 8비트 = 136비트 코드워드** | T0(초안) | jesd79_5.txt L17124-17125 | 확인일 2026-07-29 |
| 동일 수치 (제조사 확인) | "128 data bits + 8 parity bits → 136-bit codeword", SEC | T1 | micron_ddr5.txt L120-123 (Micron DDR5 백서) | T0 초안과 **일치** (교차확인 완료) |
| 코드 계열 | Hamming code | T1 | micron_ddr5.txt L124 | JEDEC 초안은 H-matrix 예시 제공(Table 82/83), 실제 구현은 다른 H-matrix 허용 |
| 코드워드 4분할 | 128비트를 4개 quarter로 분할: 상위 64비트(63:0)=Q1,Q2 / 하위 64비트(127:64)=Q3,Q4 | T0(초안) | jesd79_5.txt L17125-17127 | |
| ECS 모드 레지스터 | **MR15 (MA[7:0]=0FH) — ECS Threshold** | T0(초안) | jesd79_5.txt L88, L2662 | |
| ECS 권장 전체 스크럽 주기 | **24시간 이내 전체 배열 1회 스크럽** | T1 | micron_ddr5.txt L139-140 | JEDEC 초안 측 수치 확인 필요 |
| ECS 수동 실행 수단 | **MPC (Multi-Purpose Command)** | T1 | micron_ddr5.txt L137-138 | |
| MR15 비트 할당 (초안) | OP[7]=ECS Entry (0B: Normal Operation 기본 / 1B: ECS Entry), OP[6]=ECS Reset(Reset ECC Counter), OP[5]=RFU, OP[4:0]=ECS OP[4:0] | T0(초안) | jesd79_5.txt L2664-2718 | OP[4:0] 정의는 초안에서 **RFU(미정)** |
| ECS Error Threshold (초안) | MR15 OP[5:0] = **"TBD"** | T0(초안) | jesd79_5.txt L2736-2739 | **초안에 값이 미기재.** 비준본 확인 필요 |
| MR14 | ECC Configuration 레지스터 (MA[7:0]=0EH) | T0(초안) | jesd79_5.txt L2660 | 초안에 상세 비트 정의 없음 |
| 실제 제품의 ECS 기능 | "ECS Writeback Suppression" 및 "x4 RMW Suppression" 기능 지원 명시 | T1 | micron16gb_ddr5.txt L1330, L1334 (Micron 16Gb DDR5 SDRAM **Die Rev D**, doc rev F 04/2024) | ECS 라이트백·x4 read-modify-write가 실제 양산 다이에 존재함을 확인 |
| 삼성 DDR5 UDIMM 기능 목록 | "On-Die ECC", "ECC Transparency and Error Scrub", "CRC (Cyclic Redundancy Check)" 각각 **별도 항목**으로 병기 | T1 | samsung_ddr5_udimm.txt L72-74 | 온다이 ECC와 링크 CRC가 **서로 다른 기능**임을 제조사 문서가 구분 |
| DDR5 RDIMM 모듈 폭 | **x80** (32GB, ECC, DR 288-pin DDR5 RDIMM) | T1 | micron_32gb_rdimm.txt L3 등 | DDR5는 40비트 서브채널 2개 = 80비트. DDR4 ECC DIMM의 x72와 대비 |
| **schroeder09 FIT율** | **25,000 – 70,000 FIT/Mbit** (failures in time per billion device hours) | T2 | schroeder09.txt L132-134 | **2009년 논문 / 2006.1–2008.6 측정. 현행 세대에 그대로 적용 금지** |
| schroeder09 DIMM 영향률 | 연간 **8.2%**의 DIMM이 정정가능오류(CE) 경험 (전체 fleet) | T2 | schroeder09.txt L520-521 | 동상 |
| schroeder09 DIMM당 CE 수 | 평균 DIMM이 연간 **약 4,000회** CE. 플랫폼별 **3,351–4,530회/년** | T2 | schroeder09.txt L521-522, L529-531 | 동상 |
| schroeder09 UE 발생률 | 연간 **1.3%**의 머신이 정정불가오류(UE) 경험 (플랫폼에 따라 **2–4%**) | T2 | schroeder09.txt L511-513 | 동상 |
| schroeder09 DIMM 기준 UE | 플랫폼 A·E는 연간 **0.05–0.08%**의 DIMM, 플랫폼 C·D는 **약 0.3%** | T2 | schroeder09.txt L526-529 | 동상 |
| schroeder09 연구 범위 | Google 서버 fleet, **2006년 1월 – 2008년 6월(약 2.5년)**, 6개 하드웨어 플랫폼, 수백만 DIMM-day | T2 | schroeder09.txt L21-23, L209-213 | |
| schroeder09 핵심 결론 1 | 메모리 오류는 소프트 에러가 아니라 **하드 에러가 지배적** | T2 | schroeder09.txt L135-137 | |
| schroeder09 핵심 결론 2 | DIMM 세대가 신형이라고 해서 DIMM당 오류율이 증가한다는 증거는 **관측되지 않음** | T2 | schroeder09.txt L139-141, L1810-1814 | **셀 미세화→오류율 증가 서사를 이 논문으로 뒷받침할 수 없음.** §3 참조 |
| SECDED 정의 (해당 논문) | 단일 비트 오류는 정정, 다중 비트 오류는 **검출만 가능하고 정정 불가** | T2 | schroeder09.txt L150-154 | |
| Chipkill 정의 (해당 논문) | 인접 **4비트**까지 정정 → x4 DRAM 칩 하나가 완전히 고장나도 동작 | T2 | schroeder09.txt L155-158 | |
| **HBM3 온다이 ECC** | HBM3(JESD238)는 **on-die에 symbol-based ECC**를 도입. 아울러 **real-time error reporting 및 transparency**를 제공(플랫폼 레벨 RAS 요구 대응) | T0 (표준화기구 **보도자료**, 규격 원문 아님) | https://www.jedec.org/news/pressreleases/jedec-publishes-hbm3-update-high-bandwidth-memory-hbm-standard (확인일 2026-07-29) | HBM3 규격 발행 2022년 1월. **단일 출처** |
| HBM3 규격 번호 | **JESD238** (2022년 1월 발행) | T0(보도자료) | 동상 | |

---

## 2. 구조·메커니즘 서술

### 2.1 온다이 ECC의 표준상 위치
JEDEC DDR5 초안 §4.29 "On-Die ECC". DDR5 디바이스는 **DRAM 다이 내부**에 SEC ECC를 구현하며, 이는 "improve the data integrity within the DRAM"(다이 내부 데이터 무결성 개선)이 목적으로 명시되어 있습니다. 즉 표준상 위치가 **디바이스 내부**이며, 모듈/채널/호스트 계층이 아닙니다.

### 2.2 폭(x4/x8/x16)별 프리페치 처리 — 온다이 ECC의 핵심 비대칭
JEDEC 초안 §4.29 기준:
- **x8**: 외부 전송 크기와 프리페치가 같아 추가 프리페치 불필요. 코드워드 상위 절반 = 16비트 버스트의 앞 절반, 하위 절반 = 뒷 절반에 매핑.
- **x4**: 외부적으로는 64비트 프리페치 소자지만 **온다이 ECC용 내부 프리페치는 128비트**. 매 read/write마다 DRAM 배열의 추가 섹션을 내부적으로 접근해 나머지 64비트를 조달. 즉 x4에서는 8비트 체크비트 1워드가 **64비트 섹션 2개**에 묶임. 코드워드가 두 컬럼 액세스(N, N+y)로 나뉨.
- **x16**: 서로 다른 뱅크에서 128비트 데이터 워드 2개 + 각각의 체크비트 8비트를 가져와 **병렬로 독립 검사**. 한 코드워드는 DQ[0:7], 다른 하나는 DQ[8:15]에 매핑.

### 2.3 쓰기 경로 — x4의 내부 read-modify-write
외부 전송 크기가 128비트 코드워드보다 작은 경우(x4), DRAM은 **내부 read-modify-write**를 수행해야 합니다. 내부 읽기에서 발생한 단일 비트 오류를 정정 → 유입 쓰기 데이터와 병합 → 8비트 체크비트 재계산 → 배열에 기록. x8/x16은 내부 읽기 불필요. (jesd79_5.txt L17148-17151)

### 2.4 읽기 경로와 syndrome 디코드
Syndrome Decode 블록의 동작 (jesd79_5.txt L17161-17166, 초안):
- Syndrome = 0 → 오류 없음
- Syndrome ≠ 0 이고 H-matrix의 어떤 열과 일치 → 해당 비트 반전 (**CE, Corrected Error**)
- Syndrome ≠ 0 이고 H-matrix의 어떤 열과도 불일치 → **DUE (Detected Uncorrected)**

**결정적 사실**: "On reads, the DRAM corrects any single bit errors before returning the data to the memory controller. **The DRAM will not write the corrected data back to the array during a read cycle.**" (L17134-17135) — 즉 읽기 시 정정은 **출력 데이터에만** 적용되고 **배열은 그대로 오염된 상태로 남습니다**. 이것이 ECS(스크럽)가 별도로 필요한 이유입니다.

### 2.5 더블 비트 오류의 앨리어싱 — SEC의 한계이자 설계 의도
SEC 코드는 8체크비트/128데이터비트로는 **더블 비트 검출(DED)이 불가능**합니다(micron_ddr5.txt L125). 더블 비트 오류가 들어오면 코드는 이를 **잘못 "정정"하여 트리플 비트 오류로 악화**시킬 수 있습니다("may miss correct a double bit the error into a triple bit error", jesd79_5.txt L17135-17136).

JEDEC 초안은 이 앨리어싱을 **방치하지 않고 방향을 규정**합니다:
- Q1과 Q2에 하나씩 걸친 더블 비트 오류는 앨리어싱하지 않음. Q3과 Q4에 하나씩도 마찬가지.
- Q1 안에서 더블 비트 오류가 나면 앨리어싱된 3번째 비트는 **반드시 하위 절반(Q3 또는 Q4)** 에 나타남. 반대로 Q3에서 나면 앨리어싱 비트는 **반드시 상위 절반(Q1 또는 Q2)** 에 나타남. (jesd79_5.txt L17136-17140)
- 구현체가 다른 H-matrix를 써도 되지만, **이 앨리어싱 매핑 규칙은 반드시 지켜야 합니다**("as long as any double bit errors that are aliased into triple bits adhere to the mapping described above", L17159-17160).

**왜 이렇게 규정했는가**: x8에서 코드워드 상위 절반은 16비트 버스트의 앞 절반, 하위 절반은 뒷 절반에 매핑됩니다. 따라서 앨리어싱된 3번째 오류 비트는 **항상 버스트의 반대쪽 절반에 나타나고**, 그 결과 오류가 **시스템 레벨 ECC에게 여전히 "더블 비트 실패"로 보이게** 됩니다(jesd79_5.txt L17141-17143, micron_ddr5.txt L124-135). 즉 **온다이 ECC는 시스템 ECC를 눈멀게 하지 않도록 일부러 설계되었습니다** — 이는 온다이 ECC가 시스템 ECC를 대체하는 것이 아니라 그 아래에 깔리는 층임을 표준이 스스로 전제하고 있다는 강력한 증거입니다.

### 2.6 ECS (Error Check and Scrub)

**주의**: 로컬 `jesd79_5.txt` 초안 본문에는 "scrub"/"Error Check and Scrub"라는 **기능 설명 절이 존재하지 않습니다**(전문 grep 결과 0건). 초안에 있는 것은 **MR15 = "ECS Threshold" 레지스터 껍데기뿐**이며, 그마저 임계값 필드가 "TBD", OP[4:0]이 "RFU"로 남아 있습니다. 따라서 아래 ECS 동작 서술은 **Micron 백서(T1)** 를 주 근거로 하며, JEDEC 비준본의 ECS 절은 이 조사에서 확인하지 못했습니다.

**동작 방식** (micron_ddr5.txt L136-142, T1):
1. ECS는 **내부 데이터를 읽고, 오류가 있었다면 정정된 데이터를 배열에 되써넣는(writing back)** 동작입니다.
2. 두 가지 모드:
   - **수동(manual)**: 호스트가 **MPC(Multi-Purpose Command)** 로 개시.
   - **자동(automatic)**: DRAM이 **스스로 ECS 명령을 스케줄링·수행**하여 배열 전체 스크럽을 **권장 24시간 주기 내에** 완료.
3. **보고**: 전체 배열 스크럽 1회 완료 시점에, DDR5는 (a) 스크럽 중 정정한 **오류 개수**와 (b) 오류가 가장 많았던 **행(row)** 을 보고합니다. 단 둘 다 **최소 실패 임계값(minimum fail threshold)을 넘긴 경우에만** 보고됩니다.
4. MR15의 **OP[6] = ECS Reset**은 "Reset ECC Counter"로 정의되어 있어(jesd79_5.txt L2710-2713, 초안), 오류 카운터가 모드 레지스터로 노출·초기화되는 구조임을 확인할 수 있습니다. MR15 **OP[7] = ECS Entry**(0B 정상동작 기본 / 1B ECS 진입)로 ECS 진입을 제어합니다.

**ECS가 왜 필요한가 (핵심 논리)**: §2.4에서 본 대로 **읽기 시 정정은 배열에 반영되지 않습니다.** 따라서 정정 가능한 단일 비트 오류가 셀에 누적되면, 같은 코드워드에 두 번째 오류가 생기는 순간 SEC는 정정 불가(그리고 검출조차 못 하고 오히려 트리플 비트로 악화)가 됩니다. ECS는 이 **단일 비트 오류 누적을 주기적으로 청소**해서 코드워드가 2비트 오류 상태로 진입할 확률을 낮추는 장치입니다. Micron 16Gb DDR5 Die Rev D 문서에 "ECS Writeback Suppression"이 별도 기능으로 존재하는 것도(micron16gb_ddr5.txt L1330) ECS의 본질이 **라이트백**임을 뒷받침합니다.

### 2.7 온다이 ECC와 시스템 ECC의 차이 — "DDR5는 ECC 기본이라 서버 ECC 불필요" 오해의 정정

이 조사의 최우선 목표 항목. 확보한 근거를 오해 정정 논리 순서대로 정리합니다.

**(1) 온다이 ECC는 DRAM 다이 내부만 보호한다 — 링크는 보호하지 않는다.**
JEDEC 초안의 목적 문구가 "improve the data integrity **within the DRAM**"(jesd79_5.txt L17124)입니다. 정정은 "before returning the data to the memory controller"(L17134), 즉 **DQ 핀에서 데이터가 나가기 직전**에 끝납니다. 그 이후 DRAM→컨트롤러 구간(패키지, 모듈 배선, 커넥터, 채널)에서 발생하는 오류는 온다이 ECC의 보호 범위 **밖**입니다. DDR5가 이 구간을 위해 **별도로** CRC를 두고 있다는 점이 이를 방증합니다 — 삼성 DDR5 UDIMM 문서는 "On-Die ECC", "ECC Transparency and Error Scrub", "CRC (Cyclic Redundancy Check)"를 **세 개의 별개 기능**으로 나열합니다(samsung_ddr5_udimm.txt L72-74).

**(2) 온다이 ECC는 SEC뿐이며 더블 비트를 검출조차 못 한다.**
JEDEC 초안: "Single Error Correction (SEC)"(L17124). Micron: "Since **8 parity bits with 128 data bits do not allow for double-bit detection**"(micron_ddr5.txt L125). 더블 비트 오류는 정정되지 않을 뿐 아니라 **트리플 비트 오류로 악화될 수 있습니다**(jesd79_5.txt L17135-17136). 온다이 ECC를 "ECC가 있으니 안전"의 근거로 삼을 수 없는 직접적 이유입니다.

**(3) 온다이 ECC는 호스트에 오류를 보고하지 않는다 (실시간 기준).**
정정된 단일 비트 오류는 조용히 고쳐져 나가며, 읽기 경로에서 호스트에게 "여기서 CE가 발생했다"는 신호가 전달되는 메커니즘을 **이 조사의 자료 범위에서는 확인하지 못했습니다**(§4 참조). 확인된 유일한 보고 경로는 **ECS 완료 후 모드 레지스터로 읽는 오류 카운트와 최다 오류 행**(micron_ddr5.txt L140-142)이며, 이것도 **최소 임계값을 넘겨야만** 보고되는 **사후·집계·비실시간** 정보입니다. 즉 온다이 ECC는 시스템 ECC가 제공하는 **주소 단위 CE 로깅·페이지 오프라인·예측적 DIMM 교체** 같은 RAS 운영 기능을 제공하지 못합니다. schroeder09가 "CE 하나만으로도 DIMM 교체를 정당화할 만큼 심각하게 본다"(schroeder09.txt L85 부근)고 기술한 운영 관행이 온다이 ECC만으로는 성립하지 않습니다.

**(4) 표준 자체가 시스템 ECC의 존재를 전제하고 설계되었다.**
가장 강한 근거입니다. §2.5의 앨리어싱 규칙 — 더블 비트 오류가 트리플로 앨리어싱될 때 3번째 비트를 **반드시 버스트의 반대쪽 절반에 떨어뜨리도록** 강제하는 규정 — 의 목적은 명시적으로 "This allows the errors to **still appear as a double bit fail to the system-level error correction**"(micron_ddr5.txt L134-135)이고, Micron은 코드워드 4분할이 "to align with **system-level error correction coverage**"(L124) 때문이라고 씁니다. **온다이 ECC는 시스템 ECC를 대체하도록 설계된 것이 아니라, 시스템 ECC가 자기 위에서 계속 동작할 수 있도록 배려해서 설계되었습니다.** 온다이 ECC는 시스템 ECC의 **부담을 줄이는(reduce the system error correction burden, micron_ddr5.txt L119)** 층이지 대체재가 아닙니다.

**(5) 물증: 온다이 ECC가 있는 non-ECC 모듈이 실재한다.**
`samsung_ddr5_udimm.txt`는 **UDIMM** 문서인데 On-Die ECC를 기능으로 싣고 있습니다. 반면 서버용 `micron_32gb_rdimm.txt`는 제품명 자체가 "32GB (**x80, ECC**, DR) 288-Pin DDR5 RDIMM"으로 **모듈 폭에 ECC 비트를 물리적으로 더 갖고 있습니다**. **같은 DDR5 세대에서 온다이 ECC는 양쪽 다 있고, 시스템 ECC는 RDIMM에만 있습니다** — 두 층이 서로 다른 것임을 제품 라인업이 직접 증명합니다.

**(6) 시스템 ECC의 폭 구성 (DDR5).**
DDR5 ECC RDIMM은 **x80**(micron_32gb_rdimm.txt). DDR5는 한 DIMM이 2개 서브채널로 나뉘므로 서브채널당 40비트 = **데이터 32 + ECC 8**입니다. DDR4 ECC DIMM의 x72(데이터 64 + ECC 8)와 비교하면, DDR5는 **데이터 32비트당 체크비트 8비트**로 **체크비트 비율이 12.5% → 25%로 2배**입니다.
※ 주의: 서브채널 40비트 = 32+8이라는 **분해는 x80 표기와 DDR5 2-서브채널 구조로부터의 산술 유도**이며, 로컬 자료에서 "32 data + 8 ECC"라는 문자열을 직접 확인하지는 못했습니다(§4).

**(7) Chipkill/SDDC와 x4 vs x8.**
schroeder09(T2, 2009)의 정의: SECDED는 단일 비트 정정 / 다중 비트는 검출만. Chipkill 계열은 **인접 4비트까지 정정**하여 **x4 DRAM 칩 하나가 통째로 고장나도** 동작합니다(schroeder09.txt L150-158). 여기서 **x4가 등장하는 이유**는 구조적입니다 — 칩 하나가 코드가 정정할 수 있는 비트 폭(4비트) 안에 들어가야 "칩 하나 사망"을 흡수할 수 있으므로, 같은 정정 능력에서 **x4 구성이 x8 구성보다 칩 단위 장애에 강합니다**. x8 칩이 통째로 죽으면 8비트가 한꺼번에 나가므로 4비트 정정 코드로는 감당되지 않습니다. 이것이 서버 RDIMM이 x4를 선호해 온 이유입니다.
※ 주의: "SDDC(Single Device Data Correction)"라는 용어 자체와 DDR5 세대의 구체적 Chipkill/SDDC 구현(예: on-DIMM ECC 알고리즘, x4/x8별 정정 심볼 수)은 로컬 자료에서 확인하지 못했습니다(§4).

### 2.8 왜 DDR5 세대에서 온다이 ECC가 필수가 되었는가
확보한 근거로 말할 수 있는 것은 **동기(motivation)의 방향**까지입니다:
- JEDEC 초안: 목적은 "improve the data integrity within the DRAM"(L17124).
- Micron: 온다이 ECC는 "**reduce the system error correction burden**"하는 RAS 개선이며, 정정을 READ 시점에 DDR5 디바이스에서 데이터가 나가기 **전에** 수행한다(micron_ddr5.txt L119-120).

즉 두 1차 자료 모두 **"다이 내부 단일 비트 오류가 시스템으로 새어 나가는 양이 감당 안 될 만큼 늘었으므로 다이 안에서 먼저 걸러낸다"** 는 취지로 읽힙니다. 다만 **"셀 미세화 → 단일 비트 오류율 증가"를 정량적으로 뒷받침하는 수치(예: 노드별 FIT/Mbit 추이, 셀 커패시턴스 감소량)는 로컬 자료에서 확보하지 못했습니다**(§4). **schroeder09를 이 논거로 쓰면 안 됩니다** — 오히려 정반대 결론("신세대 DIMM에서 오류율 증가 증거 없음", schroeder09.txt L139-141)을 담고 있습니다. §3 참조.

---

## 3. 상충·불확실

| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| **"미세화로 오류율이 올라가서 온다이 ECC가 필수가 됐다"는 통념** | 온다이 ECC는 "다이 내 데이터 무결성 개선"(jesd79_5.txt L17124, T0초안) / "시스템 오류정정 부담 경감"(micron_ddr5.txt L119, T1) — 취지상 **오류 증가 대응**으로 읽힘 | schroeder09(T2, 2009): 6개 플랫폼을 비교했으나 **"신세대 DIMM일수록 오류율이 높다는 증거를 관측하지 못함"**, 오히려 신형 DIMM이 더 낮은 경우도 있음 (L139-141, L1810-1814) | **둘 다 기록.** A는 정성적 동기 서술이고 B는 DDR2/DDR3 시대(2006-2008) 실측이라 **직접 상충은 아님**(대상 세대가 다름). 다만 **schroeder09를 "미세화→오류 증가"의 근거로 인용하면 논문 결론을 뒤집어 쓰는 것**이므로 금지. DDR5 세대 미세화-오류율 정량 근거는 **미확보**(§4) |
| DDR5 온다이 ECC가 DED를 하는가 | JEDEC 초안·Micron 모두 **SEC only, DED 불가** (jesd79_5.txt L17124 / micron_ddr5.txt L125) | (상충 자료 없음) | **상충 없음.** 다만 웹·커뮤니티에서 "DDR5 온다이 ECC = SECDED"라는 서술이 흔하므로, 본 문서의 1차 자료(SEC)를 따를 것 |
| HBM3 온다이 ECC의 코드 종류 | JEDEC 보도자료: "**symbol-based** ECC" (T0 보도자료) | 웹 검색 결과 중 2·3차 매체에서 "SECDED"라는 서술이 관측됨 (T3/T4, 출처 불명확) | **JEDEC 보도자료 표현(symbol-based)만 채택.** SECDED 서술은 근거 불충분으로 **불채택**. HBM3 규격 원문(JESD238) **미확인** |
| ECS 전체 스크럽 권장 주기 | **24시간** (micron_ddr5.txt L139-140, T1) | JEDEC 초안 본문에 ECS 기능 절 자체가 **부재**(grep 0건) — 대조 불가 | **단일 출처(T1).** "24시간"은 Micron 백서 기준이며 JEDEC 비준본 확인 필요 |

---

## 4. 확인 실패 항목

솔직하게 적습니다. 아래는 찾으려 했으나 **근거를 확보하지 못한** 것입니다.

1. **JEDEC 비준본의 ECS 기능 절 전문.** 로컬 `jesd79_5.txt`(초안 Rev0.1)를 "scrub / Scrub / SCRUB"로 전문 grep한 결과 **매치 0건**. 초안에는 MR15 레지스터 껍데기만 있고 ECS 동작 규정이 없습니다. ECS 서술은 전적으로 Micron 백서(T1) 의존.
2. **ECS Error Threshold의 실제 값.** 초안 MR15 OP[5:0]의 Data 칸이 문자 그대로 **"TBD"**(jesd79_5.txt L2736-2739). OP[4:0]도 "RFU". 비준본에서 어떤 값으로 확정되었는지 미확인.
3. **MR14(ECC Configuration)의 비트 정의.** 초안에 레지스터 제목만 있고 상세 없음(jesd79_5.txt L2660-2661).
4. **온다이 ECC의 실시간 호스트 보고 유무를 표준 문구로 확정하지 못함.** "정정 사실을 호스트에 알리지 않는다"는 **명시적 부정문**을 초안에서 찾지 못했습니다. 확인된 것은 (a) 읽기 시 정정 후 데이터를 반환한다는 서술과 (b) ECS 완료 시 카운트 보고뿐입니다. 삼성 문서의 "**ECC Transparency**"(samsung_ddr5_udimm.txt L73)라는 기능명이 존재하나 **그 내용은 확인하지 못했습니다** — 이 기능이 호스트에게 온다이 ECC 상태를 노출하는 수단일 가능성이 있으므로, **"DDR5 온다이 ECC는 호스트에 아무것도 알리지 않는다"고 단정하지 마십시오.**
5. **DDR5 서브채널 40비트의 32(데이터)+8(ECC) 분해.** x80 모듈 표기는 확인(micron_32gb_rdimm.txt)했으나 "32 data + 8 ECC"라는 명시 문자열은 로컬 자료에서 미확인. §2.7(6)의 분해는 **산술 유도**임.
6. **DDR5 세대 Chipkill/SDDC의 구체 구현.** "SDDC" 용어 자체가 로컬 자료에 없음. x4/x8별 정정 심볼 수, DDR5 40비트 서브채널에서의 chipkill 성립 여부(8 체크비트로 x4 칩 하나를 커버할 수 있는지) 등 **전부 미확인**. schroeder09의 chipkill 정의는 **2009년 DDR2 시대 기준**임.
7. **셀 미세화와 단일 비트 오류율의 정량 관계.** 노드별(예: 1x/1y/1z/1α) FIT/Mbit 추이, 셀 커패시턴스·전하량 감소치 등 **수치 전무**. 온다이 ECC 도입 필연성의 정량 근거를 이 조사에서는 제시할 수 없습니다.
8. **OCP RAS 자료 확보 실패.** `ocp_ras.pdf`(5,647B)와 `ocp17.pdf`(5,815B)는 **PDF가 아니라 Cloudflare 차단 페이지 HTML**("Just a moment...")입니다. `ocp_ras.txt`(43B)도 그 잔여물. **OCP 계열 근거는 이 조사에서 전무**하며, 재수집이 필요합니다.
9. **HBM 관련 로컬 자료 확보 실패.** `mdpi_hbm.pdf`(410B)는 Akamai **"Access Denied"** HTML. HBM 근거는 JEDEC 보도자료(웹) **단일 출처**뿐이며 HBM3E/HBM4의 ECC는 미확인.
10. **DDR5 링크 CRC의 구체 사양.** 기능 존재는 확인(samsung_ddr5_udimm.txt L74)했으나 다항식, 커버 범위, 쓰기/읽기 적용 여부, 재시도 동작 등 **미확인**.
11. **온다이 ECC의 면적·전력 오버헤드**, 그리고 **온다이 ECC가 시스템 CE 로그를 가려서 RAS 예측을 방해한다는 문제**에 관한 1차 근거 — 미확보.

---

## 5. 기존 소스 팩(v3)과의 충돌

RAM-source-pack.md를 ECC/ECS/scrub/SECDED/Chipkill/parity 키워드로 grep한 결과 **매치 0건**. 기존 팩에 ECC 관련 서술이 전혀 없으므로 **충돌 없음**. 전 항목 신규.

---

## 6. 집필 시 주의 (서술 규칙 제안)

1. **"DDR5는 ECC가 내장이므로 서버 ECC가 필요 없다"는 서술은 반드시 정정 대상으로 다룰 것.** 정정 근거 우선순위: ① 표준이 앨리어싱 규칙을 통해 시스템 ECC의 존재를 **명시적으로 전제**한다("still appear as a double bit fail to the system-level error correction") ② 온다이 ECC는 **SEC뿐이라 더블 비트를 검출조차 못 한다** ③ 링크 구간은 커버하지 않는다(그래서 CRC가 별도로 있다) ④ 같은 세대의 UDIMM과 RDIMM이 온다이 ECC는 공유하되 시스템 ECC는 RDIMM에만 있다. ①이 가장 강력하므로 이것을 앞세울 것.
2. **JEDEC 인용 시 반드시 "위원회 초안"임을 표기할 것.** 로컬 jesd79_5.txt는 Rev0.1 회람본이며, ECS 임계값이 "TBD", MR15 OP[4:0]이 "RFU"로 남아 있는 **미완성 문서**입니다. "JESD79-5 표준에 따르면"이라고 단정하지 말고 "DDR5 사양 초안(JC42.3 회람본) 기준"으로 쓸 것.
3. **온다이 ECC를 "SECDED"라고 쓰지 말 것.** 1차 자료는 일관되게 **SEC**이며 Micron은 DED가 **불가능**하다고 명시합니다. SECDED는 시스템 ECC 쪽 용어로만 사용할 것.
4. **"DDR5 온다이 ECC는 호스트에 오류를 전혀 보고하지 않는다"고 단정하지 말 것.** 확인된 보고 경로는 ECS 완료 후의 집계(카운트 + 최다 오류 행, 임계값 초과 시)뿐이지만, 삼성 문서의 "ECC Transparency" 기능 내용을 확인하지 못했습니다. 안전한 표현: **"실시간·주소 단위 CE 보고는 확인되지 않았고, 확인된 보고는 ECS 완료 후의 임계값 기반 집계 정보뿐"**.
5. **schroeder09 수치를 쓸 때는 반드시 "2009년 발표, 2006년 1월–2008년 6월 Google fleet 측정"을 함께 적을 것.** DDR5는커녕 DDR3도 아닌 시기의 데이터입니다. "현재 DRAM은 연간 8%가 오류를 낸다" 식으로 현재형 서술 금지.
6. **schroeder09를 "미세화 → 오류율 증가"의 근거로 절대 인용하지 말 것.** 이 논문은 정반대로 **신세대 DIMM에서 오류율 증가 증거를 찾지 못했다**고 결론냅니다. 인용하면 논문 결론을 뒤집는 오인용이 됩니다.
7. **schroeder09의 또 다른 핵심 — "하드 에러 지배적"을 빠뜨리지 말 것.** 우주선(soft error) 중심의 통념을 이 논문이 반박했다는 점이 ECC 필요성 논의에서 중요합니다(하드 에러는 스크럽으로 안 없어지고 반복되며, 그래서 CE 발생 이력이 DIMM 교체 신호가 됩니다).
8. **"온다이 ECC가 필수가 된 이유 = 셀 미세화"를 수치로 뒷받침하려 하지 말 것.** 이 조사에서 정량 근거를 **확보하지 못했습니다**(§4-7). 서술한다면 "표준·제조사 문서가 밝힌 도입 취지"까지만 쓰고, 미세화 인과는 정성적 추정임을 표시할 것.
9. **폭(x4/x8/x16)을 특정할 것.** 온다이 ECC는 폭에 따라 동작이 다릅니다(x4는 내부 RMW 및 128비트 내부 프리페치 필요, x8은 불필요, x16은 2코드워드 병렬). "DDR5 온다이 ECC는 이렇게 동작한다"고 뭉뚱그리면 틀립니다.
10. **ECS의 요점은 "읽기 정정이 배열에 반영되지 않는다"는 점에서 출발할 것.** 이 전제(jesd79_5.txt L17134-17135)를 빼면 ECS가 왜 필요한지 설명되지 않습니다.
11. **Chipkill을 DDR5에 그대로 적용하지 말 것.** 인용 가능한 chipkill 정의는 schroeder09(2009, DDR2 시대) 것뿐이며, DDR5의 40비트 서브채널 구조에서 chipkill이 어떻게 성립하는지는 **미확인**입니다.
12. **HBM은 DDR5와 다르게 서술할 것.** JEDEC 보도자료 기준 HBM3는 **symbol-based** 온다이 ECC이고 **real-time error reporting**을 명시합니다 — DDR5 온다이 ECC(SEC, 실시간 보고 미확인)와 성격이 다릅니다. 다만 근거가 **보도자료 단일 출처**이므로 규격 원문 확인 전에는 단정 금지.
13. **OCP RAS 근거는 이 문서에 없음.** 로컬 ocp 파일들이 차단 페이지이므로, OCP를 인용하려면 재수집이 선행되어야 합니다.

---

## 7. 출처 목록

| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| jesd79_5.txt (로컬) | T0 **(위원회 초안)** | "Proposed DDR5 Full spec (79-5)", JC42.3 ballot 회람본 Rev0.1. 사용 절: §4.29 On-Die ECC (Ballot #1830.50), §3.5.16 MR14 ECC Configuration / §3.5.17 MR15 ECS Threshold (Ballot #1845.40) | 2026-07-29 |
| micron_ddr5.txt / micron_ddr5_wp.txt (로컬, 두 파일 내용 동일) | T1 | Micron DDR5 백서 — RAS 절(On-Die ECC, ECS, PPR) | 2026-07-29 |
| micron16gb_ddr5.txt (로컬) | T1 | Micron 16Gb DDR5 SDRAM **Die Rev D** Function Matrix (문서 rev F, 2024-04) — ECS Writeback Suppression / x4 RMW Suppression 기능 확인 | 2026-07-29 |
| micron_32gb_rdimm.txt (로컬) | T1 | Micron 32GB (**x80, ECC**, DR) 288-Pin DDR5 RDIMM 데이터시트 | 2026-07-29 |
| samsung_ddr5_udimm.txt (로컬) | T1 | 삼성 DDR5 UDIMM 자료 — 기능 목록에서 On-Die ECC / ECC Transparency and Error Scrub / CRC 구분 확인 | 2026-07-29 |
| schroeder09.txt (로컬) | T2 | Schroeder, Pinheiro, Weber, "DRAM Errors in the Wild: A Large-Scale Field Study", SIGMETRICS 2009. **측정 기간 2006-01–2008-06** | 2026-07-29 |
| JEDEC 보도자료 (웹) | T0 (보도자료, **규격 원문 아님**) | "JEDEC Publishes HBM3 Update to High Bandwidth Memory (HBM) Standard" (JESD238, 2022-01) — https://www.jedec.org/news/pressreleases/jedec-publishes-hbm3-update-high-bandwidth-memory-hbm-standard | 2026-07-29 |
| ~~ocp_ras.pdf / ocp17.pdf / mdpi_hbm.pdf~~ | — | **사용 불가.** 실제 내용은 Cloudflare "Just a moment..." 챌린지 페이지 및 Akamai "Access Denied" HTML. PDF 아님 | 2026-07-29 |
