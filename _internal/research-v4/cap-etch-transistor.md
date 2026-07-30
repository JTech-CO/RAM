# DRAM 커패시터 HAR 식각과 셀 트랜지스터 공정
> 조사일: 2026-07-29 / 상태: 완료
> 조사 방식: 신규 웹 조사 (로컬 1차 자료 없음). 웹 검색 12회, WebFetch 5회.
> **총평: 이 주제는 3D NAND HAR과 달리 공개 정량 데이터가 극히 빈약합니다. 종횡비 핵심 수치는 T3 단일 출처 하나뿐이며, 세대별 추이는 확보하지 못했습니다. 이 사실 자체를 집필에 반영해야 합니다.**

---

## 1. 확인된 사실

### 1-A. 커패시터 HAR 식각 (최우선 항목)

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| **DRAM 커패시터 종횡비 (현행 선단)** | **"100:1에 접근(aspect ratios are approaching 100:1)"** | T3 | SemiAnalysis, "The Memory Wall: Past, Present, and Future of DRAM" (newsletter.semianalysis.com/p/the-memory-wall) | **단일 출처 · 세대 미특정.** 확인일 2026-07-29. 이 조사에서 확보한 유일한 DRAM 측 종횡비 수치 |
| 커패시터 높이 | **약 1,000 nm (≈1 µm)** | T3 | 동상 ("~1,000nm high") | 단일 출처 · 세대 미특정 |
| 커패시터 홀 직경 | **수십 nm ("only 10s of nm in diameter")** | T3 | 동상 | 단일 출처. **정확한 nm 값 아님.** 인용 시 반드시 "수십 nm 급"으로 |
| 셀 커패시턴스 (해당 서술 세대) | 6~7 fF | T3 | 동상 | v3의 "D1z/D1a 10 fF 미만, D1c 5~6 fF 전망"과 정합 |
| 갓 쓰인 셀의 저장 전자 수 | 약 40,000개 | T3 | 동상 ("about 40,000 electrons when freshly written") | 단일 출처. 감각을 주는 좋은 소재 |
| 비트라인 총 커패시턴스 | 30 fF 초과 → 셀 커패시턴스 대비 **약 5배 희석(5x dilution)** | T3 | 동상 | 단일 출처. v3의 `Vs ≈ Vcc/2 × Cc/(Cc+Cp)` 서술에 붙일 유일한 정량 근거 |
| 커패시터 식각 난점 (서술형) | 홀이 조밀하게 패킹되어 CD·오버레이 제어가 까다롭고, 더 깊이 파려면 **더 두꺼운 하드마스크**가 필요해 난도가 가중된다 | T3 | 동상 | 하드마스크 두께 문제는 AMAT 자료(아래)와 교차 확인됨 |
| storage node "고종횡비"의 공정 정의 | **종횡비 70 이상**을 고종횡비로 규정 | T1 (특허 명세) | 커패시터 하부전극 제조 특허(US8003480 계열) 검색 결과 | 세대·업체·출원연도 미상. 위 100:1과 **직접 비교 불가**. 문맥상 구세대 값일 가능성 |
| 몰드 재료 | 몰드층은 일반적으로 산화막('mold oxide'), storage node 형성 후 **wet dip-out으로 제거** | T1 (특허 명세) | 동상 | (a)의 핵심 — NAND와의 구조적 차이의 근원 |
| 커패시터 유전체 (현행) | AlO/ZrO 계, ZrO2(NbO)/Al2O3 나노라미네이트 | T2.5 | TechInsights, "DRAM Scaling Trend and Beyond" | |
| 커패시터 유전체 (차세대 후보) | STO(SrTiO₃) + Ru 전극, "EOT < 0.5 nm 가능성" | T2.5 | 동상 | **분석기관 전망 · 양산 아님.** 상태 명시 필수 |
| 커패시터 구조 전이 | 실린더형 → 준실린더형(quasi-cylindrical), COB(capacitor-on-bitline) | T2.5 | 동상 | v3와 일치 |
| MESH supporter (원조 사례) | Si₃N₄ 재질 supporter mesh로 **lean-free** 적층 커패시터 구현. **80 nm COB DRAM**에서 실증, 셀 커패시턴스 **30 fF/cell 초과**, MIS 유전체 **EOT 2.3 nm** | T2 | IEDM 2004, "A Mechanically Enhanced Storage node for virtually unlimited Height (MESH) capacitor aiming at sub 70nm DRAMs" (IEEE Xplore 1419067) | v3는 "2004년 70 nm 세대"로 적었으나 **논문은 sub-70nm를 목표로 하되 실증은 80 nm COB DRAM** — 정정 권장 |
| 커패시터 붕괴 해석 모델 | beam-shell 모델로 **supporter crack / capacitor bending / storage-poly fracture** 3종 파괴 모드를 시뮬레이션 | T2 | SISPAD 2013, "The Novel Stress Simulation Method for Contemporary DRAM Capacitor Arrays" (IEEE 6650665) | 결함 유형 분류의 1차 근거 |
| 하부전극 응력 보상 | TiON/TiN 다층 스택 조성 엔지니어링으로 **post-etch stress** 보상 | T3 (TEL 2019 자료를 2차 인용) | 검색 경유 요약 | 원문 미확인 |
| **AMAT Sym3 + DRACO 하드마스크 성과** | 커패시터 식각용 **하드마스크 두께 30% 감소**, **커패시터 홀 직경 산포 50% 감소**, **결함 100배 이상 감소** | T1 | Applied Materials 보도자료 "Introduces Materials Engineering Solutions for DRAM Scaling" (2021-05-05) | **DRAM 커패시터 식각에 대한 유일한 정량 장비 성과치.** 2021년 발표 — 세대는 명시 안 됨 |
| AMAT Sym3 Y 용도 | RF 펄싱으로 선택비·깊이·프로파일 제어. **3D NAND, DRAM, 로직** 모두 대상 | T1 | Applied Materials, Centris Sym3 Y 소개 | Sym3는 2015년 최초 출시, 챔버 5,000대 이상 출하 |
| **극저온(cryo) 식각의 DRAM 커패시터 적용 여부** | **Lam 공식 Cryogenic Etching 페이지는 3D NAND 채널 홀만 명시. DRAM 커패시터 언급 없음** | T1 | lamresearch.com/products/our-solutions/cryogenic-etching/ (2026-07-29 확인) | **"적용된다"는 근거도 "적용 안 된다"는 근거도 없음.** 4장 참조 |
| Lam Cryo 3.0 (3D NAND) | 2024-07-31 발표. 폭 대비 **50배 이상 깊은** 메모리 채널, **프로파일 편차 0.1% 미만**, 기존 유전체 공정 대비 **식각률 2배 이상**. Flex®/Vantex®(Sense.i® 플랫폼) 호환 | T1 | Lam Research 보도자료 (2024-07-31) | **v3의 "2.5배"와 다름** — 5장 참조 |
| Lam 3D DRAM 전망 | 3D DRAM에서는 수직성이 더 극단화 — **10 µm 스택에서 프로파일 틸트 0.1도 미만** 요구 | T1 (검색 스니펫 경유, 원문 직접 확인 실패) | Lam newsroom, "How Deposition and Etch Are Reshaping Chips for the AI Era" | **v3의 "10 µm 깊이에서 CD 편차 0.1% 미만"과 다른 명제** — 5장 참조 |

### 1-B. 셀 트랜지스터·컨택

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 현행 셀 액티브 구조 | "bulky saddle fin-type active" | T2.5 | TechInsights, "DRAM Scaling Trend and Beyond" | 세대 미특정 |
| 현행 셀 통합 요소 일람 | 6F² + **BCAT** + bulky saddle fin active + **storage node landing pad and plug** + **BL air-gap spacer** + 실린더/준실린더 커패시터 + COB + AlO/ZrO 유전체 | T2.5 | 동상 | 셀 공정 전체를 한 문장에 담을 수 있는 출처 |
| bWL + saddle fin의 역할 | 매몰 금속 워드라인 + saddle(bulky fin) 채널이 **3x/2x nm 액세스 트랜지스터 스케일링**을 가능케 한 핵심. Vth 제어가 양호하고 누설이 극히 낮음 | T3 | EE Times, "Chipmakers turn to new process for sub-nm DRAM cells" / semiengineering | 세대 표현이 "3x/2x nm", "20 nm급"으로 혼재 |
| Saddle Fin 형성 시점 | **워드라인(WL) 식각 단계에서, WL 금속 증착 직전**에 형성되며 셀 워드라인 **아래**에 위치 | T1 | Lam Research newsroom, "Improving DRAM Device Performance Through Saddle Fin Process Optimization" | 공정 순서 서술의 핵심 근거 |
| Saddle Fin + BCAT의 목적 | **채널 길이 증가 → 단채널 효과(SCE) 억제 → 리텐션(데이터 보존 시간) 증가** | T1 | 동상 | |
| **bWL 공정 순서** | ① 마스크 패터닝 → 기판에 **게이트 트렌치 식각** ② **게이트 산화막** 형성 ③ **TiN 또는 WN 배리어**를 ALD/CVD 증착 ④ **W를 CVD로 충전** ⑤ **CMP 평탄화** ⑥ **W/TiN 에치백(recess)** — 트렌치를 부분적으로만 채운 상태로 남김 | T1 (특허 명세 다수) | US8309448, US12022650 등 buried word line 특허군 | 워드라인은 **TiN/W 2층 구조** |
| BWL DWMG (dual work-function metal gate) | 매몰 워드라인 게이트를 **워크펑션이 서로 다른 구간으로 분할** → 채널 방향 전계를 정밀 제어 → **GIDL 감소**, 성능 유지 | T1 | Lam Research newsroom, "Reducing Leakage Current in DRAM Using Dual Work-Function Metal Gate (DWMG) Structures" | **정량 개선치 미확보** |
| 워크펑션층의 리텐션 효과 | bWL에 워크펑션층을 두면 **off-state 누설 억제 → 리텐션·리프레시 특성 개선** | T1 (특허 명세) | buried gate structure 특허군 | 정성 서술만 |
| **DRAM에서 HKMG의 적용 위치** | **주변(peripheral)/코어 트랜지스터**. 셀 트랜지스터가 아님 | T2 | IEEE 10719458 "Integration of High-k Metal Gate (HKMG) to Core/Peri…" 및 SK하이닉스 IEDM 발표("high-k/metal gate technology devised for the peripheral transistors in the DRAM") | **집필 시 가장 자주 틀리는 지점.** 6장 규칙 참조 |
| HKMG core/peri 통합 5대 신뢰성 난제 | ① storage node contact recess 산포 열화 ② HKMG 잔류물에 의한 **셀 오염** ③ gate-to-gate bridge ④ **산소 침투로 인한 Vth 불안정** ⑤ HKMG **time-zero 절연파괴** | T2 | IEEE 10719458 | ①이 storage node contact와 직접 얽힌다는 점이 흥미로운 대목 |
| HKMG Vth 제어 기법 | 단일 TiN 금속 게이트 + **La₂O₃** + SiGe/Si epi 조합으로 Vth 제어 | T2 | IEEE 7409775, "Gate-first high-k/metal gate DRAM technology…" | 세대 미특정 |
| **비트라인 air spacer (삼성)** | BL 기생 커패시턴스 **34% 감소**, 항복전압 **30% 개선** | T2 (IEDM 2018 삼성 발표) — **확인 경로는 T3** | semiengineering 검색 결과가 IEDM 2018 삼성 논문을 인용 | **IEDM 2018 원논문 직접 미확인.** 인용 시 "IEDM 2018 삼성 발표(2차 인용)"으로 표기 권장 |
| 비트라인 airgap spacer (Lam 평가) | NON 스페이서 대비 **C_BL_NC 약 33% 개선** | T1 | Lam Research, "A Comparative Evaluation of DRAM bit-line spacer integration schemes" | 삼성 34%와 **독립 출처인데 값이 근접** — 상호 보강 |
| air spacer 도입 동기 | 셀 축소로 **BL 기생 커패시턴스(Cb) 증가 → BL 센싱 마진과 리프레시 시간 악화**. low-k 스페이서와 airgap 스페이서가 대안 | T1/T3 | Lam / semiengineering | |
| storage node contact(SNC)의 위상 | **COB 통합에서 가장 결정적인 문제.** 가장 깊고 종횡비가 높은 컨택이며 **셀 트랜지스터 접합까지 도달** | T1/T3 | SNC SAC 관련 특허·문헌 | "제곱 축소" 서술의 정성적 근거 |
| SNC 오버레이 마진 축소 | DRAM 축소에 따라 **COB 공정에서 SNC와 비트라인 사이 오버레이 마진이 축소 → 단락 위험** | T1 (특허 명세) | US11063049 등 self-aligning landing pad 특허군 | **"제곱으로 축소"라는 표현의 1차 출처는 확인 실패** (2·4장 참조) |
| 6F² 셀 SAC 요소 | maskless self-aligned buried strap node contact, STI, self-aligned poly-plug bit contact, W dual-damascene 2층 비트라인 배선 | T2 | ISSCC/IEDM급 "multigigabit DRAM technology with 6F2 open-bitline cell" | 구세대(멀티기가비트 초기) 사례 — 세대 명시 필수 |
| BCAT 시뮬레이션 게이트 길이 | **20 nm** 게이트 길이 BCAT 시뮬레이션·해석 | T2 | Micromachines 13(9), 1476, "Simulation Study: The Impact of Structural Variations on the Characteristics of a BCAT in DRAM" | 실제 양산 치수가 아니라 **시뮬레이션 조건** |
| Pass gate effect (워드라인 간 간섭) | BCAT에서 인접 워드라인이 셀에 미치는 **간섭 현상(pass gate effect)**이 존재하며, buried oxide 삽입으로 완화 가능 | T2 | Applied Sciences 14(22), 10348, "Mitigating Pass Gate Effect in BCAT Through Buried Oxide Integration" | row hammer와 **별개 현상**. 정량치 미확보 |

---

## 2. 구조·메커니즘 서술

### 2-1. DRAM 커패시터 HAR은 3D NAND 채널 홀 HAR과 무엇이 다른가 (핵심)

**뚫는 대상이 다릅니다.**

- **3D NAND 채널 홀**: 산화막/질화막이 수백 겹 교번한 **ONON 다층막**을 관통합니다. 층수가 곧 깊이이고, 식각 중 재료가 주기적으로 바뀌므로 화학·이온 조건이 층 경계마다 흔들립니다. 층수를 늘리면 깊이가 비례해 늘어나고, 이것이 "층수 → 종횡비" 로드맵이 성립하는 이유입니다.
- **DRAM 커패시터 홀**: **단일 조성의 몰드 산화막(mold oxide)** 을 관통합니다. 다만 몰드 적층 중간과 상부에 **Si₃N₄ supporter 층**이 몇 겹 끼어 있어, 그 구간에서만 선택비가 달라집니다. DRAM에는 "층수"라는 지표가 없고 **몰드 두께 = 커패시터 높이**가 직접 지표입니다.

**결정적 차이는 식각 이후에 있습니다.**

- 3D NAND 채널 홀은 뚫린 뒤 채널막·터널 절연막으로 **채워진 채 남습니다.** 구조가 주변 ONON에 계속 지지됩니다.
- DRAM 커패시터 홀은 **거푸집(mold)** 입니다. 홀을 뚫고 하부전극(TiN 등)을 컨포멀하게 입힌 뒤, **몰드 산화막 전체를 wet dip-out으로 녹여 버립니다.** 그러면 지름 수십 nm, 높이 1 µm 급의 얇은 실린더/필러 전극만 허공에 서 있게 됩니다.
- → **leaning(기울어짐)과 collapse(붕괴)는 DRAM 고유의 파괴 모드입니다.** NAND HAR 논의에는 이 항목이 없습니다. 반대로 NAND에서 크게 다뤄지는 twisting은 DRAM 문헌에서 상대적으로 덜 부각됩니다.
- 습식 제거 후 건조 과정의 **모세관력**이 인접 전극을 서로 끌어당기는 것이 leaning의 주요 물리 기구입니다.

**요구 프로파일도 다릅니다.** NAND 채널 홀은 상부-하부 CD 차이(테이퍼)가 어느 정도 허용되고 셀 특성 보정으로 흡수합니다. DRAM 커패시터는 CD가 곧 커패시턴스이므로, **홀 직경 산포가 셀 커패시턴스 산포 = 리텐션 산포**로 직결됩니다. AMAT가 자사 성과로 "홀 직경 산포 50% 감소"를 앞세우는 이유가 이것입니다 (T1).

### 2-2. supporter가 붕괴를 막는 시점 — 오해하기 쉬운 지점

supporter는 **식각 중에 홀을 붙잡는 것이 아닙니다.**

1. 몰드 산화막을 적층할 때 중간(중간 supporter)과 최상부(상부 supporter)에 Si₃N₄ 층을 끼워 넣습니다.
2. 몰드 전체를 관통하는 HAR 홀을 뚫습니다. (이때 supporter 층도 함께 뚫립니다.)
3. 하부전극을 증착합니다.
4. supporter 층에 **개구부(dip-out hole)** 를 별도로 패터닝합니다 — 습식 화학액이 몰드 산화막에 도달할 통로입니다.
5. 몰드 산화막만 선택적으로 녹여 냅니다(dip-out). Si₃N₄ supporter는 남습니다.
6. → **남은 supporter가 격자(mesh)처럼 인접 하부전극들을 수평으로 묶어 놓습니다.**

즉 supporter가 방어하는 것은 **몰드 제거 이후의 기계적 붕괴**이며, 식각 자체의 프로파일 결함(bowing 등)과는 별개 문제입니다. IEDM 2004 MESH 논문이 "virtually unlimited height"라고 주장할 수 있었던 것이 바로 이 분리 덕분입니다 — 높이 제약이 기계적 안정성에서 식각 능력으로 넘어갔습니다 (T2).

SISPAD 2013 응력 해석은 이 구조의 파괴 모드를 세 가지로 나눕니다: **supporter crack, capacitor bending, storage-poly fracture** (T2). 집필 시 "붕괴"를 뭉뚱그리지 말고 이 셋을 구분하면 정확합니다.

### 2-3. 셀 축소와 커패시터 깊이의 관계 — 정량 논리

**주의: 아래 유도는 조사자가 기본 물리식으로 계산한 것이며, 출처가 붙은 실측 수치가 아닙니다.**

실린더형 하부전극의 정전용량은
`C = ε₀ · ε_r · A / t_diel`, 여기서 측면 면적 `A ≈ π · D · H` (내벽만 쓸 때. 내·외벽 모두 쓰면 약 2배).

셀 피치가 계수 k(<1)로 축소되면 홀 직경 D도 대략 k배가 됩니다. 유전체(ε_r, t_diel)를 그대로 두고 **같은 C를 유지**하려면 H를 **1/k 배**로 키워야 합니다.
→ 종횡비 `AR = H/D` 는 `(1/k)/(k) = 1/k²`, 즉 **선폭 축소의 제곱으로 악화됩니다.**

구체적으로: 선폭을 0.7배로 줄이면 종횡비는 약 **2.04배**로 뛰어야 같은 커패시턴스가 유지됩니다. 한 세대에 2배씩 종횡비를 올리는 것은 물리적으로 불가능합니다.

**그래서 업계는 세 방향으로 나눠 부담을 흡수했습니다:**
1. **유전체 EOT 축소** — MIS EOT 2.3 nm(2004, MESH) → AlO/ZrO 계 → ZrO₂(NbO)/Al₂O₃ 나노라미네이트 → STO/Ru로 EOT 0.5 nm 미만 목표 (T2/T2.5). ε_r을 키워 A 감소를 보상.
2. **높이 증가** — 약 1 µm까지 (T3). 다만 1/k 배까지 따라가지는 못했습니다.
3. **커패시턴스 자체 인하** — 30 fF 유지 원칙을 포기하고 D1z/D1a에서 10 fF 미만, D1c에서 5~6 fF까지 (T2.5).

**즉 v3의 "결국 커패시턴스 자체를 낮추는 방향으로 선회" 서술의 정량적 근거는 "종횡비가 선폭의 제곱으로 악화되므로 높이로는 도저히 못 따라간다"는 것입니다.** 이것이 이 조사가 뒷받침하는 가장 중요한 논리 연결입니다.

**확인 실패: 세대별 커패시터 높이·직경 실측치가 없어 이 유도를 실제 D1x→D1b 데이터로 검증하지는 못했습니다.**

### 2-4. 결함 유형 정리

| 결함 | 발생 시점 | 기구 | DRAM/NAND |
|---|---|---|---|
| **leaning / collapse** | 몰드 dip-out 후 습식 건조 | 모세관력 + 세장비 과다 | **DRAM 고유** |
| **supporter crack** | dip-out 후 응력 | supporter 자체 파단 | DRAM |
| **capacitor bending** | dip-out 후 | 전극 좌굴 | DRAM |
| **storage-poly fracture** | dip-out 후 | 전극 재료 파괴 | DRAM |
| **bowing** | 식각 중, 홀 중상부 | 이온 산란·측벽 재증착 부족 → 중간 CD가 부풀어 인접 홀과 통함 | 양쪽 |
| **CD 균일도 / etch loading** | 식각 중 | 패턴 밀도 차이에 따른 식각률·깊이 편차 | 양쪽 (**DRAM에서 더 치명적** — CD가 곧 커패시턴스) |
| **twisting** | 식각 중, 심부 | 홀 중심축이 틀어짐 | 주로 NAND 문헌 |
| **post-etch stress** | 하부전극 증착 후 | TiN 막응력 → TiON/TiN 다층으로 보상 | DRAM |

### 2-5. 장비·기법

- **Applied Materials** — Centris Sym3 / Sym3 Y (2015년 최초 출시, 챔버 5,000대 이상). 고컨덕턴스 챔버로 부산물을 빠르게 배기해 프로파일을 제어. **DRACO® 하드마스크와 co-optimize** 하여 커패시터 식각 하드마스크 두께 30% 감소, 홀 직경 산포 50% 감소, 결함 100배 이상 감소 (T1, 2021-05-05).
- **Lam Research** — Flex®/Vantex® 유전체 식각. Vantex는 "현세대·차세대 NAND **및 DRAM**"을 대상으로 명시 (T1). 단, **Cryo 3.0 공식 페이지는 3D NAND 채널 홀만 언급**합니다.
- **Tokyo Electron** — 하부전극 조성 엔지니어링(TiON/TiN 다층)으로 post-etch stress 보상 (2019, T3 2차 인용).
- **Hitachi High-Tech** — DRAM 커패시터 식각 관련 공식 자료를 **확보하지 못했습니다.**

**극저온 식각의 DRAM 적용 여부 — 결론:** 2026-07-29 시점에 Lam의 공식 Cryogenic Etching 페이지와 Cryo 3.0 보도자료는 **3D NAND 채널 홀만** 적용처로 명시합니다. DRAM 커패시터 적용을 확인할 근거도, 부정할 근거도 확보하지 못했습니다. **"극저온 식각은 3D NAND 전용이다"라고 단정해서도 안 되고, "DRAM에도 쓰인다"고 써서도 안 됩니다.** 확인된 것은 "Lam이 공개적으로 내세우는 cryo 사례는 3D NAND뿐"이라는 사실뿐입니다.

### 2-6. 매몰 워드라인 (buried word line, bWL)

**왜 평면 게이트를 버렸나.** 평면 게이트에서는 (i) 워드라인이 표면에 있어 비트라인·컨택과 같은 층에서 혼잡하고 기생 커플링이 크며, (ii) 셀 면적이 8F² 이상을 요구하고, (iii) 노드가 줄면 채널 길이가 곧바로 짧아져 단채널 효과와 접합 누설이 급증합니다. DRAM 셀은 누설이 곧 리텐션이므로 이 세 번째가 치명적입니다.

**매몰형의 해법.** 활성 영역에 트렌치를 파고 게이트를 그 안에 넣습니다. 채널이 트렌치 벽을 따라 **U자로 돌아가므로 평면 투영 길이는 그대로인데 유효 채널 길이가 늘어납니다.** 표면에서 워드라인이 사라지므로 비트라인과의 커플링이 줄고, 6F² 셀 배치가 가능해집니다.

**공정 순서 (T1, 특허 명세 종합):**
1. 마스크 패터닝 → **게이트 트렌치 식각** (이 단계에서 saddle fin도 함께 형성 — 2-7 참조)
2. **게이트 절연막(gate oxide)** 형성
3. **TiN 또는 WN 배리어**를 ALD/CVD로 컨포멀 증착
4. **W를 CVD로 충전**
5. **CMP 평탄화** (W / TiN / 게이트 절연막을 트렌치 안에만 남김)
6. **W·TiN 에치백(recess)** → 트렌치를 **부분적으로만** 채운 상태로 남김
7. 상부 잔여 공간에 캡핑 절연막

**6번 리세스가 왜 필수인가.** 게이트 상단이 소스/드레인 접합과 수직으로 겹치면 게이트 전계가 접합에 걸려 **GIDL(Gate-Induced Drain Leakage)** 이 급증합니다. DRAM 셀에서 GIDL은 리텐션을 직접 갉아먹는 주범입니다. 반대로 너무 깊이 리세스하면 게이트가 채널을 다 덮지 못해 구동력이 죽습니다. **리세스 깊이는 GIDL과 구동력을 동시에 좌우하는 단일 노브**입니다.

**DWMG(dual work-function metal gate).** 리세스만으로는 한계가 있어, 워드라인 금속을 **워크펑션이 다른 두 구간으로 분할**합니다. 접합과 마주하는 상부 구간에는 GIDL을 억제하는 워크펑션을, 채널 중앙 하부에는 Vth·구동력에 맞춘 워크펑션을 배치해 채널 방향 전계를 정밀 제어합니다 (Lam, T1). 정량 개선치는 확보하지 못했습니다.

### 2-7. saddle-fin / RCAT / BCAT

용어가 혼용되므로 정리합니다.

- **RCAT (Recessed Channel Array Transistor)**: 채널을 리세스(홈)로 만들어 유효 채널 길이를 늘린 구조. 게이트가 완전히 매립되지는 않은 초기 형태.
- **BCAT (Buried Channel Array Transistor)**: 리세스 채널 + **게이트를 완전 매립**. bWL과 사실상 같은 것을 소자 관점에서 부르는 이름입니다. 현행 DRAM 셀의 표준 (T2.5).
- **Saddle-Fin (S-Fin)**: BCAT의 트렌치 바닥부에서 **STI 산화막을 더 깊이 깎아** 활성 실리콘이 fin처럼 돌출되게 만든 구조. 게이트가 fin의 **3면(안장처럼)** 을 감쌉니다. 게이트 제어력이 올라가 같은 off-current에서 on-current가 크고 Vth 산포가 작아집니다.

**형성 시점이 중요합니다.** saddle fin은 **워드라인 트렌치 식각 단계에서, 워드라인 금속 증착 직전**에 만들어지며 셀 워드라인 **아래**에 위치합니다 (Lam, T1). 즉 별도 마스크 공정이 아니라 bWL 트렌치 식각의 연장선입니다.

**목적은 하나로 수렴합니다: 채널 길이를 늘려 단채널 효과를 억제하고 리텐션을 확보한다** (Lam, T1).

**채택 세대**: "bWL + saddle 채널이 3x/2x nm 액세스 트랜지스터 스케일링의 핵심"(T3), "20 nm급 셀 스케일링을 가능케 한 신기술"(T3), 현행 선단은 "bulky saddle fin-type active"(T2.5). **업체별·세대별 최초 채택 연도는 확인 실패.**

**BCAT의 부작용 — pass gate effect**: 인접 워드라인이 셀 트랜지스터에 간섭을 일으켜 누설을 늘리는 현상이 보고됩니다. buried oxide 삽입으로 완화 가능 (T2). **row hammer와는 별개의 정적 간섭 현상**이므로 혼동하지 마십시오.

### 2-8. HKMG와 워크펑션 엔지니어링 — DRAM에서의 실제 역할

**가장 흔한 오해를 먼저 교정합니다: DRAM에서 HKMG는 셀 트랜지스터가 아니라 주변(peri)/코어 트랜지스터에 씁니다.**

근거: IEEE 논문 제목 자체가 "**Integration of High-k Metal Gate (HKMG) to Core/Peri** …"이고 (T2), SK하이닉스 IEDM 발표도 "DRAM의 **peripheral transistors**를 위해 고안된 high-k/metal gate 기술"로 소개됩니다 (T3 2차 인용).

**왜 주변회로에 필요한가.** 주변회로(센스앰프 드라이버, 워드라인 드라이버, I/O)는 로직에 준하는 속도·저전력을 요구받습니다. 폴리실리콘 게이트는 **poly depletion** 때문에 EOT를 더 줄일 수 없고, 도핑으로 Vth를 맞추는 방식은 산포가 큽니다. HKMG는 (i) high-k로 물리 두께를 유지한 채 EOT를 줄이고, (ii) **금속의 워크펑션으로 Vth를 직접 설정**합니다. 구체 기법으로 단일 TiN 게이트 + La₂O₃ + SiGe/Si epi 조합이 보고됩니다 (T2).

**셀 쪽 "워크펑션 엔지니어링"은 이것과 별개입니다.** 셀에서는 매몰 워드라인 금속(TiN/W)의 워크펑션 — 특히 DWMG로 구간을 나눈 워크펑션 — 이 GIDL과 Vth를 조절합니다. **같은 "워크펑션"이라는 단어가 서로 다른 두 곳에서 쓰인다는 점을 집필 시 반드시 분리하십시오.**

**HKMG 통합의 5대 신뢰성 난제** (T2): ① storage node contact recess 산포 열화 ② HKMG 잔류물에 의한 **셀 오염** ③ gate-to-gate bridge ④ 산소 침투로 인한 Vth 불안정 ⑤ HKMG time-zero 절연파괴. — ①이 storage node contact와 얽힌다는 점이 중요합니다. **peri에 HKMG를 넣으면 셀의 SNC 공정 마진이 영향을 받습니다.** 주변회로 개선이 셀 공정에 되돌아와 부담을 주는 구조입니다.

### 2-9. storage node contact (SNC)와 self-aligned contact

**구조.** 현행 DRAM은 COB(capacitor-over-bitline)입니다. 커패시터가 비트라인 **위**에 있으므로, 커패시터 하부전극에서 셀 트랜지스터의 저장 노드 접합까지 내려가는 컨택이 **비트라인들 사이를 통과**해야 합니다. 그래서 SNC는 **셀 영역에서 가장 깊고 종횡비가 높은 컨택**이며, 문헌은 이를 "COB DRAM 통합에서 가장 결정적인 문제"로 규정합니다 (T1/T3).

**self-aligned contact(SAC)의 원리.** 비트라인 상부와 측벽을 질화막(Si₃N₄)으로 완전히 감쌉니다. 그 위 층간절연막(산화막)에 컨택 홀을 뚫을 때 **산화막 대 질화막 선택비가 매우 높은 식각**을 씁니다. 그러면 컨택 홀이 비트라인 쪽으로 다소 어긋나 정렬되어도, 식각이 질화막에서 멈추므로 비트라인에 닿지 않고 **자동으로 비트라인 사이 공간에 정렬**됩니다. 리소그래피 오버레이 정밀도가 아니라 **선택비**가 정렬을 보장하는 것이 핵심입니다.

**landing pad.** SNC 위에 지그재그로 배치한 패드를 한 층 더 둡니다. 커패시터 하부전극(육각 밀집 배열)과 SNC(비트라인 사이 배열)의 격자가 서로 다르므로, 패드가 그 사이의 정렬 마진을 흡수합니다. TechInsights는 현행 셀 구성 요소로 "storage node landing pad and plug"를 명시합니다 (T2.5).

**"개구 마진이 셀 CD에 대해 제곱으로 축소된다"의 정량 근거.**
**주의: 아래는 조사자가 기하로 유도한 것이며, 이 표현의 1차 출처는 확인하지 못했습니다.**
컨택 개구는 2차원 면적이므로 선형 CD가 k배 줄면 면적은 **k²배**로 줄어듭니다. 그런데 개구를 잠식하는 항 — 비트라인 스페이서 두께, 오버레이 오차, 식각 CD 산포 — 은 **선형으로만** 줄거나(스페이서) **거의 줄지 않습니다**(오버레이는 노광기 성능에 묶임). 유효 개구는 대략
`A_eff ≈ (CD − 2·t_spacer − Δ_overlay)²`
형태이므로, 괄호 안이 0에 가까워질수록 **면적은 제곱으로 급격히 소멸**합니다. 이것이 "제곱으로 축소"의 기하학적 내용입니다.
확인된 것은 **정성적 명제뿐**입니다: "DRAM이 축소되면서 COB 공정의 SNC-비트라인 오버레이 마진이 줄어 단락 가능성이 생긴다" (T1, 특허 명세).

**air spacer가 여기서 다시 등장합니다.** 비트라인 스페이서를 공기로 바꾸면 유전율이 1로 떨어져 BL–SNC 기생 커패시턴스가 크게 줍니다(34% / 33%, 위 표). 그러나 스페이서가 물리적으로 비어 있으면 **SNC 식각·CMP 중 비트라인 구조를 지탱할 것이 없어집니다.** air spacer의 난이도는 유전율이 아니라 **구조 지지와 공정 순서**에 있습니다. Lam이 "spacer integration scheme 비교 평가"라는 제목으로 별도 문서를 낸 이유가 이것입니다.

### 2-10. 셀 트랜지스터 off-current와 리텐션

셀은 리프레시 주기 동안 저장 전하를 유지해야 합니다. 누설 경로는 네 가지입니다: ① 접합(junction) 누설 ② 서브스레숄드 off-current ③ **GIDL** ④ 게이트 유전체 터널링.

**감각을 위한 계산 (조사자 유도, 출처 있는 수치 아님):**
저장 전자 약 40,000개(T3) × 1.6×10⁻¹⁹ C ≈ **6.4×10⁻¹⁵ C**. 이 전하가 64 ms 동안 전부 새 나가는 누설 전류는 `6.4e-15 / 0.064 ≈ 1.0×10⁻¹³ A = 0.1 pA`. 실제로는 전하의 일부만 잃어도 센싱이 실패하므로, **셀당 총 누설은 0.1 pA를 크게 밑도는 fA~수십 fA 수준이어야 합니다.** — 이 수준의 누설 스펙 실측치는 확보하지 못했습니다.

구조가 각 항을 어떻게 막는지는 앞 절과 연결됩니다.
- **② 서브스레숄드 off-current** → BCAT/saddle fin이 유효 채널 길이를 늘려 억제. 이것이 "채널 길이 증가 → SCE 억제 → 리텐션 증가"라는 Lam의 인과 서술(T1)의 내용입니다.
- **③ GIDL** → 워드라인 리세스 깊이 + DWMG 워크펑션 분할로 억제 (T1).
- **인접 워드라인 간섭(pass gate effect)** → buried oxide 삽입으로 완화 (T2).

여기에 커패시터 쪽 사정이 겹칩니다. 셀 커패시턴스가 10 fF 미만으로 내려가면(T2.5) **같은 누설 전류에서도 전압 강하가 빨라져** 리텐션 요구가 더 가혹해집니다. **커패시터 HAR 식각과 셀 트랜지스터 누설은 리텐션이라는 하나의 예산을 나눠 쓰는 관계**이며, 이것이 두 주제를 한 장에 묶어야 하는 이유입니다.

---

## 3. 상충·불확실

| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| DRAM 커패시터 종횡비 | **100:1 접근** (T3, SemiAnalysis) | **70 이상을 HAR로 정의** (T1, 특허 명세) | **양쪽 기록.** 특허는 출원 연도·세대가 불명이라 구세대 값일 가능성이 큼. 시계열 비교로 쓰지 마십시오 |
| Lam cryo 식각률 개선 | **2배 이상** (T1, Lam 보도자료 2024-07-31, 3D NAND 문맥) | **약 2.5배** (T1, Lam newsroom 블로그, 3D DRAM 문맥) | 서로 다른 문서의 다른 문맥. **v3는 2.5배만 채택했음** — 보도자료 값(2배 이상)을 병기 권장 |
| Lam의 10 µm 관련 사양 | **프로파일 편차 0.1% 미만** (Cryo 3.0 보도자료, 깊이 조건 명시 없음) | **10 µm 스택에서 프로파일 틸트 0.1도 미만** (newsroom 3D DRAM 문맥) | **서로 다른 명제.** "0.1%"(CD 편차)와 "0.1도"(틸트)는 단위도 대상도 다름. v3의 "10 µm 깊이에서 CD 편차 0.1% 미만"은 **두 출처를 뒤섞었을 가능성** |
| 3D NAND 100:1 도달 시점 | v3: "1,000층에서 100:1 접근" | JJAP 리뷰(T2): "수백 층 ONON, 약 100 nm 홀 → 종횡비 이미 100:1 초과" | **상충.** JJAP 쪽은 "수백 층"에서 이미 100:1 초과라고 서술. 5장 참조 |
| MESH capacitor 세대 | v3: "2004년 **70 nm** 세대, 30 fF" | 원논문: "**sub-70nm를 겨냥**", 실증은 "**80 nm** COB DRAM", "30 fF/cell **초과**" | **정정 권장.** "2004년 IEDM, 80 nm COB DRAM에서 실증, sub-70nm 대응 목표"가 정확 |
| air spacer 개선폭 | 삼성 IEDM 2018: **34% 감소** | Lam 평가: NON 대비 **약 33% 개선** | **상충 아님.** 독립 출처가 근접한 값을 보고 — 상호 보강으로 서술 가능. 단 측정 대상(BL 총 커패시턴스 vs C_BL_NC)이 다를 수 있으므로 "30% 초반대"로 뭉뚱그리는 것이 안전 |

---

## 4. 확인 실패 항목 (근거를 확보하지 못한 것)

**(a) 커패시터 HAR — 실패가 많습니다. 이것이 이 조사의 가장 중요한 결과입니다.**

1. **DRAM 커패시터 종횡비의 세대별 추이.** 3D NAND처럼 "96층 50:1 → 400층 60:1 → 1,000층 100:1" 식으로 대응시킬 수 있는 **DRAM 측 세대별 표를 만들 공개 데이터가 없습니다.** D1x/D1y/D1z/D1a/D1b/D1c 각각의 종횡비를 명시한 T0~T2.5 출처를 찾지 못했습니다. 확보한 것은 세대 미특정 T3 단일 값 "100:1 접근"뿐입니다.
2. **커패시터 홀 직경의 구체 nm 값.** "수십 nm"만 확보. 세대별 직경 실측치 없음.
3. **커패시터 깊이의 세대별 실측치.** "약 1,000 nm"만 확보, 세대 미특정.
4. **극저온 식각의 DRAM 커패시터 적용 여부.** Lam 공식 자료는 3D NAND만 명시. 적용·미적용 어느 쪽도 확인 불가.
5. **Hitachi High-Tech의 DRAM 커패시터 식각 관련 공식 자료.**
6. **Tokyo Electron의 DRAM 커패시터 식각 장비 명칭·성능 수치.** (TEL 관련은 하부전극 응력 보상 건만, 그것도 2차 인용)
7. **supporter 층의 두께·층수·재질 두께 실측치.** Si₃N₄라는 재질과 mesh 구조만 확인.
8. **leaning/collapse 발생률, 임계 종횡비, 임계 세장비 수치.**
9. **몰드 산화막 총 두께의 세대별 값.**
10. **DRAM HAR 식각의 식각률·스루풋 수치.** (3D NAND는 Lam 자료로 상대값이 나오지만 DRAM은 없음)

**(b) 셀 트랜지스터·컨택**

11. **HKMG 세대별 채택 정보.** "삼성 1x, 마이크론 1z, SK하이닉스 1a"라는 서술을 발견했으나 출처가 **SemiWiki 포럼(T4)** 입니다. **수치·세대 인용 금지.** T1/T2.5 재확인이 필요합니다.
12. **air spacer 양산 채택 업체·세대.** 삼성 IEDM 2018 발표는 확인했으나 어느 양산 세대부터 적용됐는지 미확인. TechInsights가 "BL air-gap spacer"를 현행 구성 요소로 명시하지만 **어느 업체의 어느 세대인지 특정하지 않았습니다.**
13. **삼성 IEDM 2018 air spacer 원논문 직접 확인 실패** (2차 인용 상태).
14. **"storage node contact 개구 마진이 셀 CD에 대해 제곱으로 축소된다"는 표현의 1차 출처.** 기하학적으로 자명하나, 이 문장을 그대로 담은 T0~T2.5 출처는 찾지 못했습니다.
15. **비트라인 저항 실측치** (Ω/셀, Ω/µm 등). 재질(W dual-damascene)만 확인.
16. **셀 트랜지스터 off-current 실측 스펙** (fA/cell).
17. **saddle-fin / RCAT의 업체별·세대별 최초 채택 연도.**
18. **DWMG의 GIDL 감소 정량치.**
19. **워드라인 리세스 깊이의 구체 nm 값.**
20. **셀 트랜지스터 게이트 길이 실측치.** (BCAT 20 nm는 **시뮬레이션 조건**이지 양산 치수가 아님)

---

## 5. 기존 소스 팩(v3)과의 충돌

1. **[정정 권장] MESH capacitor 세대.** v3 139행 "2004년 70 nm 세대 / 30 fF". 원논문(IEDM 2004)은 **sub-70nm를 목표**로 하되 실증은 **80 nm COB DRAM**, 값은 "30 fF/cell **초과**", MIS 유전체 **EOT 2.3 nm**. → "2004년 IEDM, 80 nm COB DRAM 실증, 30 fF/cell 초과"로 정정 권장.

2. **[혼합 의심] Lam Cryo 3.0 수치.** v3 562행 "기존 HAR 대비 식각률 2.5배, 프로파일 정밀도 2배. 10 µm 깊이에서 CD 편차 0.1% 미만".
   - Lam **보도자료(2024-07-31)**: "식각률 **2배 이상**", "프로파일 편차 **0.1% 미만**", "폭 대비 **50배 이상** 깊은 채널". 깊이 조건 명시 없음.
   - Lam **newsroom 블로그**(3D DRAM 문맥): "cryo가 **약 2.5배** 빠름", "**10 µm 스택**에서 프로파일 **틸트 0.1도 미만**".
   - → v3는 두 문서의 서로 다른 수치를 하나의 문장으로 합친 것으로 보입니다. **"2.5배"와 "10 µm"와 "0.1%"는 같은 출처의 같은 조건이 아닙니다.** 또한 "프로파일 정밀도 2배"의 출처는 이번 조사에서 확인하지 못했습니다.

3. **[상충] 3D NAND 종횡비 도달 시점.** v3 413·554행 "96층 약 50:1 → 400층 60:1 초과 → **1,000층 100:1 접근**". 그러나 JJAP 리뷰(T2, IOPscience 10.35848/1347-4065/accbc7)는 **"수백 층 ONON을 약 100 nm 홀로 패터닝 → 종횡비가 이미 100:1을 넘는다"**고 서술합니다. → **"100:1은 1,000층에서 도달"이라는 v3 서술과 어긋납니다.** 양쪽을 병기하거나, v3 값의 출처를 재확인해야 합니다. (홀 직경 기준을 상부 CD로 잡느냐 최소 CD로 잡느냐에 따라 종횡비가 달라지는 점이 원인일 수 있습니다.)

4. **[보강, 충돌 아님] v3 146행 "게이트 워크펑션 엔지니어링, HKMG"** — 용어만 나열되어 있던 부분에 대해, 이번 조사로 **HKMG는 peri/코어용, 워크펑션 엔지니어링(DWMG)은 셀 bWL용**이라는 분리가 확인되었습니다. v3 서술은 틀리지 않았으나 **둘을 같은 층위로 나열해 오해를 부를 수 있습니다.**

5. **[보강, 충돌 아님] v3 186행 "storage node contact 면적이 셀 CD에 대해 제곱으로 축소"** — 정성 명제(COB에서 SNC-BL 오버레이 마진 축소 → 단락 위험)는 T1 특허 명세로 확인됐으나, **"제곱"이라는 표현의 1차 출처는 확인 실패**입니다. 서술은 유지하되 "기하학적으로" 같은 완충어를 붙이는 편이 안전합니다.

6. **[보강] v3 145행 "결국 커패시턴스 자체를 낮추는 방향으로 선회"** — 이번 조사의 2-3절이 이 서술의 정량 논리(종횡비가 선폭 축소의 제곱으로 악화)를 제공합니다. 다만 **이 유도는 조사자 계산이며 출처 있는 수치가 아닙니다.**

---

## 6. 집필 시 주의 (서술 규칙 제안)

**규칙 1 — DRAM 종횡비를 3D NAND처럼 세대별로 나열하지 마십시오.**
확보된 것은 세대 미특정 T3 단일 값 "100:1 접근" 하나뿐입니다. "D1z는 60:1, D1b는 80:1" 같은 표를 만들면 그것은 창작입니다. **"현행 선단 DRAM 커패시터의 종횡비는 100:1에 접근하는 것으로 알려져 있다(T3, 단일 출처)"** 가 쓸 수 있는 최대치입니다.

**규칙 2 — DRAM HAR과 NAND HAR을 "같은 100:1"로 병치하지 마십시오.**
숫자가 비슷해도 **뚫는 대상(산화막 몰드 vs ONON 다층막)과 이후 운명(거푸집으로 제거 vs 채워진 채 잔존)이 근본적으로 다릅니다.** DRAM은 몰드를 녹인 뒤 남는 얇은 전극이 **넘어질(leaning) 수 있다**는 점이 NAND에는 없는 조건입니다. 병치하려면 반드시 이 차이를 먼저 쓰십시오.

**규칙 3 — supporter가 "식각 중 홀을 잡아준다"고 쓰지 마십시오.**
supporter는 **몰드 dip-out 이후** 하부전극을 수평으로 묶는 역할입니다. 시점을 틀리면 공정을 아는 독자가 즉시 알아챕니다.

**규칙 4 — DRAM에서 HKMG는 셀이 아니라 주변/코어 트랜지스터입니다.**
"DRAM 셀 트랜지스터에 HKMG를 적용해 성능을 올렸다"는 서술은 확인된 출처와 어긋납니다. 셀 쪽의 금속 워크펑션 이야기는 **매몰 워드라인의 DWMG**이지 HKMG가 아닙니다. 같은 "워크펑션"이라는 단어가 두 곳에서 다른 뜻으로 쓰인다는 점을 명시적으로 갈라 쓰십시오.

**규칙 5 — 극저온 식각을 DRAM 커패시터에 적용된다고 쓰지 마십시오. 동시에 "NAND 전용"이라고 단정하지도 마십시오.**
2026-07-29 기준 확인된 사실은 **"Lam이 공개적으로 제시하는 cryo 적용 사례는 3D NAND 채널 홀뿐"** 입니다. 이 표현 이상으로 나가면 근거가 없습니다.

**규칙 6 — air spacer의 어려움은 유전율이 아니라 구조입니다.**
"공기는 유전율이 1이라 좋다"에서 멈추면 왜 어려운지가 설명되지 않습니다. 스페이서를 비우면 **비트라인을 지탱할 것이 사라져 SNC 식각·CMP 중 붕괴 위험**이 생기고, 그래서 통합 순서(integration scheme)가 논쟁거리가 됩니다.

**규칙 7 — "제곱으로 축소" 같은 스케일링 논리는 유도임을 밝히십시오.**
2-3절(종횡비 ∝ 1/k²)과 2-9절(개구 면적 제곱 소멸)은 물리·기하로는 옳지만 **출처가 붙은 실측치가 아닙니다.** "계산하면", "기하학적으로" 같은 표현으로 유도임을 드러내면 문서 전체의 신뢰도가 올라갑니다.

**규칙 8 — 6~7 fF와 10 fF 미만은 같은 이야기의 다른 표현입니다.**
SemiAnalysis(T3)의 "6~7 fF"와 TechInsights(T2.5)의 "D1z/D1a는 10 fF 미만, 업계는 6~7 fF 이상 사수 목표"는 모순이 아닙니다. 함께 쓸 때는 **T2.5 쪽을 주 근거로** 삼으십시오.

**규칙 9 — RCAT / BCAT / saddle-fin을 나란히 놓고 "세대별 채택"을 단정하지 마십시오.**
채택 연도·업체를 특정할 근거를 확보하지 못했습니다. 확인된 것은 **구조적 계보(RCAT → BCAT → saddle-fin/BCAT)** 와 "bWL+saddle이 3x/2x nm 스케일링의 핵심"(T3), 현행이 "bulky saddle fin-type active"(T2.5)라는 것뿐입니다.

**규칙 10 — 커패시터와 셀 트랜지스터를 따로 쓰지 마십시오.**
둘은 **리텐션이라는 하나의 예산**을 나눠 씁니다. 커패시턴스가 10 fF 미만으로 내려간 만큼 트랜지스터 누설 요구가 가혹해지고, 그래서 saddle fin·DWMG·리세스 최적화가 필요해집니다. 이 인과가 이 장의 뼈대입니다.

---

## 7. 출처 목록

| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| newsletter.semianalysis.com/p/the-memory-wall | T3 | The Memory Wall: Past, Present, and Future of DRAM | 2026-07-29 |
| techinsights.com/blog/dram-scaling-trend-and-beyond | T2.5 | DRAM Scaling Trend and Beyond (Jeongdong Choe) | 2026-07-29 |
| lamresearch.com/products/our-solutions/cryogenic-etching/ | T1 | Cryogenic Etching (Lam Research 제품 페이지) | 2026-07-29 |
| investor.lamresearch.com/2024-07-31-… | T1 | Lam Research Introduces Lam Cryo™ 3.0 Cryogenic Etch Technology (2024-07-31 보도자료) | 2026-07-29 |
| newsroom.lamresearch.com/how-deposition-and-etch-are-reshaping-chips-for-the-ai-era | T1 | How Deposition and Etch Are Reshaping Chips for the AI Era | 2026-07-29 (검색 스니펫 경유, **원문 직접 확인 실패**) |
| newsroom.lamresearch.com/Improving-DRAM-Device-Performance-Through-Saddle-Fin-Process-Optimization | T1 | Improving DRAM Device Performance Through Saddle Fin Process Optimization | 2026-07-29 |
| newsroom.lamresearch.com/improving-dram-performance-using-dwmg | T1 | Reducing Leakage Current in DRAM Using Dual Work-Function Metal Gate (DWMG) Structures | 2026-07-29 |
| newsroom.lamresearch.com/A-Comparative-Evaluation-of-DRAM-bit-line-spacer-integration-schemes | T1 | A Comparative Evaluation of DRAM bit-line spacer integration schemes | 2026-07-29 |
| ir.appliedmaterials.com/news-releases/… (2021-05-05) | T1 | Applied Materials Introduces Materials Engineering Solutions for DRAM Scaling (DRACO® + Sym3®) | 2026-07-29 |
| appliedmaterials.com — Centris Sym3® Y / Sym3 챔버 블로그 | T1 | Sym3 Etch System 소개 · 10,000 Chambers and Counting | 2026-07-29 |
| ieeexplore.ieee.org/document/1419067 | T2 | IEDM 2004 — A Mechanically Enhanced Storage node for virtually unlimited Height (MESH) capacitor aiming at sub 70nm DRAMs | 2026-07-29 |
| ieeexplore.ieee.org/document/6650665 (in4.iue.tuwien.ac.at/pdfs/sispad2013/22-1.pdf) | T2 | SISPAD 2013 — The Novel Stress Simulation Method for Contemporary DRAM Capacitor Arrays | 2026-07-29 |
| iopscience.iop.org/article/10.35848/1347-4065/accbc7 | T2 | JJAP — Progress report on high aspect ratio patterning for memory devices (**3D NAND 전용, DRAM 데이터 없음**) | 2026-07-29 |
| ieeexplore.ieee.org/abstract/document/10719458 | T2 | Integration of High-k Metal Gate (HKMG) to Core/Peri … | 2026-07-29 |
| ieeexplore.ieee.org/document/7409775 | T2 | Gate-first high-k/metal gate DRAM technology for low power and high performance products | 2026-07-29 |
| mdpi.com/2072-666X/13/9/1476 | T2 | Micromachines — Simulation Study: Impact of Structural Variations on BCAT in DRAM | 2026-07-29 |
| mdpi.com/2076-3417/14/22/10348 | T2 | Applied Sciences — Mitigating Pass Gate Effect in BCAT Through Buried Oxide Integration | 2026-07-29 |
| ieeexplore.ieee.org/document/934982 (archive.vlsisymposium.org/01web/technology/tec_pdf/T10P3.pdf) | T2 | VLSI 2001 — DRAM scaling-down to 0.1 µm generation using bitline spacerless storage node SAC and RIR capacitor | 2026-07-29 (검색 경유) |
| ieeexplore.ieee.org/abstract/document/1309542 | T2 | Extending the capabilities of DRAM high aspect ratio trench etching | 2026-07-29 (제목만 확인, **본문 미확보**) |
| semiengineering.com/1xnm-dram-challenges/ , /a-comparative-evaluation-of-dram-bit-line-spacer-integration-schemes/ , /improving-dram-device-performance-through-saddle-fin-process-optimization/ | T3 | Semiconductor Engineering 기사군 | 2026-07-29 |
| semiengineering.com/dram-scaling-challenges-grow/ | T3 | DRAM Scaling Challenges Grow | 2026-07-29 (**HTTP 403 — 본문 확보 실패**) |
| eetimes.com/chipmakers-turn-to-new-process-for-sub-nm-dram-cells/ | T3 | Chipmakers turn to new process for sub-nm DRAM cells | 2026-07-29 (검색 경유) |
| US8003480 / US8309448 / US12022650 / US11063049 / US10923390 등 특허군 | T1 (특허 명세) | mold oxide dip-out, buried word line TiN/W, self-aligning landing pad, air gap spacer | 2026-07-29 (검색 경유, **개별 원문 미정독**) |
| semiwiki.com/forum/threads/hkmg-on-dram-nodes.17431/ | **T4** | HKMG on DRAM nodes (포럼) | 2026-07-29 — **수치·세대 인용 금지.** 4장 11번 항목의 근거 부재 표시용으로만 기재 |
