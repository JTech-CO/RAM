# DRAM 타이밍 파라미터와 지연 분해
> 조사일: 2026-07-29 / 상태: **완료** (DDR3 구간은 확인 실패 — 4절 참조)

---

## 1. 확인된 사실

### 1-A. DDR4-3200 speed bin — Micron 16Gb DDR4 (T1)

출처: `micron_ddr4_16gb.txt` L36172-36265 (Table 158: DDR4-3200 Speed Bins and Operating Conditions)
문서: `16gb_ddr4_dram.pdf` Rev. H, 2021-08 / 등급 **T1** / 확인일 2026-07-29
tCK(AVG) = **0.625 ns** (출처 L32862)

| 파라미터 | 정의 (데이터시트 원문 표현) | -062Y (22-22-22) | -062E (22-22-22) | -062 (24-24-24) | 단위 |
|---|---|---|---|---|---|
| tAA | "Internal READ command to first data" | **13.75** (13.32)⁴ | **13.75** | **15.00** | ns |
| tAA (MAX) | | 19.006 | 19.006 | 19.006 | ns |
| tAA_DBI | read DBI 사용 시 | tAA(MIN)+4nCK | 〃 | 〃 | ns |
| tRCD | "ACTIVATE-to-internal READ or WRITE delay time" | **13.75** (13.32)⁴ | **13.75** | **15.00** | ns |
| tRP | "PRECHARGE command period" | **13.75** (13.32)⁴ | **13.75** | **15.00** | ns |
| tRAS | "ACTIVATE-to-PRECHARGE command period" | **32** (max 9×tREFI) | **32** | **32** | ns |
| tRC | "ACTIVATE-to-ACTIVATE or REFRESH command period" | **tRAS+tRP** | tRAS+tRP | tRAS+tRP | ns |

- **Note 4** (L36281): "(13.32)"는 **non-native tCK-CL-nRCD-nRP 조합**에 적용되는 값.
- **Note 5** (L36282): "When calculating tRC in clocks, values may not be used in a combination that violate tRAS or tRP."
- **Note 6** (L36283-36284): tAA(MAX) 19.006 ns는 "exceeds the JEDEC requirement in order to allow additional flexibility" — 즉 Micron 자체 확장. **JEDEC SPD 준수 모듈은 JEDEC 정의값만 지원할 수 있음.**
- 계산: tRC(-062E) = 32 + 13.75 = **45.75 ns**, tRC(-062) = 32 + 15.00 = **47.00 ns**.
- **주의**: 표에 tRC는 숫자가 아니라 수식(tRAS+tRP)으로만 적혀 있습니다. 45.75/47.00은 본 조사의 **계산값**.

### 1-B. DDR4-1600 speed bin — 같은 문서 (세대 내 비교용, T1)

출처: `micron_ddr4_16gb.txt` L34648-34720 (Table 152) / tCK = 1.25 ns

| 파라미터 | -125E (11-11-11) | -125 (12-12-12) | 단위 |
|---|---|---|---|
| tAA | **13.75** (13.50)⁴ / max 19.006 | **15.00** / max 19.006 | ns |
| tRCD | **13.75** (13.50)⁴ | **15.00** | ns |
| tRP | **13.75** (13.50)⁴ | **15.00** | ns |
| tRAS | **35** (max 9×tREFI) | **35** | ns |
| tRC | tRAS+tRP (= 48.75 계산값) | tRAS+tRP (= 50.00 계산값) | ns |

**→ 같은 다이(Micron 16Gb DDR4)에서 데이터율이 1600→3200 MT/s로 2배가 되는 동안 tRCD·tRP는 13.75 ns로 완전히 동일하고, tRAS는 35→32 ns로 8.6%만 줄었습니다.** 이것이 "ns로는 거의 안 줄었다"의 1차 자료 증거입니다.

### 1-C. DDR4 기타 코어 타이밍 (전 speed bin 공통, T1)

출처: `micron_ddr4_16gb.txt` (Table 159/160 계열 Electrical Characteristics and AC Timing Parameters)

| 파라미터 | 값 | 출처 위치 |
|---|---|---|
| tWR (WRITE recovery time, 1tCK preamble) | **MIN = 15 ns** (모든 speed bin 공통) | L39523-39527 |
| tWR2ck | MIN = 1CK + tWR1ck | L39528-39530 |
| tRTP (READ-to-PRECHARGE time) | **MIN = greater of 4CK or 7.5 ns** | L39624-39628 |
| tCCD_S (다른 bank group 간 CAS-to-CAS) | 4 CK | L39631-39638 |
| tCCD_L (같은 bank group 내 CAS-to-CAS) | MIN = greater of 4CK or **5 ns** | L39641-39657 |
| tRRD_S (다른 bank group ACT-to-ACT, 1/2KB page) | greater of 4CK or 5.0 / 4.2 / 3.7 / **3.3 ns** (1600/1866/2133/2400 순) | L37388-37398 |
| tDAL (auto-precharge write recovery + precharge) | MIN = WR + ROUND(tRP/tCK(AVG)) | L39659-39664 |

- tRCD / tRP / tRAS / tRC는 AC timing 표에 숫자가 없고 **"See Speed Bin Tables"**로만 표기됩니다 (L37367-37384). 즉 이 넷은 speed bin에 종속, 나머지는 bin 무관.

### 1-D. DDR5 speed bin — Micron 16Gb DDR5 Die Rev D (T1)

출처: `micron16gb_ddr5.txt` L114-244 (Table 2: Part Numbers and Timing Parameters), L289-297
문서: `16gb_ddr5_sdram_dierevD.pdf` Rev. F, 2024-04 / 등급 **T1** / 확인일 2026-07-29

| 데이터율 | tCK | CL-nRCD-nRP (clock) | tAA (ns) | tRCD (ns) | tRP (ns) | 제품 상태 |
|---|---|---|---|---|---|---|
| 5600 MT/s (-56B) | 0.357 ns | **46-45-45** | **16.000** | **16.000** | **16.000** | Production |
| 6400 MT/s (-64B) | 0.312 ns | **52-52-52** | **16.000** | **16.000** | **16.000** | Production |
| 7200 MT/s (-72B) | 0.277 ns | **58-58-58** | **16.000** | **16.000** | **16.000** | Advance |

- Micron 정의(L245-250): **Advance = "initial descriptions of products still under development"** → 7200 MT/s 행은 확정 사양 아님. **Production만 인용 권장.**
- 이 표에는 tRAS·tRC·tWR·tRTP가 없습니다(요약 표). 해당 값은 1-E/1-F 참조.

### 1-E. DDR5-4800B — Samsung DDR5 UDIMM (T1) ★ 가장 완결된 DDR5 한 줄

출처: `samsung_ddr5_udimm.txt` L134-156 (모듈 요약표), L5549-5590 (DDR5-4800 Speed Bins and Operations)
문서: Samsung DDR5 UDIMM datasheet Rev. 1.0, **2021-03** / 등급 **T1** / 확인일 2026-07-29

| 파라미터 | 값 | 단위 |
|---|---|---|
| 데이터율 / grade | DDR5-4800B (-EB) | |
| tCK | **0.416** | ns |
| CAS Latency (tCK) | **40** | CK |
| CL-nRCD-nRP | **40-39-39** | CK |
| tAA (Internal read command to first data) | **16.000** | ns |
| tRCD (ACT to internal read or write delay time) | **16.000** | ns |
| tRP (Row Precharge Time) | **16.000** | ns |
| tRAS (ACT to PRE command period) | **32.00** (max 5×tREFI) | ns |
| tRC (ACT to ACT or REF command period) | **48.000** | ns |
| CWL (CAS Write Latency) | **CL−2 = 38** | CK |

- **tRC = 48.000 = tRAS(32) + tRP(16)** — 표에 명시된 숫자로 tRC = tRAS + tRP 관계가 직접 검증됩니다.
- 같은 문서의 frequency down-bin 표(L5601-5654)에는 DDR5-3200C tAAmin/tRCDmin/tRPmin **17.500 ns** (CL=28, CWL=26), 3200B **16.250**, 3200A **15.000**, 3600C **17.777**, 3600B **16.666**, 3600A **14.444** 등이 있습니다. → **같은 세대 안에서도 등급에 따라 14.4~17.8 ns로 흩어집니다.**
- tRAS max가 DDR4의 `9 × tREFI`와 달리 **`5 × tREFI`**로 적혀 있습니다(L5577-5578). → 3절 참조.

### 1-F. DDR5 speed bin — JESD79-5 **초안 Rev0.1** (T0, 단 미비준)

출처: `jesd79_5.txt` L22177-22242 (Table 109 — DDR5-6400 Speed Bins and Operations, **"No Ballot"** 표기)
등급 **T0(단, 위원회 초안)** / 확인일 2026-07-29

| 파라미터 | DDR5-6400A | DDR5-6400B | DDR5-6400C | 단위 |
|---|---|---|---|---|
| tAA | **15.00** | **16.50** | **18.00** | ns |
| tRCD | **15.00** | **16.50** | **18.00** | ns |
| tRP | **15.00** | **16.50** | **18.00** | ns |
| tRAS | (min 값이 텍스트 추출에서 누락, max = 9×tREFI) | 〃 | 〃 | ns |
| tRC | **47.00** (한 값만 추출됨) | (추출 실패) | (추출 실패) | ns |
| CWL | CWL = CL−2 | 〃 | 〃 | |
| 지원 CL/CWL | **TBD** | TBD | TBD | nCK |

- **초안 한계 (반드시 명시할 것)**:
  1. 표 제목에 **"No Ballot"** — 즉 DDR5-6400 bin은 이 초안 시점에 투표 전.
  2. CL/CWL 값이 전부 **TBD**.
  3. tRAS min 숫자가 추출본에 없음. 다만 tRC 47.00 = 32 + 15.00이므로 **A 등급 tRAS min = 32 ns로 역산**됨(본 조사의 산술 추론, 원문 확인 아님).
  4. 이 초안의 표준 bin 목록은 3200/3600/4000/4400/5200/5600/6000/6400 + 미래 placeholder(6800~8400)이며 **DDR5-4800이 없습니다**(L418-431). DDR5-4800은 이후 개정에서 추가된 bin — 초안을 4800의 근거로 쓰면 안 됩니다.
- 초안 부속 표: `jesd79_5.txt` L23087-23105
  - **tRTP = 7.5 ns** (min, 열 3개 모두 동일)
  - **tWR = 45 ns** (min, 열 3개 모두 동일)
- MR6 정의 (L2416-2452): "tWR is currently defined as **45ns** across all bins" — nCK 인코딩은 전부 **TBD**. → 4절/3절 참조.

### 1-G. 지연 분해 (본 조사의 핵심) — 계산값

**계산 규칙**: 아래는 위 1차 자료의 min 값을 그대로 더한 것입니다. DRAM 디바이스 내부(핀에서 핀까지)만 포함하며, CPU가 체감하는 메모리 지연은 아닙니다(2절 참조).

| 시나리오 | 식 | DDR4-1600 -125E (11-11-11) | DDR4-3200 -062E (22-22-22) | DDR4-3200 -062 (24-24-24) | DDR5-4800B (40-39-39) | DDR5-6400 Micron (52-52-52) | DDR5-6400A JEDEC 초안 | DDR5-6400C JEDEC 초안 |
|---|---|---|---|---|---|---|---|---|
| **row hit** (해당 행이 이미 열려 있음) | CL(tAA) | **13.75 ns** | **13.75 ns** | **15.00 ns** | **16.00 ns** | **16.00 ns** | **15.00 ns** | **18.00 ns** |
| **row miss / empty** (뱅크는 닫혀 있음) | tRCD + CL | **27.50 ns** | **27.50 ns** | **30.00 ns** | **32.00 ns** | **32.00 ns** | **30.00 ns** | **36.00 ns** |
| **row conflict** (다른 행이 열려 있음) | tRP + tRCD + CL | **41.25 ns** | **41.25 ns** | **45.00 ns** | **48.00 ns** | **48.00 ns** | **45.00 ns** | **54.00 ns**|

- 클럭 수로 본 같은 값 (row conflict 기준): DDR4-1600 = 11+11+11 = **33 CK**, DDR4-3200 = 22+22+22 = **66 CK**, DDR5-4800B = 39+39+40 = **118 CK**, DDR5-6400 Micron = 52+52+52 = **156 CK**.
- **클럭 수는 33 → 156으로 4.7배가 되었는데 ns는 41.25 → 48.00으로 16% 늘었습니다(줄어든 게 아니라 늘었습니다).**

**버스트 전송 시간(첫 데이터 이후 나머지)** — 위 값에 더해지는 부분:
- DDR4 BL8 @ 3200 MT/s: 8 transfer ÷ 2 per tCK = 4 tCK × 0.625 = **2.5 ns**
- DDR5 BL16 @ 4800 MT/s: 16 ÷ 2 = 8 tCK × 0.4167 = **3.33 ns**
- (본 조사의 계산값. BL은 DDR4=8, DDR5=16이 기본.)

---

## 2. 구조·메커니즘 서술

### 2-1. 각 파라미터가 물리적으로 무엇을 기다리는가

DDR 계열의 접근은 항상 **ACT → RD/WR → PRE**의 3단 상태 기계입니다. 파라미터는 각 단계 사이의 최소 대기시간입니다.

- **tRCD (ACTIVATE-to-internal READ or WRITE delay time)** — ACT로 워드라인을 올린 뒤, 셀 커패시터가 비트라인을 흔들고(charge sharing) 감지증폭기가 그 미세 전압차를 full-rail로 증폭해 **행 전체가 감지증폭기 래치에 실릴 때까지**의 시간. 이 구간이 끝나야 열 주소로 그 행의 일부를 고를 수 있습니다. 이것이 "행을 연다"의 실체입니다.
- **CL / tAA (Internal READ command to first data)** — RD 명령이 들어온 뒤 감지증폭기 래치에서 열을 선택하고, 글로벌 데이터라인 → I/O 게이팅 → 출력 드라이버를 거쳐 **첫 비트가 DQ 핀에 나오기까지**의 시간. 데이터시트 표현이 "Internal READ command to first data"라는 점이 중요합니다 — AL(additive latency)이 있으면 외부에서 본 RL = AL + CL입니다.
- **tRP (PRECHARGE command period)** — PRE로 워드라인을 내리고 비트라인을 다시 VDD/2 기준으로 **되돌려 평형화(equalize)** 하는 시간. 끝나야 그 뱅크에 다음 ACT를 넣을 수 있습니다. 데이터시트: "After a bank is precharged, it is in the idle state and must be activated prior to any READ or WRITE commands" (`micron_ddr4_16gb.txt` L12158-12159).
- **tRAS (ACTIVATE-to-PRECHARGE command period)** — **ACT 후 최소 이만큼은 행을 열어 둬야 한다**는 하한. 이유는 restore입니다. DRAM 읽기는 파괴적입니다: charge sharing으로 셀 전하가 비트라인에 흩어지므로, 감지증폭기가 증폭한 full-rail 전압을 **다시 셀 커패시터에 써 넣어(restore)** 원래 전하를 복원해야 합니다. restore는 감지 자체보다 오래 걸리며, **restore가 끝나기 전에 precharge하면 그 행의 데이터가 손상됩니다.** 그래서 tRAS는 "기다려도 되는 시간"이 아니라 **데이터 무결성 조건**입니다. → v3 02장의 restore 서술과 정확히 같은 물리입니다.
  - 데이터시트의 간접 증거: auto-precharge는 "RAS lockout circuit을 사용해 **ARRAY RESTORE operation이 완료될 때까지** PRECHARGE를 내부적으로 지연시킨다"(`micron_ddr4_16gb.txt` L12162-12167). 즉 **precharge는 array restore 완료 이후여야 한다**는 것이 명시되어 있습니다.
  - 검증 절차에도 등장: "Wait for tRAS (MIN) before closing all the open pages" (L9179).
- **tRC (ACTIVATE-to-ACTIVATE or REFRESH command period)** — 같은 뱅크의 ACT→ACT 최소 주기. **tRC = tRAS + tRP**. Micron DDR4 표는 아예 수식으로 적어 두었고(L36255-36264), Samsung DDR5-4800B 표는 48.000 = 32.00 + 16.00으로 숫자가 맞습니다. 이것이 **한 뱅크의 최대 행 회전율**을 정의합니다: DDR5-4800B에서 한 뱅크는 48 ns에 한 행씩만 열 수 있습니다.
- **tWR (WRITE recovery time)** — 쓰기 데이터가 DQ 핀에 다 들어온 뒤, 그 데이터가 감지증폭기를 거쳐 **셀 어레이에 실제로 기록될 때까지** 필요한 시간. 이게 끝나야 precharge 가능. Micron DDR4: "The PRECHARGE operation will not begin until after the last data of the burst write sequence is properly stored in the memory array" (L12166-12167).
- **tRTP (READ-to-PRECHARGE)** — 읽기 버스트가 어레이에서 다 빠져나온 뒤 precharge까지의 최소 간격. DDR4 = max(4CK, 7.5 ns).
- **tDAL = WR + ROUND(tRP/tCK)** — auto-precharge를 건 쓰기의 총 회복시간. tWR과 tRP가 **직렬로** 붙는다는 점이 이 식에 그대로 드러납니다.

### 2-2. Speed bin 표기 "40-40-40" / "22-22-22"의 의미

데이터시트 표 헤더가 **`CL-nRCD-nRP`** 입니다(`micron_ddr4_16gb.txt` L36179, `samsung_ddr5_udimm.txt` L147). 즉 세 숫자는

1. **CL** — RD → 첫 데이터 (클럭 수)
2. **nRCD** — ACT → RD/WR (클럭 수)
3. **nRP** — PRE → ACT (클럭 수)

이며 **단위는 ns가 아니라 클럭 사이클(nCK)** 입니다. 접두 `n`이 붙은 것은 "number of clocks"라는 뜻입니다. 따라서 같은 "22-22-22"라도 tCK가 다르면 실제 시간이 다릅니다 — 그래서 speed bin 이름(DDR4-3200 등)과 반드시 함께 읽어야 합니다.

세 값이 항상 같지는 않습니다. Micron DDR5 5600 MT/s는 **46-45-45**로 CL만 1 큽니다(`micron16gb_ddr5.txt` L132), Samsung DDR5-4800B는 **40-39-39**입니다. tRCD·tRP는 16.000 ns를 0.416 ns로 나눠 38.4 → 39로 올림, tAA는 같은 16.000 ns인데 **CL은 40**입니다. 즉 **같은 ns 사양에서도 CL은 반올림·짝수 제약·CWL=CL−2 제약 때문에 한두 클럭 더 붙을 수 있습니다.** ns → nCK 변환은 항상 **올림(round to next integer)** 입니다(`micron_ddr4_16gb.txt` L3594-3596, L3600-3602).

Micron DDR4 3200 bin의 실제 상품 코드는 **-062Y / -062E / -062**이고 각각 22-22-22 / 22-22-22 / 24-24-24입니다. **동일한 클럭 표기라도 tAA min ns가 다를 수 있습니다**(-062Y는 non-native 조합에서 13.32 ns 적용). 즉 "22-22-22"만으로는 부품이 특정되지 않습니다.

### 2-3. CL이 클럭 수로는 커지는데 ns로는 비슷한 이유

CL[ns] = CL[nCK] × tCK 입니다. 그런데 CL[ns]를 결정하는 것은 **감지증폭기 래치 → 열 선택 → 글로벌 IO → 출력 드라이버**라는 아날로그 경로이고, 이 경로는 DRAM 공정(캐패시터·비트라인·감지증폭기)이 미세화되어도 거의 빨라지지 않습니다. 비트라인은 길고 용량성이며, 셀 커패시터는 미세화에도 불구하고 최소 전하량(~수십 aF급 커패시턴스)을 유지해야 해서 감지 시간이 줄지 않습니다.

반면 tCK는 인터페이스(PHY/DLL/링크)의 개선으로 계속 줄어듭니다. DDR4-1600 1.250 ns → DDR4-3200 0.625 ns → DDR5-4800 0.416 ns → DDR5-6400 0.312 ns.

**분자는 고정, 분모는 절반씩** → CL[nCK]가 커질 수밖에 없습니다. 실제 자료로:

| | tCK (ns) | tAA (ns) | CL (nCK) |
|---|---|---|---|
| DDR4-1600 -125E | 1.250 | 13.75 | 11 |
| DDR4-3200 -062E | 0.625 | 13.75 | 22 |
| DDR5-4800B | 0.416 | 16.000 | 40 |
| DDR5-6400 (Micron) | 0.312 | 16.000 | 52 |
| DDR5-7200 (Micron, Advance) | 0.277 | 16.000 | 58 |

**tAA[ns]는 13.75 → 16.00으로 거의 그대로인데 CL[nCK]는 11 → 52로 4.7배가 되었습니다.** 이것이 "CL 숫자가 커졌다 = 메모리가 느려졌다"는 통념이 틀린 이유이자, 동시에 "그런데 실제로 빨라지지도 않았다"는 사실을 같은 표로 보여주는 대목입니다.

### 2-4. "타이밍은 ns로는 거의 안 줄었다" — 1차 자료 종합

| 세대·bin | 출처 | tCK (ns) | tRCD (ns) | tRP (ns) | tRAS (ns) | tRC (ns) |
|---|---|---|---|---|---|---|
| DDR4-1600 -125E | Micron 16Gb DDR4 (T1) | 1.250 | 13.75 | 13.75 | 35 | 48.75 (계산) |
| DDR4-1600 -125 | 〃 | 1.250 | 15.00 | 15.00 | 35 | 50.00 (계산) |
| DDR4-3200 -062E | 〃 | 0.625 | 13.75 | 13.75 | 32 | 45.75 (계산) |
| DDR4-3200 -062 | 〃 | 0.625 | 15.00 | 15.00 | 32 | 47.00 (계산) |
| DDR5-4800B | Samsung DDR5 UDIMM (T1) | 0.416 | 16.000 | 16.000 | 32.00 | **48.000 (표 명시)** |
| DDR5-5600 | Micron 16Gb DDR5 (T1) | 0.357 | 16.000 | 16.000 | (표에 없음) | (표에 없음) |
| DDR5-6400 | Micron 16Gb DDR5 (T1) | 0.312 | 16.000 | 16.000 | (표에 없음) | (표에 없음) |
| DDR5-6400A | JESD79-5 **초안** (T0-draft) | 0.312 | 15.00 | 15.00 | (추출 실패) | 47.00 |
| DDR5-6400C | JESD79-5 **초안** (T0-draft) | 0.312 | 18.00 | 18.00 | (추출 실패) | (추출 실패) |

**요약할 수 있는 것**: 데이터율이 1600 → 6400 MT/s로 **4배**가 되는 동안 tRCD·tRP는 **13.75 → 15~18 ns**, tRAS는 **35 → 32 ns**, tRC는 **48.75 → 47~48 ns**입니다. 즉 **코어 타이밍의 절대 시간은 4배 구간에서 사실상 변하지 않았고, 일부는 오히려 늘었습니다.** 대역폭만 4배가 되고 지연은 그대로인 것이 DDR 진화의 형태입니다.

**단, DDR3를 로컬 1차 자료로 확인하지 못했습니다**(4절). 위 표는 **DDR4 → DDR5 구간만** 1차 자료로 뒷받침됩니다. 집필 시 "DDR3→DDR4→DDR5"로 3세대를 걸치려면 DDR3 데이터시트 확보가 추가로 필요합니다.

### 2-5. 지연 분해를 서술로 옮기면

DDR5-4800B(Samsung, 1-E) 기준으로:

- **row hit** — 컨트롤러가 이미 그 뱅크에 그 행을 열어 두었다. RD만 보내면 된다. **16 ns**. 클럭으로는 40 CK.
- **row miss (뱅크가 닫혀 있음)** — ACT부터 해야 한다. tRCD(16) + CL(16) = **32 ns**.
- **row conflict (같은 뱅크에 다른 행이 열려 있음)** — 먼저 닫아야 한다. tRP(16) + tRCD(16) + CL(16) = **48 ns**.

**즉 "행 정책(row buffer policy)"이 같은 하드웨어에서 3배(16→48 ns)의 차이를 만듭니다.** open-page 정책은 hit를 노리고 행을 열어두고, close-page 정책은 conflict를 피하려 매번 auto-precharge를 겁니다. 접근 패턴이 순차적이면 open-page가, 무작위이면 close-page가 유리합니다.

여기에 더해 실제로 관측되는 지연은 다음이 **추가로** 쌓입니다(이번 조사 범위 밖이지만 서술 시 반드시 언급):
- 버스트 전송 시간 (DDR5 BL16 @4800 = 3.33 ns)
- 같은 뱅크그룹 연속 접근 시 tCCD_L (DDR4 = max(4CK, 5 ns))
- tRRD / tFAW 로 인한 ACT 발행 제약
- refresh 블로킹 (tRFC — v4 addendum 참조)
- **칩 밖**: CPU 캐시 미스 판정, 온칩 인터커넥트, 메모리 컨트롤러 큐잉/스케줄링, PHY, (RDIMM이면) RCD 버퍼 지연

---

## 3. 상충·불확실

| 쟁점 | 값 A | 값 B | 판단 |
|---|---|---|---|
| DDR5 tWR | **45 ns** — JESD79-5 초안 Rev0.1, L23098-23105 및 MR6 노트 L2419 "currently defined as 45ns across all bins" | (DDR4는 15 ns — `micron_ddr4_16gb.txt` L39525) | **초안값 45 ns를 그대로 쓰지 마십시오.** 초안 MR6의 nCK 인코딩이 전부 TBD이고 "currently"라는 표현이 붙어 있습니다. 비준본 JESD79-5x에서 값이 바뀌었을 가능성이 큽니다. **비준본 미확인 → 4절.** |
| DDR5 tRAS max | Samsung DDR5-4800B: **5 × tREFI** (L5577-5578) | JESD79-5 초안 DDR5-6400: **9 × tREFI** (L22217-22219). DDR4도 9 × tREFI | **양쪽 기록.** 제조사 문서와 JEDEC 초안이 다릅니다. tRAS **min**(32 ns)은 양쪽 일치하므로 지연 분해에는 영향 없음. max는 "행을 얼마나 오래 열어둬도 되는가"의 상한이라 본 주제에는 부차적. |
| DDR5-6400 tRCD/tRP | JEDEC 초안 A/B/C = **15.00 / 16.50 / 18.00 ns** | Micron 16Gb DDR5 -64B = **16.000 ns**, 52-52-52 | **모순 아님.** Micron 제품은 A와 B 사이(16.000 ns)에 해당하는 자체 bin. 다만 **"DDR5-6400의 tRCD는 X"라고 단정하지 말고 반드시 등급/부품을 붙이십시오.** |
| DDR4-3200 tAA min | 13.75 ns (-062Y, -062E) | 15.00 ns (-062) / 13.32 ns (-062Y non-native 조합) | **셋 다 유효.** 같은 DDR4-3200 안에 세 값이 공존합니다. 단일 대표값을 쓰지 마십시오. |
| tRC 숫자 | Samsung DDR5-4800B: **48.000 ns 명시** | Micron DDR4: 숫자 없이 **"tRAS + tRP"** 수식만 | 계산값(45.75 / 47.00 ns)은 **본 조사의 산술**임을 명시할 것 |
| DDR5 표준 bin 목록 | JESD79-5 초안: 3200/3600/4000/4400/5200/5600/6000/6400 (**4800 없음**) | 실제 시장·Samsung/Micron: **4800이 JEDEC 기본 bin** | **초안이 오래된 것.** DDR5-4800 근거로 `jesd79_5.txt`를 인용하면 안 됩니다. Samsung/Micron 문서를 쓰십시오. |

---

## 4. 확인 실패 항목

1. **DDR3 코어 타이밍 1차 자료 — 확인 실패 (3회 시도)**
   로컬에 DDR3 자료가 없어 웹으로 시도했으나 **T0/T1 원문에서 값을 추출하지 못했습니다.**
   - 시도 1: Micron DDR3L `MT41K256M8DA-125K` 데이터시트 PDF (3.1 MB) → PDF 압축 스트림으로 텍스트 추출 실패
   - 시도 2: **JESD79-3F (JEDEC, 2012-07)** PDF (5.6 MB) → 추출 실패. *(이 문서가 DDR3 speed bin의 T0 비준본 원문이므로, 확보되면 바로 채울 수 있는 공백입니다. 검색 스니펫 수준에서는 "Table 62 = DDR3-800 Speed Bins", "Table 64 = DDR3-1333 Speed Bins"로 보이나 **표 내용은 미확인**)*
   - 시도 3: Samsung DDR3 SODIMM 데이터시트 Rev 1.2 (2008-08) PDF → 추출 실패
   - 웹 검색 요약문은 "DDR3-1600 11-11-11에서 tRCD = tRP = 13.75 ns, tRAS = 35 ns"라고 답했으나, **이는 검색엔진의 합성 요약이며 원문 표를 직접 확인한 것이 아닙니다. 인용 금지.**
   → 결론: **"DDR3→DDR4→DDR5 3세대에 걸쳐 ns 정체"를 주장하지 마십시오.** 현재 1차 자료로 뒷받침되는 구간은 **DDR4-1600 ~ DDR5-7200(데이터율 1600→7200 MT/s, 4.5배)** 뿐이며, 이 구간만으로도 논증은 충분히 성립합니다.
2. **JESD79-5 비준본(JESD79-5A/B/C)의 tWR·tRTP·tRAS 확정값** — 로컬 `jesd79_5.txt`는 "Proposed DDR5 Full spec (79-5)" 초안 Rev0.1이며 CL/CWL이 TBD입니다. 비준본 미확보.
3. **DDR5 tRAS min의 JEDEC 원문 숫자** — 초안 Table 109에서 min 칸의 숫자가 텍스트 추출에 나오지 않았습니다(max만 "9 × tREFI"). 32 ns는 **tRC−tRP 역산 + Samsung 문서 교차확인**에 의한 값이며, JEDEC 초안 원문에서 직접 읽은 것이 아닙니다.
4. **DDR5-5600 / 6400의 tRAS·tRC** — Micron 16Gb DDR5 Die Rev D의 요약 표(Table 2)에는 tAA/tRCD/tRP만 있습니다. 해당 문서 내 AC timing 상세표는 로컬 텍스트(46KB, features 발췌본)에 포함되어 있지 않습니다.
5. **CPU가 체감하는 end-to-end 메모리 지연(load-to-use)의 실측치** — 이번 조사 범위(디바이스 타이밍)에서는 확보하지 못했습니다. "10~100 ns"의 상단(100 ns 근처)은 **디바이스 타이밍만으로는 설명되지 않습니다**(최대가 conflict 48~54 ns). 나머지는 칩 밖 요소이며 별도 근거가 필요합니다.
6. **tRAS와 restore 시간의 정량 관계** — "tRAS의 대부분이 restore"라는 정량 근거(예: 감지 X ns + restore Y ns)는 데이터시트에 없습니다. 데이터시트가 주는 것은 **"precharge는 array restore 완료 후여야 한다"는 정성 서술**(L12162-12167)뿐입니다. 정량 분해는 학술 문헌이 필요합니다.
7. **AL(Additive Latency) 적용 시 RL 값** — DDR4에서 RL = AL + CL임은 확인했으나(L19552 "RL = 20 (CL = 11, AL = CL−2)"), DDR5의 AL 정책은 확인하지 못했습니다.

---

## 5. 기존 소스 팩(v3/v4)과의 충돌

**직접 충돌 없음.** 기존 팩에 코어 타이밍(tRCD/tRP/tRAS/tRC/tAA/tWR/tRTP) 값이 전혀 없어 중복도 충돌도 없습니다. 다만 **인접 항목 3건 주의**:

1. **v4 addendum L670 / L1210 — PRACtical 논문의 "tRP 15 ns → 36 ns"**
   본 조사가 확인한 정상 tRP는 DDR4-3200 **13.75~15.00 ns**, DDR5-4800B **16.000 ns**, DDR5-6400 JEDEC 초안 A/B/C **15.00/16.50/18.00 ns**입니다. → **PRACtical의 baseline "15 ns"는 본 조사의 1차 자료와 정합합니다.** 36 ns는 PRAC 적용 시의 값이므로 정상값과 섞이지 않게 하십시오.
   또한 v4 addendum이 "tRAS/tRC 값 사용 금지"로 판정한 근거(tRC ≠ tRAS + tRP)는 **본 조사가 1차 자료로 재확인했습니다**: Micron DDR4 Table 158은 tRC를 아예 "tRAS + tRP"라는 **수식으로** 정의하고 있고(L36255-36264), Samsung DDR5-4800B는 48.000 = 32.00 + 16.00으로 숫자가 맞습니다. → **v4의 사용금지 판정이 옳습니다.**

2. **v4 addendum L562 — FGR/tRFC 서술**
   본 조사의 tRAS max(9×tREFI 또는 5×tREFI)는 tREFI에 종속되므로 refresh 서술과 연결됩니다. 충돌은 없습니다.

3. **v3의 "DRAM 지연 10~100 ns"**
   본 조사 결과 **디바이스 타이밍만으로는 13.75 ~ 54 ns**입니다. 하단 10 ns는 어떤 speed bin에서도 나오지 않고(최소가 row hit 13.75 ns), 상단 100 ns도 디바이스 타이밍으로는 나오지 않습니다. → **v3 표현을 그대로 두면 근거가 없습니다.** 6절 참조.

---

## 6. 집필 시 주의 (서술 규칙 제안)

1. **"10~100 ns"를 쓰려면 무엇의 지연인지를 반드시 명시하십시오.** 디바이스 타이밍 기준은 **row hit 약 14~18 ns, row conflict 약 41~54 ns**입니다. 100 ns대는 CPU load-to-use(캐시 미스 판정 + 인터커넥트 + 컨트롤러 큐잉 + PHY 포함)여야 나옵니다. 두 층위를 섞어 쓰면 틀립니다. 이번 조사는 **디바이스 층위만** 근거를 확보했습니다.
2. **세 시나리오를 "16 / 32 / 48 ns"로 제시하는 것이 가장 안전합니다** — Samsung DDR5-4800B 기준이고, 세 값이 정확히 1:2:3이라 직관적이며, tRC = 48.000 ns가 문서에 명시된 숫자와 일치합니다. 다른 bin을 쓰면 반올림 때문에 깔끔하지 않습니다.
3. **speed bin 세 숫자의 단위는 클럭입니다.** "40-40-40"을 ns로 오해하게 쓰지 마십시오. 그리고 실제 DDR5-4800B는 40-40-40이 아니라 **40-39-39**입니다(Samsung 문서). Micron DDR5-6400은 **52-52-52**입니다. 임의로 "40-40-40" 같은 예시를 만들지 말고 실측 표기를 쓰십시오.
4. **tRC는 대부분의 데이터시트에서 숫자가 아니라 tRAS+tRP 수식으로 주어집니다.** "tRC = 45.75 ns"처럼 쓸 때는 계산값임을 밝히십시오. 숫자로 명시된 것은 Samsung DDR5-4800B의 48.000 ns뿐입니다.
5. **tRAS는 "여유"가 아니라 "무결성 조건"입니다.** restore가 끝나기 전 precharge하면 데이터가 깨집니다. 데이터시트가 auto-precharge를 "ARRAY RESTORE 완료까지 내부 지연"시킨다고 명시한 것이 근거입니다. 다만 **"tRAS의 몇 %가 restore"라는 정량 서술은 근거가 없습니다** — 하지 마십시오.
6. **DDR3를 언급하려면 별도 근거가 필요합니다.** 현재 1차 자료는 DDR4-1600 ~ DDR5-7200뿐입니다. "DDR3→DDR4→DDR5"라고 쓰면 근거 범위를 넘습니다. **"DDR4-1600 → DDR5-6400, 데이터율 4배 구간"** 으로 좁혀 쓰는 것이 정확합니다.
7. **JESD79-5 초안 인용 시 반드시 "초안 Rev0.1, 미비준, CL/CWL은 TBD"를 붙이십시오.** 특히 **tWR 45 ns는 인용하지 마십시오** — MR6 노트가 "currently defined as"라고 적고 인코딩이 전부 TBD입니다. DDR4 tWR 15 ns는 Micron 확정 데이터시트값이므로 안전합니다.
8. **DDR5-4800의 근거로 `jesd79_5.txt`를 인용하지 마십시오.** 초안 표준 bin 목록에 4800이 없습니다. Samsung UDIMM(2021-03) 또는 Micron 문서를 쓰십시오.
9. **Micron DDR5 7200 MT/s는 "Advance"(개발 중)** 입니다. 확정 사양처럼 쓰지 마십시오. Production은 5600·6400입니다.
10. **"22-22-22"만으로 부품을 특정하지 마십시오.** Micron DDR4-3200에는 22-22-22가 -062Y와 -062E 둘 다이며 tAA min이 미묘하게 다릅니다(13.32 vs 13.75, non-native 조합 조건부).
11. **문서 연도를 밝히십시오.** Samsung UDIMM은 **2021-03**, Micron DDR4는 **2021-08**, Micron DDR5 Die Rev D는 **2024-04**입니다. 2026년 현재 기준으로는 DDR5-8000/8800급 제품이 존재할 수 있으나 **본 조사는 확인하지 않았습니다.**

---

## 7. 출처 목록

| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| `micron_ddr4_16gb.txt` | **T1** | Micron 16Gb: x4, x8, x16 DDR4 SDRAM — `16gb_ddr4_dram.pdf` Rev. H, 2021-08. Table 152(DDR4-1600 bin) L34648-34720, Table 158(DDR4-3200 bin) L36172-36265, AC Timing L37367-37398 / L39515-39664, MR0 WR/RTP 설명 L3592-3604, PRECHARGE·ARRAY RESTORE L12153-12167 | 2026-07-29 |
| `micron16gb_ddr5.txt` | **T1** | Micron 16Gb DDR5 SDRAM Die Rev D — `16gb_ddr5_sdram_dierevD.pdf` Rev. F, 2024-04. Table 2 (Part Numbers and Timing Parameters) L114-244, speed 코드 L289-297 | 2026-07-29 |
| `samsung_ddr5_udimm.txt` | **T1** | Samsung DDR5 UDIMM datasheet Rev. 1.0, 2021-03. 모듈 요약표 L125-163, DDR5-4800 Speed Bins and Operations L5549-5590, frequency down bins L5591-5654 | 2026-07-29 |
| `jesd79_5.txt` | **T0 (위원회 초안, 미비준)** | "Proposed DDR5 Full spec (79-5)" Rev0.1 회람본. Speed Bin 목차 L418-431, Table 109 DDR5-6400 (No Ballot) L22177-22242, tRTP/tWR L23087-23105, MR6 tWR/tRTP L2416-2452 | 2026-07-29 |
| `RAM-source-pack-v4-addendum.md` | (내부) | 기존 소스 팩 — PRAC tRP 15→36 ns, tRFC/FGR 대조용 | 2026-07-29 |
