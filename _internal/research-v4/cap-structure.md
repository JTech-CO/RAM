# DRAM 커패시터 구조·재료·형성 공정
> 조사일: 2026-07-29 / 상태: 완료 (부분 — 세대별 종횡비·서포터 단수 최신값 확보 실패)
> 조사 방식: 신규 웹 조사(한국어/영어 병행). 로컬 1차 자료에는 커패시터 공정 층위 내용이 없어 사용하지 않음.
> **본 문서 전체에 적용되는 경고**: 아래 표의 상당수는 검색엔진이 반환한 논문 초록/블로그 요약(스니펫)에서 얻은 값입니다. 원문 PDF를 직접 열어 확인한 것은 표시했고, 나머지는 `스니펫`으로 표기했습니다. 주요 T1/T2.5 사이트(Applied Materials 블로그, SemiEngineering, TechInsights 일부, FMS 2025 프로시딩 PDF)는 **HTTP 403으로 직접 접근이 차단**되어 원문 대조를 하지 못했습니다.

---

## 1. 확인된 사실

### 1-1. 커패시터 형태·세대

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 커패시터 배치 아키텍처 | COB(Capacitor Over Bitline). 비트라인 배선 위에 수직으로 커패시터를 세움 | T3 | SemiEngineering "DRAM Scaling Challenges Grow" (스니펫, 2026-07-29) | 원문 403, 스니펫만 |
| 형태 변천 | 실린더형(cylinder) → 준실린더형(quasi-cylindrical) | T2.5 | TechInsights "DRAM Scaling Trend and Beyond" (직접 확인, 2026-07-29) | **v3에 이미 있음.** SK하이닉스 D1y/D1z, 삼성 D1z |
| OCS(One-Cylinder Stack/Storage) 형성 방식 | **이중 몰드(double-mold)** 로 형성. 1차 몰드에 스택형 하부 노드, 2차 몰드에 실린더형 상부 노드를 순차 형성하는 계열 | T1(특허) | US 6,700,153 / US 6,911,364 "One-cylinder stack capacitor and method for fabricating the same"; KR20040072086A (스니펫, 2026-07-29) | 특허는 청구 실시례이지 양산 채택 증거가 아님 |
| OCS 노드의 신뢰성 이슈 | 기가비트급 DRAM OCS 노드에서 **SILC(Stress-Induced Leakage Current)** 비교 연구가 존재 | T2 | IEEE Xplore doc 911914 "Stress-induced leakage current comparison of giga-bit scale DRAM capacitors with OCS node" (제목만 확인) | 수치 미확보 |
| 트렌치형 계보 | 딥 트렌치 커패시터는 0.11 μm 세대까지 스케일링 기법이 논문화됨 | T2 | "Novel techniques for scaling deep trench DRAM capacitor technology to 0.11 μm and beyond" (제목만 확인) | IBM/Infineon(Qimonda) 계보. 이후 스택형에 밀려 단종 |
| 필러(pillar)형 | **아직 전망 단계.** "업체들이 채택을 검토할 수 있는 혁신"으로 pillar cell capacitor가 열거됨 | T3 | SemiEngineering "DRAM Scaling Challenges Grow" (스니펫) | **양산 채택 세대 특정 실패.** 같은 문장에 high-k 상향, buried WL dual work-function, low-k spacer, air gap이 함께 열거 → 미래 옵션 목록 |

### 1-2. 지지대(supporter / lattice / mesh) — 본 조사의 핵심

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 지지대 개념의 논문급 원류 | **MESH** = Mechanically Enhanced Storage node for virtually unlimited Height. **SiN lattice(mesh)** 로 고종횡비 스토리지 노드의 기계적 불안정을 해결 | T2 | IEDM 2004, "A mechanically enhanced storage node for virtually unlimited height (MESH) capacitor aiming at sub 70nm DRAMs" (초록 스니펫, 2026-07-29) | 제목상 목표는 sub-70 nm, 초록상 **80 nm DRAM에 개발 적용** |
| MESH 셀 커패시턴스 | >30 fF/cell | T2 | 상동 | v3의 "2004년 70 nm 30 fF"와 정합 (세대 표기는 §5 참조) |
| MESH 유전체 EOT | **등가 산화막 두께 2.3 nm** (당시 conventional MIS 유전체) | T2, 단일 출처 | 상동 | 2004년 값. 현재 세대와 직접 비교 금지 |
| 지지대의 기능 정의 | "supporter는 커패시터 형성 중 스토리지 노드가 **붕괴(collapse)되거나 기울어지는(tilt)** 것을 막는다. 최소 1개의 개구(aperture)를 갖고 수평으로 연장되는 하나의 패턴일 수 있다" | T1(특허) | US 10,121,793 "Semiconductor device having supporters and method of manufacturing the same" (스니펫) | 개구(aperture)가 있어야 그 구멍으로 몰드 식각액이 들어간다 — 구조의 핵심 |
| 지지대 재료 | **SiN(질화규소)** 이 기본. 특허 청구항은 **SiN / SiCN(탄질화규소) / SiON(산질화규소)** 중 하나 이상 | T1(특허) | US 10,121,793 (스니펫) | 재료 선택지의 근거. 어느 업체가 실제로 무엇을 쓰는지는 미확인 |
| 다단 지지대 | 특허상 **upper supporter pattern**과 **intermediate supporter pattern**이 서로 다른 레벨에 배치됨. upper supporter는 유전체층 사이에 배치되고, 그 볼록한 라운드 측면이 스토리지 노드 전극 상부 측면에 접함 | T1(특허) | US 10,121,793 (스니펫) | **복수 supporter의 직접 근거.** 단, 특허 실시례 |
| 업체별 지지대 단수 | "삼성·SK하이닉스·엘피다는 **단일 질화막(single nitride layer)**, 마이크론·난야는 **이중 질화막(double nitride layers)** 으로 실린더형 커패시터를 지지한다" | T3, 단일 출처 | EE Times "Chipmakers turn to new process for sub-nm DRAM cells" (스니펫, 2026-07-29) | **연도 심각 주의.** 엘피다 언급 → 2013년 이전 기사로 추정. 현행 D1a–D1c 세대에 그대로 적용된다는 근거 없음 |
| 지지대 배치 밀도(일례) | 산소 원자 포함 지지막을 **스토리지 전극 4개당 지지막 1개**가 되도록 패터닝 | T1(특허) | KR20090043325A "반도체 메모리소자의 캐패시터 형성방법" (스니펫) | SiN이 아닌 **산소 함유(oxide 계열) 지지막** 실시례 — 재료가 SiN만은 아님을 보여줌 |
| 지지대의 공정상 요건 | "희생 패턴(sacrificial pattern)은 산화막 wet dip-out 중 쉽게 식각되지 않아 스토리지 노드 leaning 가능성을 낮춘다. dip-out 이후 수행되는 **건식 공정에서도** 인접 노드를 지지한다" | T1(특허) | US 8,048,757 / US 8,048,758 (스니펫) | 지지대는 wet 단계뿐 아니라 **후속 건조 단계까지** 버텨야 함 |

### 1-3. 공정 순서와 난제

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 몰드 제거(dip-out) 화학 | wet dip-out 시 **BOE 또는 HF 용액**을 산화막 식각액으로 사용. 식각액이 셀 영역 주변에 정의된 공간으로 **측면으로 흘러 들어가** 몰드 패턴을 제거 | T1(특허) | US 8,048,758 등 (스니펫) | 세부 농도·시간·벤더별 조성 미확인 |
| 세정 단계의 붕괴 | 캐패시터 구조가 얇고 높아지며 **collapse / leaning 결함**이 발생, 세정 공정 중요도 상승. **IPA 세정의 온도와 회전속도**가 패턴 붕괴 개선 인자 | T2 | 대한전자공학회 학술대회, "DRAM 캐패시터 공정 중 IPA 세정 시 온도와 회전속도에 따른 패턴 붕괴 개선 방법" (DBpia 서지·초록만, 2026-07-29) | **수치 미확보.** 국내 학회 발표라 접근 제한 |
| 몰드 홀 식각의 난도 | "DRAM에서 20 nm 이하로 스케일링하면 커패시터 피처 치수가 더 극단적이 되어 식각이 더 어려워진다" | T1 | Lam Research, Flex G Series 발표 자료 (2015, 스니펫) | 2015년 시점 진술. 연도 명시 필요 |
| 식각·증착 동시 난제 | "ALD와 건식 식각 **둘 다** 어렵다" (TechInsights Jeongdong Choe) | T2.5 | 검색 스니펫 (FMS 2025 프로시딩 PDF는 403으로 원문 미확인) | 인용 시 "원문 미확인" 병기 권장 |
| 몰드 패터닝 신소재 | **RuC(루테늄 카바이드)** 를 DRAM 커패시터 몰드 패터닝에 쓰는 특허 출원 존재 (2023-12-07 공개) | T1(특허) | US 출원 20230395391 "Ruthenium carbide for DRAM capacitor mold patterning" | 양산 채택 증거 아님 |

### 1-4. 유전체

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| ZAZ 도입 근거 | TiN/ZrO2/Al2O3/ZrO2/TiN 커패시터가 **HfO2 계열 유전체를 대체**하며 **45 nm 세대 DRAM**까지 확장 가능하도록 개발됨 | T2 | IEEE Xplore doc 1705205, "Development of New TiN/ZrO2/Al2O3/ZrO2/TiN Capacitors Extendable to 45nm Generation DRAMs Replacing HfO2 Based Dielectrics" (제목+스니펫) | **HfO2 → ZAZ 전환의 1차 근거.** 즉 HfO2가 먼저였고 ZrO2가 이겼다 |
| ZAZ 구조 정의 | 정방정(tetragonal) ZrO2 + 비정질 Al2O3의 조합 구조. 45 nm DRAM 적용 가능성을 이론 설계 후 실증 | T2 | 상동 계열 (스니펫) | |
| ZAZ EOT | **Tox,eq = 6.3 Å (0.63 nm)**, 누설전류 **< 1 fA/cell** | T2, 단일 출처, 스니펫 | 상동 (원문 미확인) | 스니펫에 "ZAZ TFT capacitors"라는 표기가 섞여 있어 원문 대조 필요 |
| ZAZ의 Al2O3 실체 | "ZAZ 막에서 Al2O3의 ALD 사이클 수는 **4–5 사이클 미만**이므로, 별개의 층이라기보다 **도판트(dopant)로 봐야 한다**" | T2 | Journal of Materials Research (Cambridge) 리뷰, "Recent advances in the understanding of high-k dielectric materials deposited by ALD for DRAM capacitor applications" (스니펫) | **집필 시 매우 중요.** "3층 샌드위치" 도해는 물리적으로 과장 |
| Al2O3의 역할 | 도판트 수준 농도의 Al2O3만으로도 ZrO2 내 캐리어 전도를 성공적으로 억제 → DRAM 커패시터에 적합한 누설 수준 확보 | T2 | 상동 | Al2O3는 유전율이 아니라 **누설 차단**용 |
| 현행 세대 유전체 조성 | **ZrO2(NbO)/Al2O3 기반 나노라미네이트** | T2.5, 단일 출처 | TechInsights "DRAM Scaling Trend and Beyond" (직접 확인) | **v3에 없는 신규 정보.** ZrO2에 **Nb 도핑**이 들어간다는 점. 세대 특정은 안 됨 |
| 현행 고유전율막 두께 | 7 nm → 6 nm로 축소 | T2.5 | 상동 | v3와 일치 |
| HZO 헤테로구조 | TiN/Al2O3/Hf0.5Zr0.5O2/Al2O3/TiN에서 **EOT 5.1 Å**, 저누설 | T2, 단일 출처 | Applied Physics Letters 122, 192903 (2023) — 제목·서지만 확인 | 연구 단계 |
| SrTiO3(STO) | ALD STO on TiN MIM에서 **EOT 0.5 nm**, 저누설 | T2, 단일 출처 | IEEE Xplore doc 4796852, "0.5 nm EOT low leakage ALD SrTiO3 on TiN MIM capacitors for DRAM applications" (제목) | 2008–2009년 학회. **17년 넘게 연구만 되고 양산 미진입** |
| STO 로드맵 | 향후 **STO + Ru 전극**, 스케일링 여지 **< 0.5 nm EOT** | T2.5 | TechInsights (직접 확인) | 벤더 목표/전망. 양산 확정 아님 |
| 필요 유전율 | 차세대 노드는 **k > 50** 재료가 필요 | T2.5 | TechInsights (직접 확인) | ZrO2(정방정) k≈40 수준을 넘어야 한다는 의미 |
| 루틸 TiO2 | 포스트-ZrO2 플랫폼 후보. **원리상 sub-0.3 nm EOT** 목표. 이원계 산화물이라 공정이 단순하고 ALD 전구체 선택지가 넓음 | T2 | ACS Applied Electronic Materials (2026), "Beyond ZrO2: Rutile TiO2 as the Dielectric Platform for Next-Generation DRAM Capacitors" (KIST) — 초록 스니펫 | **2026년 최신.** 목표치이지 실측 아님 |
| 루틸 TiO2 실증 | **MoO2 전극**이 루틸상 TiO2 성장을 유도, TiO2 유전율 **≈88**. MoO2 중간층이 EOT와 계면층 두께를 크게 감소. **귀금속 없는(noble-metal-free)** 경로 | T2 | Applied Surface Science (2026), "ALD of MoO2 using a tetravalent precursor for template-driven rutile TiO2 growth in DRAM capacitors" (초록 스니펫) | 루틸상 안정화에 **전극이 템플릿 역할**을 한다는 점이 핵심 |
| 루틸 TiO2 누설 | EOT **< 0.5 nm**에서 누설 **< 10⁻⁷ A/cm²** (각각 0.8 V, 0.6 V) | T2, 단일 출처, 스니펫 | 상동 계열 | 원문 미확인. 인용 시 주의 |

### 1-5. 전극

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 표준 전극 | **TiN**. MIM(Metal-Insulator-Metal) 구조로 상·하부 전극 모두 TiN | T2 | ZAZ 논문군, JMR 리뷰, ResearchGate "Top-view structure of DRAM capacitor using ZAZ with TiN electrodes" (스니펫) | 복수 출처 일치 |
| TiN ALD 화학 | TiCl4 + SiH4 + NH3로 **도핑 TiN**을 ALD 형성 | T1(특허) | 마이크론 US 11,289,487 / US 12,507,395 "Doped titanium nitride materials for DRAM capacitors" (스니펫) | SiH4가 들어가면 사실상 TiSiN 계열 |
| Nb | 유전체 쪽에 **NbO**로 들어감 (ZrO2(NbO)/Al2O3 나노라미네이트) | T2.5 | TechInsights | **주의: Nb는 전극이 아니라 ZrO2 도판트 맥락으로 확인됨.** 조사 지시의 "Nb 계열 전극"은 근거 미확보 |
| Ru | STO와 짝을 이루는 차세대 전극 후보 | T2.5 | TechInsights | 전망 |
| MoO2 | 루틸 TiO2용 전극/템플릿. 귀금속 대체 경로 | T2 | Applied Surface Science 2026 | 연구 단계 |
| 고일함수 전극 | DRAM 스케일링에 고일함수 전극 재료가 논의됨 | T3 | Eugenus, "DRAM Scaling with High Work Function Electrode Materials" (제목만) | 장비/소재사 블로그. 수치 미확보 |

### 1-6. 종횡비·커패시턴스

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 커패시터 물리 치수 | 높이 **약 1,000 nm**, 지름 **수십 nm**. 종횡비 **100:1에 접근** | T1(스니펫) | Applied Materials, "DRAM Scaling Requires New Materials Engineering Solutions" (원문 403, 검색 스니펫) | **세대 미특정.** AMAT 블로그의 게시 연도도 확인 실패 |
| 종횡비(다른 값) | 선단 DRAM 노드에서 **50:1 초과** | T3(스니펫) | SemiEngineering / TechInsights 계열 (원문 403) | §3 상충 참조 |
| ALD 검증된 종횡비 | Al2O3 막이 **AR ≈ 60**까지 우수한 step coverage로 ALD 증착됨 | T2 | Advanced Materials Technologies 리뷰 (2022) 계열 스니펫 | 실증된 상한의 감각치 |
| 셀 커패시턴스 (현행) | **D1z, D1a 세대는 10 fF/cell 미만** | T2.5 | TechInsights (직접 확인) | 세대 특정된 귀중한 값 |
| 셀 커패시턴스 (전망) | **D1c 세대는 6 또는 5 fF/cell까지 더 낮아질 수 있으나, 제조사는 6–7 fF 이상으로 유지하고 싶어 한다** | T2.5 | TechInsights (직접 확인) | **"낮아질 수 있다"는 전망 + "유지하고 싶다"는 의향.** 확정 실측 아님 |
| 셀 커패시턴스 (일반) | 6–7 fF 수준 | T1(스니펫) | Applied Materials | 위 TechInsights 값과 정합 |

### 1-7. ALD가 필수인 이유

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| CVD 대비 | "삼성의 초기 ALD 커패시터 연구가 **CVD의 step coverage로는 차세대 소자에 불충분**함을 확립했고, ALD의 등각성 우위는 수십 년에 걸쳐 소자 수준에서 검증됨" | T4 | PatSnap Eureka 블로그 (스니펫) | **T4 — 구조 이해용. 수치 인용 금지.** 원 논문 재확인 필요 |
| 원격 플라즈마 ALD | 리모트 플라즈마 ALD로 트렌치 내부에 **기판 방향과 무관하게** HfO2 균일 증착. 수직 증착에서도 트렌치 깊숙이 등각 피복 유지 | T2 | MDPI Nanomaterials 15(11), 783 (2025), "Deposition of HfO2 by Remote Plasma ALD for High-Aspect-Ratio Trench Capacitors in DRAM" | **step coverage % 수치 미확보** (본문 접근 실패) |
| 비등각 ALD(반대 방향 응용) | Lam Research 2025 특허 — 플라즈마 생성 억제제로 리세스 상부 개구 근처 증착을 선택적으로 억제하고 성막을 깊은 쪽으로 유도 | T1(특허) | Lam Research 특허 (스니펫) | 3D NAND 맥락. DRAM 커패시터에 직접 적용 근거는 없음 |

---

## 2. 구조·메커니즘 서술

**(a) 왜 지지대가 필요한가 — 기계 문제이지 전기 문제가 아니다**

스택형 커패시터는 셀 면적이 줄어드는 만큼 위로 자라서 표면적을 벌어왔습니다. 지름은 수십 nm, 높이는 1 μm에 가까워졌고, 종횡비는 수십:1을 넘습니다. 이 시점에서 커패시터의 한계는 전기가 아니라 **재료역학**입니다. 가늘고 긴 기둥은 옆으로 휘고(leaning), 이웃과 붙고(bridging), 뿌리에서 부러집니다(toppling/twisting/breaking).

지지대(supporter)는 이 기둥들을 서로 **가로로 묶어주는 격자**입니다. IEDM 2004의 MESH 커패시터가 이 개념을 명시적으로 이름 붙인 사례로, SiN 격자(lattice/mesh)로 스토리지 노드를 묶어 "사실상 무제한의 높이(virtually unlimited height)"를 얻겠다는 것이 논문 제목 그 자체입니다.

**(b) 지지대의 결정적 제약 — 구멍이 있어야 한다**

지지대는 단순한 판이 아닙니다. 특허 청구항이 일관되게 "적어도 하나의 개구(aperture)를 갖고 수평으로 연장되는 패턴"이라고 쓰는 이유가 있습니다. 몰드 산화막은 **지지대를 뚫고 지나가는 그 구멍을 통해서만** 식각액이 도달해 제거됩니다. 즉 지지대 설계는 두 요구의 정면 충돌입니다.

- 지지대 면적이 넓을수록 → 기계적으로 튼튼함, 그러나 몰드가 안 빠짐
- 개구가 클수록 → 몰드는 잘 빠짐, 그러나 기둥이 쓰러짐

이 충돌이 지지대를 **여러 층(다단)** 으로 나누게 만드는 동인입니다. 한 층당 개구를 충분히 크게 유지하면서도, 높이 방향으로 여러 지점에서 잡아주면 좌굴 길이가 짧아집니다.

**(c) 다단 지지대 — 확인된 것과 확인 안 된 것**

특허 수준에서는 **upper supporter + intermediate supporter가 서로 다른 레벨에 놓이는** 구조가 명확히 기술되어 있습니다(US 10,121,793). 재료는 SiN이 기본이고, SiCN·SiON도 청구 범위에 들어 있습니다. 별도 계열 특허에는 산소 함유 지지막을 스토리지 전극 4개당 1개 배치하는 실시례도 있습니다 — 지지대가 반드시 질화막만은 아니라는 뜻입니다.

반면 **"어느 업체가 지금 몇 단을 쓰는가"** 는 신뢰할 만한 최신 근거를 확보하지 못했습니다. 유일하게 찾은 업체별 비교는 EE Times 기사의 "삼성·SK하이닉스·엘피다=단일 질화막 / 마이크론·난야=이중 질화막"인데, **엘피다가 현존 업체로 서술된다는 점에서 2013년 이전 기사**로 봐야 합니다. 현행 D1a–D1c에 그대로 옮기면 안 됩니다.

**(d) 공정 순서 — 지시된 순서를 근거로 재구성**

1. 스토리지 노드 컨택 형성 (하부 층간절연막)
2. **식각 정지막(etch stop, SiN 계열) + 몰드 산화막 적층.** 다단 지지대를 쓰면 몰드 산화막 사이사이에 지지막(SiN)을 끼워 **산화막/질화막/산화막/질화막** 다층 스택으로 쌓습니다.
3. **홀 식각(HAR etch).** 100:1에 접근하는 홀을 위에서 아래까지 CD 변동 없이 뚫어야 합니다. 20 nm 이하 스케일링에서 이 식각이 급격히 어려워진다는 것이 Lam의 진술입니다. 난제: bowing(중간이 불룩), twisting(홀이 휨), 바닥 미개구(etch stop 미관통).
4. **하부 전극 증착 — TiN ALD.** 홀 내벽 전체에 균일 두께로 입혀야 합니다. 마이크론 특허 기준 TiCl4/SiH4/NH3 화학의 도핑 TiN.
5. **지지대 패터닝.** 최상부 지지막에 개구를 뚫어 몰드 식각액의 통로를 냅니다.
6. **몰드 제거 = wet dip-out.** BOE 또는 HF로 산화막만 선택 제거. 식각액이 셀 영역 주변 공간으로 **측면 유입**되어 몰드를 빼냅니다. 지지대(질화막)와 전극(TiN)은 남습니다.
7. **건조/세정.** 여기가 최대 붕괴 구간입니다. 액체가 마르면서 생기는 모세관력이 기둥을 서로 끌어당깁니다. 그래서 국내 학회 발표조차 "IPA 세정의 온도와 회전속도"를 붕괴 개선 변수로 다룹니다. 특허들이 "희생 패턴은 wet dip-out 이후 **건식 공정에서도** 인접 노드를 지지한다"고 명시하는 것도 같은 이유입니다.
8. **유전체 ALD (ZAZ 등).** 이제 기둥의 **안쪽과 바깥쪽 양면**에 등각 증착해야 합니다. 몰드를 뺐기 때문에 실효 종횡비가 오히려 더 가혹해집니다.
9. **상부 전극(TiN) 증착 + 기둥 사이 공간 매립.**

**(e) 유전체 — ZAZ의 실체**

ZAZ는 "ZrO2/Al2O3/ZrO2 3층 샌드위치"로 흔히 그려지지만, JMR 리뷰는 **Al2O3의 ALD 사이클 수가 4–5회 미만이라 별개의 층이 아니라 도판트로 봐야 한다**고 명시합니다. 역할 분담이 명확합니다.

- **ZrO2(정방정)**: 유전율 담당. 커패시턴스를 만든다.
- **Al2O3**: 유전율이 아니라 **누설 차단** 담당. 밴드갭이 커서 ZrO2 내 캐리어 전도를 막는다. 도판트 수준 농도로도 충분하다.

ZAZ는 **HfO2를 밀어내고** 45 nm 세대까지 확장하기 위해 개발된 것입니다(IEEE 논문 제목이 명시적으로 "Replacing HfO2 Based Dielectrics"). 즉 DRAM 커패시터에서 HfO2는 ZrO2의 후계가 아니라 **전임자**입니다. 로직의 게이트 유전체 서사(SiO2→HfO2)와 순서가 다르므로 혼동하면 안 됩니다.

현행 세대는 여기서 한 걸음 더 나가 **ZrO2(NbO)/Al2O3 나노라미네이트** — ZrO2에 Nb가 도핑된 형태 — 라는 것이 TechInsights의 서술입니다.

**(f) 왜 ALD인가**

세 가지가 동시에 요구됩니다.

1. **등각성**: 100:1 구조의 바닥과 입구 두께가 같아야 합니다. CVD는 전구체가 입구에서 소모되어 위는 두껍고 아래는 얇아집니다(step coverage 부족). ALD는 표면 반응이 **자기제한적(self-limiting)** 이므로 전구체가 도달하기만 하면 두께가 위치와 무관하게 결정됩니다.
2. **두께 정밀도**: 유전체 물리 두께가 6–7 nm이고 EOT는 옹스트롬 단위로 관리됩니다. 사이클 단위(≈1 원자층) 제어가 아니면 불가능합니다.
3. **저온**: 이미 형성된 트랜지스터·비트라인의 열예산을 넘지 않아야 합니다.

그리고 여기서 **생산성과 충돌**합니다. 자기제한 반응이 홀 바닥까지 포화하려면 전구체 노출 시간과 퍼지 시간이 종횡비에 따라 급격히 늘어납니다(전구체가 좁고 깊은 관을 확산해 들어갔다가, 부산물이 다시 빠져나와야 함). 사이클당 성막 두께는 원자층 수준이므로 6–7 nm를 쌓으려면 수십–수백 사이클이 필요하고, 각 사이클의 노출·퍼지가 길어지면 웨이퍼당 시간이 선형으로 증가합니다. **등각성을 사려면 처리량을 지불해야 한다** — 이것이 DRAM 커패시터 ALD의 본질적 트레이드오프입니다.
> 주의: 위 문단의 "종횡비에 따라 급격히/제곱으로" 라는 정량 관계는 **이번 조사에서 DRAM 커패시터에 대해 근거를 확보하지 못했습니다.** v3 소스 팩에는 3D NAND ALE 맥락으로 "종횡비의 제곱에 비례"라는 서술이 있으나 이는 ALE이고 대상이 다릅니다. 집필 시 정량 표현을 피하고 정성 서술로 남기십시오.

**(g) 형태 변천의 논리**

- **트렌치형**: 기판을 파고 들어감. 0.11 μm 세대까지 스케일링 기법이 논문화되었으나 이후 도태.
- **스택형 → 실린더(OCS)**: 위로 쌓음. 실린더는 **안쪽 벽까지 표면적으로 쓴다**는 것이 핵심 이점. 같은 높이에서 평면 대비 표면적이 크게 늘어납니다. 이중 몰드로 형성하는 계열이 특허화되어 있습니다.
- **실린더 → 준실린더(quasi-cylindrical)**: SK하이닉스 D1y/D1z, 삼성 D1z (TechInsights). 지름이 너무 좁아지면 안쪽 벽을 쓸 공간 자체가 사라지고, 유전체와 상부 전극을 안쪽에 채울 여유도 없어집니다.
- **→ 필러(pillar)**: 안쪽 벽을 포기하고 **속이 찬 기둥**으로 갑니다. 표면적은 바깥면만 남지만, 기계적으로 훨씬 튼튼하고 공정이 단순해집니다. 다만 **이번 조사에서 필러형의 양산 채택 세대를 특정하는 근거는 확보하지 못했습니다** — SemiEngineering이 "검토 가능한 혁신" 목록에 넣은 수준입니다.

---

## 3. 상충·불확실

| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| 현행 커패시터 종횡비 | **100:1에 접근** — Applied Materials 블로그 (T1, 스니펫) | **50:1 초과** — SemiEngineering/TechInsights 계열 (T3, 스니펫) | 양쪽 다 세대 미특정이고 원문 미확인. **둘 중 하나를 고르지 말 것.** 안전한 서술은 "수십:1을 넘어 100:1에 접근하는 수준으로 보고된다(출처마다 50:1 초과 – 100:1 접근으로 폭이 있음)" |
| MESH 커패시터의 대상 세대 | v3 소스 팩: "2004년 **70 nm 세대** 30 fF" | 논문 제목/초록: "**sub 70nm**을 겨냥", "**80 nm** DRAM용으로 개발" | 논문은 80 nm 적용 / sub-70 nm 목표. v3의 "70 nm 세대" 표기는 부정확할 수 있음. §5 참조 |
| D1c 셀 커패시턴스 | 5–6 fF/cell로 더 낮아질 수 있음 (TechInsights) | 제조사는 6–7 fF 이상 유지를 원함 (동일 출처) | 같은 출처 내 두 진술. **하나는 물리적 추세, 하나는 제조사 의향.** 실측치가 아니므로 "전망"으로 표기 필수 |
| 지지대 단수 (업체별) | 삼성·SK하이닉스=단일 / 마이크론·난야=이중 (EE Times, T3) | 특허(US 10,121,793)는 upper+intermediate 다단 구조를 기술 | EE Times는 2013년 이전 추정. 특허는 시점·업체 불명. **현행 세대의 업체별 단수는 미확인**으로 처리 |
| Nb의 역할 | 조사 지시문: "전극 — Nb 계열" | 확인된 근거: ZrO2(**NbO**)/Al2O3 나노라미네이트 = **유전체 도판트** (TechInsights) | 확인된 것은 유전체 쪽. **Nb 전극에 대한 근거는 찾지 못함** |

---

## 4. 확인 실패 항목

솔직하게 적습니다. 아래는 찾으려 했으나 근거를 확보하지 못했습니다.

1. **세대별 커패시터 종횡비 추이 (D1x / D1y / D1z / D1a / D1b / D1c)** — 조사 지시가 "확보되면 매우 가치가 높다"고 한 항목. **완전 실패.** 세대에 종횡비 숫자를 붙인 공개 자료를 찾지 못했습니다. 얻은 것은 세대 미특정의 "50:1 초과" 또는 "100:1 접근"뿐입니다. TechInsights 다이 분석 유료 리포트에 있을 가능성이 높으나 접근 불가.
2. **세대별 커패시터 높이(nm)** — Applied Materials의 "약 1,000 nm" 하나뿐이고 세대 미특정.
3. **세대별 스토리지 노드 홀 CD(지름)** — 미확보. "수십 nm"라는 정성 표현만.
4. **현행 세대의 지지대 단수(단일/2단/3단)를 업체·세대별로 특정** — 미확보. 2013년 이전 추정 EE Times 기사 하나뿐.
5. **지지대 두께(nm), 개구율(%), 개구 패턴 형상** — 전부 미확보.
6. **ALD step coverage 실측 퍼센트** (예: AR 60에서 95% 등) — 미확보. MDPI HfO2 논문 본문 접근 실패(리다이렉트), "AR≈60까지 우수한 step coverage"라는 정성 표현만 확보.
7. **ALD 사이클 시간 / 웨이퍼당 처리 시간 / WPH 수치** — **완전 실패.** "사이클 시간과 생산성의 충돌"은 원리적으로만 서술 가능하며, 정량 근거는 없습니다.
8. **필러형 커패시터의 실제 양산 채택 세대·업체** — 미확보. 전망 수준 언급만.
9. **dip-out 화학의 벤더별 조성·농도·시간** — 미확보. 특허 수준의 "BOE 또는 HF"만.
10. **HfO2 → ZrO2 전환이 실제로 일어난 세대(nm)** — 논문은 "45 nm 세대까지 확장 가능"이라 하지만 각 업체가 몇 nm에서 갈아탔는지는 미확보.
11. **ZAZ의 현행 세대 실측 EOT** — 미확보. 확보한 6.3 Å은 45 nm 세대 개발 논문 값이고 원문 미확인 스니펫입니다. TechInsights의 "물리 두께 6–7 nm"는 있으나 **물리 두께이지 EOT가 아닙니다.**
12. **TiN 전극의 실제 두께·일함수 수치** — 미확보.
13. **삼성/SK하이닉스/마이크론 공식(T1) 커패시터 구조 자료** — 세 업체 모두 커패시터 단면 구조를 공식 문서로 공개하지 않으며, 접근 가능한 T1은 특허와 장비사 자료뿐이었습니다.

**접근 차단으로 확인 못 한 고가치 출처 (재시도 권장)**
- Applied Materials 블로그 "DRAM Scaling Requires New Materials Engineering Solutions" — HTTP 403
- SemiEngineering "DRAM Scaling Challenges Grow" — HTTP 403
- SemiEngineering "Rutile TiO2 as a Post-ZrO2 Dielectric Platform (KIST)" — HTTP 403
- FMS 2025 프로시딩 PDF (Jeongdong Choe, TechInsights, DRAM-304-1) — HTTP 403. **세대별 종횡비가 여기 있을 가능성이 가장 높습니다.**
- MDPI Nanomaterials 15(11) 783 — 리다이렉트로 본문 미확보

---

## 5. 기존 소스 팩(v3)과의 충돌

**직접 충돌: 1건 (경미)**

| v3 서술 | 이번 조사 | 처리 |
|---|---|---|
| "2004년 **70 nm 세대** \| 30 fF \| T2 (IEDM 2004, MESH capacitor)" | 논문 제목은 "aiming at sub **70nm** DRAMs", 초록은 "**80 nm** DRAM용으로 성공적으로 개발" | v3의 "70 nm 세대"는 **논문의 목표 세대**를 실적용 세대처럼 적은 것으로 보입니다. "2004년, 80 nm 적용 / sub-70 nm 목표"로 고치거나, 최소한 "70 nm를 겨냥한 2004년 MESH 커패시터"로 완화 권장 |

**보강(충돌 아님)**

- v3 "high-k 유전체 두께를 6–7 nm까지 줄이고" → 이번 조사에서 동일 출처(TechInsights)로 재확인. 추가로 **조성이 ZrO2(NbO)/Al2O3 나노라미네이트**라는 정보 확보. v3에 없던 내용.
- v3 "실린더형 → 준실린더형(SK하이닉스 D1y/D1z, 삼성 D1z)" → 동일 출처 재확인. **이 뒤에 필러형이 온다는 서술은 v3에 없고, 이번 조사로도 확정하지 못했습니다.**
- v3 "10 fF 미만 커패시턴스에서 센싱 마진 확보" → TechInsights의 "D1z/D1a는 10 fF/cell 미만"으로 세대가 특정됨. v3보다 구체화 가능.
- v3에 없던 신규 축: **지지대(supporter) 구조 전체**, **wet dip-out 공정**, **ZAZ 내 Al2O3의 도판트 성격**, **HfO2→ZrO2 전임/후계 관계**, **루틸 TiO2·MoO2(2026)**.

---

## 6. 집필 시 주의 (서술 규칙 제안)

1. **"ZAZ = ZrO2/Al2O3/ZrO2 3층 샌드위치"로 그리지 말 것.** Al2O3는 ALD 4–5 사이클 미만의 도판트 수준입니다(T2). 도해를 그린다면 "ZrO2 매트릭스 안에 Al이 얇게 삽입된 나노라미네이트"로, 캡션에 도판트 성격을 명기하십시오.
2. **HfO2를 ZrO2의 후계로 쓰지 말 것.** DRAM 커패시터에서는 **HfO2가 먼저였고 ZAZ가 그것을 대체**했습니다(IEEE 논문 제목이 "Replacing HfO2 Based Dielectrics"). 로직 게이트 유전체 서사와 순서가 반대입니다.
3. **종횡비 숫자에 세대를 붙이지 말 것.** "D1a는 종횡비 70:1" 같은 문장은 이번 조사로 쓸 수 없습니다. 출처가 있는 표현은 "선단 노드에서 50:1을 넘어 100:1에 접근하는 것으로 보고된다(출처별 편차 있음)"까지입니다.
4. **"물리 두께 6–7 nm"와 "EOT"를 섞지 말 것.** TechInsights의 6–7 nm는 고유전율막의 **물리 두께**입니다. EOT는 옹스트롬 단위(ZAZ 개발 논문 6.3 Å, STO 연구 0.5 nm, 루틸 TiO2 목표 0.3 nm 미만)로 자릿수가 다릅니다.
5. **지지대 단수를 업체에 귀속시키지 말 것.** "삼성은 단일, 마이크론은 이중"이라는 유일한 근거는 **엘피다가 살아 있던 시기(2013년 이전 추정)의 T3 기사**입니다. 쓰려면 반드시 "2010년대 초 기준"이라고 시점을 못 박으십시오.
6. **필러형을 현재형으로 쓰지 말 것.** "업체들이 필러형으로 갔다"가 아니라 "필러형이 후보로 거론된다"가 근거에 맞습니다.
7. **Nb를 전극으로 쓰지 말 것.** 확인된 것은 유전체 측 NbO 도핑(ZrO2(NbO))입니다. Nb 전극 근거는 못 찾았습니다.
8. **STO와 루틸 TiO2는 "연구/전망"임을 반드시 병기.** STO는 2008–2009년에 EOT 0.5 nm가 나왔는데도 2026년까지 양산에 못 들어갔습니다. 이 사실 자체가 좋은 서술 소재입니다 — **"실험실에서 되는 것과 양산에서 되는 것 사이의 거리"**.
9. **D1c 커패시턴스 "5–6 fF"는 전망치.** 같은 출처가 "제조사는 6–7 fF 이상을 유지하고 싶어 한다"고 덧붙입니다. 확정 실측처럼 쓰지 마십시오.
10. **지지대 서술의 핵심은 "개구(aperture)"입니다.** 지지대를 그냥 "받침대"로 설명하면 왜 여러 층이 필요한지 설명되지 않습니다. "몰드를 빼내려면 지지대에 구멍이 있어야 하고, 구멍이 클수록 안 튼튼해진다"는 충돌을 먼저 세운 다음 다단 구조를 설명하십시오. 이것이 이 주제에서 가장 설명 가치가 높은 지점입니다.
11. **붕괴는 wet 단계가 아니라 건조 단계에서 일어난다**는 점을 강조할 것. 특허가 "dip-out 이후 건식 공정에서도 지지한다"고 쓰고, 국내 학회가 IPA 세정 조건을 다루는 이유입니다. 모세관력에 의한 pattern collapse는 반도체 공정 일반의 고전 문제이며 커패시터가 그 극단입니다.
12. **ALD 처리량 충돌은 정성으로만.** 사이클 시간·WPH 수치 근거가 없습니다. "종횡비의 제곱에 비례" 같은 표현은 v3의 3D NAND ALE 서술에서 온 것이므로 DRAM 커패시터 ALD에 옮겨 쓰지 마십시오.
13. **본 문서의 다수 값이 검색 스니펫 기반**입니다. 최종 원고에 수치를 넣기 전, §4 말미의 "접근 차단 출처"를 다른 경로로 재확인하는 것이 안전합니다.
14. **특허를 양산 증거로 쓰지 말 것.** US 10,121,793의 다단 supporter, RuC 몰드 패터닝, 도핑 TiN 등은 전부 **청구된 실시례**입니다. "삼성이 이렇게 만든다"가 아니라 "이런 구조가 특허로 제시되어 있다"가 정확합니다.

---

## 7. 출처 목록

| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| techinsights.com/blog/dram-scaling-trend-and-beyond | T2.5 | DRAM Scaling Trend and Beyond (Jeongdong Choe) — **원문 직접 확인** | 2026-07-29 |
| IEEE IEDM 2004 (초록, academia.edu / researchgate 경유) | T2 | A mechanically enhanced storage node for virtually unlimited height (MESH) capacitor aiming at sub 70nm DRAMs | 2026-07-29 |
| IEEE Xplore doc 1705205 | T2 | Development of New TiN/ZrO2/Al2O3/ZrO2/TiN Capacitors Extendable to 45nm Generation DRAMs Replacing HfO2 Based Dielectrics | 2026-07-29 |
| IEEE Xplore doc 4796852 | T2 | 0.5 nm EOT low leakage ALD SrTiO3 on TiN MIM capacitors for DRAM applications | 2026-07-29 |
| IEEE Xplore doc 911914 | T2 | Stress-induced leakage current comparison of giga-bit scale DRAM capacitors with OCS node (제목만) | 2026-07-29 |
| Journal of Materials Research (Cambridge) | T2 | Recent advances in the understanding of high-k dielectric materials deposited by ALD for DRAM capacitor applications | 2026-07-29 |
| Applied Physics Letters 122, 192903 (2023) | T2 | 5.1 Å EOT and low leakage TiN/Al2O3/Hf0.5Zr0.5O2/Al2O3/TiN heterostructure for DRAM capacitor (서지만) | 2026-07-29 |
| ACS Applied Electronic Materials (2026), KIST | T2 | Beyond ZrO2: Rutile TiO2 as the Dielectric Platform for Next-Generation DRAM Capacitors | 2026-07-29 |
| Applied Surface Science (2026) | T2 | Atomic layer deposition of MoO2 using a tetravalent precursor for template-driven rutile TiO2 growth in DRAM capacitors | 2026-07-29 |
| MDPI Nanomaterials 15(11), 783 (2025) | T2 | Deposition of HfO2 by Remote Plasma ALD for High-Aspect-Ratio Trench Capacitors in DRAM (본문 미확보) | 2026-07-29 |
| 대한전자공학회 학술대회 (DBpia) | T2 | DRAM 캐패시터 공정 중 IPA 세정 시 온도와 회전속도에 따른 패턴 붕괴 개선 방법 (서지·초록만) | 2026-07-29 |
| Advanced Materials Technologies 리뷰 (2022) | T2 | ALD step coverage at AR≈60 관련 (스니펫) | 2026-07-29 |
| US 10,121,793 | T1(특허) | Semiconductor device having supporters and method of manufacturing the same | 2026-07-29 |
| US 8,048,757 / US 8,048,758 | T1(특허) | Method for fabricating a capacitor utilizing a sacrificial pattern (wet dip-out, leaning 방지) | 2026-07-29 |
| US 6,700,153 / US 6,911,364 | T1(특허) | One-cylinder stack capacitor and method for fabricating the same (double-mold) | 2026-07-29 |
| US 11,289,487 / US 12,507,395 (Micron) | T1(특허) | Doped titanium nitride materials for DRAM capacitors | 2026-07-29 |
| US 출원 20230395391 | T1(특허) | Ruthenium carbide for DRAM capacitor mold patterning | 2026-07-29 |
| KR20090043325A | T1(특허) | 반도체 메모리소자의 캐패시터 형성방법 (산소 함유 지지막, 4개당 1개) | 2026-07-29 |
| KR20040072086A | T1(특허) | 디램 셀 커패시터 제조 방법 (이중 몰드 산화막) | 2026-07-29 |
| Lam Research 투자자 릴리스 (2015) | T1 | Lam Research Launches Flex G Series for High-Aspect-Ratio Dielectric Etch | 2026-07-29 |
| appliedmaterials.com 블로그 | T1 | DRAM Scaling Requires New Materials Engineering Solutions — **HTTP 403, 검색 스니펫만** | 2026-07-29 |
| semiengineering.com | T3 | DRAM Scaling Challenges Grow — **HTTP 403, 검색 스니펫만** | 2026-07-29 |
| eetimes.com | T3 | Chipmakers turn to new process for sub-nm DRAM cells (**2013년 이전 추정**) | 2026-07-29 |
| eugenustech.com 블로그 | T3 | DRAM Scaling with High Work Function Electrode Materials (제목만) | 2026-07-29 |
| PatSnap Eureka 블로그 | T4 | ALD Conformal Coating in 3D NAND — **구조 이해용, 수치 인용 금지** | 2026-07-29 |

**JEDEC 관련 주의**: 본 주제는 커패시터 물리 구조·공정이므로 JEDEC 문서를 인용하지 않았습니다. 로컬 `jesd79_5.txt`는 "DDR5 Full Spec Draft Rev0.1"(JC42.3 위원회 회람본)이므로 최종 비준 사양과 다를 수 있으며, 어떤 경우에도 커패시터 구조 근거로 쓸 수 없습니다.
