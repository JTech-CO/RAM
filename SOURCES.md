# SOURCES — 출처 인덱스

> **최종 검증: 2026-07-29**
> 이 문서 모음집의 모든 수치는 여기에 등록된 출처로 소급됩니다.
> 반도체 수치는 6개월이면 낡습니다. 인용 전 각 항목의 확인일과 등급을 확인하십시오.

**근거 자료는 두 묶음입니다.**

| 묶음 | 조사일 | 담당 범위 |
|---|---|---|
| v3 소스 팩 | 2026-07-28 | 5계층·공정(노광·식각·본딩)·CXL·워크로드·시장 |
| [v4 부록](_internal/RAM-source-pack-v4-addendum.md) | 2026-07-29 | DRAM 커패시터 제조 공정, 셀 트랜지스터, 리텐션·refresh, Row Hammer, ECC, 계층별 신뢰성 |

v4 부록의 전체 출처 인덱스는 해당 파일 10절에, **확인 실패 항목 전체 목록은 11절**에 있습니다. 아래 8절은 그중 핵심만 옮긴 것입니다.

각 문서의 `참고 문헌` 절은 이 인덱스를 가리킵니다. 본문에서 특정 수치의 근거를 추적할 때는 해당 문서의 각주 → 이 인덱스의 등급별 절 순서로 따라오십시오.

---

## 1. 출처 등급 체계

| 등급 | 정의 | 집필 시 취급 |
|---|---|---|
| **T0** | 표준화 기구 원문 (JEDEC, OCP, CXL Consortium) | 무조건 우선. 단 **유료 문서 제약**이 있음 — [5절](#5-t0-접근-제약과-대응-규칙) 참조 |
| **T1** | 제조사·장비사 공식 발표·기술 문서 (SK하이닉스, 삼성, 마이크론, SanDisk/Kioxia, TSMC, ASML, Lam, TEL, NVIDIA) | 마케팅 표현을 걷어내고 수치만 사용 |
| **T2** | 동료평가 논문·학회 발표 (IEEE, ISSCC, IEDM, VLSI, arXiv) | DOI 또는 arXiv ID 명시 |
| **T2.5** | **TechInsights 다이 분석** — 실물 역공학 실측치 | **수치 근거로는 T1급 신뢰.** 다만 상당수 보고서가 유료. 공개 블로그·컨퍼런스 발표 자료 우선 활용 |
| **T3** | 전문 분석기관·기술 매체 (SemiAnalysis, SemiEngineering, Tom's Hardware, EE Times, TrendForce, Blocks & Files, The Elec, ZDNet Korea) | 교차 확인 후 사용 |
| **T4** | 개인·기업 기술 블로그, 위키 | 구조 이해용 참고만. **수치 인용 금지** |

**등급 밖 표기 두 가지**

| 표기 | 뜻 |
|---|---|
| **일반 통용** | 특정 출처에 귀속시킬 수 없을 만큼 널리 확립된 값. 예: SRAM 접근 지연 1 ns 이하, NAND 랜덤 읽기 50~100 µs, SSD 대역폭 약 7 GB/s. 등급을 붙이면 없는 근거를 만들어내는 셈이 되므로 그대로 둡니다 |
| **—** (또는 정성 표기) | 수치가 아닌 정성 값. 예: 비트당 비용 "높음", 결합도 "인터포저". 등급 부여 대상이 아닙니다 |

**신뢰도 한정 표기 (v4 신규)** — 등급만으로는 부족한 경우 함께 답니다.

| 표기 | 뜻 |
|---|---|
| `T0 (초안)` | JC42.3 위원회 회람본(`DDR5 Full Spec Draft Rev0.1`) 기반. **"JESD79-5 표준에 따르면"이라 단정하지 말고 "DDR5 사양 초안 기준"으로** 서술합니다. 이 초안에는 ECS 임계값이 `TBD`, MR15 일부가 `RFU`로 남아 있고 RFM·PRAC 조항 자체가 없습니다 |
| `T1 (특허)` | 특허 명세 기반. **청구된 실시례이지 양산 채택 증거가 아닙니다** |
| `단일 출처` | 교차 확인이 되지 않은 값 |
| `2차 인용` | 원문 미확인, 인용의 인용 |
| `스니펫` | 검색엔진이 반환한 초록·요약만 확인, 원문 미정독 (다수 T1/T3 사이트가 HTTP 403) |

**적용 규칙**

- 표에 들어가는 수치에는 `출처` 열을 두고 등급 태그를 답니다.
- 본문 산문 속 핵심 수치에는 각주를 답니다. 각주에는 등급과 확인일을 함께 적습니다.
- T4 출처에서 가져온 것은 구조 설명에 한정하며, 같은 내용의 수치는 반드시 T0~T3로 백업합니다.
- 미비준·미공개 표준의 수치는 본문에서 `[미비준]` / `[초안 목표]` / `[벤더 목표치]` / `[미공개]` / `[미확정]` 배지를 달아 확정 사실과 구분합니다.

---

## 2. 표준화 기구 (T0)

| 기구 | 문서 / 항목 | 비고 |
|---|---|---|
| **JEDEC** (`jedec.org`) | **JESD270-4** — HBM4, 2025-04 공개 | [03-hbm.md](03-hbm.md) |
| JEDEC | **JESD209-6** — LPDDR6, 2025-07 공개 | DDR6 계열 중 최초 확정 표준. [02-dram.md](02-dram.md) |
| JEDEC | DDR5 MRDIMM / MDB / MRCD | MDB 표준 공개, MRCD 진행 중, Gen2 로드맵 진행(2026-04) |
| JEDEC | JC-40 / JC-45 / **JC-42.3** | JC-42.3에서 DDR6 타이밍·시그널링 파라미터 조율 중 |
| JEDEC | HBM4E 패키지 높이 | **통합 표준 부재. 825~900 µm 논의 중, 2026-07 현재 확정 발표 확인되지 않음** |
| **Open Compute Project** | HBF 표준화 워크스트림 (2026-02 개설) | HBF는 JEDEC이 아니라 OCP 경로. [04-hbf.md](04-hbf.md) |
| **CXL Consortium** (`computeexpresslink.org`) | CXL 3.1 사양 개요 | [appendix-a-cxl.md](appendix-a-cxl.md) |
| **trade.gov** | Country Commercial Guide — Japan, Semiconductors (2025-11-20 갱신) | [appendix-c-industry.md](appendix-c-industry.md) |

> **제약**: DDR6를 포함한 다수 JEDEC 문서가 유료 회원 전용입니다. 대응 규칙은 [5절](#5-t0-접근-제약과-대응-규칙)을 참조하십시오.

---

## 3. 제조사·장비사 공식 (T1)

### 3-1. 메모리

| 출처 | 주요 인용 항목 | 관련 문서 |
|---|---|---|
| **SK하이닉스 뉴스룸** (`news.skhynix.com`, `news.skhynix.co.kr`) | HBF 표준화(2026-02-26), 「반도체의 이해」 연재, Research Inside 3D NAND CTI, CTF 상용화 | [04](04-hbf.md), [05](05-nand.md), [06](06-process.md) |
| **삼성반도체 기술블로그** (`semiconductor.samsung.com/kr/support/tools-resources/fabrication-process/`) | 반도체 백과사전, 8대 공정 | [06](06-process.md) |
| **삼성전자 반도체 뉴스룸** (`news.samsungsemiconductor.com/kr/`) | 「반도체 8대 공정」 1~9탄 | [06](06-process.md) |
| **삼성 뉴스룸** | HBM4E at NVIDIA GTC 2026 | [03](03-hbm.md) |
| **SanDisk 뉴스룸** | HBF Fact Sheet, SK하이닉스 MOU(2025-08-06), OCP 킥오프(2026-02-25) | [04](04-hbf.md) |
| **Kioxia** | BiCS10 발표 (332층, 29 Gb/mm² 초과, 4,800 MT/s) | [05](05-nand.md) |
| **마이크론** (`micron.com/products/memory/cxl-memory`) | CZ120 / CZ122 CXL 메모리 확장 | [부록 A](appendix-a-cxl.md) |

### 3-2. 로직·장비

| 출처 | 주요 인용 항목 | 관련 문서 |
|---|---|---|
| **TSMC Research** | 메모리 페이지, N2 SRAM 매크로 밀도 | [01](01-sram.md) |
| **ASML** (`asml.com/en/products/euv-lithography-systems`) | TWINSCAN EXE:5200B, High-NA EUV(NA 0.55), 2026 EUV/DUV 전망 | [06](06-process.md) |
| **Lam Research** (`lamresearch.com/products/our-solutions/cryogenic-etching/`) | Cryo 3.0, HAR 식각 챔버 7,500대 이상·누적 500만 장 이상, backside deposition(Coronus DX, VECTOR DT, EOS) | [06](06-process.md) |
| **Lam Newsroom** | "How Deposition and Etch Are Reshaping Chips for the AI Era" (2026-04) | [06](06-process.md) |
| **Tokyo Electron** | 400층용 10 µm 초고속 극저온 식각(GWP 84% 저감), VCT/4F² 2027~2028 전망 | [02](02-dram.md), [06](06-process.md) |
| **NVIDIA** (`docs.nvidia.com/gpudirect-storage/`) | GPUDirect Storage, Rubin 아키텍처 발표 | [03](03-hbm.md), [05](05-nand.md), [부록 B](appendix-b-workloads.md) |
| **Astera Labs**, **Panmnesia** (`panmnesia.com`) | Leo(Microsoft Azure M-series 채용), PANSWITCH CXL 3.2 | [부록 A](appendix-a-cxl.md) |

---

## 4. TechInsights 다이 분석 (T2.5)

실물 역공학 실측치이므로 수치 근거로는 T1급으로 취급합니다.

| 보고서 / 자료 | 인용 항목 | 관련 문서 |
|---|---|---|
| "DRAM Scaling Trend and Beyond" | 셀 커패시턴스 추이, 6F² 한계(10 nm이 마지막 노드 가능성), 2T0C IGZO 전망. EE Times Asia 재게재본으로 공개 확인 가능 | [02](02-dram.md) |
| D1b DRAM 셀 비교 (삼성 / SK하이닉스 / 마이크론) | 다이 면적·비트 밀도·셀 크기·F. FMS 2025 발표자료 `files.futurememorystorage.com` 공개본 | [02](02-dram.md), [00](00-memory-hierarchy.md) |
| "Samsung D1b DRAM Confirmed" | 0.436 Gb/mm², 다이 면적 36.68 mm² | [02](02-dram.md) |
| "Industry-leading DDR5 Technology" | D1y/D1z 세대 3사 다이 면적 비교 | [02](02-dram.md) |
| "Micron DDR5 DIMM Technology" | D1z 0.241 Gb/mm² | [02](02-dram.md) |
| "First China-made DDR5 Memory Released from CXMT" | G4 노드 0.239 Gb/mm² | [02](02-dram.md) |
| "Micron D1γ 16 Gb DDR5 DRAM Analysis" (2026-06) | 마이크론 최초 EUV 적용 DRAM 전 공정 분석(DPF), 0.33 NA | [06](06-process.md) |
| "Micron Y52K D1β 16 Gb DDR5 DRAM Transistor Characterization" (2026-06) | 트랜지스터 특성 | [02](02-dram.md) |
| 메모리 기술 로드맵 Q3 2026 | 추적 항목: 3D DRAM, X-DRAM, IGZO DRAM, VCT 기반 4F², EUVL | [02](02-dram.md) |
| "The 4F² Breakthrough: VCT DRAM and the Hybrid Bonding Era" | ISSCC 2026 기준 DRAM 다음 변곡점 | [02](02-dram.md), [06](06-process.md) |

> **주의**: 상당수 보고서가 유료 구독 전용입니다. 공개 블로그, FMS/ISSCC 발표자료, EE Times Asia 재게재본을 우선 활용하고, 인용 시 "TechInsights 다이 분석 기준"으로 출처를 명시하십시오.

**7.8F² 관련 미확인 사항**: TechInsights가 삼성 D1b 셀 크기(0.00123 µm²)에서 F를 추출할 때 7.8F² 기준을 사용했습니다. 교과서적 6F²와의 괴리에 대한 원문 근거는 아직 확인하지 못했으며, [02-dram.md](02-dram.md)에서 각주로 처리했습니다.

---

## 5. T0 접근 제약과 대응 규칙

JEDEC 사이트에서 DDR6 관련 문서는 대부분 유료 회원 전용이라 원문 직접 확인이 불가합니다. 이 모음집의 DDR6 서술은 **T3(기술 매체) + 벤더 로드맵 자료** 기반입니다.

**대응 규칙 (DDR6·HBM4E·HBF 공통 적용)**

1. 해당 서술에 다음 취지의 각주를 답니다.
   > JEDEC 사양서는 유료 공개이며, 이 수치는 공개 보도 및 벤더 로드맵을 종합한 값으로 최종 비준 사양과 다를 수 있습니다.
2. 확정형 서술을 쓰지 않습니다. `DDR6는 ~이다` 대신 `DDR6 초안은 ~를 목표로 합니다`.
3. 배지로 상태를 표시합니다 — `[미비준]`, `[초안 목표]`, `[벤더 목표치]`, `[미공개]`, `[미확정]`.

**HBF 동결 정책**: HBF는 2026-07-28 시점 공개 정보만 사용하며, 미공개 스펙에 대한 추정·유추 서술을 금지합니다. 미공개 항목 목록은 [04-hbf.md](04-hbf.md)에 명시되어 있습니다.

---

## 6. 논문 (T2)

| 약칭 | 서지 | 식별자 | 관련 문서 |
|---|---|---|---|
| **H³** | M. Ha, E. Kim, H. Kim, "H³: Hybrid Architecture using High Bandwidth Memory and High Bandwidth Flash for Cost-Efficient LLM Inference," *IEEE Computer Architecture Letters*, 2026 | DOI 10.1109/LCA.2026.3660969 | [04](04-hbf.md) |
| **하이브리드 본딩 열특성** | "System-Level Thermal Characterization of Hybrid Cu Bonding HBM with 2.5D Advanced Packaging," IEEE, 2026-06 | — | [06](06-process.md) |
| **CAG** | B. J. Chan et al., "Don't Do RAG: When Cache-Augmented Generation is All You Need for Knowledge Tasks," WWW 2025 | arXiv:2412.15605 | [04](04-hbf.md), [부록 B](appendix-b-workloads.md) |
| **HAVEN** | 거대 vector DB를 HBF에 배치, 인접 search 엔진에서 top-k만 전달 | arXiv:2603.01175 | [부록 B](appendix-b-workloads.md) |
| **StreamingLLM** | attention sink + sliding window (ICLR 2024) | arXiv:2309.17453 | [04](04-hbf.md), [부록 B](appendix-b-workloads.md) |
| **InfLLM** | query 기반 동적 KV 선택 (NeurIPS 2024) | arXiv:2402.04617 | [부록 B](appendix-b-workloads.md) |
| **Quest** | query 기반 동적 KV 선택 (ICML 2024) | arXiv:2406.10774 | [부록 B](appendix-b-workloads.md) |
| **FlexGen** | (ICML 2023) | arXiv:2303.06865 | [부록 B](appendix-b-workloads.md) — 목록 등재만, 본문 서술 없음 |
| **MoE SSD offloading 반론** | K. Kyung, S. Yun, J. H. Ahn (SNU), "SSD Offloading for LLM Mixture-of-Experts Weights Considered Harmful in Energy Efficiency," IEEE CAL 2025 | arXiv:2508.06978 | [부록 B](appendix-b-workloads.md) |
| **Memory Pooling With CXL** | IEEE Micro 43(2) | DOI 10.1109/MM.2023.3237491 | [부록 A](appendix-a-cxl.md) |
| **CXL 개론** | ACM Computing Surveys 56(11) Art.290 | DOI 10.1145/3669900 (arXiv:2306.11227) | [부록 A](appendix-a-cxl.md) |
| **NVMe offloading I/O 분석** | CHEOPS '25 | DOI 10.1145/3719330.3721230 | [부록 B](appendix-b-workloads.md) |
| **3nm GAA-FET SRAM self-heating/방사선** | SJSU, Sandia, 2026-07 | — | [01](01-sram.md) |
| **DRAM 셀 커패시턴스 역사** | IEEE JSSC 1985 (1Mb, 32 fF), IEEE JSSC 1988 (16Mb, 33 fF), IEDM 2004 MESH capacitor (30 fF) | — | [02](02-dram.md) |

**등급 예외 1건**: Counterpoint Research, "Scaling to 1,000-Layer 3D NAND in the AI Era"는 소스 자료에서 논문 목록 끝에 놓여 있었으나, 실제로는 **장비사(Lam) 후원 백서**이므로 동료평가 논문(T2)이 아니라 **T3(분석기관)**으로 취급합니다. 인용 시 후원 관계를 함께 밝힙니다. → [05-nand.md](05-nand.md), [06-process.md](06-process.md)

---

## 7. 분석기관·기술 매체 (T3)

| 출처 | 주요 인용 항목 | 관련 문서 |
|---|---|---|
| **SemiAnalysis** | "The Memory Wall: Past, Present, and Future of DRAM", VLSI 2025 리뷰, DRAM 노드 로드맵(1c HVM, 1d 전망) | [02](02-dram.md) |
| **SemiEngineering** | "HBM4 Sticks With Microbumps, Postponing Hybrid Bonding"(2026-01), "Flash Getting Stacked High-Bandwidth Version"(2026-05), "Metrology Digs Deep To Produce Next-Generation 3D NAND"(2025-12) | [03](03-hbm.md), [04](04-hbf.md), [06](06-process.md) |
| **Blocks & Files** | 332층 BiCS10 샘플링(2026-07-03), 삼성 900층(2026-05-28) | [05](05-nand.md) |
| **Tom's Hardware** | BiCS10, LPDDR6, SRAM 밀도 비교, HBM 로드맵 | [01](01-sram.md), [02](02-dram.md), [05](05-nand.md) |
| **EE Times / EE Times Asia** | "The State of HBM4 Chronicled at CES 2026", TechInsights 칼럼 재게재 | [02](02-dram.md), [03](03-hbm.md) |
| **TrendForce** | 400층 NAND, HBF 표준화, HBM4E 커스텀, High-NA EUV, HBM 높이 완화(2026-03-06, 2026-04-01), NAND 가격 전망 | [03](03-hbm.md), [05](05-nand.md), [부록 C](appendix-c-industry.md) |
| **Semiconductor Digest** | "How Etch Breakthroughs Are Tackling 3D NAND Scaling Challenges" | [06](06-process.md) |
| **The Elec / ZDNet Korea / 조선일보 / 뉴시스 / 전자신문** | 국내 공정·장비·표준 동향. HBM 높이 완화 논의의 1차 보도원, 삼성 커스텀 HBM 조직 개편, SK하이닉스 하이브리드 본딩 견해 | [03](03-hbm.md), [06](06-process.md) |
| **KAIST TERALAB** | "2026 HBF Workload and Roadmap" (YouTube), `tera.kaist.ac.kr` | [04](04-hbf.md) |
| **FinancialContent / Introl** | HBM 2026년 시장 규모 추정 (각각 546억 / 580억 달러) | [부록 C](appendix-c-industry.md) |
| **Gartner / Raymond James** | 2026 DRAM 가격 전망(+47%) / ASP 정점 시점 반대 견해 | [부록 C](appendix-c-industry.md) |
| **Brookings** | 일본 소재·장비 점유율 (2024-06 인용) | [부록 C](appendix-c-industry.md) |

---

## 8. 구조 이해용 참고 (T4) — 수치 인용 금지

| URL | 수집일 | 용도 |
|---|---|---|
| `hyper-accel.github.io/posts/what-is-hbf/` | 2026-04-23 | HBF 개념 구조 |
| `hyper-accel.github.io/posts/hbf-workload/` | 2026-04-29 | HBF 워크로드 개념 |
| `hyper-accel.github.io/posts/hbf-challenge/` | 2026-05-28 | HBF 과제 개념 |
| `hyper-accel.github.io/posts/what-is-cxl/` | 2026-06-04 | CXL 개념 구조 |

이 항목들에서 얻은 구조 설명은 본문에 반영하되, 수치는 전부 T0~T3 출처로 백업했습니다.

---

## 9. 미확정·추적 항목

이 모음집이 다루는 주제 중 아래는 2026-07-28 기준으로 확정되지 않았습니다. 확정 시 해당 문서를 갱신해야 합니다.

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| JEDEC HBM4E 패키지 높이 규격 (825~900 µm 논의) | **미확정** | [03-hbm.md](03-hbm.md), [06-process.md](06-process.md), [appendix-c-industry.md](appendix-c-industry.md) |
| HBM4E 통합 JEDEC 표준 존재 여부 | **부재** (벤더별 차별화 버전) | [03-hbm.md](03-hbm.md) |
| HBF 세부 스펙 (패키징·인터페이스·내구성·전력·가격) | **미공개** | [04-hbf.md](04-hbf.md) |
| DDR6 JEDEC 비준 | **미비준** (JC-42.3 조율 중) | [02-dram.md](02-dram.md) |
| TSMC N2 HD SRAM 비트셀 크기 논쟁 | **진행 중** (0.0175~0.021 µm² 보고 편차) | [01-sram.md](01-sram.md) |
| D1c 세대 다이 분석 공개 | **미공개** | [02-dram.md](02-dram.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |
| HBM4E 양산 시점 | **보도 상충** — 삼성 2026-02 양산 개시라는 서술과 2027년 출시라는 서술이 병존. HBM4 양산과 혼동됐을 가능성이 높아 이 모음집은 인용하지 않음 | [03-hbm.md](03-hbm.md) |
| DDR5 세대의 Row Hammer 실측 임계값 | **확인 실패** — 온다이 ECC가 단일 비트 플립을 조용히 정정하고 내장 완화 로직이 임계 도달 전 개입해 외부 관측이 곤란 (T2, DRAM-Profiler arXiv:2404.18396) | [07-reliability.md](07-reliability.md) |
| DDR4 MAC 값 표 (200K/300K/…) | **확인 실패** — JEDEC SPD Annex L byte 41이 로그인 벽 뒤 | [07-reliability.md](07-reliability.md) |
| PRAC의 실제 양산 탑재 현황 | **확인 실패** — JESD79-5C는 사양이지 탑재 현황이 아님. 어느 벤더 제품이 탑재했는지 T1 근거 없음 | [07-reliability.md](07-reliability.md) |
| 셀 커패시턴스(10 fF 미만)와 리텐션 마진의 정량 관계 | **확인 실패** — fF 단위 근거가 어느 자료 계열에도 없음. **두 사실을 인과로 연결하는 서술 금지** | [02-dram.md](02-dram.md), [07-reliability.md](07-reliability.md) |
| DRAM 커패시터 세대별 종횡비 (D1x~D1c) | **확인 실패** — 세대에 종횡비를 붙인 공개 자료 없음. 확보된 것은 세대 미특정 `단일 출처` "100:1 접근"뿐 | [06-process.md](06-process.md) |
| 3D NAND 100:1 도달 시점 | **상충** — v3는 "1,000층에서 접근", JJAP 리뷰(T2, DOI 10.35848/1347-4065/accbc7)는 "수백 층에서 이미 초과". 홀 직경 기준(상부 CD vs 최소 CD) 차이 가능성 | [06-process.md](06-process.md), [05-nand.md](05-nand.md) |
| 극저온 식각의 DRAM 커패시터 적용 여부 | **확인 실패** — Lam 공식 페이지는 3D NAND만 명시. 적용·미적용 어느 쪽 근거도 없음 | [06-process.md](06-process.md) |
| HBM ECC 규격 원문 | **미확인** — JESD238(HBM3) 보도자료 `단일 출처`만 확보, 규격 원문 아님 | [03-hbm.md](03-hbm.md), [07-reliability.md](07-reliability.md) |
| 3nm GAA-FET SRAM self-heating·방사선 연구 (SJSU/Sandia) | **원문 미확보** — v3에 등재되어 있으나 검증도 반박도 되지 않음 | [01-sram.md](01-sram.md) |
| TechInsights의 7.8F² 기준 근거 | **원문 미확인** | [02-dram.md](02-dram.md) |
| 4F²의 이론적 밀도 이득 "약 30%" | **수치 정합 불일치** — 셀 면적비 2/3를 밀도로 환산하면 1.5배(약 50%)이며, 30%는 면적 축소율(약 33%)에 가까움. 셀 층위인지 다이 층위인지 명시한 1차 자료 미확인 | [02-dram.md](02-dram.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |

---

## 10. 갱신 이력

| 날짜 | 내용 |
|---|---|
| 2026-07-28 | 초판. 소스 팩 v3 기준으로 전 문서 작성 및 출처 인덱스 구축 |
| 2026-07-29 | v4 부록 조사 반영. [06-process.md](06-process.md)에 5절(DRAM 셀을 만든다는 것) 신설, [07-reliability.md](07-reliability.md) 신설. v3 정정 2건(MESH 세대 표기, Lam Cryo 3.0 수치 혼합), 상충 1건 병기(3D NAND 100:1 도달 시점) |

**v4에서 새로 확인된 주요 오인용 함정** — 인용 전 반드시 확인하십시오.

| 함정 | 실제 |
|---|---|
| Schroeder 2009를 "미세화 → 오류율 증가"의 근거로 인용 | 논문 결론은 **정반대**입니다. "신세대 DIMM에서 오류율 증가 증거를 관측하지 못했다"고 명시합니다 |
| DDR5 온다이 ECC를 "SECDED"로 표기 | 1차 자료는 일관되게 **SEC(단일 정정)**뿐입니다. Micron이 128 데이터 비트 + 8 패리티로는 더블 비트 검출이 불가함을 명시합니다 |
| 세대 무관하게 "64 ms refresh" 사용 | DDR3/DDR4 한정입니다. **DDR5는 refresh window 32 ms, tREFI 3.9 µs** |
| HKMG를 DRAM "셀 트랜지스터"에 적용한다고 서술 | HKMG는 **주변/코어 트랜지스터**용입니다. 셀 매몰 워드라인 쪽은 DWMG(워크펑션 분할)입니다 |
| ZAZ를 "3층 샌드위치"로 서술 | Al₂O₃는 ALD 4~5 사이클 미만이라 **별개 층이 아니라 도판트**이며, 역할도 유전율이 아니라 **누설 차단**입니다 |
| NAND P/E 사이클 수치를 현행 3D NAND에 적용 | 확보된 값은 **2017년 발표, 평면(planar) NAND 기준**입니다 |

**갱신 규칙**

- 수치를 바꿀 때는 본문·이 인덱스·[assets/IMAGE-MANIFEST.md](assets/IMAGE-MANIFEST.md)의 해당 이미지 유의사항을 **동시에** 갱신합니다.
- 각 문서 상단의 `최종 검증` 배너 날짜를 함께 올립니다.
- 9절의 미확정 항목이 확정되면 해당 행을 10절 갱신 이력으로 옮깁니다.
