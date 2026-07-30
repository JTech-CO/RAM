# 리텐션 분포와 refresh 정책
> 조사일: 2026-07-29 / 상태: 완료 (웹 검색 0회 — 전부 로컬 1차 자료 기반)

## 1. 확인된 사실

### 1-1. tREFI (평균 refresh 간격) — DDR4 vs DDR5

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR4 tREFI(base), 2/4/8/16Gb 공통 | 7.8 µs | T0 | jesd79_4.txt L4383-4388 (JESD79-4, Table 23) | 16Gb 열은 원문에서 `TBD` |
| DDR4 1X 모드 tREFI1, 0 ≤ Tcase ≤ 85°C | tREFI(base) = 7.8 µs | T0 | jesd79_4.txt L4389-4396 | |
| DDR4 1X 모드 tREFI1, 85 < Tcase ≤ 95°C | tREFI(base)/2 = 3.9 µs | T0 | jesd79_4.txt L4397-4402 | **85°C 초과 시 절반**의 표준 근거 |
| DDR4 2X 모드 tREFI2 (0~85°C / 85~95°C) | tREFI(base)/2 / tREFI(base)/4 | T0 | jesd79_4.txt L4409-4422 | |
| DDR4 4X 모드 tREFI4 (0~85°C / 85~95°C) | tREFI(base)/4 / tREFI(base)/8 | T0 | jesd79_4.txt L4429-4442 | |
| DDR5 Normal 모드 tREFI1, 0 ≤ Tcase ≤ 85°C | tREFI = **3.9 µs** | T0(초안) | jesd79_5.txt L11466-11479 (DDR5 Full Spec **Draft Rev0.1**, Table 24) | DDR4의 절반 |
| DDR5 Normal 모드 tREFI1, 85 < Tcase ≤ 95°C | tREFI/2 = **1.95 µs** | T0(초안) | jesd79_5.txt L11480-11483 | |
| DDR5 FGR 모드 tREFI2, 0~85°C | tREFI/2 = 1.95 µs | T0(초안) | jesd79_5.txt L11484-11489 | |
| DDR5 FGR 모드 tREFI2, 85~95°C | tREFI/4 = **0.975 µs** | T0(초안) | jesd79_5.txt L11490-11493 | |
| DDR5 16Gb 실제품: 32 ms 내 8,192 REF → tREFI 3.9 µs | 8192 REF / 32 ms | T1 | micron16gb_ddr5.txt L405-407 (Micron 16Gb DDR5 Die Rev D, Rev.F 04/2024) | **DDR5의 refresh window는 32 ms** (DDR4의 64 ms가 아님) |
| DDR5 16Gb 실제품: 85~95°C 구간 8,192 REF / 16 ms → tREFI 1.95 µs | 8192 REF / 16 ms | T1 | micron16gb_ddr5.txt L406-407 | |

### 1-2. tRFC (refresh cycle time) — 다이 용량별

| 표준/제품 | 파라미터 | 2Gb | 4Gb | 8Gb | 16Gb | 32Gb | 등급 | 출처 |
|---|---|---|---|---|---|---|---|---|
| DDR4 (JESD79-4) | tRFC1(min) | 160 ns | 260 ns | 350 ns | TBD | — | T0 | jesd79_4.txt L4403-4408 |
| DDR4 (JESD79-4) | tRFC2(min) (2X/FGR) | 110 ns | 160 ns | 260 ns | TBD | — | T0 | jesd79_4.txt L4423-4428 |
| DDR4 (JESD79-4) | tRFC4(min) (4X) | 90 ns | (추가 확인 필요) | | TBD | — | T0 | jesd79_4.txt L4443-4444 |
| DDR5 Draft Rev0.1 | tRFC1(min) (Normal REFab) | — | — | **195 ns** | **295 ns** | TBD | T0(초안) | jesd79_5.txt L11500-11505 |
| DDR5 Draft Rev0.1 | tRFC2(min) (FGR REFab) | — | — | 130 ns | 160 ns | TBD | T0(초안) | jesd79_5.txt L11506-11511 |
| DDR5 Draft Rev0.1 | tRFCsb(min) (Same-bank REFsb) | — | — | 115 ns | 130 ns | TBD | T0(초안) | jesd79_5.txt L11512-11517 |
| DDR5 Draft Rev0.1 | tREFSBRD(min) (REFsb→ACT) | — | — | 30 ns | 30 ns | TBD | T0(초안) | jesd79_5.txt L11524-11529 |

**용량↑ → tRFC↑ 추세 (확정 근거)**
- DDR2 → DDR3 → DDR4 세대별 tRFC 표 (T2, jacob_refresh.txt L474-540, Bhati et al. "DRAM Refresh Mechanisms, Penalties, and Trade-Offs", IEEE Trans. Computers):

| 세대 (tREFI) | 1Gb | 2Gb | 4Gb | 8Gb | 16Gb | 32Gb |
|---|---|---|---|---|---|---|
| DDR2 (tREFI 7.8 µs) tRFC | 127.5 ns | 197.5 ns | 327.5 ns | — | — | — |
| DDR3 (tREFI 7.8 µs) tRFC | 110 ns | 160 ns | 300 ns | 350 ns | — | — |
| DDR4 1x (tREFI 7.8 µs) tRFC | — | 160 ns | 260 ns | 350 ns | TBD | — |
| DDR4 2x (tREFI 3.9 µs) tRFC | — | 110 ns | 160 ns | 260 ns | TBD | — |
| DDR4 4x (tREFI 1.95 µs) tRFC | — | 90 ns | 110 ns | 160 ns | TBD | — |
| LPDDR3 (tREFI 3.9 µs, **tREFW 32 ms**) tRFCab | — | — | 130 ns | 210 ns | TBD | TBD |
| LPDDR3 tRFCpb (per-bank) | — | — | 60 ns | 90 ns | TBD | TBD |

- DDR4 JEDEC 원문 값과 일치 (2Gb 160 → 4Gb 260 → 8Gb 350 ns). 용량 2배마다 약 +90~100 ns.
- DDR5: 8Gb 195 → 16Gb 295 ns (T0 초안). 용량 2배에 +100 ns.
- **Mukundan et al. (MICRO 2013) 외삽치** (T2, mukundan.txt L109-132) — 원문이 "Values for large chips are **extrapolated**"라고 명시:

| Chip Size | tRFC_1x | tRFC_2x | tRFC_4x |
|---|---|---|---|
| 8 Gb (실측/표준) | 350 ns | 260 ns | 160 ns |
| 16 Gb (**외삽**) | 480 ns | 350 ns | 260 ns |
| 32 Gb (**외삽**) | 640 ns | 480 ns | 350 ns |

- 24Gb / 32Gb DDR5 실제 값: **확인 실패** (아래 §4)

### 1-3. refresh가 잡아먹는 대역폭·전력 (용량 증가에 따른 추세)

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 32Gb 디바이스 사용 시 refresh가 DRAM 에너지의 20% 초과, 시스템 성능 30% 초과 저하 | >20% 에너지 / >30% 성능 | T2 | jacob_refresh.txt L45-49 | 시뮬레이션 기반 |
| 32Gb 디바이스, LOW-bandwidth 워크로드에서 refresh가 DRAM 에너지의 25~30% | 25~30% | T2 | jacob_refresh.txt L672-676 | |
| 32Gb 디바이스, HIGH-bandwidth 워크로드(libquantum, mcf)에서 IPC 저하 30% 초과 | >30% | T2 | jacob_refresh.txt L678-681 | 워크로드 특정 필요 |
| 디바이스 속도 변화 시 HIGH-bandwidth 워크로드 IPC 손실 | 최대 11.4% | T2 | jacob_refresh.txt L657-659 | |
| refresh로 인한 throughput loss = tRFC / tREFI (정의) | — | T2 | raidr.txt L377-381 | 계산 규칙 |
| 64Gb 밀도 노드에서 throughput loss가 **약 50%**에 도달 (extended-temperature 조건) | ≈50% | T2 | raidr.txt L381-384 | **추정·외삽치**, Figure 3b |
| 32Gb 밀도 노드에서 auto-refresh 명령 latency가 **1 µs 초과** | >1 µs | T2 | raidr.txt L374-377 | **추정·외삽치**. 전력 제약 때문에 refresh latency가 밀도에 거의 선형 비례 |
| RAIDR 효과: 2-bin 구성으로 refresh 74.6% 감소, DRAM 시스템 전력 16.1% 감소, 성능 8.6% 향상 (32GB 시스템) | 74.6% / 16.1% / 8.6% | T2 | raidr.txt L90-104 | 제안 기법의 시뮬레이션 결과 |
| Mukundan AR+DCE+PCD: 1x 대비 성능 8%(normal) / 14%(extended temp) 향상 | 8% / 14% | T2 | mukundan.txt L154-160 | 제안 기법 결과 |

### 1-4. 리텐션 시간 분포 (tail bit이 refresh 주기를 결정)

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 32GB DRAM 시스템(총 셀 10^11 초과)에서 256 ms보다 짧은 refresh 간격을 요구하는 셀 수 | **1,000개 미만** | T2 | raidr.txt L69-75, L124, L147 | 60 nm 공정 데이터 기반 (RAIDR Fig.1, 원출처 [21]) |
| 같은 시스템에서 128 ms를 못 견디는 셀 수 | **약 30개** | T2 | raidr.txt L146, L434-435 | 단일 출처 |
| 리텐션 분포 모델 | 셀을 normal / leaky 두 범주로 나누고, 각 범주 내에서 **log-normal 분포** | T2 | raidr.txt L426-430 | |
| leaky 셀의 누설 전류 | normal 셀 대비 **자릿수(order of magnitude) 단위로 높음** | T2 | jacob_refresh.txt L462-465 | |
| normal 셀 대다수의 리텐션 시간 | **1초 이상** | T2 | jacob_refresh.txt L465-467 | 단일 출처 |
| 디바이스 리텐션 시간 결정 원리 | 가장 누설이 심한 셀(leakiest cell)이 디바이스 전체 리텐션 시간을 결정 | T2 | jacob_refresh.txt L467-469 | |
| 64 ms 미만 리텐션 셀의 처리 | 다이 폐기(die discarded) → 분포 곡선이 64 ms에서 좌측 절단됨 | T2 | raidr.txt L458-459 | 분포 그림 해석 시 필수 주의점 |
| 64 ms 최소 refresh 간격이 여러 DRAM 세대에 걸쳐 유지됨 | 64 ms | T2 | raidr.txt L321 | |
| 산업계가 per-cell 리텐션 64 ms와 tREFI를 상수로 두고 대신 tRFC를 늘려온 설계 결정 | — | T2 | mukundan.txt L67-75 | 서사의 핵심 |

### 1-5. VRT (Variable Retention Time)

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| VRT 최초 보고 시점 | **1987년** | T2 | avatar_vrt.txt L346 (Qureshi et al., AVATAR, DSN 2015) | 원출처는 AVATAR 참고문헌 [45] |
| VRT 물리 기전 | **GIDL(gate-induced drain leakage) 전류의 요동**. 게이트 영역 근처의 트랩(trap)이 무작위로 점유/해제되면서 누설 전류가 변동 | T2 | avatar_vrt.txt L345-355 | 메커니즘 서술의 핵심 |
| 2GB 메모리의 Active-VRT Pool (AVP), 15분 구간 평균 | **350~500 셀** | T2 | avatar_vrt.txt L153-155 | 24개 상용 DRAM 칩 실험. 단일 출처 |
| Active-VRT Injection (AVI) rate | 15분당 **약 1개**의 새 셀 | T2 | avatar_vrt.txt L155-157 | 단일 출처 |
| 초기 테스트에서 검출된 weak cell 수 (2GB DIMM, 벤더 3사) | A: 27,841 / B: 24,503 / C: 22,414 | T2 | avatar_vrt.txt L438-440 | Slow Refresh 320 ms 기준 |
| 그 결과 Fast Refresh로 지정되는 행 비율 | 전체 행의 **약 9~10%** (2GB DIMM, 256K rows, 8KB/row) | T2 | avatar_vrt.txt L443-446 | |
| weak cell의 공간 분포 | weak row 수 ≈ weak cell 수 → weak cell이 메모리 전체에 **무작위로 흩어져 있음** | T2 | avatar_vrt.txt L449-452 | |
| ECC DIMM(SECDED)만으로 multirate refresh를 쓸 때 | 소프트에러가 전혀 없어도 **6~8개월에 한 번 정정 불가 오류** 발생 | T2 | avatar_vrt.txt L168-173 | AVATAR의 문제제기 |
| AVATAR 효과 | 기존 multirate refresh 대비 신뢰성 **100배** 개선, TTF를 수개월 → 수십 년 | T2 | avatar_vrt.txt L190-193 | 제안 기법 결과 |
| VRT가 데이터 오류를 일으키는 조건 | 셀이 **고(高)리텐션 영역 → 저(低)리텐션 영역**으로 이동할 때만. 리텐션이 늘어나는 방향의 VRT는 무해 | T2 | avatar_vrt.txt L370-400 | |
| 삼성·인텔 공동 논문이 VRT를 미세화 스케일링의 최대 난제 중 하나로 지목 | — | T2 (재인용) | avatar_vrt.txt L366-369 (참고문헌 [18]) | **재인용**. 원문 미확인 |
| VRT는 후공정(post-packaging) 테스트 이후에도 발생 → 제조사 스크리닝으로 걸러낼 수 없음 | — | T2 | avatar_vrt.txt L358-360 | |
| 리텐션 프로파일링의 또 다른 난제: **데이터 패턴 의존성(DPD)** | 단일 데이터 패턴 한 번으로는 전체 weak cell의 **15% 미만**만 검출 | T2 | isca13_retention.txt L96-103 (Liu et al., ISCA 2013) | 단일 출처. 리텐션 프로파일링 무용론의 정량 근거 |

### 1-6. 온도 의존성

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR4/DDR5 공통: Tcase > 85°C에서 refresh 주기 **1/2** | tREFI/2 | T0 / T0(초안) | jesd79_4.txt L4397-4402, jesd79_5.txt L11480-11483 | 표준 근거 |
| Micron 16Gb DDR5: 85°C 초과 시 refresh window 32 ms → **16 ms** | 16 ms / 8192 REF | T1 | micron16gb_ddr5.txt L405-407 | |
| Industrial Temperature(IT) 옵션: Tc −40~95°C, 85°C 초과 시 refresh rate 2배 + high-temp self-refresh 필수 | 2X | T1 | micron16gb_ddr5.txt L408-414 | |
| Automotive Temperature(AT) 옵션: Tc −40~105°C, **85°C 이상 2X, 105°C 이상 4X** | 2X / 4X | T1 | micron16gb_ddr5.txt L415-419 | 4X 규정의 유일한 로컬 근거 |
| 실험적 온도 환산: 45°C에서 4초 리텐션 = 85°C에서 **328 ms** | 4 s @45°C ↔ 328 ms @85°C | T2 | avatar_vrt.txt L405-410 | **실험 가정치**, 40°C 차이에 약 12배. 표준 값 아님 |
| 서버·데스크톱 실제 동작 온도 (100% 사용률에서도) | **40~60°C** | T2 (재인용) | avatar_vrt.txt L411-414 | 논문이 선행연구 [9,25]를 인용 |
| DDR4 Temperature Controlled Refresh(TCR) 모드 사용 제약 | TCR 활성 시 **Fixed 1x 모드만 허용** (2x/4x/on-the-fly 금지) | T0 | jesd79_4.txt L4372-4375 | |
| DDR4 TCR: 45°C 미만에서는 SDRAM이 내부 refresh 주기를 tREFI보다 **길게** 조정(스킵) 가능 | — | T0 | jesd79_4.txt L4154-4166 | Normal / Extended 두 모드 존재 |

### 1-7. FGR / auto vs self refresh / same-bank refresh

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR4 FGR 모드 종류 | Fixed 1x / Fixed 2x / Fixed 4x + on-the-fly 1x/2x/4x. MRS(MR3 A8:A7:A6)로 설정 | T0 | jesd79_4.txt L4223-4247, L4302-4346 | |
| DDR5 refresh 모드 | Normal(tRFC1) / Fine Granularity(tRFC2) 2종. **DDR4의 4x는 없음** | T0(초안) | jesd79_5.txt L2335-2336, L11338-11340 | 세대 차이로 명시할 것 |
| DDR5 FGR 정의 | tRFC2는 짧아지지만 REFab를 2배 자주 발행 (tREFI2 = tREFI1/2) | T0(초안) | jesd79_5.txt L11338-11340 | |
| DDR5 **REFsb (Same-Bank Refresh)** 신규 도입 | 모든 뱅크 그룹의 동일 번호 뱅크만 refresh. 나머지 뱅크는 **접근 가능** | T0(초안) / T1 | jesd79_5.txt L11406-11423, micron_ddr5.txt L46-63 | DDR5의 핵심 신규 기능 |
| REFsb 사용 제약 | **FGR 모드에서만** 발행 가능. 각 뱅크가 평균 1.95 µs마다 REFsb를 받아야 함 | T1 | micron_ddr5.txt L59-61 | |
| REFsb tREFIsb 계산식 | tREFI/(2n) (0~85°C), tREFI/(4n) (85~95°C). n = 뱅크 그룹당 뱅크 수 (8Gb: n=2, 16Gb: n=4) | T1 | samsung_ddr5_udimm.txt L1106-1180 (Samsung DDR5 UDIMM, Rev 1.0 / Mar. 2021) | |
| 16Gb DDR5 REFsb 지속시간 | **130 ns** (REFab 295 ns 대비) | T1 | micron_ddr5.txt L60-61 | JEDEC 초안값과 일치 |
| REFsb burst 제약 | 각 burst는 4 × (tRFCsb + [(n−1) × tRRD_L])로 규정 | T0(초안) | jesd79_5.txt L11423 | |
| DDR5 refresh 스케줄링 유연성 (Normal) | 최대 **4개** postpone / 4개 pull-in, 최대 간격 **5 × tREFI1** | T0(초안) | jesd79_5.txt L11534-11544 | |
| DDR5 refresh 스케줄링 유연성 (FGR) | 최대 간격 **9 × tREFI2** | T0(초안) | jesd79_5.txt L11322-11330, L11548-11550 | |
| DDR4/DDRx 스케줄링 유연성 | 최대 **8개** AR postpone / 8개 pull-in | T2 | jacob_refresh.txt L470-471 | **DDR5 초안(4개)과 다름** — 세대 차이 |
| LPDDRx는 per-bank(REFpb)와 all-bank(REFab) 모두 보유, DDRx는 all-bank만 (DDR4 시점) | — | T2 | jacob_refresh.txt L539-540 | DDR5에서 REFsb로 상황이 바뀜 |
| refresh와 ACT-PRE는 물리적으로 동일한 동작(전하를 sense amp로 옮겼다가 복원) | — | T2 | rtc_refresh.txt L260-264 | "읽기가 곧 refresh"의 근거 |

## 2. 구조·메커니즘 서술

**(1) refresh 주기는 "평균 셀"이 아니라 "최악 셀"이 정한다**
DRAM 셀의 리텐션 시간은 셀 커패시터와 액세스 트랜지스터의 누설 전류에 의해 결정되며, 공정 편차 때문에 셀마다 다르다 (isca13_retention.txt L267-269). 누설 경로는 junction leakage, GIDL, off-leakage, field transistor leakage, capacitor dielectric leakage로 열거된다 (jacob_refresh.txt L453-455). 셀은 크게 *normal*과 *leaky* 두 범주로 나뉘고, 각 범주 안에서 리텐션 시간이 **로그정규(log-normal) 분포**를 따른다는 것이 통상적인 모델이다 (raidr.txt L426-430). leaky 셀은 normal 셀보다 누설 전류가 자릿수 단위로 크다 (jacob_refresh.txt L462-465). 그런데 refresh 로직은 단순화를 위해 모든 행을 같은 속도로 refresh하므로, **디바이스 전체의 refresh 주기는 가장 누설이 심한 단 하나의 셀에 의해 결정된다** (jacob_refresh.txt L467-469, isca13_retention.txt L257-259).

**(2) 꼬리(tail)의 정량적 실체**
RAIDR가 60 nm 공정 데이터로 제시한 분포에 따르면, 10^11개가 넘는 셀을 가진 32GB DRAM 시스템에서 128 ms를 못 견디는 셀은 **약 30개**, 256 ms를 못 견디는 셀은 **1,000개 미만**이다 (raidr.txt L124, L146-147, L434-437). 즉 64 ms라는 표준 요건은 전체의 10^-8 수준 비율의 셀 때문에 나머지 전부가 치르는 비용이다. 이것이 retention-aware refresh 연구 전체의 출발점이다.

**(3) 분포 그림을 읽을 때의 절단(truncation) 주의**
공개된 리텐션 분포 곡선은 좌측이 64 ms에서 잘려 있다. 리텐션 64 ms 미만 셀이 있는 다이는 **폐기되기 때문**이다 (raidr.txt L458-459, isca13_retention.txt L243-244). 따라서 "64 ms 미만 셀이 없다"가 아니라 "64 ms 미만 셀이 있으면 그 다이가 출하되지 않는다"가 정확한 서술이다. 표준의 64 ms는 물리 상수가 아니라 **수율 선별 기준(screening threshold)**이다.

**(4) 왜 tREFI는 그대로인데 tRFC만 길어졌는가**
용량이 커지면 refresh해야 할 비트 수가 늘어난다. 업계는 per-cell 리텐션 요건(64 ms)과 refresh 간격(tREFI)을 상수로 고정하고, 대신 **refresh 명령 하나가 처리하는 행 수를 늘려 tRFC를 키우는** 선택을 했다 (mukundan.txt L67-75). 그 결과 DDR3 1Gb 110 ns → DDR4 8Gb 350 ns → DDR5 16Gb 295 ns 식으로 tRFC가 밀도에 따라 증가한다. refresh로 인한 throughput 손실은 정의상 **tRFC / tREFI**이므로 (raidr.txt L377-381), tREFI가 고정된 채 tRFC만 커지면 오버헤드는 밀도에 거의 선형으로 증가한다. RAIDR는 이 추세를 외삽해 64Gb 노드에서 throughput 손실이 50%에 육박할 것으로 추정했다 (raidr.txt L381-384).

**(5) DDR5가 이 곡선을 꺾은 방식 — REFsb**
DDR5의 tRFC1은 16Gb에서 295 ns로, DDR4 8Gb의 350 ns보다 오히려 짧다. 대신 DDR5는 tREFI를 7.8 µs에서 3.9 µs로 절반으로 줄여 refresh window를 32 ms로 가져갔다 (jesd79_5.txt L11466-11479, micron16gb_ddr5.txt L405-407). 더 중요한 변화는 **REFsb(Same-Bank Refresh)**다. REFab는 랭크 전체를 tRFC1(295 ns) 동안 막아버리지만, REFsb는 모든 뱅크 그룹의 같은 번호 뱅크만 130 ns 동안 막고 나머지 뱅크는 계속 접근할 수 있다 (micron_ddr5.txt L46-63, jesd79_5.txt L11406-11423). 비(非)refresh 뱅크에 대한 유일한 제약은 tREFSBRD(30 ns)뿐이다 (jesd79_5.txt L11524-11528). 이는 mukundan.txt가 지적한 "command queue seizure"(랭크 전체가 막히면 명령 큐가 그 랭크 명령으로 가득 차 다른 랭크 요청까지 못 넣는 현상, mukundan.txt L135-142) 문제를 구조적으로 완화한다.

**(6) FGR의 본질은 트레이드오프이지 절감이 아니다**
FGR/2x/4x 모드는 tRFC를 줄이는 대신 refresh 명령 발행 빈도를 늘린다. 총 refresh 작업량은 오히려 늘어난다 — DDR4 8Gb 기준 1x는 350 ns를 7.8 µs마다(듀티 4.5%), 4x는 160 ns를 1.95 µs마다(듀티 8.2%)이다 (jesd79_4.txt Table 23 값으로 계산). FGR가 주는 것은 **평균 접근 지연의 개선(긴 블로킹 구간 제거)**이지 refresh 총량의 절감이 아니다. mukundan.txt가 AR(Adaptive Refresh)로 워크로드별로 모드를 골라야 한다고 주장하는 이유가 이것이며, 나아가 DCE/PCD를 붙이면 FGR가 대부분의 경우 불필요해진다고 결론짓는다 (mukundan.txt L154-158).

**(7) VRT — 프로파일링을 원리적으로 무력화하는 현상**
retention-aware refresh는 "어느 행이 weak인지 미리 알아낸다"를 전제로 한다. VRT는 이 전제를 깬다. 게이트 근처 트랩이 무작위로 점유·해제되면서 GIDL 전류가 요동치고, **같은 셀이 시점에 따라 다른 리텐션 상태를 오간다** (avatar_vrt.txt L335-355). VRT는 1987년에 처음 보고됐고 (L346), 후공정 테스트 이후에도 발생하므로 제조사가 선별할 수 없다 (L358-360). AVATAR의 측정에서 2GB 메모리는 15분 구간마다 평균 350~500개의 활성 VRT 셀을 갖고, 15분당 약 1개의 새로운 VRT 셀이 나타난다 (L153-157). 여기에 **데이터 패턴 의존성(DPD)**이 겹친다 — 단일 데이터 패턴으로 한 번 테스트해서는 전체 weak cell의 15% 미만만 검출된다 (isca13_retention.txt L96-103). 결론적으로 리텐션 프로파일링은 1회성 테스트로 완결될 수 없고, 런타임 ECC + 스크러빙과 결합돼야 한다.

**(8) 온도**
누설은 온도에 지수적으로 민감하다. 표준은 이를 이산적으로 반영해 Tcase가 85°C를 넘으면 tREFI를 절반으로 줄이도록 규정한다 (jesd79_4.txt L4397-4402, jesd79_5.txt L11480-11483). 자동차용 옵션은 105°C 이상에서 4배까지 간다 (micron16gb_ddr5.txt L415-419). 반대 방향으로, DDR4의 Temperature Controlled Refresh는 45°C 미만에서 내부 refresh 주기를 tREFI보다 **늘릴 수** 있게 한다 (jesd79_4.txt L4154-4166). 실험 논문에서 쓰는 환산은 45°C에서 4초 ≈ 85°C에서 328 ms 수준이다 (avatar_vrt.txt L405-410) — 이는 **연구용 가정치이지 표준 규정이 아니다**.

## 3. 상충·불확실

| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| DDR4 16Gb tRFC1 | **480 ns** — Mukundan et al. MICRO 2013 (mukundan.txt L121-124), T2 | **TBD** — JESD79-4 원문 (jesd79_4.txt L4407), jacob_refresh.txt L506도 TBD | Mukundan은 본문에서 "large chips are **extrapolated**"라고 명시. **외삽치를 실측치로 인용하면 안 됨.** 최종 비준본 JESD79-4B의 실제 값은 로컬 자료로 **확인 실패** |
| DDR3 4Gb tRFC | **300 ns** (jacob_refresh.txt L496) | **260 ns** (DDR4 4Gb, jesd79_4.txt L4405) | 세대가 다르므로 상충 아님. 다만 "4Gb tRFC"라고만 쓰면 혼동되므로 반드시 세대 병기 |
| refresh 스케줄링 postpone/pull-in 한도 | **8개** (DDRx 일반, jacob_refresh.txt L470-471, T2) | **4개** (DDR5 Normal 모드, jesd79_5.txt L11538-11540, T0 초안) | 세대 차이로 보이나 DDR4 원문 확인은 못 함. **DDR5는 4개**로 특정해 쓸 것 |
| refresh가 차지하는 DRAM 에너지 비율 | **15%** (4Gb DDR3, Liu et al. 재인용, rtc_refresh.txt L251) / **20% 초과·25~30%** (32Gb, jacob_refresh.txt L47, L675) / **50%** (64Gb 전망, rtc_refresh.txt L253) | **40%** (조건 미상, rtc_refresh.txt L14) | 40%는 rtc_refresh 초록의 요약치로 **어느 밀도·워크로드인지 불명**. 인용 시 15%(4Gb DDR3) → 25~30%(32Gb) → 50%(64Gb 전망) 계열을 쓰고, 40%는 피할 것 |
| DDR5의 refresh window | **32 ms** (8192 REF × 3.9 µs, micron16gb_ddr5.txt L405-407, T1) | DDR4/DDR3는 **64 ms** (isca13_retention.txt L259-261, T2) | 상충 아님. **DDR5에서 window가 절반으로 줄었다**는 것이 사실. "DRAM은 64 ms마다 refresh한다"는 서술은 DDR4 이전에만 유효 |

## 4. 확인 실패 항목

1. **DDR5 24Gb / 32Gb의 tRFC 실제 값.** 로컬 jesd79_5.txt는 Draft Rev0.1이라 32Gb 열이 전부 `TBD`이고 24Gb 열은 아예 없다. micron_32gb_rdimm.txt에는 tRFC/tREFI 문자열 자체가 없다(모듈 레벨 문서). 24Gb·32Gb 다이는 DDR5 후기 개정판(JESD79-5B/5C)에서 추가된 것으로 보이나 **로컬 자료로 확인 불가**. 웹 미검색.
2. **DDR4 16Gb tRFC1의 비준 최종값.** 로컬 JESD79-4 판본에서 `TBD`.
3. **셀 커패시턴스(현행 10 fF 미만)와 리텐션 마진의 정량 관계.** 로컬 자료 전체(`*.txt`)를 "capacitance / fF / femto"로 grep했으나 **fF 단위 수치가 단 하나도 없음**. 확보한 것은 정성적 연결뿐: (a) 리텐션 시간이 "셀 커패시턴스와 누설 전류의 편차" 때문에 달라진다 (avatar_vrt.txt L237-239, T2), (b) 리텐션 시간은 커패시터와 액세스 트랜지스터의 누설 전류에 의존한다 (isca13_retention.txt L267-269, T2). **"C가 줄면 리텐션 마진이 줄어든다"를 수치로 뒷받침하는 근거는 확보 실패.** 기존 소스 팩 §3-2의 10 fF 서술과 refresh를 직접 잇는 정량 다리는 아직 없음.
4. **각 다이 용량별 refresh 대상 행 수 / REF 명령당 refresh되는 행 수.** 표준 원문에 명시되지 않음(내부 구현). 확인 실패.
5. **DDR5 self-refresh 진입/이탈 타이밍(tCKSRE/tCKSRX)과 self-refresh 전력의 정량치.** 시간 제약으로 미조사. auto refresh vs self refresh의 구조적 차이는 §2에 정성적으로만 있음.
6. **삼성/SK하이닉스 D1z·D1a·D1b 등 특정 노드의 리텐션 분포 실측.** 로컬 자료의 리텐션 분포 근거는 모두 **60 nm 공정(RAIDR, 2012)** 또는 **2GB DDR3급 DIMM(AVATAR, 2015)**이다. 최신 노드 데이터 확인 실패.

## 5. 기존 소스 팩(v3)과의 충돌

**직접 충돌: 없음.** 기존 소스 팩은 refresh를 "전하 누설 → 주기적 refresh 필요('Dynamic'의 어원)" 수준(L129)으로만 다루고 tREFI/tRFC 수치를 갖고 있지 않다. 따라서 본 문서는 전부 공백 보충이다.

**보완이 필요한 지점 2가지:**
- v3 L131-133의 **커패시턴스 정정(25 fF → 10 fF 미만)**과 refresh를 잇는 정량 근거는 이번 조사에서 **확보하지 못했다**(§4-3). v3의 커패시턴스 서술을 "그래서 refresh 주기가 짧아졌다"로 연결하는 것은 현재 근거로는 **불가**. 두 사실을 나란히 놓되 인과를 단정하지 말 것.
- v3는 refresh 주기를 명시하지 않았지만, 앞으로 쓸 때 "64 ms"를 무조건 쓰면 DDR5(32 ms window)와 어긋난다. §3의 마지막 항목 참조.

## 6. 집필 시 주의 (서술 규칙 제안)

1. **"DRAM은 64 ms마다 refresh한다"고 단정하지 말 것.** DDR3/DDR4는 64 ms window·tREFI 7.8 µs, **DDR5는 32 ms window·tREFI 3.9 µs**다 (T0 초안 + T1 데이터시트 확인). 세대를 반드시 붙일 것.
2. **64 ms는 물리 상수가 아니라 수율 선별 기준이다.** 리텐션 64 ms 미만 셀이 있는 다이는 폐기된다(raidr.txt L458-459). "셀이 64 ms 동안 전하를 유지한다"가 아니라 "64 ms를 못 버티는 셀이 있으면 그 다이는 출하되지 않는다"로 쓸 것.
3. **tRFC 수치를 쓸 때는 세대 + 다이 용량 + refresh 모드(1x/2x/4x, Normal/FGR/REFsb)를 셋 다 특정할 것.** "DDR4 tRFC는 350 ns"는 8Gb·1x 모드에서만 참이다.
4. **Mukundan의 16Gb 480 ns / 32Gb 640 ns는 2013년 논문의 외삽치**다. 표준 실측치처럼 쓰지 말 것. 실제로 DDR5 16Gb는 295 ns로, 이 외삽 방향과 다르게 흘러갔다.
5. **jesd79_5.txt는 "Proposed DDR5 Full spec (79-5)" Draft Rev0.1(위원회 회람본)**이다. 여기서 나온 195/295/130/115 ns는 **초안 값**으로 표기할 것. 다만 tRFC1 295 ns와 tRFCsb 130 ns(16Gb)는 Micron 백서(T1)와 일치하므로 실제 제품 값으로 보아도 무방하다 — 이 교차확인 사실을 함께 적을 것.
6. **"용량이 커지면 refresh 오버헤드가 커진다"는 방향은 맞지만, DDR5는 REFsb로 이를 되돌렸다.** DDR4 8Gb REFab 350 ns 랭크 전체 블로킹 → DDR5 16Gb REFsb 130 ns 뱅크 단위 블로킹. 단선적 악화 서사로만 쓰면 DDR5 세대를 왜곡한다.
7. **FGR를 "refresh를 줄이는 기능"으로 쓰지 말 것.** 총 refresh 작업량은 오히려 늘고, 얻는 것은 지연 분산이다.
8. **refresh 오버헤드 수치(20%, 30%, 50%)는 모두 시뮬레이션·외삽이다.** 실측 필드 데이터가 아니다. "~로 추정된다"로 쓰고 출처의 조건(밀도, 워크로드, 온도 범위)을 반드시 병기할 것. 특히 RAIDR의 "64Gb에서 50%"는 extended-temperature 조건의 외삽이다.
9. **VRT를 "일부 불량 셀 문제"로 축소하지 말 것.** 후공정 테스트 이후에도 새로 발생하며(avatar_vrt.txt L358-360), 프로파일링 기반 refresh 최적화를 원리적으로 제약한다.
10. **리텐션 분포 수치의 연도·공정을 밝힐 것.** 본 문서의 분포 근거는 60 nm(RAIDR, ISCA 2012)와 DDR3급 2GB DIMM(AVATAR, DSN 2015)이다. **1x nm 이하 최신 노드 데이터가 아니다.**
11. **커패시턴스 10 fF와 refresh 주기를 인과로 잇지 말 것** (§4-3, §5).

## 7. 출처 목록
| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| jesd79_4.txt | T0 | JEDEC JESD79-4, DDR4 SDRAM Standard (Table 23 = tREFI/tRFC parameters) | 2026-07-29 |
| jesd79_5.txt | T0 (**초안**) | "Proposed DDR5 Full spec (79-5)" — JC-42.3 위원회 회람 **Draft Rev0.1**, Item No. xxxx.yyy. Table 24/25/26 | 2026-07-29 |
| micron16gb_ddr5.txt | T1 | Micron 16Gb DDR5 SDRAM Die Rev D 데이터시트 (16gb_ddr5_sdram_dierevD.pdf, Rev. F, 04/2024) | 2026-07-29 |
| micron_ddr5.txt (= micron_ddr5_wp.txt) | T1 | Micron DDR5 기술 백서 (same-bank refresh / 2x banks / BL16 설명) | 2026-07-29 |
| samsung_ddr5_udimm.txt | T1 | Samsung DDR5 UDIMM 데이터시트, Rev. 1.0 / Mar. 2021 (tREFI parameters for REFab and REFsb) | 2026-07-29 |
| raidr.txt | T2 | J. Liu, B. Jaiyen, R. Veras, O. Mutlu, "RAIDR: Retention-Aware Intelligent DRAM Refresh", ISCA 2012 | 2026-07-29 |
| isca13_retention.txt | T2 | J. Liu et al., "An Experimental Study of Data Retention Behavior in Modern DRAM Devices: Implications for Retention Time Profiling Mechanisms", ISCA 2013 | 2026-07-29 |
| avatar_vrt.txt | T2 | M. Qureshi et al., "AVATAR: A Variable-Retention-Time (VRT) Aware Refresh for DRAM Systems", DSN 2015 | 2026-07-29 |
| jacob_refresh.txt | T2 | I. Bhati, M.-T. Chang, Z. Chishti, S.-L. Lu, B. Jacob, "DRAM Refresh Mechanisms, Penalties, and Trade-Offs", IEEE Trans. on Computers | 2026-07-29 |
| mukundan.txt | T2 | J. Mukundan et al., "Understanding and Mitigating Refresh Overheads in High-Density DDR4 DRAM Systems", ISCA/MICRO 2013 | 2026-07-29 |
| rtc_refresh.txt | T2 | "Refresh Triggered Computation (RTC)" — CNN 워크로드용 refresh 절감, O. Mutlu 등 (ACM TACO 계열) | 2026-07-29 |

