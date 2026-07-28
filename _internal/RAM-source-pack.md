# RAM(Revealing Anatomy of Memory) — 집필용 소스 팩 v3

> 수집일: 2026-07-28
> 대상 독자: 반도체 기초 지식 보유층 (전공 재학생 ~ 엔지니어 지망생)
> 이 문서는 최종 산출물이 아니라 **Claude Code 집필 세션에 투입할 근거 자료 묶음**입니다.
>
> **v2 → v3 변경점**
> 1. **DRAM 셀 리텐션 커패시턴스 수치 정정** — 통용되던 25 fF는 레거시 수치. 현행은 10 fF 미만 (3-2절)
> 2. **DRAM 면적당 밀도를 TechInsights 다이 분석 실측치로 교체** — 중앙값 + 범위 표기 (3-2, 4절)
> 3. **JEDEC HBM4E 높이 완화 추적 결과 반영** — 미확정, 825~900 µm 논의 중. HBM4E 자체가 통합 표준 부재 (3-3절)
> 4. **DDR6 출처 제약 명시** — JEDEC 문서 유료화로 T3 + 벤더 자료 기반임을 본문 규칙에 반영 (7절)
> 5. **HBF는 현재 공개분으로 동결** — 추정 서술 금지 규칙 추가 (3-4절)
> 6. **이미지 플레이스홀더 규약 및 전체 이미지 매니페스트 신설** (9절)

---

## 1. 계층 축의 정의 — 이 문서 모음집의 뼈대

"상위일수록 빠르고 비싸고 작다"는 서술은 직관적이지만, 실제 계층은 단일 지표로 정렬되지 않습니다. HBM과 DRAM은 셀이 동일하고 접근 지연도 사실상 동급인데도 HBM이 상위에 놓입니다. 따라서 이 문서 모음집은 계층을 **5개 축의 복합**으로 정의합니다.

### 1-1. 정렬 축 (5개)

| # | 축 | 단위 | 의미 |
|---|---|---|---|
| **A1** | **접근 지연** | ns / µs | 요청이 데이터로 돌아오기까지의 시간. 셀 구조가 지배 |
| **A2** | **대역폭** | GB/s ~ TB/s | 단위 시간당 전송량. 버스 폭 × 전송률. 패키징으로 개선 가능 |
| **A3** | **용량** | MB ~ TB | 디바이스/스택 단위 저장량. 셀 밀도와 적층 수가 지배 |
| **A4** | **비트당 비용** | $/GB | 셀 면적, 공정 난도, 수율, 패키징 비용의 합 |
| **A5** | **프로세서 결합도** | 온다이 / 인터포저 / PCB / PCIe | 물리적 거리. 지연·전력·신호 무결성에 동시 작용 |

### 1-2. 부가 속성 (정렬 축은 아니나 계층 성격을 결정)

- **휘발성**: 전원 차단 시 데이터 유지 여부
- **접근 입도(granularity)**: 한 번의 요청이 다루는 최소 단위 (워드 / 캐시라인 64B / HBM4 32B / NAND page 약 4KB)
- **쓰기 내구성**: 반복 write에 대한 물리적 수명 제한 유무

### 1-3. 5계층 좌표

`[개념도 - 5계층 피라미드, 5개 축(A1~A5)을 축 라벨로 병기, 각 계층 박스에 대표 수치]`

| | SRAM | HBM | DRAM (DDR5) | HBF | NAND (SSD) |
|---|---|---|---|---|---|
| **셀** | 6T | 1T1C + TSV 적층 | 1T1C | CTF + TSV 적층 | CTF (구세대 FG) |
| **A1 지연** | ~1 ns 이하 | 10~100 ns | 10~100 ns | 10~20 µs | 50~100 µs |
| **A2 대역폭** | 수 TB/s (온칩) | ~2 TB/s (HBM4 스택) | ~50 GB/s (모듈) | 1.6 TB/s (Gen1) | ~7 GB/s |
| **A3 용량** | 수 MB ~ 수십 MB | 36~48 GB (스택) | 수 GB ~ 수십 GB | 512 GB (Gen1 스택) | 수 TB |
| **A4 비트당 비용** | 매우 높음 | 높음 | 중간 | 낮음 | 매우 낮음 |
| **A5 결합도** | 온다이 | 인터포저 (수 mm) | PCB (수십 cm) | 인터포저 / D2D | PCIe (수십 cm+) |
| **휘발성** | 휘발성 | 휘발성 | 휘발성 | **비휘발성** | 비휘발성 |
| **입도** | 워드 | 32B | 64B | **약 4KB page** | 4KB page |
| **쓰기 내구성** | 무제한 | 무제한 | 무제한 | **제한** | **제한** |

### 1-4. 이 정의가 해결하는 두 가지 서술 문제

**(1) HBM이 DRAM 위에 오는 근거**
HBM과 DRAM은 **동일한 1T1C 셀**입니다. A1(지연)에서는 동률입니다. HBM이 상위인 근거는 **A2(대역폭)와 A5(결합도)** 단 두 축이며, 그 대가로 A3(용량)와 A4(비용)에서 DRAM에 밀립니다.
→ 서술 원칙: HBM 챕터에서 "HBM은 빠른 DRAM이 아니라 **넓은** DRAM"임을 명시할 것. 이 구분을 하지 않는 자료가 대부분이므로 차별화 지점이 됩니다.

**(2) HBF의 위치가 애매한 이유**
HBF는 축마다 소속이 다릅니다.
- A1·입도·쓰기 내구성: **NAND에 가까움** (사실상 NAND 셀 그 자체)
- A2·A5: **HBM에 가까움** (TB/s 대역폭, 인터포저 인접 배치)
- A3·A4: **NAND와 HBM 사이**

→ 서술 원칙: HBF를 단일 위치에 고정하지 말고 **"축마다 소속이 갈리는 최초의 계층"** 으로 제시할 것.

### 1-5. 계층 밖 항목 처리 원칙

- **CXL**: 메모리 소자가 아니라 캐시 일관성 인터커넥트. A5 축을 확장하는 수단 → 부록
- **PIM / NMP**: 메모리에 연산을 붙이는 아키텍처 축 → 부록
- **공정**: 5계층 전체를 관통하는 횡단 관심사 → 별도 챕터 (6절)

---

## 2. 출처 등급 체계

| 등급 | 정의 | 집필 시 취급 |
|---|---|---|
| **T0** | 표준화 기구 원문 (JEDEC, OCP, CXL Consortium) | 무조건 우선. 단 **유료 문서 제약 있음** — 7절 참조 |
| **T1** | 제조사·장비사 공식 발표·기술 문서 (SK하이닉스, 삼성, 마이크론, SanDisk/Kioxia, TSMC, ASML, Lam, TEL, NVIDIA) | 마케팅 표현 걷어내고 수치만 사용 |
| **T2** | 동료평가 논문·학회 발표 (IEEE, ISSCC, IEDM, VLSI, arXiv) | DOI/arXiv ID 명시 |
| **T2.5** | **TechInsights 다이 분석** — 실물 역공학 실측치 | **수치 근거로는 T1급 신뢰.** 다만 상당수 보고서가 유료. 공개 블로그·컨퍼런스 발표 자료 우선 활용 |
| **T3** | 전문 분석기관·기술 매체 (SemiAnalysis, SemiEngineering, Tom's Hardware, EE Times, TrendForce, Blocks & Files, The Elec, ZDNet Korea) | 교차 확인 후 사용 |
| **T4** | 개인/기업 기술 블로그, 위키 | 구조 이해용 참고만. **수치 인용 금지** |

---

## 3. 계층별 핵심 데이터

### 3-1. SRAM

`[셀 구조도 - 6T SRAM, 크로스커플 인버터 2개 + 패스게이트 2개, 회로도]`

**셀 구조**
- 6T 셀: 교차 결합(cross-coupled) 인버터 4개가 래치 형성 + 패스 게이트 2개
- 래치가 자체적으로 상태 유지 → 리프레시 불필요("Static"의 어원)
- 읽기 = 래치 전압을 비트라인으로 전달하는 것이 전부 → A1이 가장 짧은 이유

**수치**
| 항목 | 값 | 출처 |
|---|---|---|
| 접근 지연 | 1 ns 이하 | 일반 통용 |
| **TSMC N2 SRAM 매크로 밀도** | **38.1 Mb/mm²** (≈0.038 Gb/mm²) | T1/T3, **주 지표** |
| TSMC N2 HD 비트셀 | 0.0175 ~ 0.021 µm² (출처별 상이) | T3, **범위 병기** |
| TSMC N5 / N3E HD 비트셀 | 0.021 µm² | T3 |
| Intel 18A HD 비트셀 / 매크로 밀도 | 0.021 µm² / 약 31.8 Mb/mm² | T3 (ISSCC 2025 Advance Program) |
| Intel 4 HD 비트셀 | 0.024 µm² | T3 |

> **서술 규칙 (상충 #1 처리)**: 비트셀 크기와 매크로 밀도는 **다른 지표**입니다. 매크로 밀도는 비트셀 + 주변회로(디코더, 센스앰프, 워드라인 드라이버)를 포함합니다. 본문에서는 매크로 밀도 38.1 Mb/mm²를 주 지표로 쓰고, 비트셀은 "출처에 따라 0.0175~0.021 µm²로 보고됨"으로 범위 병기하십시오. N2 개선분이 비트셀 축소인지 DTCO에 의한 주변회로 축소인지가 논쟁 중인 사안이며, 그 논쟁을 그대로 서술하는 편이 정확합니다.

**서사 포인트**
- N5 → N3E 구간에서 비트셀이 정체된 것이 "SRAM 스케일링 정체" 서사의 핵심. N3B/N3E는 N5 대비 SRAM 면적 이점이 거의 없었습니다.
- GAA 나노시트 + BSPDN + DTCO로 N2에서 매크로 밀도가 다시 개선. 다만 로직 밀도 개선폭에는 미치지 못합니다 → **로직은 줄어드는데 SRAM은 덜 줄어드는** 구조적 비대칭이 캐시 비용을 계속 밀어올립니다.
- 온칩 SRAM 중심 가속기: Groq, Cerebras (HBM 없이 SRAM 대역폭만으로 구성)
- HBF의 지연 은닉용 LHB(Latency Hiding Buffer)도 결국 SRAM → HBF 챕터와 연결되는 고리
- 신뢰성 이슈: 3nm GAA-FET SRAM의 self-heating 및 방사선 내성 연구 (SJSU/Sandia, 2026-07, T2) — 미세화가 SRAM에 남긴 문제가 면적만이 아님

---

### 3-2. DRAM

`[셀 구조도 - 1T1C DRAM, 트랜지스터 1개 + 커패시터 1개, 워드라인/비트라인 표기, 회로도]`
`[단면도 - DRAM 셀 수직 구조, 실린더형 커패시터 + 매몰 워드라인 + 비트라인 컨택]`

**셀 구조**
- 1T1C: 트랜지스터 1개(스위치) + 커패시터 1개(전하 저장)
- 셀 면적이 SRAM의 1/4 ~ 1/6
- 읽기 경로: charge sharing → sense amplifier 증폭 → **파괴적 읽기이므로 restore 필요**
- 전하 누설 → 주기적 refresh 필요("Dynamic"의 어원)

**셀 리텐션 커패시턴스 — 통용 수치 정정 (v3 신규)**

널리 인용되는 "DRAM 셀은 리텐션을 위해 약 25 fF가 필요하다"는 서술은 **ITRS 로드맵 시절의 레거시 수치**이며 현행 세대에는 맞지 않습니다.

| 시기 / 세대 | 셀 커패시턴스 | 출처 |
|---|---|---|
| 1985년 1Mb DRAM (0.9 µm) | 32 fF | T2 (IEEE JSSC 1985) |
| 1988년 16Mb DRAM (0.6 µm) | 33 fF | T2 (IEEE JSSC 1988) |
| 2004년 70 nm 세대 | 30 fF | T2 (IEDM 2004, MESH capacitor) |
| ITRS 가정치 (레거시) | 최소 25 fF | T2, **현행 아님** |
| **D1z / D1a 세대** | **10 fF 미만** | **T2.5 (TechInsights)** |
| **D1c 세대 (전망)** | **5 ~ 6 fF** | **T2.5 (TechInsights)** |

- 2000년대 중반까지는 노드가 바뀌어도 셀 커패시턴스를 약 30 fF로 **일정하게 유지**하는 것이 원칙이었습니다. 비트라인 센싱 전압 `Vs ≈ Vcc/2 × Cc/(Cc+Cp)` 를 일정하게 유지하기 위해서였습니다.
- 이 원칙이 깨진 것이 최근 10년의 핵심 변화입니다. high-k 유전체 두께를 6~7 nm까지 줄이고, 커패시터 구조를 실린더형 → 준실린더형으로 바꾸면서(SK하이닉스 D1y/D1z, 삼성 D1z) 버텨왔지만, **결국 커패시턴스 자체를 낮추는 방향으로 선회**했습니다.
- 낮은 커패시턴스를 감당하기 위해 센싱 마진 개선, 센스앰프 트랜지스터 구조 변경(SK하이닉스는 recessed channel 채택), 게이트 워크펑션 엔지니어링, HKMG, row-hammer 대응이 병행됩니다.
- **10 nm이 6F² DRAM 셀의 마지막 노드가 될 가능성** (T2.5, TechInsights). 이후 2028년 전후로 **2T0C capacitorless DRAM(IGZO TFT 기반)** 같은 접근이 필요해집니다.

> 서술 규칙: "DRAM은 25 fF가 필요하다"고 쓰지 마십시오. **"과거에는 약 30 fF를 세대와 무관하게 유지하는 것이 원칙이었으나, 현행 D1z/D1a는 10 fF 미만이며 D1c에서 5~6 fF까지 내려갈 전망"** 이 정확한 서술입니다. 이 정정 자체가 좋은 소재입니다 — 대부분의 국내 블로그·강의 자료가 아직 25~30 fF를 인용하고 있습니다.

**면적당 밀도 — TechInsights 다이 분석 실측치 (v3 신규)**

동일 용량(16 Gb)·동일 세대 기준으로 재수집했습니다. 3사 간 차이가 남아 **중앙값 + 범위**로 표기합니다.

| 세대 | 업체 | 다이 면적 | 비트 밀도 | 셀 크기 | F (D/R) |
|---|---|---|---|---|---|
| **D1b / D1β** | 삼성 | 36.68 mm² | 446.67 Mb/mm² | 0.00123 µm² | 12.5 nm |
| **D1b / D1β** | SK하이닉스 | 37.98 mm² | 431.40 Mb/mm² | 0.00125 µm² | 12.6 nm |
| **D1b / D1β** | 마이크론 | 36.78 mm² | 435.00 Mb/mm² | 0.00133 µm² | 13.1 nm |
| D1y / D1z (DDR5 초기) | 마이크론 | 66.26 mm² | 약 247 Mb/mm² | — | 15.9 nm |
| D1y / D1z (DDR5 초기) | 삼성 | 73.58 mm² | 약 223 Mb/mm² | — | — |
| D1y / D1z (DDR5 초기) | SK하이닉스 | 75.21 mm² | 약 218 Mb/mm² | — | — |
| G4 (참고: CXMT) | CXMT | 66.99 mm² | 239 Mb/mm² | 0.0020 µm² | 16.0 nm |

**→ 문서 인용값 (D1b 세대 16 Gb 기준)**
- **중앙값 435 Mb/mm² (≈ 0.435 Gb/mm²)**
- **범위 431 ~ 447 Mb/mm² (≈ 0.43 ~ 0.45 Gb/mm²)**

부가 관찰:
- D1z(약 0.22~0.25 Gb/mm²) → D1b(약 0.43~0.45 Gb/mm²)로 **두 세대 만에 밀도가 약 2배**. 셀 스케일링 정체 서사와 병치하면 오히려 흥미로운 대비가 됩니다
- v2의 T4 개략치 "0.2~0.3 Gb/mm²"는 D1y/D1z 세대 값에 해당하며, **현행 선단 세대를 과소평가**합니다
- 주의: TechInsights는 삼성 D1b 셀 크기(0.00123 µm²)에서 F를 추출할 때 **7.8F² 기준**을 사용했습니다. 교과서적 "6F² 셀"과 실측 셀 면적을 직접 대응시키면 어긋나므로, 레이아웃 오버헤드를 포함한 실효 F²가 6보다 크다는 점을 각주로 달아두십시오
- DDR5와 LPDDR5X 다이가 섞여 있어 제품군 간 소폭 편차 존재. 비교 시 제품군을 맞출 것

**기타 수치**
| 항목 | 값 | 출처 |
|---|---|---|
| 접근 지연 | 10~100 ns | 일반 통용 |
| DDR5 native 지연 | 약 80~100 ns | CXL 비교 기준값 |
| DDR5 버스 폭 | 64-bit (32-bit 서브채널 2개) | T0 |
| DDR5 프리페치 | 16n (DDR4는 8n) | T0 |
| DDR5 모듈 대역폭 | 약 50 GB/s | T3 |

**공정 노드 로드맵 (2026-07 기준)**
- 현행: 1a / 1b / 1c. **1c가 HVM 진입**, 1d가 향후 1~2년 내 등장 예상 (T3, SemiAnalysis)
- 6F² 셀은 1d까지가 한계. **셀 컨택 개구 마진**이 병목 — storage node contact 면적이 셀 CD에 대해 제곱으로 축소되어, 트랜지스터-커패시터 연결은 충분히 크되 인접 셀과 단락되지 않는 창이 매 노드 좁아집니다
- TechInsights는 **10 nm이 6F² DRAM의 마지막 노드**가 될 가능성을 제기
- 변곡점 1: **4F² + VCT(Vertical Channel Transistor)**
  - 4F²는 6F² 대비 셀 면적 2/3 → 이론상 약 30% 밀도 향상 (최소 피처 F를 줄이지 않고도)
  - 6F²에서는 비트라인과 buried contact이 같은 층에서 혼잡. VCT 4F²는 buried bitline이 독립 공간을 차지하고 전류 경로가 커패시터 → 수직 채널 → 비트라인으로 직선화되어 저항도 감소
  - Tokyo Electron 전망: VCT/4F² DRAM 2027~2028년 등장 (T3). 커패시터·비트라인용 신규 소재 필요
  - TechInsights: 3D/4F²/VCT는 0C 노드 양산 진입 전망
- 변곡점 2: **3D DRAM**. 삼성은 2030년대 초 stacked DRAM 도입 계획 언급 (T3)
- 변곡점 3: **2T0C capacitorless DRAM (IGZO TFT)** — 2028년 이후 프로토타입 필요 영역 (T2.5)
- TechInsights Q3 2026 로드맵 추적 항목: 3D DRAM, X-DRAM, IGZO DRAM, VCT 기반 4F², EUVL
- ISSCC 2026 관측: VCT 4F² + **하이브리드 본딩**이 DRAM/NAND 공통 변곡점. 경쟁축이 "얼마나 줄이나"에서 "얼마나 잘 쌓고 붙이고 수율을 내나"로 이동

`[비교도 - 6F² vs 4F²+VCT 셀 레이아웃, 평면도 + 전류 경로 비교]`

**인터페이스 표준**
- **LPDDR6 (JESD209-6, 2025-07 공개, T0)**
  - 10,667 ~ 14,400 MT/s. 64-bit 버스 환산 유효 대역폭 약 28.5 ~ 38.4 GB/s (LPDDR5X 최대 8,533 MT/s 대비)
  - 서브채널 재구성: 다이당 24-bit 인터페이스를 12-bit 서브채널 2개로 분할. 데이터 12라인 + 커맨드/어드레스 4라인
  - 버스트 길이 32B / 64B 동적 전환, static efficiency mode, DVFSL, per-row activation tracking
  - **JEDEC이 2026-04에 LPDDR6의 데이터센터 및 PIM 확장 로드맵 예고** → LPDDR이 모바일 전용에서 벗어나는 흐름
- **DDR5 MRDIMM (T0)**: 멀티플렉싱으로 native 대비 최대 2배 피크 대역폭, 12.8 Gbps 목표. RDIMM과 플랫폼 호환. MDB 표준 공개, MRCD 진행 중, MRDIMM Gen2 로드맵 진행 (2026-04). Tall MRDIMM으로 3DS 없이 다이 수 2배 탑재 계획
- **DDR6**: **2026-07 현재 미비준** (7절 참조)

---

### 3-3. HBM

`[구조도 - HBM 스택 단면, TSV 관통 DRAM 다이 12단 + 로직 base die + 실리콘 인터포저 위 GPU 병렬 배치]`

**핵심 아이디어**: 셀은 그대로 두고 **패키징으로 핀 수 한계를 돌파** (A2·A5만 개선)

**세대별 수치**
| 항목 | DDR5 | HBM3E | HBM4 |
|---|---|---|---|
| 버스 폭 | 64-bit | 1024-bit | **2048-bit** |
| 독립 채널 수 | — | 16 | **32** |
| 스택당 대역폭 | ~50 GB/s | ~1.2 TB/s | 2 TB/s 이상 |
| 스택당 용량 | — | 24~36 GB | 36~48 GB |
| **패키지 높이 규격** | — | **약 720 µm** | **775 µm** |
| 프로세서 거리 | 수십 cm | 수 mm | 수 mm |

**HBM4 현황 (T0/T1/T3, 2026-07 기준)**
- JEDEC **JESD270-4**, 2025년 4월 공개
- **SK하이닉스**: CES 2026에서 16단 48GB HBM4 공개, >2 TB/s. MR-MUF로 DRAM 웨이퍼를 **30 µm**까지 박막화. 양산 목표 2026 Q3. JEDEC 기준 8 GT/s 대비 **10 GT/s 이상**
- **삼성**: 1c DRAM + **자사 4nm 파운드리 로직 base die**, 최대 11.7 Gbps, 2026년 2월 출하
- **마이크론**: 11 Gbps/pin 초과 샘플, 스택당 2.8 TB/s 초과 주장
- NVIDIA가 16-Hi HBM4를 2026 Q4 납품 요청 (T3)
- 시장 규모 (기관명 병기): 2025년 약 380억 달러 → 2026년 **546억(FinancialContent) ~ 580억 달러(Introl)**

**HBM4E 상태 — 추적 결과 (v3 신규)**

두 가지가 모두 **미확정**입니다. 서술 시 반드시 상태를 명시하십시오.

**(a) 통합 표준 자체가 없음**
- 2026년 중반 기준 **HBM4E에는 통합 JEDEC 표준이 존재하지 않습니다.** 삼성·SK하이닉스·마이크론이 핀 속도·공정 노드·패키징을 각자 차별화한 버전을 개발 중입니다 (T3)
- 이는 HBM4E/HBM5 세대가 **커스텀 HBM 중심**으로 간다는 흐름과 일치합니다. 삼성은 HBM4부터 표준팀과 커스텀팀을 분리 운영하고 커스텀 프로젝트에 인력 250명을 추가 투입했다고 보도되었습니다 (T3, The Elec)
- 벤더별 목표치(참고, 확정 아님): 삼성 13 Gb/s/pin 초과 · 총 3.25 TB/s

**(b) 패키지 높이 완화 — 논의 중, 미확정**
| 시점 | 내용 | 출처 |
|---|---|---|
| 2026-03-06 | 업계에서 **825 ~ 900 µm** 범위 논의 중. 20단 적층 대비 | T3 (ZDNet Korea → TrendForce) |
| 2026-03-30 | JEDEC이 900 µm 확대 공식 논의 착수 보도 | T3 |
| 2026-04-01 | **약 900 µm 검토, HBM4E부터 적용 전망** | T3 (조선일보/뉴시스 → TrendForce) |
| 2026-07 현재 | **확정 발표 확인되지 않음** | — |

- 완화가 확정될 경우의 파급: 초박막 DRAM 웨이퍼 가공 부담 감소, 적층 오류 관리 완화 → **기존 TC 본더로 16~20단 대응 가능** → 하이브리드 본딩 전면 도입이 HBM4E 이후로 지연
- 반대 견해: SK하이닉스 패키지개발 담당 임원은 "**20단 이상에서는 하이브리드 본딩이 필수**"라고 언급 (T3, 조선일보)
- 최종 결정 변수는 NVIDIA의 성능 요구. 삼성·SK하이닉스 모두 NVIDIA 요구에 맞춰 개발·공급하는 구조

> 서술 규칙: HBM4E 관련 수치는 전부 **"논의 중" / "벤더 목표치"** 로 한정하고, JEDEC 확정 표기를 쓰지 마십시오. 확정 시 이 절 전면 갱신.

**NVIDIA Rubin 실측 사양 (T1/T3, 검증 완료)**
| 항목 | 값 |
|---|---|
| GPU당 HBM4 용량 | **288 GB** (8 스택 × **12-high**) |
| GPU당 대역폭 | **최대 22 TB/s** (Blackwell 8 TB/s 대비 약 2.8배) |
| 핀당 전송률 | 약 10.8 GT/s |
| 패키지 | TSMC N3, 컴퓨트 다이 2개 + I/O 다이, 4× 레티클 CoWoS-L 인터포저 |
| NVL72 랙 | HBM4 총 20.7 TB, 집계 대역폭 1.6 PB/s |

> v1의 "384GB"는 오류입니다. 384GB는 16단 48GB × 8스택 가정 이론값이며, Rubin 실제 사양이 아닙니다.

**서사 포인트**
- HBM4에서 **base die가 로직 공정 커스텀 실리콘으로 전환**된 것이 세대 최대 변화. 삼성·SK하이닉스가 4~5 nm 노드를 base die에 사용합니다. 메모리 회사가 파운드리 로직을 끌어오는 구조 변화이며, HBF의 컨트롤러 논의와 직결
- 한계: 셀은 여전히 1T1C. Rubin이 288GB인데 프론티어 LLM 파라미터는 수백 GB ~ 수 TB → **A3(용량) 격차가 HBF 등장의 직접 동기**

---

### 3-4. HBF (High Bandwidth Flash)

> **집필 정책 (v3 확정)**: HBF는 **2026-07-28 시점 공개된 정보만** 사용합니다. 미공개 스펙에 대한 추정·유추·"~일 것으로 보인다" 서술을 금지합니다. 각 미공개 항목은 `미공개 (2026-07 기준)` 으로 명시하고, 스펙 공개 시 이 절 전면 갱신합니다.

`[구조도 - HBF 스택 단면, TSV 적층 NAND 다이 16단 + CBA 구조, 인터포저 위 가속기 인접 배치]`

**기술 구성 (공개분)**
- SanDisk **CBA(CMOS Bonded Array)**: 단일 대형 배열 순차 접근 구조를 **수천 개 독립 서브어레이**로 분할, 각자 read/write 채널을 갖고 병렬 동작
- SanDisk **BiCS NAND** 다이를 TSV로 수직 적층
- HBM4와 물리적 footprint 및 PHY 레벨 전기 인터페이스 근접 → 기존 인터포저·패키징 인프라 재활용 가능
- **drop-in 대체 불가**: 접근 단위(page vs word), erase 사이클, wear leveling 차이로 호스트 컨트롤러 프로토콜 변경 필수

**세대별 목표 스펙 (T1, SanDisk 공개분)**
| 항목 | HBM4 | HBF Gen1 | Gen2 | Gen3 |
|---|---|---|---|---|
| 읽기 대역폭 | ~2 TB/s | **1.6 TB/s** | >2 TB/s | >3.2 TB/s |
| 스택 용량 | 36~48 GB | **512 GB** (16-die × 256 Gb) | 1 TB | 1.5 TB |
| 접근 지연 | ~10~100 ns | **~10~20 µs** | 미공개 | 미공개 |

- HBM 대비 **8~16배 용량을 유사 대역폭·유사 비용**으로 제공하는 것이 가치 제안
- 1.6 TB/s는 최상급 PCIe 5.0 SSD 대비 50배 이상

**미공개 항목 (2026-07 기준)**
- 최종 패키징 규격 (높이, 핀 배치, footprint 세부)
- 전기 인터페이스 최종 사양 및 프로토콜
- 컨트롤러 분담 구조 (host / base die / HBF 컨트롤러 간 역할 경계)
- 쓰기 내구성 정량 스펙 (P/E 사이클, DWPD 상당치)
- 전력 프로파일, 열 설계 조건
- 가격·비트당 비용 실측치

**3대 약점 (공개된 특성 기반)**
1. **A1 지연**: 약 10~20 µs. HBM 대비 약 100배. 셀 차원 한계라 패키징으로 해소 불가
2. **쓰기 내구성**: erase/write 사이클 물리적 수명 제한. 학습(training)에 부적합
3. **접근 입도**: NAND page 단위(약 4KB). HBM4의 32B fine-grained access와 대조. 랜덤 소량 접근 시 **명목 대역폭이 아무리 높아도 실효 대역폭이 급락**

**표준화 현황 (T1)**
- 2025-08: SanDisk ↔ SK하이닉스 MOU. SanDisk는 FMS 2025에서 HBF 프로토타입 시연 및 Technical Advisory Board 구성
- **2026-02-25: HBF Spec. Standardization Consortium Kick-Off** (Milpitas, SanDisk 본사)
- 표준화 창구는 **JEDEC이 아니라 OCP(Open Compute Project) 전용 워크스트림**
  → HBM 계열이 JEDEC을 거친 것과 대비되는 특이점. SemiEngineering도 이 선택을 "다소 의외"로 평가. HBF가 메모리 소자 표준이라기보다 **시스템 아키텍처 표준** 성격을 갖는다는 방증
- 일정: HBF 샘플 2026년 하반기 → HBF 탑재 AI 추론 디바이스 샘플 2027년 초 → 수요 본격화 2030년 전후 전망

**미해결 과제 (공개 논의 기반)**
- **수명 mismatch**: GPU/DRAM 수명 5~7년 vs NAND 수명은 사용 패턴 의존. 동일 패키지 통합 시 부분 교체 불가
- 인터페이스 선택지 2개 (어느 쪽으로 갈지 **미공개**)
  - **PCIe 기반**: 검증됨, 슬롯 분리로 교체 가능. 그러나 Gen5 x16 기준 약 64 GB/s로 **TB/s 목표에 물리적으로 도달 불가**
  - **HBM 스타일 인터포저 통합**: HBF 본래 강점을 살릴 사실상 유일한 선택지. 그러나 수명 mismatch가 부분 교체 불가 형태로 따라붙고, 발열·전력 예산을 같은 패키지에서 해결해야 함
- 기존 SSD offloading에서 host CPU/DPU가 하던 정책 판단(swap 정책, prefetch 결정)을 **HBM/HBF 컨트롤러 또는 base die가 흡수**해야 할 가능성

**활용 아키텍처 — SK하이닉스 H³ (T2)**
> M. Ha, E. Kim, H. Kim, "H³: Hybrid Architecture using High Bandwidth Memory and High Bandwidth Flash for Cost-Efficient LLM Inference," *IEEE Computer Architecture Letters*, 2026. DOI: 10.1109/LCA.2026.3660969

`[아키텍처도 - H³ 구성, GPU shoreline에 HBM 직결 + HBM base die 뒤로 D2D 경유 HBF daisy-chain + base die 내 LHB SRAM]`

- HBM을 GPU shoreline에 직결하고, HBM base die에 **D2D 인터페이스**를 추가해 HBF 스택을 뒤에 daisy-chain
- GPU에는 HBM+HBF가 **통합 주소 공간**으로 보이며, base die의 address decoder/router가 분기
- 데이터 배치: HBF에 model weight + CAG 사전 계산 공유 KV cache / HBM에 생성 중 KV cache, activation
- **LHB(Latency Hiding Buffer)**: base die 내 prefetch 전용 SRAM
  - `Capacity_LHB = 2 × BW_HBF × Latency_HBF` (double buffering 가정)
  - 1 TB/s × 20 µs → 약 40 MB → 3nm SRAM 기준 약 8 mm², base die 약 121 mm²의 6.7%
- 가정 스케일: GPU당 HBM3e 192GB / 8 TB/s + HBF 약 3TB / 8 TB/s → 용량 약 16배 확장
- 시뮬레이션 (Llama 3.1 405B FP8, NVIDIA B200, HBM-only 대비)

| 지표 | 1M context | 10M context |
|---|---|---|
| 최대 batch size | ~2.6× | ~18.8× |
| Throughput (TPS/request) | ~1.25× | ~6.14× |
| Throughput per power | — | 최대 ~2.69× |

- 단일 GPU로 1M context, GPU 2장으로 10M context 추론 (HBM-only는 각각 8장, 32장 필요)

**HBF에 맞는 워크로드 3조건**
1. 한 번 적재 후 반복 읽기 → 쓰기 내구성 문제 회피
2. 접근 패턴이 예측 가능 → prefetch로 A1 은닉
3. 큰 단위로 묶어 읽기 → page 단위 실효 대역폭 유지

→ **CAG(Cache-Augmented Generation)** 가 대표 사례
> B. J. Chan et al., "Don't Do RAG: When Cache-Augmented Generation is All You Need for Knowledge Tasks," WWW 2025. arXiv:2412.15605

`[흐름도 - RAG vs CAG 비교, RAG는 매 요청 retrieve+KV 재계산 / CAG는 사전 1회 KV 생성 후 다중 요청 공유]`

**반론 축 (문서 균형용 — 반드시 포함)**
| 기법 | 동작 | KV cache 접근 예측 가능성 |
|---|---|---|
| StreamingLLM (arXiv:2309.17453) | attention sink + sliding window | 위치가 규칙적 → prefetch 친화적. 단 중간 토큰 정보 손실 |
| InfLLM (arXiv:2402.04617) / Quest (arXiv:2406.10774) | query 기반 동적 KV idx 선택 | **토큰마다 달라 사전 예측 곤란** |
| CSA / HCA (DeepSeek-V4) | KV cache를 토큰 방향 압축 후 압축본 재사용 | 압축본은 결정론적 → 예측 용이. 단 파이프라인 복잡 |

- DeepSeek은 압축 KV를 SSD storage에 보관해 재사용 이점을 살린다고 소개
- MoE weight 저장소로서의 HBF는 라우터 결정이 attention 이후에 나오므로 prefetch hint 확보가 난제
- **반대 방향 논문**: K. Kyung, S. Yun, J. H. Ahn (SNU), "SSD Offloading for LLM Mixture-of-Experts Weights Considered Harmful in Energy Efficiency," IEEE CAL 2025. arXiv:2508.06978
- HAVEN (arXiv:2603.01175): 거대 vector DB를 HBF에 두고 인접에 search 엔진 배치, top-k만 가속기로 전달. 단 **custom base die 제작 필요**

---

### 3-5. NAND Flash

`[셀 구조도 - CTF 방식, 질화물 트랩층에 전하 저장, FG와의 대비 표기]`
`[단면도 - 3D NAND 수직 적층 구조, 332층 채널 홀 관통 + CBA 본딩 계면, 종횡비 강조]`

**셀 구조**
- **플로팅 게이트(FG)**: 절연층으로 둘러싸인 전도체에 전하 저장
- **CTF(Charge Trap Flash)**: 전하를 도체가 아닌 **부도체(질화물층)** 에 저장. 셀 간 간섭 해결, 셀 면적 축소와 read/write 성능 확보를 동시에. 국내 최초 상용화 (T1, SK하이닉스 뉴스룸)
- 고전압 인가 → 터널링으로 전자 주입 → 절연층이 탈출 차단 → **비휘발성**
- 읽기 = 저장 전하량에 따라 달라지는 문턱 전압 측정. 멀티 레벨일수록 전압 구분 단계가 늘어 시간 증가

> 서술 주의: 현대 3D NAND는 대부분 **CTF 기반**입니다. "플로팅 게이트"로 뭉뚱그리는 자료가 많은데, FG → CTF 전환은 3D 적층을 가능하게 한 전제 조건이므로 구분해서 서술하십시오.

**수치**
| 항목 | 값 | 출처 |
|---|---|---|
| 랜덤 읽기 지연 | 약 50~100 µs | 일반 통용 |
| **BiCS10 면적 밀도** | **29 Gb/mm² 초과** | T1 (Kioxia/SanDisk), **주 지표** |
| BiCS10 전송률 | 4,800 MT/s | T1 |
| SSD 대역폭 | ~7 GB/s (PCIe 4.0급) | 일반 통용 |

**적층 경쟁 현황 (2026-07 기준, T1/T3)**
| 업체 | 세대 | 층수 | 상태 |
|---|---|---|---|
| SK하이닉스 | V9 | **321** | 양산 중 (2024~), triple string stack |
| 삼성 | V9 | 286~290 | 양산 중 (2024-04~) |
| 삼성 | V10 | **400+** | triple stack, **CoP(Cell-on-Periphery)**, 1 Tbit die |
| Kioxia/SanDisk | BiCS8 | 218 | **CBA 최초 양산** |
| Kioxia/SanDisk | **BiCS10** | **332** | 2026년 여름 샘플 출하. 데이터센터 전용 (BiCS9는 클라이언트용) |
| 마이크론 | G8 | 276 | 양산 중. Gen7에서 400층 직행 준비 |
| Solidigm | — | 192 | QLC |
| YMTC | — | 300급 | — |

**BiCS10 상세 (T1)**
- 332 active layers, 29 Gb/mm² 초과, 4,800 MT/s, PCIe 5.0/6.0 데이터센터 SSD 타깃
- BiCS8(218층) 대비 면적 밀도 **+59%**, 전송 속도 **+33%**
- 읽기 지연 약 4 µs 단축(약 10%), 읽기 전력 약 100 mJ/GB → 약 75 mJ/GB (**-29%**)
- 개선 원리: 332층 초고적층에서 긴 워드라인 체인을 매 사이클 VSS↔VREAD로 완전 충방전하는 대신, 중간 전압까지만 낮췄다 복원해 스윙 폭 축소
- **MSA-CBA**를 1,000층 기술에 적용 (VLSI 2026)

> **서술 규칙 (상충 #7 처리)**: **층수와 면적당 비트 밀도는 별개 지표**입니다. 삼성 V10이 400층이고 BiCS10이 332층이지만, 면적 밀도에서는 BiCS10이 앞선다는 것이 Kioxia/SanDisk의 주장입니다. 층수는 Z축, 밀도는 XY×Z의 결과이며 워드라인 피치·채널 홀 직경·주변회로 배치가 함께 작용합니다.

**적층 한계 — 6절 공정과 직결**
- 종횡비 추이 (T1/T3): 96층 약 50:1 → 400층 60:1 초과 → **1,000층 100:1 접근**
- 100:1에서 중성 반응종 flux가 표면 대비 약 1.3%까지 감소 → **transport가 근본 문제**
- 삼성 **900층 연구 소자** 시연 (2026-05, T3). 셀 동작 확인 단계
- Kioxia/SanDisk **1,000층 기술** VLSI 2026 세계 최초 발표 (T3)
- SK하이닉스: 2030년까지 1,000층 돌파 공개 목표

**AI 서버에서의 현재 역할**
- 모델 가중치 보관 및 기동 시 HBM 로드. 다중 노드 서빙에서 공유 SSD storage는 사실상 필수
- vLLM 등 서빙 프레임워크의 **KV cache swap-out** 대상 (비활성 세션 → CPU DRAM → SSD)
- **NVIDIA GPU Direct Storage(GDS)**: PCIe P2P DMA로 NVMe 컨트롤러 ↔ GPU 직접 전송. 호스트 DRAM 경유 제거
- 구조적 한계: Flash → GPU 경로가 PCIe를 거쳐야 하고, PCIe 대역폭이 HBM 대비 낮아 병목 불가피 → **HBF가 노리는 지점**

`[경로도 - 전통적 SSD→CPU DRAM→GPU 경로 vs GDS의 PCIe P2P DMA 직결 경로 비교]`

---

## 4. 계층 간 밀도 비교 (v3 갱신)

v3에서 DRAM과 NAND 수치를 실측 근거로 교체하면서 계층 간 배율이 크게 바뀌었습니다.

| 계층 | 면적당 밀도 | 근거 | 3D 여부 |
|---|---|---|---|
| SRAM | **0.038 Gb/mm²** (38.1 Mb/mm²) | TSMC N2 매크로, T1/T3 | 2D (셀 1층) |
| DRAM | **0.435 Gb/mm²** (범위 0.43~0.45) | D1b 세대 16Gb 3사, T2.5 | 2D (셀 1층) |
| NAND | **29 Gb/mm² 초과** | BiCS10 332층, T1 | **3D (332층 적층)** |

**배율: 약 1 : 11 : 760**

> v2의 T4 개략치(1 : 5~7 : 125~375)보다 격차가 훨씬 큽니다. 특히 NAND 쪽을 크게 과소평가하고 있었습니다.

**방법론적 주의 (본문에 반드시 명시)**
SRAM과 DRAM의 밀도는 **셀 1개 층**의 값인 반면, 3D NAND의 Gb/mm²는 **332층을 Z축으로 쌓은 결과**입니다. 같은 단위로 나열하면 "NAND 셀이 본질적으로 760배 작다"는 잘못된 인상을 줍니다.

- BiCS10의 층당 환산 밀도는 대략 29 ÷ 332 ≈ **0.087 Gb/mm²/층** 수준으로, DRAM(0.435)보다 오히려 **낮습니다**
- 즉 NAND 셀이 DRAM 셀보다 작아서가 아니라, **NAND만 3차원으로 확장했기 때문**에 면적당 밀도가 앞서는 것입니다
- 이것이 DRAM 로드맵이 4F²를 거쳐 3D DRAM으로 향하는 이유이며, "왜 DRAM은 아직 못 쌓는가"를 별도 문단으로 다룰 근거입니다 (답: 커패시터 형성과 리텐션 요구가 수직 적층과 충돌)

→ 권장 서술: 밀도 비교표에 `(2D 셀 기준)` / `(N층 적층 결과)` 를 명시하고, 층당 환산치를 병기할 것

`[비교도 - SRAM/DRAM/NAND 면적당 밀도 로그 스케일 막대, 2D vs 3D 구분 표시 + NAND 층당 환산치 병기]`

---

## 5. 계층 밖 — CXL (부록 챕터용)

**등장 배경**: DDR은 채널 수가 천장, PCIe는 캐시 일관성이 없음. 그 사이의 빈 자리
- 서버 CPU 최신 세대도 메모리 채널 8~16개, 채널당 모듈 1~2개 → 소켓당 DRAM 용량 수 TB가 물리적 천장
- PCIe Gen5 x16은 단방향 약 64 GB/s로 대역폭 자체는 DDR5 채널 하나와 견줄 만하지만, ① 캐시 일관성 없음 ② 캐시라인(64B) 단위 fine-grained access 불가
- CXL = **PCIe PHY를 그대로 빌리고 그 위에 캐시 일관성 프로토콜을 얹은** 표준

`[구성도 - CXL.io/.cache/.mem 3개 서브프로토콜이 단일 PCIe 링크 위에서 동시에 흐르는 구조, 데이터 방향 화살표]`

**3개 sub-protocol**
| Sub-protocol | 역할 | 방향 |
|---|---|---|
| CXL.io | 디바이스 발견, 설정, DMA (PCIe와 동일). **모든 CXL 디바이스 필수** | — |
| CXL.cache | 디바이스가 호스트 메모리를 캐시라인(64B) 단위 캐싱, MESI류 일관성 확장 | 디바이스 → 호스트 |
| CXL.mem | 호스트가 디바이스 메모리를 물리 주소 공간의 한 구간으로 load/store | 호스트 → 디바이스 |

**Type 1/2/3**
| | Type 1 | Type 2 | Type 3 |
|---|---|---|---|
| 프로토콜 | io + cache | io + cache + mem | io + mem |
| 자체 메모리 | 없음 | 있음 | 있음 |
| 호스트 캐싱 | 함 | 함 | 안 함 |
| 예시 | SmartNIC, FPGA | GPU, AI 가속기 | 메모리 확장 모듈 |

- Type 2는 양방향 일관성(bias-based coherency) 구현 부담이 커서 양산 사례가 적음 → **실제 시장은 Type 3 중심**

**버전 진화**
- **1.1**: 한 호스트에 직접 연결. 단일 노드 용량 확장
- **2.0**: CXL 스위치 도입, **메모리 풀링**. MLD로 chunk 분할 + Fabric Manager가 배분. "동시 공유"가 아닌 **동적 할당**(한 chunk = 한 시점에 한 호스트) → 일관성 충돌 영역 자체가 없음
- **3.x** (3.0/2022, 3.1/2023, 3.2/2024): **GFAM**으로 다중 호스트 동시 접근 + HW 캐시 일관성. **PBR**로 mesh/dragonfly/3D torus 토폴로지 지원
- **2026년 현재 양산 제품 대부분은 CXL 2.0**

`[토폴로지도 - CXL 1.1 단일 호스트 직결 → 2.0 스위치+풀링 → 3.x 패브릭+멀티호스트, 3단계 진화]`

**제품군 (T1/T4)**
| 회사 | 제품 | 폼팩터 | 특징 |
|---|---|---|---|
| 삼성 | CMM-D | E3.S | 단순 메모리 확장 |
| 삼성 | CMM-B | 박스형 | 랙 레벨 풀링, CXL 2.0 스위치 내장 |
| 삼성 | CMM-H | E3.S | DRAM + NAND 하이브리드 |
| SK하이닉스 | CMM-DDR5 | E3.S | DDR5 기반 확장 |
| SK하이닉스 | CMM-Ax | E3.S | 메모리 + 연산 엔진 통합 |
| 마이크론 | CZ120 / CZ122 | E3.S | 메모리 확장 (Microchip SMC 2000 컨트롤러) |

- 용량 96 ~ 256 GB, 인터페이스 PCIe Gen5 x8 공통
- IP/실리콘 진영: Astera Labs Leo(Microsoft Azure M-series 채용), Marvell, Microchip, **Panmnesia**(KAIST CAMELab 출신 한국 fabless, PANSWITCH CXL 3.2 fabric switch, 2026-04 pre-release 실리콘 공급 및 하반기 양산 발표)

**남는 숙제**
- **지연 비용(Latency Tax)**: DDR5 native 약 80~100 ns vs CXL Type 3 약 170~300 ns → **약 2~3배**
- → 메인 메모리 전체 대체가 아니라 **"가까운 DDR + 한 단계 멀리의 CXL"이라는 2-tier 구성**의 두 번째 칸
- 소프트웨어 스택 미성숙: CPU에게 CXL 메모리는 "약간 느린 NUMA 노드". Linux 커널의 hot/cold page tracking, transparent page migration이 정비 중
- LLM 추론처럼 접근 패턴이 결정론적인 워크로드는 OS 자동 tiering보다 애플리케이션 직접 배치가 유리 → HBF의 prefetch hint 논의와 같은 구조의 문제

---

## 6. 반도체 공정 — 계층을 관통하는 횡단 챕터

### 6-1. 기본 틀 — 8대 공정 (T1, 삼성전자 DS부문 공식 분류)

`① 웨이퍼 제조 → ② 산화 → ③ 포토(노광) → ④ 식각 → ⑤ 증착·이온주입 → ⑥ 금속배선 → ⑦ EDS → ⑧ 패키징`

- ①~⑥이 **전공정(Fab)**, ⑦~⑧이 **후공정**
- 실제로는 `산화 → 포토 → 식각 → 증착/이온주입 → 금속배선 → CMP`를 수백 번 반복
- 식각: 습식(화학약품, 저비용) / 건식(플라즈마, 미세화에서 비중 증가). 증착: CVD / PVD / **ALD**
- **T1 국문 원문**
  - 삼성반도체 기술블로그 반도체 백과사전: `semiconductor.samsung.com/kr/support/tools-resources/fabrication-process/`
  - 삼성전자 반도체 뉴스룸 "반도체 8대 공정" 1~9탄: `news.samsungsemiconductor.com/kr/`
  - SK하이닉스 뉴스룸 "반도체의 이해" 연재: `news.skhynix.co.kr/`

> 서술 규칙: 8대 공정은 **공통 어휘를 세우는 용도**로만 간략히 다루고, 지면은 6-2 ~ 6-5의 메모리 특화 공정에 배분하십시오. 타겟 독자는 8대 공정을 이미 아는 층입니다.

`[흐름도 - 8대 공정 순서, 전공정/후공정 구분 + 반복 루프 표기]`

### 6-2. 노광 — EUV와 DRAM

DRAM에서만 의미 있는 공정입니다. NAND는 수직 스케일링이라 노광 의존도가 낮습니다.

**EUV 도입 경과 (T1/T3)**
- SK하이닉스: 2021년 **1a DRAM에 EUV 1개 레이어** 최초 적용 → 1b에서 4개 → **1c에서 5~6개 레이어**
- 마이크론: **1γ(1-gamma)가 자사 최초 EUV 적용** DRAM. 0.33 NA EUV. TechInsights가 Y62E 다이 전체 공정 분석(DPF) 완료 (2026-06, T2.5)
- EUV는 13.5 nm 파장으로 DUV 멀티패터닝을 단일 노광으로 대체 → 공정 스텝·결함 감소, 수율 개선
- ASML은 2026년 EUV 사업이 **선단 DRAM 수요로 급성장**하고 DUV는 2025년 대비 감소할 것으로 전망 (T1)

**High-NA EUV (NA 0.55)**
- 해상도: NA 0.33이 노광당 13 nm → **NA 0.55는 8 nm**. 약 1.7배 미세한 피처, 약 3배 밀도
- 장비: ASML **TWINSCAN EXE:5200B**. 대당 약 4억 달러 수준
- **SK하이닉스가 DRAM 업계 최초로 이천 M16 팹에 EXE:5200B 설치** (2025-09, T3)
- 삼성: 2025년 말 1호기, 2026년 상반기 2호기 / Intel: 2025-12 인수 테스트 통과, 14A 개발 지원 / imec: 2026 Q4 자격 검증 목표
- ASML CEO는 2026-05 기준 **"수개월 내 High-NA EUV 생산 칩 등장"** 언급
- **메모리는 극도로 비용 민감**하므로 모든 공정 스텝을 비트당 원가로 정당화해야 합니다. High-NA가 DRAM에 매력적인 조건은 "패터닝 스텝 수를 줄이거나 수율을 올릴 때"이며, NAND에는 상대적으로 덜 중심적입니다

`[비교도 - NA 0.33 vs NA 0.55 해상도 차이, 13nm vs 8nm 피처 + 멀티패터닝 스텝 축소 개념]`

### 6-3. 식각 — 3D NAND의 진짜 병목

**HAR 채널 홀 식각**
- 3D NAND는 ONON(oxide/nitride) 다층막을 쌓은 뒤 위에서 아래로 **수직 홀**을 뚫습니다
- 홀 직경 100 nm 미만, 깊이 6~10 µm. 웨이퍼 한 장에 **수조 개의 완벽한 홀**을 균일하게
- 종횡비: 96층 약 50:1 → 400층 60:1 초과 → **1,000층 100:1 접근**
- 100:1에서 중성 반응종 flux가 표면 대비 약 1.3%까지 감소 → **transport가 근본 문제**
- 주요 결함: bowing(중간 부풂), twisting(비틀림), tilting(기울어짐), 홀 간 편차
- 비정질 카본 하드마스크가 수직 식각 보조

**극저온(cryogenic) 식각**
- 저온(최대 -60°C 수준)에서 반응종 농도와 제거 능력이 높아져 식각률 상승
- **Lam Research**가 2019년 세계 최초 cryo HAR 식각 양산 도입. 현재 HAR 유전체 식각 챔버 7,500대 이상, 누적 500만 장 이상 웨이퍼 처리 (T1)
- **Lam Cryo 3.0**: 400층 이상 대상. 기존 HAR 대비 **식각률 2.5배, 프로파일 정밀도 2배**. 10 µm 깊이에서 CD 편차 0.1% 미만
- **Tokyo Electron**: 400층용 10 µm 초고속 극저온 식각, 지구온난화지수(GWP) **84% 저감** — 환경 규제가 공정 선택에 개입하기 시작한 사례
- 보조: **ALE(Atomic Layer Etching)**. 100:1에서 두 half-reaction이 홀 바닥까지 포화하려면 노출 시간이 종횡비의 제곱에 비례 증가 → **정밀도와 생산성의 직접 충돌**

**웨이퍼 스트레스·warpage 관리**
- 적층이 높아질수록 웨이퍼 휨(bow) 심화
- Lam은 backside deposition으로 bow 보상 (Coronus DX, VECTOR DT, EOS)
- 삼성은 Upper Chuck 설계와 오버레이 보정으로 대응
- 워드라인 금속화도 병목: 얇아지는 연결부 저항을 낮추기 위해 저저항 금속(Mo 등) void-free HAR 충전 필요

`[단면도 - HAR 채널 홀 식각 결함 유형, bowing/twisting/tilting 3종 비교]`

### 6-4. 본딩 — HBM·HBF·차세대 NAND를 관통하는 축

2026년 메모리 공정의 최대 화두입니다. **DRAM·NAND·패키징이 모두 같은 기술로 수렴**합니다.

**(a) 다이 적층 본딩 — HBM**

| 방식 | 원리 | 특징 |
|---|---|---|
| **TC-NCF** | 마이크로 범프 + 비전도성 필름, 열압착 | 초기 방식. warpage·손상 이슈 |
| **MR-MUF** | 마이크로 범프 + 스택 전체 가열 후 언더필 충전 | SK하이닉스 주력. warpage 개선, 생산성 향상 |
| **하이브리드 본딩 (HCB)** | **범프 제거**, Cu-Cu 직접 접합 | 스택 높이 축소, 전력·대역폭 개선. 완벽한 표면 청정도·정렬 요구 |

- **HBM4는 결국 마이크로범프를 유지**하고 하이브리드 본딩을 미뤘습니다 (T3, SemiEngineering 2026-01). 이유: 현행 기법이 pad pitch 약 10 µm까지 커버하는데 HBM4 pad pitch가 정확히 10 µm이라 경제성이 안 나옴
- **SK하이닉스**: 12단 하이브리드 본딩 HBM 검증 완료, 양산 수율 확보 중 (2026-04). MR-MUF를 먼저 고도화해 16-Hi HBM4의 **775 µm 높이 제한** 대응. 하이브리드 본딩 인라인 장비(Applied Materials CMP·플라즈마 + Besi 본더, 약 200억 원) 발주
- **삼성**: **HBM4E 16단부터 HCB를 TCB와 병행 도입, HBM5에서 전면 전환** 계획. 2026-06 IEEE 논문에서 HCB가 TCB 대비 **열저항 20% 이상 감소, 스택 높이 15% 축소**임을 시스템 레벨로 정량 입증 (T2)
- **변수**: JEDEC HBM4E 높이 완화(825~900 µm) 논의 — **미확정** (3-3절). 완화 시 MR-MUF/TC-NCF가 16~20단에서 한 세대 더 생존
- 장비 시장 영향: 완화 시 TC 본더 시장(한미반도체가 약 71.2% 점유)이 수혜, 하이브리드 본딩 장비 진영은 상용화 지연 (T3)
- 업계 전망은 **HBM5 20-Hi(2028~2029)** 를 하이브리드 본딩 본격 채택 시점으로 봅니다 (T3)

`[비교도 - TC-NCF vs MR-MUF vs 하이브리드 본딩, 다이 간 접합부 단면 3종 비교, 범프 유무와 갭 차이 강조]`

**(b) 웨이퍼 대 웨이퍼 본딩 — NAND와 DRAM**
- **CBA(CMOS Bonded to Array) / CoP(Cell-on-Periphery)**: 메모리 셀 웨이퍼와 CMOS 주변회로 웨이퍼를 **각각 최적 공정으로 따로 제작**한 뒤 미세 구리 패드로 본딩
  - Kioxia가 218층 BiCS8에서 최초 양산. 경쟁 제품 대비 read/write 20~30% 빠름 (Nikkei 인용)
  - 삼성 V10도 같은 접근을 CoP로 명명
  - **HBF의 CBA가 바로 이 기술의 연장** — 3-4절과 직결
- **DRAM**: TechInsights는 ISSCC 2026 기준으로 **VCT 4F² + 하이브리드 본딩**을 DRAM의 다음 변곡점으로 지목

> **집필 시 핵심 연결고리**: SRAM(3nm 로직) · DRAM(4F²+본딩) · HBM(적층 본딩) · HBF(CBA) · NAND(CBA·CoP) — **다섯 계층이 모두 "웨이퍼를 붙이는 기술"로 수렴**하고 있습니다. 이것이 2026년 메모리 공정의 단일 서사이며, 문서 모음집 전체를 관통하는 축으로 쓸 수 있습니다.

`[개념도 - 5계층이 각기 다른 경로로 '본딩'에 수렴하는 구조, 화살표 수렴 다이어그램]`

### 6-5. 계층별 공정 병목 요약

| 계층 | 1차 병목 공정 | 구체적 난제 | 현재 해법 |
|---|---|---|---|
| SRAM | 노광 + DTCO | 비트셀이 로직만큼 안 줄어듦 | GAA, BSPDN, DTCO, 3D 적층 캐시 |
| DRAM | 노광 + 커패시터 형성 | 셀 컨택 개구 마진, **10 fF 미만 커패시턴스에서 센싱 마진 확보** | EUV 레이어 확대, High-NA, 4F²+VCT, HKMG |
| HBM | 적층 본딩 + 열 | 775 µm 높이 제한, 16단 발열, 30 µm 박막화 | MR-MUF 고도화, HCB, 로직 base die |
| HBF | 본딩 + 인터페이스 | CBA 서브어레이 병렬화, 표준 미확정 | CBA + TSV, OCP 표준화 진행 중 |
| NAND | HAR 식각 | 100:1 종횡비, transport 한계, warpage | 극저온 식각, ALE, CBA, backside dep |

---

## 7. 상충·미확정 항목 처리 현황

| # | 쟁점 | 상태 | 처리 |
|---|---|---|---|
| 1 | TSMC N2 HD SRAM 비트셀 | **처리 완료** | 매크로 밀도 38.1 Mb/mm² 주 지표, 비트셀 0.0175~0.021 µm² 범위 병기 |
| 2 | 면적당 밀도 삼종 | **v3 실측 교체 완료** | SRAM 0.038 / DRAM 0.435(범위 0.43~0.45) / NAND 29+ Gb/mm². 2D vs 3D 구분 및 층당 환산치 병기 규칙 추가 |
| 3 | Vera Rubin 용량 | **검증 완료** | 288 GB (8스택 × 12-high) / 최대 22 TB/s. 384GB는 오류 |
| 4 | DDR6 비준 시점 | **검증 완료 — 미비준** | 아래 별도 항목 |
| 5 | HBF 세부 스펙 | **미공개 — 동결 정책 적용** | 공개분만 사용, 미공개 항목 명시 리스트화 (3-4절) |
| 6 | HBM4 시장 규모 | **처리 완료** | 546억(FinancialContent) ~ 580억 달러(Introl), 기관명 병기 |
| 7 | V-NAND 층수 혼선 | **처리 완료** | 층수(Z축)와 면적 밀도(XY×Z)를 별개 지표로 분리 서술 |
| 8 | 공정 자료 부재 | **대체 완료** | 6절 신설 |
| **9** | **DRAM 셀 리텐션 커패시턴스** | **v3 정정 완료** | 25 fF는 레거시. 현행 D1z/D1a 10 fF 미만, D1c 5~6 fF 전망 (T2.5) |
| **10** | **HBM4E 패키지 높이 완화** | **추적 결과: 미확정** | 825~900 µm 논의 중. HBM4E 자체가 통합 JEDEC 표준 부재. "논의 중"으로만 서술 |

### DDR6 — 확정 사항 및 출처 제약

**출처 제약 (v3 신규)**
JEDEC 사이트에서 DDR6 관련 문서는 대부분 **유료 회원 전용**이라 원문 직접 확인이 불가합니다. 따라서 이 문서의 DDR6 서술은 **T3(기술 매체) + 벤더 로드맵 자료** 기반입니다.

→ **집필 규칙**: DDR6 관련 서술에는 반드시 다음 취지의 각주를 붙이십시오.
> "JEDEC DDR6 사양서는 유료 공개이며, 아래 수치는 공개 보도 및 벤더 로드맵을 종합한 값으로 최종 비준 사양과 다를 수 있습니다."

이 제약은 **T0 접근이 막힐 때의 표준 대응 패턴**이므로, HBF·HBM4E 등 다른 미확정 항목에도 동일하게 적용하십시오.

**확정 사항 (2026-07-28 기준)**
- **JEDEC 미비준**. JC-42.3 소위에서 타이밍·시그널링 파라미터 조율 중
- 초안 수치(비준 전): 8,800 ~ 17,600 MT/s. OC 모듈은 21,000 MT/s 초과 목표
- 구조: DDR5의 32-bit 서브채널 2개 → **24-bit 서브채널 4개**
- 폼팩터: DIMM → **CAMM2** 전환 예상
- LPDDR6(JESD209-6)가 DDR6 계열 중 **최초 확정 표준** (2025-07)
- 제품 일정 전망 (편차 큼): 엔터프라이즈/데이터센터 2027~2028년, 컨슈머 데스크톱 2028~2029년
- 서술 규칙: "DDR6는 ~이다"가 아니라 **"DDR6 초안은 ~를 목표로 한다"**

---

## 8. 문서 모음집 구조 (확정안)

```
RAM/
├── README.md                      # 계층 조감도 + 읽는 순서 + 용어 정의 + 공정 미니 사전
├── 00-memory-hierarchy.md         # 속도·용량·비용 트릴레마
│                                  # ★ 1절의 5축 복합 지표 정의
├── 01-sram.md                     # 6T 셀 / 스케일링 정체 / 온칩 캐시·SRAM 중심 가속기
├── 02-dram.md                     # 1T1C / refresh·restore / 커패시턴스 축소 서사
│                                  # 6F²→4F²+VCT→3D DRAM 로드맵 / DDR·LPDDR 표준
├── 03-hbm.md                      # TSV·인터포저 / 2048-bit / base die 로직화 / Rubin 사례
├── 04-hbf.md                      # CBA / 3대 약점 / OCP 표준화 / H³ / sparse attention 반론
├── 05-nand.md                     # FG→CTF / 3D 적층 경쟁 / 층수 vs 밀도 / AI 서버 역할
├── 06-process.md                  # ★ 횡단 챕터: EUV·HAR 식각·본딩
│                                  # "다섯 계층이 본딩으로 수렴한다"는 단일 서사
├── appendix-a-cxl.md              # 인터커넥트: .io/.cache/.mem, Type 1/2/3, 1.1→2.0→3.x
├── appendix-b-workloads.md        # LLM 추론이 각 계층에 요구하는 것 (CAG, sparse attention, GDS)
├── appendix-c-industry.md         # 공급망·시장 (날짜 명시, 본문과 격리)
├── SOURCES.md                     # 전체 출처 인덱스 + 확인일 + 등급
└── assets/                        # 이미지 (추후 AI 생성)
    └── IMAGE-MANIFEST.md          # 9절 매니페스트를 이 파일로 분리 관리
```

**각 계층 문서 공통 템플릿**
```
1. 한 줄 정의
2. 셀 구조 — 왜 이렇게 생겼는가          [셀 구조도 플레이스홀더]
3. 왜 빠른가 / 느린가 (물리적 근거)
4. 왜 비싼가 / 싼가 (면적·공정 근거)
5. 5축 좌표 표 (A1~A5) + 부가 속성 (휘발성 / 입도 / 쓰기 내구성)
6. 인터페이스와 표준 현황
7. 공정 병목과 로드맵 → 06-process.md 링크
8. AI 워크로드에서의 실제 역할
9. 이 계층이 풀지 못하는 문제 → 다음 계층으로 연결
10. 참고 문헌
```

**집필 규칙**
- 모든 수치에 **출처 각주 + 확인 시점**. 반도체 수치는 6개월이면 낡습니다
- 표준 명칭은 문서 번호까지 (JESD270-4, JESD209-6)
- 논문은 DOI 또는 arXiv ID 표기
- **미비준·미공개 표준의 수치는 "초안 목표" 또는 "벤더 목표치"로 서술** (DDR6, HBF, HBM4E)
- **T0 원문이 유료라 확인 불가한 경우 그 사실을 각주로 명시** (7절 DDR6 패턴 참조)
- "업계 최초", "혁신적" 같은 제조사 마케팅 어휘 배제
- 각 문서 최상단에 `> 최종 검증: YYYY-MM-DD` 배너, `SOURCES.md`와 동기화
- T4 출처는 구조 이해용으로만. 수치는 반드시 T0~T3로 백업

---

## 9. 이미지 플레이스홀더 규약 및 매니페스트

이미지는 추후 AI로 생성하며, 집필 단계에서는 **플레이스홀더만 표기**합니다.

### 9-1. 표기 규약

```
[<이미지 종류> - <담아야 할 핵심 요소>, <표현 형식>]
```

- 마크다운 이미지 문법(`![]()`)을 쓰지 말고 **대괄호 텍스트 그대로** 남깁니다. 미생성 상태가 렌더링에서 즉시 눈에 띄어야 하기 때문입니다
- 종류는 다음 6종으로 통일: `셀 구조도` / `단면도` / `구조도` / `비교도` / `흐름도` / `개념도`
- 캡션이 필요하면 플레이스홀더 바로 아래 이탤릭으로 별도 작성
- 생성 완료 시 플레이스홀더를 `![캡션](assets/파일명.svg)` 로 치환하고, 원래 플레이스홀더 문구는 `IMAGE-MANIFEST.md`에 보존

**예시**
```markdown
[단면도 - DRAM 셀 수직 구조, 실린더형 커패시터 + 매몰 워드라인 + 비트라인 컨택]

*그림 2-1. 1T1C DRAM 셀의 수직 단면 구조*
```

### 9-2. 이미지 매니페스트

| # | 챕터 | 플레이스홀더 | 생성 시 유의사항 |
|---|---|---|---|
| 1 | 00 | `[개념도 - 5계층 피라미드, 5개 축(A1~A5)을 축 라벨로 병기, 각 계층 박스에 대표 수치]` | 단일 속도축이 아님을 시각적으로 드러낼 것 |
| 2 | 01 | `[셀 구조도 - 6T SRAM, 크로스커플 인버터 2개 + 패스게이트 2개, 회로도]` | 표준 회로 기호. WL/BL/BLB 라벨 필수 |
| 3 | 01 | `[비교도 - 노드별 SRAM 비트셀 크기 추이, N5/N3E/N2/18A, 정체 구간 강조]` | 정체 구간(N5→N3E)을 시각적으로 강조 |
| 4 | 02 | `[셀 구조도 - 1T1C DRAM, 트랜지스터 1개 + 커패시터 1개, 워드라인/비트라인 표기, 회로도]` | 센스앰프 위치까지 포함 권장 |
| 5 | 02 | `[단면도 - DRAM 셀 수직 구조, 실린더형 커패시터 + 매몰 워드라인 + 비트라인 컨택]` | storage node contact를 명확히 — 스케일링 병목 지점 |
| 6 | 02 | `[비교도 - 6F² vs 4F²+VCT 셀 레이아웃, 평면도 + 전류 경로 비교]` | 전류 경로 길이 차이가 핵심 |
| 7 | 02 | `[그래프 - DRAM 셀 커패시턴스 추이, 1985년 32 fF → 현행 10 fF 미만 → D1c 5~6 fF]` | "일정 유지" 원칙이 깨지는 변곡점 표시 |
| 8 | 03 | `[구조도 - HBM 스택 단면, TSV 관통 DRAM 다이 12단 + 로직 base die + 실리콘 인터포저 위 GPU 병렬 배치]` | base die를 다른 색으로 — 로직 공정임을 구분 |
| 9 | 03 | `[비교도 - DDR5 vs HBM3E vs HBM4 버스 폭, 64 / 1024 / 2048-bit 시각화]` | 배율 감각이 전달되게 |
| 10 | 04 | `[구조도 - HBF 스택 단면, TSV 적층 NAND 다이 16단 + CBA 구조, 인터포저 위 가속기 인접 배치]` | HBM 구조도(#8)와 나란히 놓고 비교 가능한 동일 스케일 |
| 11 | 04 | `[아키텍처도 - H³ 구성, GPU shoreline에 HBM 직결 + HBM base die 뒤로 D2D 경유 HBF daisy-chain + base die 내 LHB SRAM]` | shoreline 개념이 보이게 |
| 12 | 04 | `[흐름도 - RAG vs CAG 비교, RAG는 매 요청 retrieve+KV 재계산 / CAG는 사전 1회 KV 생성 후 다중 요청 공유]` | 재사용 화살표가 핵심 |
| 13 | 05 | `[셀 구조도 - CTF 방식, 질화물 트랩층에 전하 저장, FG와의 대비 표기]` | FG와 CTF를 좌우 배치 |
| 14 | 05 | `[단면도 - 3D NAND 수직 적층 구조, 332층 채널 홀 관통 + CBA 본딩 계면, 종횡비 강조]` | 종횡비를 과장 없이 — 실제 100:1 감각 |
| 15 | 05 | `[경로도 - 전통적 SSD→CPU DRAM→GPU 경로 vs GDS의 PCIe P2P DMA 직결 경로 비교]` | 병목 지점 표시 |
| 16 | 06 | `[흐름도 - 8대 공정 순서, 전공정/후공정 구분 + 반복 루프 표기]` | 수백 회 반복임이 드러나게 |
| 17 | 06 | `[비교도 - NA 0.33 vs NA 0.55 해상도 차이, 13nm vs 8nm 피처 + 멀티패터닝 스텝 축소 개념]` | 스텝 수 감소가 비용 논리의 핵심 |
| 18 | 06 | `[단면도 - HAR 채널 홀 식각 결함 유형, bowing/twisting/tilting 3종 비교]` | 정상 프로파일과 나란히 |
| 19 | 06 | `[비교도 - TC-NCF vs MR-MUF vs 하이브리드 본딩, 다이 간 접합부 단면 3종 비교, 범프 유무와 갭 차이 강조]` | 갭 축소가 높이 규격과 직결됨을 표시 |
| 20 | 06 | `[개념도 - 5계층이 각기 다른 경로로 '본딩'에 수렴하는 구조, 화살표 수렴 다이어그램]` | 문서 전체의 핵심 서사 이미지 |
| 21 | 04(밀도) | `[비교도 - SRAM/DRAM/NAND 면적당 밀도 로그 스케일 막대, 2D vs 3D 구분 표시 + NAND 층당 환산치 병기]` | 로그 스케일 필수. 선형이면 SRAM/DRAM이 안 보임 |
| 22 | 부록A | `[구성도 - CXL.io/.cache/.mem 3개 서브프로토콜이 단일 PCIe 링크 위에서 동시에 흐르는 구조, 데이터 방향 화살표]` | 방향성이 Type 분류의 근거 |
| 23 | 부록A | `[토폴로지도 - CXL 1.1 단일 호스트 직결 → 2.0 스위치+풀링 → 3.x 패브릭+멀티호스트, 3단계 진화]` | 3단 나열 |

**생성 시 공통 원칙**
- 제조사 공식 이미지 전재 불가 → **전부 자체 생성**. 참고는 하되 재현하지 말 것
- 텍스트 라벨은 한글 + 영문 약어 병기 (예: `매몰 워드라인 (Buried WL)`)
- 계층 간 비교 이미지(#8, #10 등)는 **동일 스케일·동일 스타일**로 생성해야 비교가 성립
- 수치가 들어가는 이미지(#3, #7, #9, #21)는 본문 수치와 반드시 일치시킬 것. 본문 수치 갱신 시 이미지도 함께 갱신

---

## 10. 전체 출처 인덱스

### 10-1. 지정 자료
| URL | 등급 | 상태 |
|---|---|---|
| hyper-accel.github.io/posts/what-is-hbf/ | T4 | 수집 완료 (2026-04-23) |
| hyper-accel.github.io/posts/hbf-workload/ | T4 | 수집 완료 (2026-04-29) |
| hyper-accel.github.io/posts/hbf-challenge/ | T4 | 수집 완료 (2026-05-28) |
| hyper-accel.github.io/posts/what-is-cxl/ | T4 | 수집 완료 (2026-06-04) |
| m.blog.naver.com/tb_elec_engineer/221625396999 | — | **6절로 대체 완료** |
| trade.gov/country-commercial-guides/japan-semiconductors | T0 | 수집 완료 (2025-11-20 갱신) |

### 10-2. 표준화 기구 (T0)
- **JEDEC** `jedec.org` — JESD270-4 (HBM4, 2025-04), JESD209-6 (LPDDR6, 2025-07), DDR5 MRDIMM/MDB/MRCD, JC-40/JC-45/JC-42.3
  - **제약**: DDR6 등 다수 문서가 유료 회원 전용. 7절 대응 규칙 참조
- **Open Compute Project** — HBF 표준화 워크스트림 (2026-02 개설)
- **CXL Consortium** `computeexpresslink.org` — CXL 3.1 사양 개요

### 10-3. 제조사·장비사 공식 (T1)
**메모리**
- SK하이닉스 뉴스룸 `news.skhynix.com` / `news.skhynix.co.kr` — HBF 표준화(2026-02-26), 반도체의 이해 연재, Research Inside 3D NAND CTI
- 삼성반도체 기술블로그 `semiconductor.samsung.com/kr/support/tools-resources/fabrication-process/` — 반도체 백과사전, 8대 공정
- 삼성전자 반도체 뉴스룸 `news.samsungsemiconductor.com/kr/` — 8대 공정 1~9탄
- 삼성 뉴스룸 — HBM4E at NVIDIA GTC 2026
- SanDisk 뉴스룸 — HBF Fact Sheet, MOU(2025-08-06), OCP 킥오프(2026-02-25)
- Kioxia — BiCS10 발표
- 마이크론 `micron.com/products/memory/cxl-memory`

**로직·장비**
- TSMC Research 메모리 페이지
- **ASML** `asml.com/en/products/euv-lithography-systems` — EXE:5200B, High-NA EUV
- **Lam Research** `lamresearch.com/products/our-solutions/cryogenic-etching/` — Cryo 3.0, HAR 식각, backside dep
- **Lam Newsroom** — "How Deposition and Etch Are Reshaping Chips for the AI Era" (2026-04)
- **Tokyo Electron** — 400층 극저온 식각, VCT/4F² 전망
- NVIDIA — GPUDirect Storage `docs.nvidia.com/gpudirect-storage/`, Rubin 아키텍처 발표
- Astera Labs, Panmnesia `panmnesia.com`

### 10-4. TechInsights 다이 분석 (T2.5) — v3 신규 분류
- "DRAM Scaling Trend and Beyond" — 셀 커패시턴스 추이, 6F² 한계, 2T0C IGZO 전망 (EE Times Asia 재게재본으로 공개 확인 가능)
- D1b DRAM 셀 비교 (삼성/SK하이닉스/마이크론) — FMS 2025 발표자료 `files.futurememorystorage.com` 공개본
- "Samsung D1b DRAM Confirmed" — 0.436 Gb/mm², 36.68 mm²
- "Industry-leading DDR5 Technology" — D1y/D1z 세대 3사 다이 면적 비교
- "Micron DDR5 DIMM Technology" — D1z 0.241 Gb/mm²
- "First China-made DDR5 Memory Released from CXMT" — G4 노드 0.239 Gb/mm²
- "Micron D1γ 16 Gb DDR5 DRAM Analysis" (2026-06) — 마이크론 최초 EUV 적용 DRAM 전체 공정 분석
- "Micron Y52K D1β 16 Gb DDR5 DRAM Transistor Characterization" (2026-06)
- 메모리 기술 로드맵 Q3 2026 / "The 4F² Breakthrough: VCT DRAM and the Hybrid Bonding Era"

> **주의**: 상당수 보고서가 유료 구독 전용입니다. 공개 블로그, FMS/ISSCC 발표자료, EE Times Asia 재게재본을 우선 활용하고, 인용 시 "TechInsights 다이 분석 기준"으로 출처를 명시하십시오.

### 10-5. 논문 (T2)
- **H³**: IEEE CAL 2026, DOI 10.1109/LCA.2026.3660969
- **하이브리드 본딩 열특성**: "System-Level Thermal Characterization of Hybrid Cu Bonding HBM with 2.5D Advanced Packaging", IEEE, 2026-06
- **CAG**: arXiv:2412.15605 (WWW 2025)
- **HAVEN**: arXiv:2603.01175
- **StreamingLLM**: arXiv:2309.17453 (ICLR 2024)
- **InfLLM**: arXiv:2402.04617 (NeurIPS 2024)
- **Quest**: arXiv:2406.10774 (ICML 2024)
- **FlexGen**: arXiv:2303.06865 (ICML 2023)
- **MoE SSD offloading 반론** (SNU): arXiv:2508.06978 (IEEE CAL 2025)
- **Memory Pooling With CXL**: IEEE Micro 43(2), DOI 10.1109/MM.2023.3237491
- **CXL 개론**: ACM Computing Surveys 56(11) Art.290, DOI 10.1145/3669900 (arXiv:2306.11227)
- **NVMe offloading I/O 분석**: DOI 10.1145/3719330.3721230 (CHEOPS '25)
- **3nm GAA-FET SRAM self-heating/방사선** (SJSU, Sandia), 2026-07
- **DRAM 셀 커패시턴스 역사**: IEEE JSSC 1985 (32 fF), IEEE JSSC 1988 (33 fF), IEDM 2004 MESH capacitor (30 fF)
- Counterpoint Research, "Scaling to 1,000-Layer 3D NAND in the AI Era" (Lam 후원 백서)

### 10-6. 분석기관·기술 매체 (T3)
- **SemiAnalysis** — "The Memory Wall: Past, Present, and Future of DRAM", VLSI 2025 리뷰
- **SemiEngineering** — "HBM4 Sticks With Microbumps, Postponing Hybrid Bonding"(2026-01), "Flash Getting Stacked High-Bandwidth Version"(2026-05), "Metrology Digs Deep To Produce Next-Generation 3D NAND"(2025-12)
- **Blocks & Files** — 332층 BiCS10 샘플링(2026-07-03), 삼성 900층(2026-05-28)
- **Tom's Hardware** — BiCS10, LPDDR6, SRAM 밀도 비교, HBM 로드맵
- **EE Times / EE Times Asia** — "The State of HBM4 Chronicled at CES 2026", TechInsights 칼럼 재게재
- **TrendForce** — 400층 NAND, HBF 표준화, HBM4E 커스텀, High-NA EUV, HBM 높이 완화(2026-03-06, 2026-04-01)
- **Semiconductor Digest** — "How Etch Breakthroughs Are Tackling 3D NAND Scaling Challenges"
- **The Elec / ZDNet Korea / 조선일보 / 뉴시스 / 전자신문** — 국내 공정·장비·표준 동향 (HBM 높이 완화 논의의 1차 보도원)
- **KAIST TERALAB** — "2026 HBF Workload and Roadmap" (YouTube), `tera.kaist.ac.kr`

---

## 11. 산업·시장 컨텍스트 (appendix-c 전용, 본문 격리)

**일본 반도체 (trade.gov, 2025-11-20 갱신, T0)**
- 일본 반도체 시장: 2024년 474억 달러 → 2025년 추정 519억 달러. 글로벌은 2030년 1조 달러 전망
- 일본 정부 3년간 지원: GDP의 0.71%, 약 257억 달러
- 소재·장비 점유율: 코터/디벨로퍼 약 88%, 실리콘 웨이퍼 53%, 포토레지스트 50% (2024-06 Brookings 인용)
- Shin-Etsu + SUMCO 실리콘 웨이퍼 약 90%, JSR·Tokyo Ohka Kogyo 포토레지스트 약 90%, 포토마스크 약 30%
- Rapidus: 2nm 양산 목표 2027년, 정부 지원 61억 달러 이상. 홋카이도 치토세 팹에서 2nm급 프로토타입 트랜지스터 동작 검증. IBM 공동 개발
- **6절 연결**: 일본이 장악한 코터/디벨로퍼·레지스트·웨이퍼는 모두 6-2 노광 공정의 전제 조건입니다. 시장 자료로만 쓰지 말고 **공정 챕터의 공급망 각주**로 활용하십시오

**2026 메모리 시장 (T3, 시각 차이 큼 — 양측 병기 필수)**
- 강세: DRAM 3사 2026 CapEx 전년 대비 평균 40% 이상 상향, 유의미한 출하 확대는 2027년 하반기 이후 / TrendForce 2026 Q1 NAND 가격 QoQ +85~90% 전망 / Gartner 2026년 DRAM 가격 +47% 전망 / SK하이닉스는 2027년이 최악의 공급 부족 해가 될 가능성 언급
- 약세: Raymond James는 DRAM·NAND ASP가 2026년 중반 정점 가능성 제기
- **집필 규칙**: 시장 전망은 반년이면 뒤집힙니다. 기술 문서 본문에 시황 수치를 섞지 말고 부록에 날짜를 박아 격리하십시오

---

## 12. 남은 확인 항목 (v3 갱신)

**해소됨**
- ~~DDR6 JEDEC 원문 확인~~ → 유료 제약 확인, T3 기반 + 각주 명시 방침 확정
- ~~DRAM 셀 리텐션 커패시턴스~~ → 정정 완료 (10 fF 미만)
- ~~DRAM 면적당 밀도 재수집~~ → 중앙값 435 Mb/mm² / 범위 431~447 확정
- ~~HBM4E 높이 완화 확정 여부~~ → 미확정 확인, "논의 중" 서술로 확정
- ~~HBF 스펙 대응 방침~~ → 공개분 동결 정책 확정
- ~~다이어그램 정책~~ → 플레이스홀더 규약 + 매니페스트 23건 확정 (9절)

**추적 지속 (집필 중 재확인)**
- [ ] JEDEC HBM4E 높이 규격 확정 발표 → 확정 시 3-3절 및 6-4절 동시 갱신
- [ ] HBF 세부 스펙 공개 → 3-4절 전면 갱신
- [ ] DDR6 비준 → 3-2절 및 7절 갱신
- [ ] TSMC N2 비트셀 크기 논쟁 결론 (IEDM/ISSCC 후속 발표)
- [ ] D1c 세대 다이 분석 공개 시 4절 밀도 표 갱신

**신규 확인 필요**
- [ ] HBM4E 양산 시점 보도 상충: 일부 자료가 삼성 2026-02 HBM4E 양산 개시라 서술하나, 다른 자료는 2027년 출시로 봄. HBM4 양산과 혼동됐을 가능성이 높으므로 인용 전 교차 확인 필요
- [ ] TechInsights가 삼성 D1b 셀 크기에서 F 추출 시 사용한 **7.8F² 기준**의 근거 — 교과서적 6F²와의 괴리를 각주로 설명하려면 원문 확인 권장
