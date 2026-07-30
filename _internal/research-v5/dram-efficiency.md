# 뱅크 병렬성과 실효 대역폭
> 조사일: 2026-07-29 / 상태: **완료** (로컬 1차 자료 중심 + 웹 검색 2회·WebFetch 3회 보조)

**조사 범위 주의**: 이 주제는 "구조적 제약(스펙 값)"과 "성능 결과(시뮬레이션 값)"가 섞여 있습니다.
아래 §1은 **스펙 원문에서 직접 읽은 값**, §2-B는 **시뮬레이션/모델 값**으로 분리했습니다. 절대 섞지 마십시오.

---

## 1. 확인된 사실

### 1-A. 뱅크·뱅크그룹 구성 (구조)

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR4 16Gb 뱅크 구성 | x4/x8: 4 뱅크그룹 × 4 뱅크 = **16 뱅크** / x16: 2 BG × 4 = **8 뱅크** | T1 | micron_ddr4_16gb.txt (16Gb x4/x8/x16 DDR4 SDRAM, Rev. H 8/2021) — "Bank Group 0–3", 각 BG에 Bank 0–3 블록도 L16440–16460 | 페이지 크기: x4=512B(1/2KB), x8=1KB, x16=2KB |
| DDR5 16Gb 뱅크 구성 | x4: 8 BG × 4 = **32 뱅크** / x8: 8 BG × 4 = **32 뱅크** / x16: 4 BG × 4 = **16 뱅크** | T1 | micron16gb_ddr5.txt L78-89 (Table 1: 16Gb Addressing, Micron 16Gb DDR5 Die Rev D, 2024-04) | 페이지 크기 x4=1KB. **DDR4 대비 뱅크그룹 2배, 뱅크 총수 2배** |
| DDR5 뱅크 증설의 목적 (제조사 서술) | "뱅크그룹 수를 2배로 늘리고 BG당 뱅크 수는 유지 → 동시에 열어 둘 수 있는 페이지가 늘고, **짧은 타이밍(tCCD_S/tRRD_S/tWTR_S)이 쓰일 확률이 올라감**" | T1 | micron_ddr5.txt L17-27 (Micron DDR5 백서, "Overall Bank Increase") | 백서 원문: "tCCD_L can be nearly double tCCD_S" |
| DDR5 32GB RDIMM 랭크 | 2랭크(DR), x80 모듈 폭, 구성 부품 16Gb(2Gb x8), **32 banks** | T1 | micron_32gb_rdimm.txt L82 | 소스팩 v4 L816과 일치 |

### 1-B. 뱅크 병렬성을 제한하는 타이밍 (DDR4, Micron 16Gb, Rev. H 8/2021)

**세 열 = DDR4-2666 / DDR4-2933 / DDR4-3200** (헤더 확인: micron_ddr4_16gb.txt L39270 "Table 161 … DDR4-2666 / DDR4-2933 / DDR4-3200"). 모두 T1, 확인일 2026-07-29.

| 파라미터 | DDR4-2666 | DDR4-2933 | DDR4-3200 | 출처 라인 |
|---|---|---|---|---|
| tCCD_S (다른 BG 간 CAS→CAS) | 4nCK | 4nCK | 4nCK | micron_ddr4_16gb.txt L16390–16400 (Table 70 예시표는 1600/2133/2400) |
| tCCD_L (같은 BG 내 CAS→CAS) | **1600: max(4nCK, 6.25ns) / 2133: max(4nCK, 5.355ns) / 2400: max(4nCK, 5ns)** | — | — | 같은 표. **2666–3200 열의 tCCD_L 값은 텍스트 추출 깨짐으로 확인 실패** (아래 §4) |
| tRRD_S (1/2KB 페이지) | max(4CK, 3.0ns) | max(4CK, 2.7ns) | max(4CK, 2.5ns) | L39312–39340 |
| tRRD_S (1KB) | max(4CK, 3.0ns) | max(4CK, 2.7ns) | max(4CK, 2.5ns) | L39322~ |
| tRRD_S (2KB) | max(4CK, 5.3ns) | max(4CK, 5.3ns) | max(4CK, 5.3ns) | L39332~ |
| tRRD_L (1/2KB, 1KB) | max(4CK, 4.9ns) | max(4CK, 4.9ns) | max(4CK, 4.9ns) | L39344–39370 |
| tRRD_L (2KB) | max(4CK, 6.4ns) | max(4CK, 6.4ns) | max(4CK, 6.4ns) | L39372~ |
| **tFAW (1/2KB)** | max(16CK, 12ns) | max(16CK, 10.875ns) | max(16CK, **10ns**) | L39388–39400 |
| **tFAW (1KB)** | max(20CK, 21ns) | max(20CK, 21ns) | max(20CK, **21ns**) | L39402–39410 |
| **tFAW (2KB)** | max(28CK, 30ns) | max(28CK, 30ns) | max(28CK, **30ns**) | L39412–39420 |
| **tWTR_L** (WRITE→READ, 같은 BG) | max(4CK, 7.5ns) | max(4CK, 7.5ns) | max(4CK, 7.5ns) | L37451– ("tWTR_L1ck MIN = greater of 4CK or 7.5ns") |
| **tWTR_S** (WRITE→READ, 다른 BG) | max(2CK, 2.5ns) | max(2CK, 2.5ns) | max(2CK, 2.5ns) | L16485–16490 (Table 70; 1600/2133/2400 열 전부 동일 값) — **2666–3200 열 직접 확인은 못했으나 JEDEC상 값이 속도무관 고정** |
| tRTP (READ→PRECHARGE) | max(4nCK, 7.5ns) | 〃 | 〃 | L19383 원문: "tRTP (MIN) = MAX (4 nCK, 7.5ns)" |
| tWR (WRITE recovery) | 15ns | 15ns | 15ns | L37428 "tWR1ck MIN = 15ns" |
| tRCD / tRP (DDR4-3200) | — | — | **13.75ns** (22-22-22 빈) | L97-106, L34562 등. 스피드빈 표 |

**중요**: DDR4 spec에는 **tRTW(READ→WRITE turnaround)라는 이름의 파라미터가 없습니다.** 버스 방향 전환은 CL/CWL/버스트 길이로부터 컨트롤러가 계산합니다(§2-C 참조). 로컬 자료에서 WRITE→READ 방향은 `CWL + WBL/2 + tWTR_L` (같은 BG) / `CWL + WBL/2 + tWTR_S` (다른 BG)로 명시됨 — micron_ddr4_16gb.txt L16847, L16850 (T1).

### 1-C. DDR5 타이밍 (JESD79-5 **Full Spec Draft Rev0.1 회람본**)

⚠ **비준본이 아닙니다.** 이 표의 세 속도등급 열은 **DDR5-3200 / DDR5-3600 / DDR5-4000**입니다
(근거: 목차 §10.1/10.2/10.3 "DDR5-3200 / 3600 / 4000 Speed Bins", jesd79_5.txt L419-421; §12.2.1 "Timing Parameters for DDR-3200 to DDR5-4000", L439). **DDR5-4800 이상 값은 이 문서에 없습니다.**

| 파라미터 | DDR5-3200 | DDR5-3600 | DDR5-4000 | 출처 라인 | 등급 |
|---|---|---|---|---|---|
| **tCCD_L** (같은 BG CAS→CAS) | max(8nCK, 5ns) | max(8nCK, 5ns) | max(8nCK, 5ns) | jesd79_5.txt L22916-22928 | T0(초안) |
| **tCCD_L_WR** (같은 BG WR→WR) | max(32nCK, 20ns) | 〃 | 〃 | L22929-22941 | T0(초안) |
| **tCCD_S** (다른 BG CAS→CAS, BL16/BC8) | **8nCK 고정** | 8nCK | 8nCK | L22942-22952 | T0(초안) |
| tRRD_S (2K / 1K / 1/2K) | 8nCK | 8nCK | 8nCK | L22953-22985 | T0(초안) |
| tRRD_L (2K / 1K / 1/2K) | max(8nCK, 5ns) | 〃 | 〃 | L22986-23027 | T0(초안) |
| **tFAW_2K** | max(40nCK, 25ns) | max(40nCK, 22.22ns) | max(40nCK, 20ns) | L23028-23039 | T0(초안) |
| **tFAW_1K** | max(32nCK, 20ns) | max(32nCK, 17.77ns) | max(32nCK, 16ns) | L23040-23051 | T0(초안) |
| **tFAW_1/2K** | max(32nCK, 20ns) | max(32nCK, 17.77ns) | max(32nCK, 16ns) | L23052-23064 | T0(초안) |
| **tWTR_S** | 2.5ns | 2.5ns | 2.5ns | L23065-23075 | T0(초안) |
| **tWTR_L** | 7.5ns | 7.5ns | 7.5ns | L23076-23086 | T0(초안) |
| tRTP | 7.5ns | 7.5ns | 7.5ns | L23087-23096 | T0(초안) |
| tWR | 30ns | 30ns | 30ns | L23097-23104 (표에 "45"로 추출됨 → **추출 오류 의심, 확인 실패 처리**) | — |

> **tWR 주의**: jesd79_5.txt L23099에 "45"로 추출되었으나 단위·열 정렬이 불확실합니다. **인용하지 마십시오.**

### 1-D. DDR5 리프레시 파라미터 (JESD79-5 Draft Rev0.1 Table 26)

| 파라미터 | 8Gb | 16Gb | 32Gb | 등급 | 출처 |
|---|---|---|---|---|---|
| tRFC1 (REFab, Normal) | 195ns | **295ns** | **TBD** | T0(초안) | jesd79_5.txt L11500-11505 |
| tRFC2 (REFab, FGR) | 130ns | **160ns** | TBD | T0(초안) | L11506-11511 |
| **tRFCsb (REFsb, Same-Bank)** | 115ns | **130ns** | TBD | T0(초안) | L11512-11517 |
| tREFSBRD (REFsb→ACT, 다른 뱅크) | 30ns | **30ns** | TBD | T0(초안) | L11524-11529 |
| tREFI (Normal, 0–85°C) | 3.9µs (85–95°C: 1.95µs) | 〃 | 〃 | T0(초안) | L11474-11483 |
| tREFI2 (FGR, 0–85°C) | 1.95µs (85–95°C: 0.975µs) | 〃 | 〃 | T0(초안) | L11484-11493 |

**32Gb는 TBD입니다. 32Gb DDR5 tRFC를 인용하지 마십시오.**

### 1-E. DDR5 same-bank refresh(REFsb)의 동작 규칙 — 실효 대역폭 관점

| 항목 | 내용 | 등급 | 출처 |
|---|---|---|---|
| REFsb 대상 | "각 뱅크그룹 내 특정 뱅크 하나"에 리프레시 적용 | T0(초안) | jesd79_5.txt L11389-11393 (§4.10.3) |
| 접근 차단 범위 | "REFsb가 발행되면 대상 뱅크(각 BG에 하나씩)는 tRFCsb 동안 접근 불가. **그러나 각 BG의 나머지 뱅크는 접근 가능하며 이 same-bank refresh 사이클 동안에도 주소 지정 가능**" | T0(초안) | jesd79_5.txt L11411-11413 |
| 조건 | FGR 모드(MR4[OP4]=1)에서만 허용. 모든 뱅크가 REFsb를 한 번씩 받기 전에 같은 뱅크에 재발행 불가 | T0(초안) | L11393-11399, L11421 |
| REFab ↔ REFsb 치환 | "REFab 1개는 스케줄링(postpone/pull-in) 목적으로 **REFsb 2개 또는 4개로 대체 가능**" | T0(초안) | L11422-11423 |
| 버스트 제한식 | 4 × (tRFCsb + [(n-1) × tRRD_L]), n = 뱅크 수 | T0(초안) | L11423 |
| 제조사 서술 | "16Gb x4/x8 기준 나머지 **12개 뱅크는 idle일 필요가 없고**, 비대상 뱅크에 대한 유일한 제약은 tREFSBRD" | T1 | micron_ddr5.txt L56-59 |

### 1-F. DDR5 서브채널·버스트 (실효 효율 관점)

| 항목 | 값 | 등급 | 출처 |
|---|---|---|---|
| DDR5 기본 버스트 길이 | BL8(DDR4) → **BL16**. "동일한 read/write CA 트랜잭션이 데이터 버스에 2배의 데이터를 실어 준다" | T1 | micron_ddr5.txt L35-38 |
| BL16과 서브채널의 인과관계 | "기본 버스트 길이 증가가 **DDR5 DIMM의 dual sub-channel 아키텍처를 가능하게 하며**, 채널 동시성(concurrency)·유연성·개수를 늘린다" | T1 | micron_ddr5.txt L40-42 |
| 서브채널 폭 | 40핀 서브채널 (Figure 2 제목: "Simplified DDR5 40-Pin Sub-Channel DIMM Example") | T1 | micron_ddr5.txt L64 |
| BL32 옵션 | 128B 캐시라인 시스템을 위해 **x4 구성 전용 BL32** 추가 | T1 | micron_ddr5.txt L42-44 |
| DDR5 버스 폭 | 64-bit = 32-bit 서브채널 2개 | T0 | 기존 소스팩 v3 L180 (중복 — 재수집 안 함) |

### 1-G. row buffer hit rate — 확보한 유일한 정량 자료 (웹 보조, **전부 시뮬레이션**)

출처: Ghose, Li, Hajinazar, Senol Cali, Mutlu, *"Understanding the Interactions of Workloads and DRAM Types:
A Comprehensive Experimental Study"*, **arXiv:1902.07609** (CMU / SFU / ETH Zürich). 등급 **T2**. 확인일 2026-07-29.
확인 경로: https://ar5iv.labs.arxiv.org/html/1902.07609

| 워크로드 조건 | row buffer hit rate | 비고 |
|---|---|---|
| **단일 스레드 데스크톱·과학 응용 (DDR3)** | **2.4% – 53.1%** (응용별 분포) | 원문: "row buffer hit rates falling anywhere between 2.4–53.1%" |
| **멀티프로그램 번들 D9 (DDR3 및 그 밖 모든 DRAM 타입)**, MPKI = 167.4 | **5.6%를 넘지 않음** | 원문: "the row buffer hit rate never exceeds 5.6% on any DRAM type" |
| **멀티스레드 quicksilver (DDR3)** | **1스레드 83.1% → 32스레드 7.2%** | 스레드 수만 늘려도 hit rate가 12배 붕괴 |
| **mcf (모든 DRAM 타입)** | 정성 서술 | "대부분의 메모리 요청이 row conflict" |
| **facesim, 32스레드** | 정성 서술 | "row buffer locality를 활용하지 못함" |

동 논문은 **Bank Parallelism Utilization (BPU)**라는 지표(= 평균 동시 활성 뱅크 수)를 제안하고 다음 값을 보고합니다:

| 워크로드 | BPU | 조건 |
|---|---|---|
| namd | **4.03** | DDR3 |
| gobmk | **2.91** | DDR3 |
| mcf | **5.33** | **DDR4** — 데스크톱 응용 중 최고 |
| 멀티프로그램 번들 D7 | HMC에서 DDR3 대비 **2.05배** | — |

⚠ **주의 3가지**
- 이 값들은 **전부 시뮬레이션**입니다. 실측이 아닙니다.
- **시뮬레이터 이름·코어 수·페이지 정책·스케줄러 등 세부 조건은 이번 조사에서 확보하지 못했습니다.**
  인용하려면 원문 §Methodology를 직접 확인해야 합니다.
- 게재 학회(SIGMETRICS/POMACS 등) 확인 실패. **arXiv 프리프린트로만 인용하십시오.**

---

## 2. 구조·메커니즘 서술

### 2-A. 왜 대역폭은 1/지연이 아닌가 — 뱅크 병렬성과 파이프라이닝

**핵심 논리 (스펙 값으로 직접 검증 가능):**

한 뱅크는 ACT를 받은 뒤 다음 ACT를 받기까지 tRC 동안 묶입니다. 만약 메모리가 뱅크 하나뿐이라면
채널 대역폭은 `버스트 데이터량 ÷ tRC`가 상한이 됩니다. 그러나 DRAM은 뱅크가 여러 개이고,
**어떤 뱅크가 tRC 동안 회복 중이어도 다른 뱅크는 독립적으로 ACT/RD/PRE를 진행할 수 있습니다.**

- RAIDR(ISCA 2012) 원문 서술 (T2, raidr.txt L209-214):
  "각 뱅크는 별개의 DRAM 셀 어레이에 대응한다. 따라서 한 랭크 내 모든 뱅크는 병렬로 동작할 수 있다.
  단, 이 **bank-level parallelism은 (a) 공유 채널 대역폭과 (b) DRAM 디바이스 내 뱅크 간 공유 자원
  (예: 디바이스 전력)에 의해 제약된다**."
- 같은 문헌은 랭크에 대해서도 동일 논리를 적용합니다 (L205-208): "한 채널의 모든 랭크는 병렬 동작
  가능하나 **공유 채널 대역폭에 의해 제약**된다."

**따라서 실효 대역폭의 상한은 두 겹입니다.**
1. **버스(핀) 상한** — 채널 폭 × 데이터레이트. 이건 tRC와 무관.
2. **어레이 측 공급 능력** — 뱅크 수 × (버스트 데이터량 / tRC), 그리고 tRRD/tFAW/전력 제약.

이 둘 중 작은 쪽이 실효 상한입니다. 뱅크가 충분히 많고 접근이 뱅크에 골고루 흩어지면 (1)이 지배하고,
그때 대역폭은 지연과 사실상 무관해집니다. 반대로 접근이 소수 뱅크에 몰리면 (2)가 지배하고 **대역폭이
tRC에 묶입니다** — 이것이 "대역폭 ≠ 1/지연"이면서 동시에 "지연이 대역폭에 전혀 무관하지도 않은" 이유입니다.

### 2-B. tCCD가 만드는 "버스 채움률" 상한 — 뱅크그룹의 존재 이유

이 부분은 **스펙 값으로부터의 산술 유도**입니다(집필 시 "유도"라고 밝히십시오).

DDR5는 BL16이므로 한 CAS의 데이터 전송은 **8 tCK** 동안 버스를 씁니다(16 beats ÷ 2 beats/tCK).

- **다른 뱅크그룹 간**: tCCD_S = **8nCK 고정** (jesd79_5.txt L22945-22951, T0 초안).
  → 8 tCK 간격으로 CAS를 낼 수 있고 각 CAS가 8 tCK를 채우므로 **버스 100% 채움이 원리적으로 가능**.
- **같은 뱅크그룹 내**: tCCD_L = **max(8nCK, 5ns)** (L22918-22927).
  - DDR5-3200: tCK = 0.625ns → 8nCK = 5ns → tCCD_L = 8 tCK → 채움률 8/8 = **100%**
  - DDR5-4800(가정, tCK ≈ 0.4167ns): 5ns = 12 tCK → 채움률 8/12 ≈ **67%** *(유도값. 단, 4800 스피드빈의 tCCD_L 실제 규정값은 로컬 초안에 없음 → §4)*
  - DDR5-6400(가정, tCK = 0.3125ns): 5ns = 16 tCK → 8/16 = **50%** *(같은 단서)*
- **쓰기는 더 나쁩니다**: tCCD_L_WR = **max(32nCK, 20ns)** (L22931-22940). 같은 BG로 연속 쓰기를 하면
  8 tCK 데이터에 대해 최소 32 tCK를 기다립니다 → **채움률 8/32 = 25%** (DDR5-3200 기준 유도).

**결론**: 뱅크그룹은 "속도가 올라갈수록 tCCD_L(ns 고정)이 tCK 대비 길어지는" 문제를 우회하려고 만든 구조입니다.
같은 BG로만 접근이 몰리면 데이터레이트를 올려도 실효 대역폭이 비례해서 오르지 않습니다.
DDR5가 뱅크그룹을 4개→8개로 늘린 것이 정확히 이 확률을 낮추기 위함이라고 마이크론이 명시합니다
(micron_ddr5.txt L27: "Increased bank groups mitigate internal timing constraints by increasing the probability
that the short timings are in use").

DDR4에서도 같은 구조입니다. BL8 → 데이터 전송 4 tCK, tCCD_S = 4nCK → 다른 BG 간 100% 가능.
tCCD_L은 DDR4-2400에서 max(4nCK, 5ns) = 12 tCK... 아니라 **8 tCK**(tCK=0.833ns 기준 5ns≈6 tCK) —
정확한 열 값이 추출 실패이므로 **DDR4-3200의 tCCD_L 수치는 §4(확인 실패)로 넘깁니다.**

### 2-C. read/write turnaround — 버스 방향 전환 비용

**DDR4/DDR5 스펙에는 "tRTW"라는 파라미터가 없습니다.** 방향 전환 비용은 두 갈래로 나뉩니다.

**(1) WRITE → READ**: 스펙에 명시적 파라미터가 있습니다.
- 컨트롤러가 지켜야 하는 총 간격 = `CWL + WBL/2 + tWTR_L` (같은 뱅크그룹) 또는 `CWL + WBL/2 + tWTR_S` (다른 BG).
  출처: micron_ddr4_16gb.txt L16847, L16850 (T1).
- tWTR_L = max(4CK, **7.5ns**), tWTR_S = max(2CK, **2.5ns**) — DDR4 (micron_ddr4_16gb.txt L37451 이하, L16485 이하).
- tWTR_L = **7.5ns**, tWTR_S = **2.5ns** — DDR5-3200/3600/4000 (jesd79_5.txt L23068-23086, T0 초안).
- 즉 **DDR4→DDR5로 오면서 tWTR의 ns 값은 그대로**입니다. 클럭이 빨라진 만큼 **tCK 단위 페널티는 커집니다.**
  DDR5-4000(tCK=0.5ns) 기준 tWTR_L = 15 tCK. 이 동안 데이터 버스는 비어 있습니다. (유도)
- 뱅크그룹이 다르면 **7.5ns → 2.5ns로 3배 줄어듭니다.** 이것도 뱅크그룹 병렬성의 직접 효과입니다.

**(2) READ → WRITE**: 스펙에 별도 파라미터가 없고, 컨트롤러가 CL/CWL과 버스트 길이, 그리고 DQS
프리앰블/포스트앰블로부터 계산합니다. **로컬 자료에서 구체적 tRTW 수치를 확인하지 못했습니다** (§4).

**(3) 랭크 전환(tRTRS)**: **tRTRS는 JEDEC 파라미터가 아니라 시뮬레이터/아키텍처 모델 파라미터입니다.**
- 로컬에서 확인된 유일한 값: **tRTRS = 2 DRAM cycles** — mukundan.txt L1062-1063.
  조건: **DDR4 @1600 Mbps, 16Gb 칩 시뮬레이션 파라미터 표** (T2, 학회 논문의 시뮬레이션 설정).
- jesd79_4.txt / jesd79_5.txt / micron 데이터시트 전체에서 "tRTRS" 문자열 **0건** (검색 확인, 2026-07-29).
- **집필 시 "JEDEC이 tRTRS를 규정한다"고 쓰면 틀립니다.**

### 2-D. row buffer hit rate와 open-page / close-page

**구조**: ACT가 한 행 전체를 센스앰프(row buffer)로 올립니다. 후속 접근이 같은 행이면 CAS만으로 끝나고
(row hit), 다른 행이면 PRE→ACT→CAS가 필요합니다(row conflict/miss).

- **open-page**: 접근 후 행을 열어 둠. 지역성이 있으면 hit로 tRCD+tRP를 절약. 없으면 conflict 시 tRP를 추가로 물음.
- **close-page**: 접근 직후 auto-precharge로 닫음. hit 기회를 포기하는 대신 conflict 페널티를 없앰.
- 로컬 자료에서 확인된 실제 사용례:
  - RAIDR(ISCA 2012) 평가 시스템: "FR-FCFS scheduling, line-interleaved mapping, **open-page policy**",
    8코어 4GHz, 32GB, 2채널 × 4랭크/채널 × 8뱅크/랭크, 64K rows/bank, **8KB rows**, DDR3-1333
    (raidr.txt L872-878, T2).
  - Bhati et al. (IEEE TC 2015) 시뮬레이션: "**Open page**, first ready first come first serve,
    'RW:BK:RK:CH:CL' address mapping, 64-entry queue, 1 channel", 4코어 2GHz OoO, L2 8MB 공유
    (jacob_refresh.txt L606-608, T2).
  - Mukundan et al. (ISCA 2013): "우리는 **open page 정책**으로 실험했고, 결과와 통찰은 우리가 제시하는
    **closed page**의 것과 거의 같다" (mukundan.txt L1083-1085, T2). → **정책 선택이 refresh 오버헤드
    결론을 바꾸지 않았다는 저자들의 명시적 진술.** 인용 가치 높음.

**refresh가 row hit rate를 파괴한다** (RAIDR, raidr.txt L357-361, T2 — 원문 3가지 열화 경로):
1. **bank-level parallelism 손실**: 리프레시 중인 뱅크는 요청을 서비스할 수 없음 → 메모리 시스템 throughput 감소.
2. **접근 지연 증가**: 리프레시 중인 뱅크에 대한 접근은 tRFC를 기다려야 함. "현대 DRAM에서 300ns 수준".
3. **row hit rate 감소**: "리프레시는 **한 랭크의 열린 행을 모두 닫게 만들고**, 리프레시 직후 대량의
   row miss를 유발하여 throughput 감소·지연 증가로 이어진다."

**FR-FCFS가 최적화하는 것** (개념 수준 — 컨트롤러 알고리즘 상세는 본 문서 범위 밖):
- RAIDR 원문 (raidr.txt L1177-1181, T2): "흔히 쓰이는 **FR-FCFS 메모리 스케줄링 정책은 메모리 throughput을
  최대화하지만, 시스템 성능을 반드시 최대화하지는 않는다. row hit rate가 높은 응용이 row hit rate가
  낮은 응용을 굶길 수 있다**."
- Mukundan et al. (mukundan.txt L751-754, T2): "대부분의 현대 메모리 스케줄러는 FR-FCFS의 변형을 쓴다.
  **FR-FCFS 스케줄링 정책은 RAS(=ACT) 명령보다 CAS 명령을 우선한다.**"
- → 집필 요지: **FR-FCFS는 "지연 최소화"가 아니라 "데이터 버스 점유율(throughput) 최대화"를 목적함수로
  삼는다. 공정성(fairness)은 목적함수에 없다.** 이것이 정확한 개념 수준 서술입니다.

### 2-E. 버스 효율을 갉아먹는 요인 — 정리

| 요인 | 메커니즘 | 확인된 정량 근거 |
|---|---|---|
| **refresh** | 대상 뱅크/랭크 tRFC 동안 정지 + 열린 행 강제 닫힘 | DDR5 16Gb tRFC1=295ns / tRFC2=160ns / tRFCsb=130ns, tREFI=3.9µs (§1-D). 성능 영향은 §2-F |
| **row conflict** | PRE(tRP) + ACT(tRCD) 추가. DDR4-3200에서 각 13.75ns | micron_ddr4_16gb.txt 스피드빈 22-22-22 (T1) |
| **tFAW** | 임의의 rolling window 내 ACT 4회 초과 불가 → 뱅크가 아무리 많아도 **ACT 발행률 상한**. 전력(피크 전류) 제약이 근원 | DDR4-3200 1KB: 21ns / DDR5-4000 1K: max(32nCK,16ns) (§1-B/1-C) |
| **tRRD** | 연속 ACT 간 최소 간격. 같은 BG(tRRD_L)가 다른 BG(tRRD_S)보다 김 | DDR4-3200 1KB: tRRD_S 2.5ns vs tRRD_L 4.9ns → **약 2배** (T1) |
| **tCCD_L** | 같은 BG 연속 CAS 간격이 버스트 시간보다 길어짐 → 버스 빈칸 | DDR5 tCCD_L=max(8nCK,5ns) vs tCCD_S=8nCK (§2-B) |
| **write→read turnaround** | tWTR_L 7.5ns / tWTR_S 2.5ns 동안 데이터 버스 유휴 | DDR4·DDR5 공통 (§2-C) |
| **rank 전환 (tRTRS)** | 서로 다른 랭크의 드라이버가 겹치지 않게 버스에 갭 삽입 | **JEDEC 규정 없음.** 모델값 2 DRAM cycles (mukundan.txt, DDR4-1600 시뮬레이션 설정) |
| **tCCD_L_WR** | DDR5 같은 BG 연속 쓰기 max(32nCK, 20ns) | jesd79_5.txt L22931 (T0 초안) |

**핵심 관찰**: 위 요인 대부분이 "**같은 뱅크그룹**이면 페널티가 크고, **다른 뱅크그룹**이면 작다"는
동일한 패턴을 갖습니다. tCCD, tRRD, tWTR 세 개가 전부 `_L`/`_S` 쌍으로 정의되어 있습니다.
DDR5가 뱅크그룹을 8개로 늘린 것은 이 세 페널티를 동시에 겨냥한 단일 조치입니다.

### 2-F. 시뮬레이션·모델 값 (실측 아님 — 반드시 구분)

| 결과 | 값 | 조건 (반드시 병기) | 등급 | 출처 |
|---|---|---|---|---|
| refresh로 인한 IPC 손실 (HIGH bandwidth 워크로드) | **최대 11.4%** | 4코어 2GHz OoO, 8GB, **8Gb DDR4 디바이스**, open-page + FR-FCFS, 1채널. 워크로드: libquantum, mcf, mix2. 디바이스 속도 1066–3200 Mbps 스윕. **시뮬레이션** | T2 | jacob_refresh.txt L657-659 |
| 디바이스 밀도 증가 시 IPC 손실 | **32Gb 디바이스에서 30% 초과** (libquantum, mcf) | 같은 시뮬레이션 환경, 밀도 1Gb→32Gb 스윕. **32Gb는 당시(2015) 미출시 — 외삽 tRFC 사용** | T2 | jacob_refresh.txt L679-681 |
| refresh 에너지 비중 | 32Gb, LOW bandwidth 프로그램에서 DRAM 에너지의 **25–30%** | 같은 조건 | T2 | jacob_refresh.txt L675-677 |
| LOW bandwidth 워크로드의 평균 지연 열화 | **13% → 23.5%** (속도 증가에 따라) | hmmer, namd, mix1. 시뮬레이션 | T2 | jacob_refresh.txt L668-670 |
| **REFsb vs REFab 시스템 throughput** | **6–9% 향상** (read/write 명령 비율에 따라) | **마이크론 시뮬레이션.** Figure 4의 y축은 100–110%, x축 Read% = 0/10/33/50/66/90/100 | T1 | micron_ddr5.txt L72-73, L86-101 |
| **REFsb의 평균 idle latency adder** | REFab **11.2ns** → REFsb **5.0ns** | **"표준 대기행렬이론(queuing theory) 기반 계산이며, 랜덤 트래픽이 걸리는 단일 뱅크에 적용됨"** — 저자 명시 단서 | T1 | micron_ddr5.txt L74-82 |
| DDR5 종합 성능 향상 | "2x banks, 2x bank groups, BL16, same-bank refresh를 합쳐 **64B 랜덤 액세스 워크로드**를 시뮬레이션하면 **DDR4 dual-rank 3200 MT/s 모듈 대비 상당한 성능 증가**" | 8채널/시스템, 1DPC 가정. **구체 수치는 Figure 5 이미지에 있어 텍스트 추출 실패** | T1 | micron_ddr5.txt L111-113 |
| RAIDR의 성능 이득 | 메모리 강도 100% 카테고리에서 평균 **4.8%(단일 코어 9.8%)** | 8코어 4GHz, 32GB DDR3-1333, FR-FCFS + open-page. **시뮬레이션** | T2 | raidr.txt L1170-1174 |

**대기행렬이론 기반 값(11.2ns/5.0ns)은 실측이 아니라 해석적 모델값입니다. 마이크론 스스로 그렇게 밝힙니다.**

---

## 3. 상충·불확실

| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| DDR5 16Gb tRFC1 | **295ns** — jesd79_5.txt Table 26 (T0, **Draft Rev0.1**) | 비준본 JESD79-5B 이후 값 미확인 | 초안값임을 반드시 명시. 32Gb는 TBD |
| open-page vs close-page의 refresh 결론 영향 | Mukundan: "open page로 실험했고 결과·통찰은 closed page와 **거의 같다**" (mukundan.txt L1083) | 일반 통념: 정책에 따라 성능 크게 갈림 | **refresh 오버헤드 결론에 한정하여** 정책 무관하다는 뜻. 일반화 금지 |
| tRTRS의 지위 | mukundan.txt: 2 DRAM cycles (시뮬레이션 파라미터, DDR4-1600) | JEDEC 문서 내 정의: **없음** | tRTRS는 컨트롤러/시뮬레이터 개념. JEDEC 파라미터로 서술 금지 |
| DDR4 tFAW(1KB) | 21ns (2666/2933/3200 전부 동일, micron_ddr4_16gb.txt) | 20CK 조건도 병존 → max로 결정 | 상충 아님. **"max(20CK, 21ns)"로 온전히 인용할 것.** ns만 인용하면 저속 빈에서 틀림 |

---

## 4. 확인 실패 항목

1. **DDR4-2666/2933/3200의 tCCD_L 정확한 규정값.** micron_ddr4_16gb.txt의 Table 70(뱅크그룹 타이밍 예시)은
   DDR4-1600(max 4nCK/6.25ns) / 2133(5.355ns) / 2400(5ns)까지만 텍스트로 추출되었고, DDR4-2666 이상 열이
   담긴 AC 타이밍 표 영역은 **문자 깨짐(t22$?3 등)으로 판독 불가**. → **DDR4-3200 tCCD_L 수치를 쓰지 마십시오.**
2. **DDR5-4800 / 5600 / 6400의 tCCD_L, tFAW, tRRD 규정값.** 로컬 jesd79_5.txt는 Rev0.1 초안이라
   **DDR5-4000까지만** 수록. micron16gb_ddr5.txt(Die Rev D)에서 CCD/FAW/WTR/RRD 문자열 **0건**(검색 확인).
   웹 검색(2026-07-29) 요약에서 "DDR5-4800/6400도 tCCD_L = max(8nCK, 5ns)로 동일"이라는 진술을 얻었으나
   **T0(JESD79-5B/C 원문)이나 T1(제조사 데이터시트 표) 원문으로 검증하지 못했습니다. 인용 금지.**
   (참고로 이 값이 맞다면 §2-B의 유도 — 4800에서 채움률 67%, 6400에서 50% — 가 성립합니다.
   본문에 쓰려면 JESD79-5C 또는 마이크론/삼성 DDR5-6400 데이터시트 타이밍 표를 직접 확인하십시오.)
3. **tRTW(READ→WRITE turnaround)의 구체 수치.** 스펙에 파라미터 자체가 없고, 로컬 자료에서 컨트롤러가
   쓰는 계산식/실측값을 찾지 못함.
4. **tRTRS의 JEDEC 규정값.** 존재하지 않음(위 §2-C). 실제 시스템의 랭크 전환 갭 실측값도 확인 실패.
5. **row buffer hit rate — 로컬 자료에서는 확인 실패, 웹에서 부분 확보.** 로컬 3개 주 자료(jacob_refresh,
   mukundan, rtc_refresh)와 raidr 모두 **정책(open-page)과 그 정성적 효과는 서술하나 "hit rate = XX%"
   수치는 제시하지 않음.** 웹 보조로 Ghose et al.(arXiv:1902.07609)의 값을 확보했으나(§1-G),
   **시뮬레이터·코어 수·페이지 정책 등 세부 조건은 미확보**입니다.
   → **"일반적으로 row buffer hit rate는 몇 %"라는 일반화 문장을 쓰지 마십시오.** §1-G가 보여주듯
   같은 응용도 스레드 수 하나로 83.1% → 7.2%까지 움직입니다.

5-b. **Intel "Performance Differences for Open-Page / Close-Page Policy" (문서번호 826015, T1)** 를
   검색으로 발견했으나 **PDF 텍스트 추출 실패로 내용 확인 실패.**
   URL: https://cdrdv2-public.intel.com/826015/826015_Perf_Diff_Open_Pg_Rev0-9.pdf
   → open-page/close-page의 **제조사(T1) 정량 비교가 필요하면 이 문서를 우선 확보하십시오.**
6. **실제 시스템의 버스 이용률(bus utilization) 실측 %.** Mukundan et al.은 버스 이용률을 성능 프록시로
   "측정한다"고 하나(mukundan.txt L505-520), **절대 % 수치는 그래프에만 있고 텍스트에 없음.**
7. **micron_ddr5.txt Figure 5(DDR5 vs DDR4 성능 향상 배수)의 구체 수치.** 이미지 내부라 추출 실패.
8. **DDR5 서브채널 2개가 "독립 CA 버스를 갖는다"는 JEDEC 원문 문장.** jesd79_5.txt에서 "sub-channel"/
   "subchannel" 문자열 **0건**(검색 확인) — 서브채널은 **디바이스 스펙(79-5)이 아니라 모듈 스펙(DIMM)
   차원의 개념**이기 때문. 마이크론 백서(T1)의 Figure 2 제목으로만 확인됨.
9. **DDR5 tWR 규정값.** 표 추출이 "45"로 나왔으나 열 정렬 불확실 → 인용 금지.

---

## 5. 기존 소스 팩(v3/v4)과의 충돌

**직접적 충돌 없음.** 겹치는 항목과 관계는 다음과 같습니다.

- v3 L180 "DDR5 버스 폭 64-bit (32-bit 서브채널 2개) T0" — 본 조사와 **일치**. 본 문서는 여기에
  "서브채널은 40핀이며 BL16 도입이 그 전제였다"(micron_ddr5.txt, T1)는 **인과 설명을 추가**합니다.
- v4 L816-817 "DDR5 RDIMM x80 = 40비트 서브채널 2개, 40 = 데이터 32 + ECC 8은 **산술 유도**" —
  본 조사에서도 "32 data + 8 ECC" 명시 문자열은 **여전히 미확인**. v4의 단서를 유지하십시오.
- v3 L308 "랜덤 소량 접근 시 명목 대역폭이 아무리 높아도 실효 대역폭이 급락" — NAND 맥락의 서술.
  본 문서 §2-B(tCCD_L / tCCD_L_WR로 인한 버스 채움률 저하)는 **DRAM 쪽의 같은 취지 근거**로 보완재입니다.

---

## 6. 집필 시 주의 (서술 규칙 제안)

1. **"대역폭 = 1/지연"이 아닌 이유를 설명할 때, "그러니 지연은 대역폭과 무관하다"로 넘어가지 마십시오.**
   정확한 문장은 "**뱅크 수가 충분하고 접근이 흩어지면 버스가 병목이 되어 tRC가 감춰지지만, 접근이
   소수 뱅크에 몰리면 tRC가 다시 대역폭 상한이 된다**"입니다. RAIDR 원문도 bank-level parallelism이
   "공유 채널 대역폭과 디바이스 전력에 의해 제약된다"고 못 박습니다.

2. **tCCD/tRRD/tWTR을 인용할 때 반드시 `_L`/`_S`를 붙이고 세대·속도등급을 특정하십시오.**
   예: "DDR5-3200 tCCD_L = max(8nCK, 5ns)" (○) / "DDR5 tCCD는 5ns" (×).

3. **§2-B의 버스 채움률 백분율(100%/67%/50%/25%)은 전부 산술 유도값입니다.**
   본문에 쓸 때는 "스펙 값으로부터 계산하면"이라고 밝히십시오. 특히 **DDR5-4800/6400의 tCCD_L을
   5ns로 가정한 계산은 로컬 자료로 검증되지 않았습니다**(초안은 4000까지). 쓰려면 비준본 확인 필요.

4. **tRTRS를 JEDEC 파라미터처럼 쓰지 마십시오.** JEDEC 문서·마이크론 데이터시트에 없습니다.
   시뮬레이터 파라미터로만 존재하며 확인된 유일한 값은 "DDR4-1600 시뮬레이션 설정에서 2 DRAM cycles"입니다.

5. **"tRTW"라는 파라미터는 없습니다.** WRITE→READ는 tWTR로 규정되지만 READ→WRITE는 컨트롤러가
   CL/CWL로 계산합니다. "tWTR, tRTW" 식으로 나란히 쓰면 스펙에 대한 오해를 심습니다.

6. **row buffer hit rate는 "대표값"이 존재하지 않습니다.** §1-G의 확보 값을 쓸 때는 반드시 워크로드와
   조건을 함께 쓰십시오. 특히 **quicksilver가 1스레드 83.1% → 32스레드 7.2%로 무너지는 사례**는
   "hit rate는 응용의 성질이 아니라 응용×동시성×주소매핑의 함수"라는 논지에 가장 좋은 근거입니다.
   반대로 "DRAM의 row buffer hit rate는 보통 XX%" 같은 일반화 문장은 어떤 출처로도 뒷받침되지 않습니다.
   또한 §1-G 값은 **DDR3/DDR4 시뮬레이션**이며 DDR5 값이 아닙니다.

7. **refresh 성능 손실 11.4% / 30%를 인용할 때 반드시 조건을 붙이십시오.**
   - 11.4%: **8Gb DDR4, 4코어 시뮬레이션, HIGH bandwidth 워크로드(libquantum/mcf/mix2)**
   - 30%+: **32Gb 디바이스 가정, 2015년 당시 외삽 tRFC 사용** — 실제 32Gb DDR5의 tRFC는 로컬 초안에서
     **TBD**입니다. "32Gb에서 30% 손실"을 현재 제품 이야기처럼 쓰면 오도입니다.

8. **마이크론의 REFsb 수치(6–9%, 11.2ns→5.0ns)는 시뮬레이션·대기행렬 모델값이며 제조사 자체 발표입니다.**
   "실측"으로 쓰지 마십시오. 11.2/5.0ns는 특히 "**랜덤 트래픽 단일 뱅크**"라는 강한 단순화 위에서 나온 값입니다.

9. **JESD79-5 로컬본은 "Proposed DDR5 Full spec (79-5)" 회람 초안 Rev0.1입니다.** 인용 시
   "DDR5 규격 초안(Rev0.1)" 또는 "비준 전 회람본"이라고 명시하고, 32Gb TBD 항목은 인용하지 마십시오.

10. **FR-FCFS는 개념 수준까지만.** 정확한 개념 서술 = "①준비된(row hit) 요청 우선, ②그다음 오래된 요청 우선.
    목적함수는 데이터 버스 throughput 최대화이며 공정성은 목적함수에 없다." 여기서 더 들어가지 마십시오.

11. **뱅크그룹은 "뱅크를 더 넣기 위한 것"이 아니라 "속도가 오를 때 ns 고정 제약이 tCK 대비 길어지는 것을
    우회하기 위한 것"입니다.** 마이크론 백서가 이 인과를 명시합니다. 순서를 뒤집지 마십시오.

12. **DDR5 서브채널을 JEDEC 79-5(디바이스 스펙)의 개념으로 서술하지 마십시오.** 디바이스 스펙에는
    "sub-channel"이라는 단어가 나오지 않습니다. 서브채널은 **모듈(DIMM) 레벨** 구조입니다.

---

## 7. 출처 목록

| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| jesd79_5.txt (로컬) | T0 (**비준 전 초안**) | Proposed DDR5 Full Spec (JESD79-5) Draft Rev0.1 회람본 — §4.10.3 Same Bank Refresh, Table 26, §12.2.1 Timing Parameters (DDR5-3200–4000) | 2026-07-29 |
| jesd79_4.txt (로컬) | T0 | JESD79-4 DDR4 SDRAM (2012-09 원판) — tRTRS 문자열 부재 확인용 | 2026-07-29 |
| micron_ddr4_16gb.txt (로컬) | T1 | Micron 16Gb: x4/x8/x16 DDR4 SDRAM, Rev. H 8/2021 — Table 70(BG 타이밍), Table 160/161(AC 타이밍), 스피드빈 | 2026-07-29 |
| micron16gb_ddr5.txt (로컬) | T1 | Micron 16Gb DDR5 SDRAM Die Rev D (2024-04) — Table 1: 16Gb Addressing (뱅크/BG 구성) | 2026-07-29 |
| micron_ddr5.txt = micron_ddr5_wp.txt (로컬) | T1 | Micron DDR5 White Paper — Overall Bank Increase / Data Burst Length Increase / Same-Bank Refresh / Performance Improvement | 2026-07-29 |
| micron_32gb_rdimm.txt (로컬) | T1 | Micron 32GB x80 ECC DR RDIMM — 랭크·뱅크 구성 | 2026-07-29 |
| jacob_refresh.txt (로컬) | T2 | Bhati, Chang, Chishti, Lu, Jacob, "DRAM Refresh Mechanisms, Penalties, and Trade-Offs", IEEE Transactions on Computers vol.64 (2015) | 2026-07-29 |
| mukundan.txt (로컬) | T2 | Mukundan et al., "Understanding and Mitigating Refresh Overheads in High-Density DDR4 DRAM Systems", ISCA 2013 | 2026-07-29 |
| raidr.txt (로컬) | T2 | Liu, Jaiyen, Veras, Mutlu, "RAIDR: Retention-Aware Intelligent DRAM Refresh", ISCA 2012 | 2026-07-29 |
| rtc_refresh.txt (로컬) | T2 | (refresh 관련 논문) — bank-level parallelism 언급 확인 | 2026-07-29 |
| https://ar5iv.labs.arxiv.org/html/1902.07609 | T2 | Ghose, Li, Hajinazar, Senol Cali, Mutlu, "Understanding the Interactions of Workloads and DRAM Types: A Comprehensive Experimental Study", arXiv:1902.07609 — row buffer hit rate 및 BPU 수치 (§1-G) | 2026-07-29 |
| https://cdrdv2-public.intel.com/826015/826015_Perf_Diff_Open_Pg_Rev0-9.pdf | T1 | Intel, "Performance Differences for Open-Page / Close-Page Policy" (826015, Rev 0.9) — **PDF 텍스트 추출 실패, 미확인. 후속 확보 대상** | 2026-07-29 (열람 실패) |
| RAM-source-pack.md / -v4-addendum.md | — | 기존 소스 팩(중복 회피용 대조) | 2026-07-29 |

---

## 8. 집필자가 바로 쓸 수 있는 "한 줄 근거" 모음

- 뱅크 병렬성의 한계: "bank-level parallelism은 **공유 채널 대역폭**과 **디바이스 전력** 두 가지에 의해 제약된다" — RAIDR, ISCA 2012 (T2)
- 뱅크그룹의 존재 이유: "뱅크그룹 증가는 **짧은 타이밍이 쓰일 확률을 높여** 내부 타이밍 제약을 완화한다" — Micron DDR5 백서 (T1)
- 뱅크그룹 페널티 배율: "tCCD_L은 tCCD_S의 **거의 2배**가 될 수 있다" — Micron DDR5 백서 (T1)
- 스케줄러의 목적함수: "FR-FCFS는 메모리 throughput을 최대화하지만 **시스템 성능을 최대화하지는 않는다**" — RAIDR (T2)
- refresh의 3중 손실: 뱅크 병렬성 손실 + 지연 증가 + **열린 행 강제 닫힘에 의한 row hit rate 하락** — RAIDR (T2)
- REFsb의 요점: "대상 뱅크는 tRFCsb 동안 접근 불가이나, **각 뱅크그룹의 나머지 뱅크는 그동안에도 주소 지정 가능**" — JESD79-5 초안 §4.10.3 (T0 초안)
- BL16의 파급: "기본 버스트 길이 증가가 **DDR5 DIMM의 dual sub-channel 아키텍처를 가능하게 했다**" — Micron DDR5 백서 (T1)
