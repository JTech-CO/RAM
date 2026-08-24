# SOURCES - 출처 인덱스

> **최종 검증: 2026-08-25**
> 이 문서 모음집의 모든 수치는 여기에 등록된 출처로 소급됩니다.
> 반도체 수치는 6개월이면 낡습니다. 인용 전 각 항목의 확인일과 등급을 확인하십시오.

**근거 자료는 세 묶음입니다.**

| 묶음 | 조사일 | 담당 범위 | 저장소 내 위치 |
|---|---|---|---|
| v3 소스 팩 | 2026-07-28 | 5계층·공정(노광·식각·본딩)·CXL·워크로드·시장 | `_internal/RAM-source-pack.md` |
| [v4 부록](_internal/RAM-source-pack-v4-addendum.md) | 2026-07-29 | DRAM 커패시터 제조 공정, 셀 트랜지스터, 리텐션·refresh, Row Hammer, ECC, 계층별 신뢰성 | `_internal/RAM-source-pack-v4-addendum.md` |
| **v5 조사** | 2026-07-29 | DRAM 뱅크·랭크·서브채널, 코어 타이밍, 대역폭 효율 / 웨이퍼 테스트(EDS), 리던던시·리페어, 적층 수율 | `_internal/research-v5/` (6종). **통합 부록 없이 조사 파일이 곧 근거**입니다 |
| **v6 갱신** | 2026-08-12 (2026-08-22 · 08-25 재확인) | 초판 공개 후 2주간의 표준·제품 변화 추적 (SPHBM4 공표, HBF OCP 첫 사양, FMS 2026 NAND 세대 전환, HBM4E 샘플 출하, 3Q26 계약가) | **조사 파일 없음.** 근거는 각 문서의 각주에 직접 등재했으며, 아래 2·3·7절 인덱스에도 반영했습니다 |
| **v6.2 갱신** | 2026-08-25 | Hot Chips 2026(2026-08-23 – 25) 메모리 세션 - 삼성 base die 로드맵과 zHBM, SK하이닉스 패키징 로드맵, HBF 튜토리얼 | **조사 파일 없음.** 근거가 **전부 학회 현장 보도(T3, `2차 인용`)이며 발표 슬라이드 원문을 확보하지 못했습니다** |

v4 부록의 원 조사 파일 6종도 `_internal/research-v4/`에 있습니다. 부록은 이들을 통합·정리한 것이며, 개별 출처 URL과 확인 경로는 조사 파일 쪽이 더 상세합니다.

v4 부록의 전체 출처 인덱스는 해당 파일 10절에, **확인 실패 항목 전체 목록은 11절**에 있습니다. 아래 8절은 그중 핵심만 옮긴 것입니다.

**v5 조사 파일은 `_internal/research-v5/`에 있습니다.** 조사에서 인용된 **1차 출처는 아래 2·3·6절 인덱스에도 직접 등록**해 두었습니다. v5 서술의 근거를 확인할 때는 조사 파일과 함께 [02-dram.md](02-dram.md) 10절, [08-test-yield.md](08-test-yield.md) 6절의 각주·참고 문헌을 보십시오. 두 문서의 각주가 1차 자료의 리비전·발행일·확인 경로(원문 직접 확인 / 검색 요약 경유 / 접근 실패)를 항목별로 밝힙니다.

각 문서의 `참고 문헌` 절은 이 인덱스를 가리킵니다. 본문에서 특정 수치의 근거를 추적할 때는 해당 문서의 각주 → 이 인덱스의 등급별 절 순서로 따라오십시오.

---

## 1. 출처 등급 체계

| 등급 | 정의 | 집필 시 취급 |
|---|---|---|
| **T0** | 표준화 기구 원문 (JEDEC, OCP, CXL Consortium) | 무조건 우선. 단 **유료 문서 제약**이 있음 - [5절](#5-t0-접근-제약과-대응-규칙) 참조 |
| **T1** | 제조사·장비사 공식 발표·기술 문서 (SK하이닉스, 삼성, 마이크론, SanDisk/Kioxia, TSMC, ASML, Lam, TEL, NVIDIA) | 마케팅 표현을 걷어내고 수치만 사용 |
| **T2** | 동료평가 논문·학회 발표 (IEEE, ISSCC, IEDM, VLSI, arXiv) | DOI 또는 arXiv ID 명시 |
| **T2.5** | **TechInsights 다이 분석** - 실물 역공학 실측치 | **수치 근거로는 T1급 신뢰.** 다만 상당수 보고서가 유료. 공개 블로그·컨퍼런스 발표 자료 우선 활용 |
| **T3** | 전문 분석기관·기술 매체 (SemiAnalysis, SemiEngineering, Tom's Hardware, EE Times, TrendForce, Blocks & Files, The Elec, ZDNet Korea) | 교차 확인 후 사용 |
| **T4** | 개인·기업 기술 블로그, 위키 | 구조 이해용 참고만. **수치 인용 금지** |

**등급 밖 표기 두 가지**

| 표기 | 뜻 |
|---|---|
| **일반 통용** | 특정 출처에 귀속시킬 수 없을 만큼 널리 확립된 값. 예: SRAM 접근 지연 1 ns 이하, NAND 랜덤 읽기 50–100 µs, SSD 대역폭 약 7 GB/s. 등급을 붙이면 없는 근거를 만들어내는 셈이 되므로 그대로 둡니다 |
| ** - ** (또는 정성 표기) | 수치가 아닌 정성 값. 예: 비트당 비용 "높음", 결합도 "인터포저". 등급 부여 대상이 아닙니다 |

**신뢰도 한정 표기 (v4 신규)** - 등급만으로는 부족한 경우 함께 답니다.

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
- T4 출처에서 가져온 것은 구조 설명에 한정하며, 같은 내용의 수치는 반드시 T0–T3로 백업합니다.
- 미비준·미공개 표준의 수치는 본문에서 `[미비준]` / `[초안 목표]` / `[벤더 목표치]` / `[미공개]` / `[미확정]` 배지를 달아 확정 사실과 구분합니다.

---

## 2. 표준화 기구 (T0)

| 기구 | 문서 / 항목 | 비고 |
|---|---|---|
| **JEDEC** (`jedec.org`) | **JESD270-4** - HBM4, 2025-04 공개 | [03-hbm.md](03-hbm.md) |
| JEDEC | **JESD209-6** - LPDDR6, 2025-07 공개 | DDR6 계열 중 최초 확정 표준. [02-dram.md](02-dram.md) |
| JEDEC | **JESD79-4** - DDR4 SDRAM, **2012-09 원판** | 로컬 확보본이 원판이라 이후 개정 반영 여부를 확인할 수 없고, **DDR4-2666 이상 speed bin의 타이밍 열이 전부 TBD**입니다. 고속 DDR4 값의 근거는 마이크론 데이터시트가 유일합니다. [02-dram.md](02-dram.md) |
| JEDEC | **"Proposed DDR5 Full spec (JESD79-5)" Rev0.1** - JC42.3 위원회 회람본 | **`T0 (초안)` · [미비준]**. 뱅크 구성·어드레싱, DDR5-6400 A/B/C bin, tCCD_L·tCCD_L_WR, §4.23 PPR 및 MR25 guard key 조항의 근거. **표 다수에 "No Ballot"이 붙어 있고 CL·MR6·MR12가 TBD입니다.** 이 초안의 bin 목록에 DDR5-4800이 없고, tWR 45 ns에는 "currently defined as" 단서가 붙어 있어 두 값 모두 이 모음집에서 인용하지 않습니다. [02-dram.md](02-dram.md), [08-test-yield.md](08-test-yield.md) |
| JEDEC | DDR5 MRDIMM / MDB / MRCD | MDB 표준 공개, MRCD 진행 중, Gen2 로드맵 진행(2026-04) |
| JEDEC | JC-40 / JC-45 / **JC-42.3** | JC-42.3에서 DDR6 타이밍·시그널링 파라미터 조율 중 |
| JEDEC | **JESD330-4** - Standard Package High Bandwidth Memory (SPHBM4), **2026-07-13 공표** | HBM4와 동일 DRAM 다이 + 새 인터페이스 base die. 512 데이터 신호 + 4:1 직렬화로 유기 기판 실장. **보도자료만 확인, 규격 원문은 유료 회원 전용.** [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| JEDEC | HBM4E 패키지 높이 | **통합 표준 부재. 825–900 µm 논의 중, 2026-08-25 재확인 시점에도 확정 발표 확인되지 않음** |
| **Open Compute Project** | HBF 표준화 워크스트림 (2026-02 개설) → **첫 기술 사양 공표 (2026-08, FMS 2026)** | HBF는 JEDEC이 아니라 OCP 경로. UCIe 인터커넥트, 8·16단, 최대 512 GB, 성능 등급 3종. **사양 원문 미확인.** [04-hbf.md](04-hbf.md) |
| **CXL Consortium** (`computeexpresslink.org`) | CXL 3.1 사양 개요 | [appendix-a-cxl.md](appendix-a-cxl.md) |
| **trade.gov** | Country Commercial Guide - Japan, Semiconductors (2025-11-20 갱신) | [appendix-c-industry.md](appendix-c-industry.md) |

> **제약**: DDR6를 포함한 다수 JEDEC 문서가 유료 회원 전용입니다. 대응 규칙은 [5절](#5-t0-접근-제약과-대응-규칙)을 참조하십시오.

---

## 3. 제조사·장비사 공식 (T1)

### 3-1. 메모리

| 출처 | 주요 인용 항목 | 관련 문서 |
|---|---|---|
| **SK하이닉스 뉴스룸** (`news.skhynix.com`, `news.skhynix.co.kr`) | HBF 표준화(2026-02-26), 「반도체의 이해」 연재, Research Inside 3D NAND CTI, CTF 상용화 | [04](04-hbf.md), [05](05-nand.md), [06](06-process.md) |
| **삼성반도체 기술블로그** (`semiconductor.samsung.com/kr/support/tools-resources/fabrication-process/`) | 반도체 백과사전, 8대 공정 | [06](06-process.md) |
| **삼성전자 반도체 뉴스룸** (`news.samsungsemiconductor.com/kr/`) | 「반도체 8대 공정」 1–9탄 | [06](06-process.md) |
| **삼성 뉴스룸** | HBM4E at NVIDIA GTC 2026 | [03](03-hbm.md) |
| **SanDisk 뉴스룸** | HBF Fact Sheet, SK하이닉스 MOU(2025-08-06), OCP 킥오프(2026-02-25) | [04](04-hbf.md) |
| **Kioxia** | BiCS10 발표 (332층, TLC 29.1 / QLC 37.6 Gb/mm², 4,800 MT/s) | [05](05-nand.md) |
| **마이크론** (`micron.com/products/memory/cxl-memory`) | CZ120 / CZ122 CXL 메모리 확장 | [부록 A](appendix-a-cxl.md) |

**데이터시트·기술 노트 (v5에서 신규 등록)** - 조사 파일과 별개로 1차 자료를 직접 등재합니다.

| 출처 | 리비전 / 발행 | 주요 인용 항목 | 관련 문서 |
|---|---|---|---|
| **마이크론 16 Gb DDR4 SDRAM 데이터시트** | Rev. H, **2021-08** | DDR4-1600 / DDR4-3200 speed bin 표와 AC 타이밍(tRCD·tAA·tRP·tRAS), 부품 등급 -125E / -062Y / -062E / -062, tCCD_S·tCCD_L 규정값, tFAW의 페이지 크기 의존, 뱅크 그룹의 인과("8n 프리페치에 머문 데 따른 페널티"), CS_n의 랭크 정의, 3DS와 DDP의 구분, PRECHARGE / ARRAY RESTORE 서술 | [02](02-dram.md) |
| **마이크론 16 Gb DDR5 SDRAM Die Rev D 데이터시트** | doc rev F, **2024-04** | DDR5-5600 / 6400 speed bin(-56B, -64B), 16 Gb 뱅크 구성, 32 ms / 8,192 REF, x4 RMW Suppression, ECS Writeback Suppression. 같은 표의 **DDR5-7200은 "Advance(개발 중)"이므로 인용하지 않습니다** | [02](02-dram.md), [07](07-reliability.md) |
| **삼성 DDR5 UDIMM 데이터시트** | Rev. 1.0, **2021-03** | DDR5-4800B 전체 타이밍(40-39-39, tRC 48.000 ns 숫자 명시), 채널 A/B 핀 구성과 CB0–CB3 체크비트, 모듈 구성표(랭크 수), tREFIsb 계산식, On-Die ECC / ECC Transparency and Error Scrub / CRC의 기능 항목 분리, 3DS logical rank 표현 | [02](02-dram.md), [07](07-reliability.md) |
| **마이크론 32 GB DDR5 RDIMM 데이터시트** | Rev. F, **2022-12** | "32GB (x80, ECC, DR)" 제품 구성. 서브채널 40비트의 "32 데이터 + 8 ECC" 분해는 **산술 유도**이며 명시 문자열은 미확인 | [02](02-dram.md), [07](07-reliability.md) |
| **삼성반도체 「반도체 8대 공정」 8탄 - EDS** | 원문 직접 확인 | EDS 정의와 단계 구성(ET Test & WBI → Hot/Cold Test → Repair/Final Test → Inking), ET의 소자 파라미터(DC) 검사 정의, WBI 설명, "수선이 끝나면 Final Test 공정을 통해 재차 검증". **삼성전자 반도체 뉴스룸 EDS 편은 같은 공정을 5단계로 쓰며 두 공식 서술이 상충합니다**(후자는 검색 요약 경유 `2차 인용`) | [08](08-test-yield.md), [06](06-process.md) |
| **마이크론 TN-29-59 "Bad Block Management in NAND Flash Memory"** | Rev. H, **2011-04** | 공장 불량 블록 표식 위치와 FFh 규칙, 표식 소실 경고(지워지면 복구 불가), reserved block 용도, 수명 누적 불량 상한 2%. **2011년 평면(planar) NAND 기준이며 현행 3D NAND 적용 근거 없음.** 원본 PDF 추출 실패로 재호스팅본 확인 | [08](08-test-yield.md), [05](05-nand.md) |

### 3-2. 로직·장비

| 출처 | 주요 인용 항목 | 관련 문서 |
|---|---|---|
| **TSMC Research** | 메모리 페이지, N2 SRAM 매크로 밀도 | [01](01-sram.md) |
| **ASML** (`asml.com/en/products/euv-lithography-systems`) | TWINSCAN EXE:5200B, High-NA EUV(NA 0.55), 2026 EUV/DUV 전망 | [06](06-process.md) |
| **Lam Research** (`lamresearch.com/products/our-solutions/cryogenic-etching/`) | Cryo 3.0, HAR 식각 챔버 7,500대 이상·누적 500만 장 이상, backside deposition(Coronus DX, VECTOR DT, EOS) | [06](06-process.md) |
| **Lam Newsroom** | "How Deposition and Etch Are Reshaping Chips for the AI Era" (2026-04) | [06](06-process.md) |
| **Tokyo Electron** | 400층용 10 µm 초고속 극저온 식각(GWP 84% 저감), VCT/4F² 2027–2028 전망 | [02](02-dram.md), [06](06-process.md) |
| **NVIDIA** (`docs.nvidia.com/gpudirect-storage/`) | GPUDirect Storage, Rubin 아키텍처 발표 | [03](03-hbm.md), [05](05-nand.md), [부록 B](appendix-b-workloads.md) |
| **Astera Labs**, **Panmnesia** (`panmnesia.com`) | Leo(Microsoft Azure M-series 채용), PANSWITCH CXL 3.2 | [부록 A](appendix-a-cxl.md) |

---

## 4. TechInsights 다이 분석 (T2.5)

실물 역공학 실측치이므로 수치 근거로는 T1급으로 취급합니다.

| 보고서 / 자료 | 인용 항목 | 관련 문서 |
|---|---|---|
| "DRAM Scaling Trend and Beyond" | 셀 커패시턴스 추이, 6F² 한계(10 nm가 마지막 노드일 가능성), 2T0C IGZO 전망. EE Times Asia 재게재본으로 공개 확인 가능 | [02](02-dram.md) |
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

**7.8F² 관련 미확인 사항**: TechInsights가 삼성 D1b 셀 크기(0.00123 µm²)에서 F를 추출할 때 7.8F² 기준을 사용했습니다. 교과서적 6F²와의 괴리를 설명한 원문 근거는 아직 확인하지 못했으며, [02-dram.md](02-dram.md)에서 각주로 처리했습니다.

---

## 5. T0 접근 제약과 대응 규칙

JEDEC 사이트에서 DDR6 관련 문서는 대부분 유료 회원 전용이라 원문을 직접 확인할 수 없습니다. 이 모음집의 DDR6 서술은 **T3(기술 매체) + 벤더 로드맵 자료** 기반입니다.

**대응 규칙 (DDR6·HBM4E·HBF 공통 적용)**

1. 해당 서술에 다음 취지의 각주를 답니다.
   > JEDEC 사양서는 유료 공개이며, 이 수치는 공개 보도 및 벤더 로드맵을 종합한 값으로 최종 비준 사양과 다를 수 있습니다.
2. 확정형 서술을 쓰지 않습니다. `DDR6는 ~이다` 대신 `DDR6 초안은 ~를 목표로 합니다`.
3. 배지로 상태를 표시합니다 - `[미비준]`, `[초안 목표]`, `[벤더 목표치]`, `[미공개]`, `[미확정]`.

**HBF 동결 정책**: HBF는 2026-07-28 시점 공개 정보만 사용하며, 미공개 스펙을 추정하거나 유추하는 서술을 금지합니다. 미공개 항목 목록은 [04-hbf.md](04-hbf.md)에 명시되어 있습니다.

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
| **FlexGen** | (ICML 2023) | arXiv:2303.06865 | [부록 B](appendix-b-workloads.md) - 목록 등재만, 본문 서술 없음 |
| **MoE SSD offloading 반론** | K. Kyung, S. Yun, J. H. Ahn (SNU), "SSD Offloading for LLM Mixture-of-Experts Weights Considered Harmful in Energy Efficiency," IEEE CAL 2025 | arXiv:2508.06978 | [부록 B](appendix-b-workloads.md) |
| **Memory Pooling With CXL** | IEEE Micro 43(2) | DOI 10.1109/MM.2023.3237491 | [부록 A](appendix-a-cxl.md) |
| **CXL 개론** | ACM Computing Surveys 56(11) Art.290 | DOI 10.1145/3669900 (arXiv:2306.11227) | [부록 A](appendix-a-cxl.md) |
| **NVMe offloading I/O 분석** | CHEOPS '25 | DOI 10.1145/3719330.3721230 | [부록 B](appendix-b-workloads.md) |
| **3nm GAA-FET SRAM self-heating/방사선** | SJSU, Sandia, 2026-07 | — | [01](01-sram.md) |
| **DRAM 셀 커패시턴스 역사** | IEEE JSSC 1985 (1Mb, 32 fF), IEEE JSSC 1988 (16Mb, 33 fF), IEDM 2004 MESH capacitor (30 fF) | — | [02](02-dram.md) |
| **Cai 2017** (v5에서 인덱스 등재) | Y. Cai, S. Ghose, E. F. Haratsch, Y. Luo, O. Mutlu, "Error Characterization, Mitigation, and Recovery in Flash-Memory-Based Solid-State Drives," *Proceedings of the IEEE*, **2017** - v5에서 추가로 쓴 항목은 bad block table 작성(컨트롤러가 최초 전원 인가 시 전수 스캔), OBB의 plane 내 리매핑과 superpage 병렬도 유지, GBB의 블록 단위 격리 처리, ECC 강도와 over-provisioning의 경쟁 관계입니다. **수치·비교 기준은 전부 평면(planar) NAND**이며, 같은 논문이 인용한 "OBB 2% 미만"의 원출처는 위키(T4)입니다 | — | [08](08-test-yield.md), [05](05-nand.md), [07](07-reliability.md) |

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

## 8. 구조 이해용 참고 (T4) - 수치 인용 금지

| URL | 수집일 | 용도 |
|---|---|---|
| `hyper-accel.github.io/posts/what-is-hbf/` | 2026-04-23 | HBF 개념 구조 |
| `hyper-accel.github.io/posts/hbf-workload/` | 2026-04-29 | HBF 워크로드 개념 |
| `hyper-accel.github.io/posts/hbf-challenge/` | 2026-05-28 | HBF 과제 개념 |
| `hyper-accel.github.io/posts/what-is-cxl/` | 2026-06-04 | CXL 개념 구조 |

이 항목들에서 얻은 구조 설명은 본문에 반영하되, 수치는 전부 T0–T3 출처로 백업했습니다.

---

## 9. 미확정·추적 항목

이 모음집이 다루는 주제 중 아래는 **2026-08-25 재확인 기준**으로 확정되지 않았습니다. 확정 시 해당 문서를 갱신해야 합니다.

> **2026-08-12 회차에서 상태가 바뀐 항목이 셋 있습니다.** 아래 표의 `부분 해소` 표시가 그것이며, 무엇으로 어떻게 바뀌었는지는 10절 갱신 이력에 적었습니다.
>
> **2026-08-22 회차에서는 상태가 바뀐 항목이 없습니다.** 열 건을 다시 확인했고 전부 이전과 같았습니다.
>
> **2026-08-25 회차에서는 Hot Chips 2026이 열려 항목 하나가 `발표 전`에서 벗어났습니다.** 다만 슬라이드 원문을 확보하지 못해 `원문 미확인`으로 이동했을 뿐이고, 같은 발표를 두고 보도가 엇갈리는 항목이 하나 새로 생겼습니다.

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| JEDEC HBM4E 패키지 높이 규격 (825–900 µm 논의) | **미확정** (2026-08-25 재확인까지 변화 없음) | [03-hbm.md](03-hbm.md), [06-process.md](06-process.md), [appendix-c-industry.md](appendix-c-industry.md) |
| HBM4E 통합 JEDEC 표준 존재 여부 | **부재** (벤더별 차별화 버전. 2026-08-25 재확인까지 변화 없음. 다만 삼성·SK하이닉스가 12단 샘플 출하) | [03-hbm.md](03-hbm.md) |
| HBF 세부 스펙 (패키징·인터페이스·내구성·전력·가격) | **부분 해소** - 2026-08 OCP 첫 기술 사양 공표로 인터페이스(UCIe)·패키징·컨트롤러 분담이 사양 범위에 들어옴. **다만 사양 원문 미확인.** 내구성·전력·가격은 **[미공개] 유지** | [04-hbf.md](04-hbf.md) |
| DDR6 JEDEC 비준 | **미비준** (JC-42.3 조율 중. 2026-08-25 재확인까지 변화 없음) | [02-dram.md](02-dram.md) |
| TSMC N2 HD SRAM 비트셀 크기 논쟁 | **진행 중** (0.0175–0.021 µm² 보고 편차. 2026-08-22 재확인까지 변화 없음) | [01-sram.md](01-sram.md) |
| D1c 세대 다이 분석 공개 | **부분 해소** - TechInsights가 SK하이닉스 D1c 분석을 2026-06-09 공개. **공개 블로그에 수치가 없고 실측값은 유료 보고서 영역이라 `원문 미확인`** | [02-dram.md](02-dram.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |
| SPHBM4 (JESD330-4)의 핀 속도·등급별 대역폭·지원 단수 | **원문 미확인** - 2026-07-13 공표되었으나 보도자료에 해당 값이 없고 규격 원문은 유료. 기술 매체가 인용하는 전송률 범위는 **1차 근거 미확인이라 이 모음집이 쓰지 않음** | [03-hbm.md](03-hbm.md) |
| SPHBM4 채택 벤더·제품 | **없음** (2026-08-25 재확인까지 발표 확인되지 않음) | [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| 삼성 V10 BV-NAND의 공식 면적 밀도와 셀 타입 | **미확인** (2026-08-25 재확인까지 변화 없음) - 유통되는 약 28 Gb/mm²와 TLC 표기는 **기술 매체(T3) 값**이며 삼성 발표 원문에서 확인하지 못함. 층수도 "400층 이상"과 "약 430층"이 병존 | [05-nand.md](05-nand.md) |
| 삼성 V10 양산 여부 | **보도 상충** (2026-08-25 재확인까지 변화 없음) - 이미 양산해 공급 중이라는 국내 매체 보도와 공급 시점 미발표라는 해외 매체 서술이 병존(둘 다 T3) | [05-nand.md](05-nand.md) |
| HBM4E 양산 시점 | **보도 상충** - 삼성 2026-02 양산 개시라는 서술과 2027년 출시라는 서술이 병존. HBM4 양산과 혼동됐을 가능성이 높아 이 모음집은 인용하지 않음 | [03-hbm.md](03-hbm.md) |
| DDR5 세대의 Row Hammer 실측 임계값 | **확인 실패** - 온다이 ECC가 단일 비트 플립을 조용히 정정하고 내장 완화 로직이 임계 도달 전 개입해 외부 관측이 곤란 (T2, DRAM-Profiler arXiv:2404.18396) | [07-reliability.md](07-reliability.md) |
| DDR4 MAC 값 표 (200K/300K/…) | **확인 실패** - JEDEC SPD Annex L byte 41이 로그인 벽 뒤 | [07-reliability.md](07-reliability.md) |
| PRAC의 실제 양산 탑재 현황 | **확인 실패** - JESD79-5C는 사양이지 탑재 현황이 아님. 어느 벤더 제품이 탑재했는지 T1 근거 없음 | [07-reliability.md](07-reliability.md) |
| 셀 커패시턴스(10 fF 미만)와 리텐션 마진의 정량 관계 | **확인 실패** - fF 단위 근거가 어느 자료 계열에도 없음. **두 사실을 인과로 연결하는 서술 금지** | [02-dram.md](02-dram.md), [07-reliability.md](07-reliability.md) |
| DRAM 커패시터 세대별 종횡비 (D1x–D1c) | **확인 실패** - 세대에 종횡비를 붙인 공개 자료 없음. 확보된 것은 세대 미특정 `단일 출처` "100:1 접근"뿐 | [06-process.md](06-process.md) |
| 3D NAND 100:1 도달 시점 | **상충** - v3는 "1,000층에서 접근", JJAP 리뷰(T2, DOI 10.35848/1347-4065/accbc7)는 "수백 층에서 이미 초과". 홀 직경 기준(상부 CD vs 최소 CD) 차이 가능성 | [06-process.md](06-process.md), [05-nand.md](05-nand.md) |
| 극저온 식각의 DRAM 커패시터 적용 여부 | **확인 실패** - Lam 공식 페이지는 3D NAND만 명시. 적용·미적용 어느 쪽 근거도 없음 | [06-process.md](06-process.md) |
| HBM ECC 규격 원문 | **미확인** - JESD238(HBM3) 보도자료 `단일 출처`만 확보, 규격 원문 아님 | [03-hbm.md](03-hbm.md), [07-reliability.md](07-reliability.md) |
| 3nm GAA-FET SRAM self-heating·방사선 연구 (SJSU/Sandia) | **원문 미확보** - v3에 등재되어 있으나 검증도 반박도 되지 않음 | [01-sram.md](01-sram.md) |
| TechInsights의 7.8F² 기준 근거 | **원문 미확인** | [02-dram.md](02-dram.md) |
| 4F²의 이론적 밀도 이득 "약 30%" | **수치 정합 불일치** - 셀 면적비 2/3를 밀도로 환산하면 1.5배(약 50%)이며, 30%는 면적 축소율(약 33%)에 가까움. 셀 층위인지 다이 층위인지 명시한 1차 자료 미확인 | [02-dram.md](02-dram.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |

| Hot Chips 2026 발표 내용 (2026-08-23 – 25) | **원문 미확인** - 삼성 base die 3단계 로드맵과 zHBM, SK하이닉스 패키징 로드맵을 [03-hbm.md](03-hbm.md) 2-2절·7-1절에, HBF 튜토리얼을 [04-hbf.md](04-hbf.md)에 반영했습니다. 근거는 전부 **학회 현장 보도(T3)이며 발표 슬라이드 원문을 확보하지 못했습니다.** 슬라이드 공개 시 해당 절 재대조 필요 | [03-hbm.md](03-hbm.md), [04-hbf.md](04-hbf.md), [appendix-c-industry.md](appendix-c-industry.md) |
| **(신규)** 하이브리드 본딩의 세대별 도입 시점 | **보도 상충** - 같은 SK하이닉스 발표를 두고 한 매체는 "HBM4E에는 준비되지 않아 MR-MUF를 연장한다"로, 다른 매체는 "16단 너머의 핵심 경로"로 정리했습니다. 전자는 **제목만 확보하고 본문을 열지 못했습니다.** 어느 쪽도 채택하지 않았습니다 | [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| **(신규)** zHBM의 이득 수치 두 종의 관계 | **미확인** - "표준 HBM4E 대비 전력 효율 +70%"와 "zHBM 4스택 + 1200 W GPU에서 약 100 W 절감"이 같은 계산에서 나온 값인지 확인하지 못했습니다 | [03-hbm.md](03-hbm.md) |
| **(신규)** HBF 실효 접근 단위 (읽기 64 KB / 쓰기 1 MB) | **미확인** - Hot Chips 2026 튜토리얼에서 제시된 값이나, **사양 규정값인지 발표자의 시뮬레이션 가정인지 보도에서 구분되지 않습니다.** 5절 좌표표의 입도 항목은 page 단위 그대로 두었습니다 | [04-hbf.md](04-hbf.md) |

**v5 조사에서 추가된 항목 (2026-07-29)**

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| DRAM 예비 행·열의 비율 | **확인 실패** - 상용 제품의 spare row/column 비율을 밝힌 T0–T2.5 근거 없음. 검색에 섞여 나오는 값은 **특허 명세의 예시 계산과 소형 학술 예제의 BISR 면적 오버헤드**이며 상용 비율이 아님. Dell KB 000053203(T1)도 "소자와 용량에 따라 다르다"고만 기술. **어떤 수치도 인용 금지** | [08-test-yield.md](08-test-yield.md) |
| HBM 실제 스택 수율 | **확인 실패 (v5 조사의 최대 공백)** - 어느 세대·어느 업체도 제조사 공식 수치가 없음. T3 추정치가 가장 활발히 유통되는 영역 | [08-test-yield.md](08-test-yield.md), [03-hbm.md](03-hbm.md) |
| HBM 리던던시·TSV repair의 규격상 지위 | **확인 실패** - JESD235 계열 원문 미확보. 확보된 TSV 리던던시 수치는 전부 **학계 제안 아키텍처의 시뮬레이션값**이며 제품 사양이 아님 | [08-test-yield.md](08-test-yield.md), [03-hbm.md](03-hbm.md) |
| 번인(WBI)의 조건 - 온도·전압·지속 시간 | **[미공개]** - 삼성·SK하이닉스 공식 자료 모두 "고온·고전압"이라고만 기술 | [08-test-yield.md](08-test-yield.md) |
| 테스트 비용 비중 | **확인 실패** - 분모가 **매출**("IC 매출의 2–3% 미만", ITRS 2015)인지 **제조원가**("총 제조원가의 2% 관행값", T3)인지가 자료마다 다르고, 둘 다 원문 접근 실패. 메모리 특정 비중은 확보 불가 | [08-test-yield.md](08-test-yield.md) |
| KGD 테스트의 결함 검출률 | **확인 실패** - 유통되는 검출률 수치의 출처가 **AI 생성 요약 사이트**이며 원 출처 불명. 같은 성격으로 적층 패키지 폐기 금액도 **개인 블로그** 출처 | [08-test-yield.md](08-test-yield.md) |
| 컬럼(열) 리페어의 규격상 지위 | **확인 실패** - JEDEC PPR은 원문이 "Fail Row address repair"이며 **행 수리만 규정.** 컬럼 리페어가 패키지 후에 가능한지 규격 근거 없음 | [08-test-yield.md](08-test-yield.md), [07-reliability.md](07-reliability.md) |
| DDR4 PPR 도입 시점의 1차 근거 | **확인 실패** - 로컬 확보본이 JESD79-4 **2012-09 원판**이라 이후 개정 반영 여부를 확인할 수 없음. "DDR4부터 PPR"이라는 통설의 1차 근거를 얻지 못해 DDR5 초안 기준으로만 서술 | [08-test-yield.md](08-test-yield.md), [07-reliability.md](07-reliability.md) |
| DDR5 비준본의 tWR·tRAS 확정값 | **[미비준]** - 초안의 tWR 45 ns에 "currently defined as" 단서가 붙고 MR6 인코딩이 전부 TBD. 또한 DDR5-4800 / 5600 / 6400의 tCCD_L·tCCD_L_WR·tRRD·tFAW는 초안이 DDR5-4000까지만 담고 있어 **확인 실패** | [02-dram.md](02-dram.md) |
| DDR3 코어 타이밍의 1차 자료 | **확인 실패** - T0/T1 원문 확보 3회 시도 후 실패. 그래서 근거 구간을 DDR4-1600 – DDR5-6400으로 한정했고, **"DDR3부터 3세대에 걸친 정체"라고 쓰지 않음** | [02-dram.md](02-dram.md) |

> 08에 속한 확인 실패 항목의 전체 목록(20건)은 [08-test-yield.md](08-test-yield.md) 5절에 있습니다. 위 표는 그중 다른 문서에도 영향을 주는 것만 옮긴 것입니다.

---

## 10. 갱신 이력

| 날짜 | 내용 |
|---|---|
| 2026-07-28 | 초판. 소스 팩 v3 기준으로 전 문서 작성 및 출처 인덱스 구축 |
| 2026-07-29 | v4 부록 조사 반영. [06-process.md](06-process.md)에 5절(DRAM 셀을 만든다는 것) 신설, [07-reliability.md](07-reliability.md) 신설. v3 정정 2건(MESH 세대 표기, Lam Cryo 3.0 수치 혼합), 상충 1건 병기(3D NAND 100:1 도달 시점) |
| 2026-07-29 | **v5 조사 반영.** [08-test-yield.md](08-test-yield.md) 신설(세 번째 횡단 챕터 - EDS, 리던던시·리페어, 적층 수율, KGD). [02-dram.md](02-dram.md) 확장 - 3절에 코어 타이밍 파라미터·지연 분해·뱅크 병렬성 소절(3-5 – 3-7), 6절에 조직 구조·뱅크 그룹·서브채널과 랭크 소절(6-5 – 6-7) 추가. v4 정정 1건(**DDR5 체크비트 비율 25%는 RDIMM 한정**이며 삼성 ECC UDIMM은 x72로 12.5%), 상충 1건 병기(삼성 공식 EDS 서술의 4단계 / 5단계). **v5 조사 파일은 저장소에 없으며 1차 출처만 2·3·6절에 등재** |

| **2026-08-12** | **v6 갱신 (초판 공개 2주 후 전면 재검토).** 표준 2건 확정 반영 - JEDEC **SPHBM4(JESD330-4)** 공표(2026-07-13)로 [03-hbm.md](03-hbm.md) 6-3절 신설, OCP **HBF 첫 기술 사양** 공표(2026-08)로 [04-hbf.md](04-hbf.md) 6절 재작성 및 미공개 6항목을 3항목으로 축소. **FMS 2026 반영** - [05-nand.md](05-nand.md) 적층 경쟁 표를 V10 세대로 갱신(삼성 400층 이상, SK하이닉스 375층), BiCS10 밀도를 셀 타입별로 분리(TLC 29.1 / QLC 37.6 Gb/mm²)하고 4-1-1절에 QLC·TLC 혼동 함정 신설. HBM4E 12단 샘플 출하 반영. [appendix-c-industry.md](appendix-c-industry.md)에 3Q26 계약가 전망과 SPHBM4 장비 시장 절 신설. **정정 없음, 상충 2건 신규 병기**(삼성 V10 양산 여부, 3Q26 계약가 관측 주체별 편차) |

| **2026-08-25** | **v6.2 갱신 (Hot Chips 2026 반영).** [03-hbm.md](03-hbm.md) 2-2절에 삼성 base die 3단계 로드맵, 7-1절 신설(삼성 zHBM과 SK하이닉스 패키징 로드맵, EMIB 등재, 하이브리드 본딩 조건, HBM4 TSV 20,000개 초과·base 마이크로범프 16,148개). [04-hbf.md](04-hbf.md)에 실효 접근 단위(읽기 64 KB / 쓰기 1 MB)와 **제3자 반론 신규 1건**("노력 대비 이득이 SSD 스트리밍과 크게 다르지 않다") 추가, 제품 부재를 학회 자리에서 재확인. [appendix-c-industry.md](appendix-c-industry.md) 4절에 EMIB 등재와 두 제조사의 방향 분기 반영. **근거가 전부 학회 현장 보도(T3, `2차 인용`)이며 슬라이드 원문은 확보하지 못했습니다.** 상충 1건과 미확인 3건을 9절에 신규 등록 |
| **2026-08-22** | **v6.1 재확인.** 9절 추적 항목 열 건을 다시 확인했고 **상태가 바뀐 항목은 없습니다.** DDR6 미비준, HBM4E 통합 표준 부재와 높이 미확정, SPHBM4 채택 벤더 부재, 삼성 V10 양산 여부 상충, HBF 사양 원문 미확인이 모두 그대로였습니다. 본문 00–08의 기술 서술은 한 줄도 고치지 않았습니다. [appendix-c-industry.md](appendix-c-industry.md)에 3-5절(2027년 DRAM·NAND 전망 분기)과 3-6절(설비투자 승인에서 첫 클린룸까지 약 3년)을 신설했고, 9절에 **Hot Chips 2026(2026-08-23 – 25)** 을 발표 전 추적 항목으로 등록했습니다 |

**v4에서 새로 확인된 주요 오인용 함정** - 인용 전 반드시 확인하십시오.

| 함정 | 실제 |
|---|---|
| Schroeder 2009를 "미세화 → 오류율 증가"의 근거로 인용 | 논문 결론은 **정반대**입니다. "신세대 DIMM에서 오류율 증가 증거를 관측하지 못했다"고 명시합니다 |
| DDR5 온다이 ECC를 "SECDED"로 표기 | 1차 자료는 일관되게 **SEC(단일 정정)**뿐입니다. Micron은 128 데이터 비트 + 8 패리티로 더블 비트를 검출할 수 없다고 명시합니다 |
| 세대 무관하게 "64 ms refresh" 사용 | DDR3/DDR4 한정입니다. **DDR5는 refresh window 32 ms, tREFI 3.9 µs** |
| HKMG를 DRAM "셀 트랜지스터"에 적용한다고 서술 | HKMG는 **주변/코어 트랜지스터**용입니다. 셀 매몰 워드라인 쪽은 DWMG(워크펑션 분할)입니다 |
| ZAZ를 "3층 샌드위치"로 서술 | Al₂O₃는 ALD 4–5 사이클 미만이라 **별개 층이 아니라 도판트**이며, 역할도 유전율이 아니라 **누설 차단**입니다 |
| NAND P/E 사이클 수치를 현행 3D NAND에 적용 | 확보된 값은 **2017년 발표, 평면(planar) NAND 기준**입니다 |
| **(v5)** "DDR5는 32뱅크"를 조건 없이 서술 | **16 Gb 이상 x4/x8 한정**입니다. 8 Gb는 16뱅크(8 BG × 2), x16은 전 밀도에서 16뱅크(4 BG × 4). 같은 이유로 "DDR4는 16뱅크"도 x4/x8 한정이며 x16은 8뱅크입니다. **밀도와 DQ 폭을 반드시 병기**하십시오 |
| **(v5)** 랭크를 병렬성 계층으로 서술 | 랭크는 **DQ 버스를 공유**합니다. 병렬화되는 것은 뱅크 상태(열린 행)이지 데이터 전송이 아닙니다. 한 랭크 안의 칩 여러 개도 병렬성이 아니라 **데이터 폭을 만드는 수단**이며, 1차 정의는 오직 "CS_n 하나를 공유하는 칩 집합"입니다 |
| **(v5)** 서브채널을 SDRAM 레벨 구조로 서술 | 서브채널은 **모듈(DIMM) 레벨 구조**입니다. DDR5 SDRAM 컴포넌트 사양 초안에 `sub-channel` 문자열이 **0건**이고, 제조사 데이터시트는 `Channel A / Channel B`라고 부릅니다. 분할의 인과도 성능·동시성이 아니라 **BL16으로 128B가 된 것을 32-bit 분할로 64B 캐시라인에 다시 맞춘 것**이며, 동시성 증가는 원인이 아니라 결과입니다 |
| **(v5)** 디바이스 타이밍과 시스템 지연을 같은 값으로 취급 | 데이터시트 타이밍만으로 계산되는 최악값은 **약 54 ns**(row conflict)입니다. 통용되는 "DDR5 native 약 80–100 ns"는 **컨트롤러·큐잉·링크를 포함한 시스템 값**입니다. 두 값의 차이가 어디에 얼마씩 배분되는지는 **확인 실패**이므로 추정하지 마십시오 |
| **(v5)** HBM 수율 추정치를 확정 사실로 인용 | 어느 세대·어느 업체도 **제조사 공식 스택 수율 수치가 없습니다.** 유통되는 값은 익명 소식통 기반 T3 추정치이며, KGD 검출률과 폐기 금액은 각각 AI 생성 요약 사이트와 개인 블로그가 출처입니다. 어떤 수치를 만나든 (a) 세대·업체, (b) 시점, (c) 발화 주체, (d) 다이 수율인지 스택 수율인지를 먼저 확인하십시오 |
| **(v6)** NAND 면적 밀도를 셀 타입 없이 비교 | 같은 332층 BiCS10에서 **TLC는 29.1, QLC는 37.6 Gb/mm²**입니다. FMS 2026 직후 널리 인용된 "332층이 400층보다 38% 높다"는 **BiCS10 QLC와 삼성 V10 TLC를 맞붙인 문장**입니다. 셀당 비트로 나누면 두 제품의 셀 밀도는 1% 이내이고, 같은 TLC끼리 비교하면 격차는 약 4%로 줄어듭니다. **밀도 수치에는 반드시 셀 타입을 병기하십시오** |
| **(v6)** SPHBM4를 "더 빠른 HBM4"로 서술 | SPHBM4의 **총 대역폭은 HBM4와 같습니다.** 바뀐 것은 2048 신호를 512 신호 + 4:1 직렬화로 재배분한 것이고, 목적은 성능이 아니라 **실리콘 인터포저 없이 유기 기판에 실장하는 것**입니다. 셀도 코어 다이도 같으므로 A1 지연도 변하지 않습니다 |
| **(v6)** HBM 높이 완화 논의를 HBM4에 적용 | **HBM4의 775 µm는 12단·16단 모두 확정된 값입니다.** 825–900 µm 논의의 대상은 20단 적층을 겨냥한 차세대(HBM4E·HBM5)이며, 2026-08-12 기준 확정 발표가 없습니다 |
| **(v6.2)** zHBM의 "+70%"와 "약 100 W 절감"을 같은 근거로 인용 | 앞은 **표준 HBM4E 스택 대비 비율**이고 뒤는 **zHBM 4스택 + 1200 W GPU라는 특정 구성의 절대값**입니다. 두 값이 같은 계산에서 나왔는지 확인되지 않았으므로 한쪽만 옮기면서 다른 쪽 기준을 붙이면 안 됩니다 |
| **(v6.2)** Hot Chips 발표를 제조사 공식 사양으로 인용 | 이 모음집이 확보한 것은 **학회 현장 보도**이며 발표 슬라이드 원문이 아닙니다. 수치는 전부 `2차 인용`이고, 특히 하이브리드 본딩의 세대별 도입 시점은 **같은 발표를 두고 매체 간 서술이 엇갈립니다** |
| **(v6)** HBF 사양 공개를 "스펙 확인 완료"로 취급 | OCP 첫 기술 사양이 공표된 것은 사실이나, 이 모음집은 **사양 원문을 확인하지 못했습니다.** 상태는 `[미공개]`에서 **`원문 미확인`으로 이동**한 것입니다. 쓰기 내구성·전력 프로파일·가격은 여전히 `[미공개]`입니다 |

**갱신 규칙**

- 수치를 바꿀 때는 본문·이 인덱스·[assets/IMAGE-MANIFEST.md](assets/IMAGE-MANIFEST.md)의 해당 이미지 유의사항을 **동시에** 갱신합니다.
- 각 문서 상단의 `최종 검증` 배너 날짜를 함께 올립니다.
- 9절의 미확정 항목이 확정되면 해당 행을 10절 갱신 이력으로 옮깁니다.
