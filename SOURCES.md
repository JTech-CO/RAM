# SOURCES - 출처 인덱스

> **최종 검증: 2026-09-26**
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
| **v6.3 갱신** | **2026-09-01** | **Hot Chips 2026 종료 후 원문 대조.** OCP HBF 사양 원문(T0) 확보, 발표 슬라이드 3종 확보, 추적 항목 6건 해소, **기존 서술 정정 4건** | **조사 파일 없음.** 근거는 각 문서 각주에 등재. **v6.2가 학회 진행 중에 작성되어 생긴 오류를 원문으로 바로잡는 것**이 주된 목적이었습니다 |
| **v6.4 갱신** | **2026-09-01** | **누락 구간(2026-08-25 – 09-01) 보완과 추적 항목 재확인.** 메모리 월 원논문(T2) 확보, NVHBM(T1) 등재, d-Matrix 적층 상충 해소, TSMC N2 유보 종결, **v6.3의 서술 오류 1건 정정** | v6.3과 같은 날 이어서 수행했습니다. **v6.3의 조사가 오늘 날짜를 2026-08-27로 잘못 잡아 8월 하순 발행분을 놓쳤을 위험**이 있어 그 구간을 다시 훑은 회차입니다 |

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
| JEDEC | **JESD82-542 / JESD82-543** - DDR5MRCD02 · MRCD03 멀티플렉스드 랭크 레지스터링 클록 드라이버, **2026-09 공표** | **2026-09-15 회차(v6.5) 신규 확인. 이전 판의 "MRCD 진행 중"을 대체합니다.** 소자 ID는 각각 DID 0x0542 / 0x0543이며 초록이 "MRDIMM 용도"를 명시합니다. 위원회 JC-40 / JC-40.4. **공표 목록의 서지 정보와 초록까지만 확보, 규격 본문은 로그인 벽 뒤.** [02-dram.md](02-dram.md) |
| JEDEC | **JESD82-553** - DDR5MDB03 멀티플렉스드 랭크 데이터 버퍼, **2026-08 공표** | **2026-09-15 회차(v6.5) 신규 확인.** 기존 MDB 표준의 후속 소자입니다. **원문 미확인.** [02-dram.md](02-dram.md) |
| JEDEC | DDR5 MRDIMM Gen2 로드맵 | **진행 중(2026-04 기준, 2026-09-15 재확인까지 변화 없음).** 위 세 문서는 **부품 규격**이지 모듈 세대 규격이 아니므로 Gen2 확정 근거가 아닙니다 |
| JEDEC | **JESD328** - LPDDR5/5X SOCAMM2 Common Standard, **2026-06 공표** | **2026-09-15 회차(v6.5) 신규 확인.** 위원회 **JC-45**. 데이터센터·AI 서버 메인 메모리용 LPDDR5/5X 압착 결합 모듈. 초록이 **"SOCAMM은 범주명, SOCAMM2가 JEDEC 표준판"** 이라고 직접 구분합니다. 핀당 9.6 Gb/s와 SPD는 **공표 8개월 전 보도자료(2025-10-20)의 미래형 서술**이며 규격 본문은 미확인. 부속 등록으로 트레이 `CO-043A`(모듈) · `CO-044A`(커넥터)가 2026-08자로 있습니다. [02-dram.md](02-dram.md) |
| JEDEC | JC-40 / JC-45 / **JC-42.3** | JC-42.3에서 DDR6 타이밍·시그널링 파라미터 조율 중 |
| **JEDEC** | **JESD270-4A** - HBM4 개정 1.1, **2025-12 공표** | 2026-09-01 기준 **현행 최신 HBM 표준**입니다. 본문이 참조하는 JESD270-4의 개정판이며, **개정 내용은 확인하지 못했습니다.** [03-hbm.md](03-hbm.md) |
| JEDEC | **JESD330-4** - Standard Package High Bandwidth Memory (SPHBM4) | **공표 시점 표기가 갈립니다.** JEDEC 문서 페이지는 "Published: Jun 2026", 보도자료는 "2026-07-13 발표"로 적습니다. 모순이 아니라 **공표월과 대외 발표일의 차이**로 보이나 확인하지 못해 병기합니다. HBM4와 동일 DRAM 다이 + 새 인터페이스 base die. **보도자료만 확인, 규격 원문은 유료 회원 전용.** [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| JEDEC | **JESD330-4-1** - SPHBM4 Bump Map 부속서 No. 1, **2026-08 공표** | **2026-09-01 회차 신규 확인.** 범프 맵을 다루는 부속서이며 **원문 미확인.** [03-hbm.md](03-hbm.md) |
| JEDEC | **JESD239F** - GDDR7 개정, 2026-08 공표 | **2026-09-01 회차 신규 확인.** 이 모음집의 범위 밖 소자이나, 같은 회차 공표 목록으로 등재합니다 |
| JEDEC | **JESD230G.02** - NAND Flash Interface Interoperability, **2026-09 공표** | **2026-09-26 회차(v6.6) 신규 확인.** **JEDEC과 ONFI 공동 개발**이며 Asynchronous SDR · Synchronous DDR · **Toggle DDR** 세 방식의 **상호운용성**을 규정합니다. 소자 규격 자체가 아니라 상호운용 규격이라는 점이 중요합니다. [05-nand.md](05-nand.md) 6절이 "표준 문서 번호 미확인"으로 두었던 항목을 **해소**합니다. **규격 본문은 로그인 벽 뒤이며 미확인** |
| JEDEC | **JEP106BP** - 제조사 식별 코드, **2026-09 공표** | **2026-09-15 회차(v6.5) 신규 확인.** 정기 개정이며 이 모음집의 서술에 영향을 주지 않습니다. 같은 회차 공표 목록으로만 등재합니다 |
| JEDEC | **JESD317-2 / JESD319-2 / JESD325-2** - CXL 메모리 모듈(CMM02) · 컨트롤러(CMC02) · 디바이스 관리(CMG02), **2026-05 공표** | **2026-09-01 회차 신규 확인.** JESD325-2는 대상을 "PCIe Gen 6이며 **CXL 3.2 사양 또는 그 이후**"로 명시합니다. 컨소시엄 사양이 4.0인 것과 **기준선이 다릅니다. 세 문서 모두 원문 미확인.** [appendix-a-cxl.md](appendix-a-cxl.md) |
| JEDEC | HBM4E 패키지 높이 | **통합 표준 부재. 825–900 µm 논의 중, 2026-09-01 재확인 시점에도 확정 발표 확인되지 않음.** JC-42.2 최근 문서 목록에 HBM4E 관련 문서가 한 건도 없음을 확인했습니다 |
| JEDEC | DDR6 | **미비준.** JEDEC 공식 기술영역 페이지가 **2026-09-15 재접속 시점에도 문구가 한 글자도 바뀌지 않았습니다**: "DDR6 and HBM5 are in development in JEDEC's JC-42 Committee for Solid State Memories and JC-42.2 High Bandwidth Memory (HBM) Subcommittee, respectively." **같은 문장이 HBM5도 JC-42.2에서 개발 중임을 밝힙니다** |
| **Open Compute Project** | **HBF High-Level Base Die Specification v0.7.0**, 문서 일자 **2026-08-03**, 130쪽 | **2026-09-01 회차에 원문을 확보했습니다.** 인증 없이 공개 다운로드되며 SHA-256 재현 확인. 이전 판의 `원문 미확인` 표기를 대체합니다. 속도 등급 3종(0.384 / 1.536 / 3.072 TB/s), 큐브 512 GiB, UCIe 3.0, 호스트 채널 16개, 접근 입도(읽기 64 B – 4 KiB / 쓰기 4 KiB), 리텐션 24시간@85°C, 리프레시 24 – 48시간, 수명 10년. **버전이 1.0 미만인 초안 성격이며 원문 내부에 TiB/s와 GB/s 단위 불일치가 있습니다.** [04-hbf.md](04-hbf.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |
| **CXL Consortium** (`computeexpresslink.org`) | CXL 3.1 사양 개요 / **CXL 4.0 (2025-11-18 공개)** | 4.0에서 전송률 64 → 128 GT/s, bundled port 도입. 2026-09-01 접속 기준 **4.1·5.0 없음**. **사양 원문은 인용하지 않았습니다** - 요청 방식 제공이며 컨소시엄 이용 정책이 비회원의 원문 처리에 제약을 둡니다. 근거는 보도자료와 공개 페이지입니다. [appendix-a-cxl.md](appendix-a-cxl.md) |
| **UCIe Consortium** (`uciexpress.org`) | UCIe 1.0 / 1.1 / 2.0 / **3.0** | 2026-09-01 접속 기준 **3.0이 최신**이며 48·64 GT/s 지원. UCIe-3D는 10 – 25 µm에서 1 µm 미만까지의 범프 피치를 대상으로 하이브리드 본딩에 최적화. **사양은 요청 방식 제공이며 원문 미확인.** 공개 페이지에 "organic substrate" 표현은 없습니다. [04-hbf.md](04-hbf.md) |
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
| **삼성 뉴스룸** | HBM4E at NVIDIA GTC 2026. **(v6.5)** ASML 협력 확대 - **2028년까지 DRAM 양산에 High-NA EUV 도입 계획**(2026-09-08), 브로드컴 MOU - HBM 포함 메모리·파운드리 합산 "2,000억 달러 이상 추정"(2026-07-25) | [03](03-hbm.md), [06](06-process.md), [부록 C](appendix-c-industry.md) |
| **삼성반도체 기술 블로그** (`semiconductor.samsung.com/news-events/tech-blog/`) | **(v6.5)** SOCAMM2 소개(기사 날짜 2025-12-18) - RDIMM 대비 대역폭 2배 이상, 전력 55% 이상 감소, **기준선 미기재** | [02](02-dram.md) |
| **SK하이닉스 뉴스룸 (v6.5 추가분)** | SOCAMM2 192 GB **양산**(2026-04-20, 1c LPDDR5X, 기준선 미기재) · Future Forum 2026(2026-09-08, **정량 수치 0건**) | [02](02-dram.md), [04](04-hbf.md) |
| **SK하이닉스 뉴스룸 (v6.6 추가분)** | AI Infra Summit 2026(행사 2026-09-15 – 17, 게재 09-17) - **HBF는 구조 모형으로만 전시**, PIM(AiM·AiMX)과 **SALT-KV**는 동작 시연. 워크로드 대응(HBF = long-context, PIM = fast-decoding). **제품 정량 수치 0건** · 2026 Global Forum(행사 09-18, 게재 09-21) - 채용·비전 행사, **정량 수치 0건** | [04](04-hbf.md), [부록 B](appendix-b-workloads.md) |
| **SanDisk 뉴스룸** | HBF Fact Sheet, SK하이닉스 MOU(2025-08-06), OCP 킥오프(2026-02-25) | [04](04-hbf.md) |
| **Kioxia** | BiCS10 발표 (332층, TLC 29.1 / QLC 37.6 Gb/mm², 4,800 MT/s) | [05](05-nand.md) |
| **마이크론** (`micron.com/products/memory/cxl-memory`) | CZ120 / CZ122 CXL 메모리 확장 | [부록 A](appendix-a-cxl.md) |
| **마이크론 IR 보도자료** (`investors.micron.com`) | **(v6.5)** SOCAMM2 192 GB 샘플(2025-10-22) · 256 GB 샘플(2026-03-03). **두 보도자료의 각주 기준선이 서로 다릅니다** - 각주 전문을 [02-dram.md](02-dram.md) 각주에 옮겼습니다. **(v6.6)** **512 GB DDR5 RDIMM 실증**(2026-09-15) - TSV 수직 적층, 최대 9,200 MT/s, 24슬롯 2소켓에서 12 TB, 양산 목표 2027년 하반기. 전력 각주가 **절대 와트(16.0 W 대 44.2 W)와 용량 정합 기준선**을 제시해 SOCAMM2 각주와 대비됩니다 | [02](02-dram.md) |

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

> **2026-09-01 추가.** A. Gholami 외, **"AI and Memory Wall"**, *IEEE Micro*, 2024 (DOI 10.1109/MM.2024.3373763, arXiv:2403.14123, 원래 Hot Chips 2023 테마 논문). **PDF 원문 확보 후 초록·결론 직접 대조.** 20년 구간에서 서버 피크 FLOPS 2년 3.0배 대 DRAM 대역폭 1.6배 대 인터커넥트 대역폭 1.4배, 누적으로 각각 약 60,000배 / 100배 / 30배. 학습 연산량 2년 750배, 모델 파라미터 2년 410배. → [00-memory-hierarchy.md](00-memory-hierarchy.md) 1-1절.
> 이 논문의 존재는 SK하이닉스 뉴스룸 기고(2026-08-30)가 지목해 확인했으며, 이 모음집은 원 논문을 직접 열어 대조했습니다. **DRAM 대역폭 1.6배는 DRAM 일반의 값이며 HBM만 따로 잰 것이 아닙니다.**

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

이 모음집이 다루는 주제 중 아래는 **2026-09-26 재확인 기준**으로 확정되지 않았습니다. 확정 시 해당 문서를 갱신해야 합니다.

> **2026-08-12 회차에서 상태가 바뀐 항목이 셋 있습니다.** 아래 표의 `부분 해소` 표시가 그것이며, 무엇으로 어떻게 바뀌었는지는 10절 갱신 이력에 적었습니다.
>
> **2026-08-22 회차에서는 상태가 바뀐 항목이 없습니다.** 열 건을 다시 확인했고 전부 이전과 같았습니다.
>
> **2026-08-25 회차에서는 Hot Chips 2026이 열려 항목 하나가 `발표 전`에서 벗어났습니다.** 다만 슬라이드 원문을 확보하지 못해 `원문 미확인`으로 이동했을 뿐이고, 같은 발표를 두고 보도가 엇갈리는 항목이 하나 새로 생겼습니다.
>
> **2026-09-01 회차는 이 표에서 가장 많이 움직인 회차입니다.** 학회 종료 후 원문을 다시 찾은 결과 **여섯 항목이 해소되고 세 항목이 새로 등록**되었습니다. 해소된 항목은 10절 갱신 이력으로 옮겼습니다.
>
> **해소의 성격이 두 갈래입니다.** 하나는 **원문을 구했기 때문**입니다(OCP HBF 사양, Hot Chips 발표 슬라이드, 삼성 보도자료, TSMC 공식 페이지). 다른 하나는 **원래 발화가 무엇이었는지 확인했기 때문**입니다. 하이브리드 본딩 도입 시점이 그런 경우인데, 두 매체가 다투는 것처럼 보였던 사안이 실은 **발표자가 세대를 지목하지 않았고 한 매체가 추론을 제목으로 올린 것**이었습니다. 상충으로 보이는 항목을 만나면 양쪽 보도를 비교하기 전에 **1차 발화가 무엇이었는지**를 먼저 확인해야 한다는 사례로 남깁니다.

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| JEDEC HBM4E 패키지 높이 규격 (825–900 µm 논의) | **미확정** (2026-09-01 재확인까지 변화 없음). JC-42.2 최근 문서 목록에 HBM4E 관련 문서 **0건**을 확인. 다만 **775 µm 상한의 근거가 밝혀졌습니다** - 로직 웨이퍼 두께가 같은 775 µm이기 때문 | [03-hbm.md](03-hbm.md), [06-process.md](06-process.md), [appendix-c-industry.md](appendix-c-industry.md) |
| HBM4E 통합 JEDEC 표준 존재 여부 | **부재** (2026-09-01 재확인까지 변화 없음). JEDEC 공식 페이지가 HBM4·SPHBM4·개발 중인 HBM5만 언급하고 **HBM4E를 한 번도 거명하지 않습니다.** 현행 최신 HBM 표준은 **JESD270-4A**(2025-12) | [03-hbm.md](03-hbm.md) |
| HBF 세부 스펙 (패키징·인터페이스·내구성·전력·가격) | **대폭 해소 (2026-09-01)** - **사양 원문 v0.7.0을 확보했습니다.** 인터페이스(UCIe 3.0)·패키징(10.975 × 16 mm, 775 µm)·컨트롤러 분담이 전부 확인되었습니다. **남은 [미공개]는 셋** - 쓰기 내구성 정량 스펙(사양이 "제품별"로 **의도적으로 비워 둠**), 전력 프로파일, 가격. 확인 실패와 설계된 공백을 구분해야 합니다 | [04-hbf.md](04-hbf.md) |
| DDR6 JEDEC 비준 | **미비준** (2026-09-26 재확인까지 변화 없음). JEDEC 공식 페이지 문구가 **한 글자도 바뀌지 않았습니다**. **2026-08-24 – 28 San Diego 합동 위원회(JC-16/40/42/45/63/64) 회의가 열렸으나 회의 종료 한 달이 지난 2026-09-26까지도 공개 발표가 없습니다.** 같은 기간 JEDEC 공표 목록에는 DDR5 계열 부품 규격(JESD82-542/-543)만 올라왔습니다. 보도자료 목록의 최신 항목도 여전히 **2026년 8월자**(Automotive Electronics Forum 안내)입니다. 차기 회의는 2026-11-30 – 12-04 | [02-dram.md](02-dram.md) |
| TSMC N2 HD SRAM 비트셀 크기 논쟁 | **종결 (2026-09-01)** - **0.0175 µm²는 발표 전에 나온 추정값이었습니다.** 그 값을 처음 실은 기사는 IEDM 발표 **이전** 시점에 "약(around)"이라는 한정어와 함께 매크로 밀도에서 역산해 적었고, 같은 매체의 발표 후 현장 보도는 이를 반복하지 않습니다. IEDM 2024 논문 초록도 매크로 밀도만 적고 **비트셀 면적을 제시하지 않습니다.** ISSCC 2025 현장 보도와 TSMC 공식 페이지는 모두 **0.021 µm²** 입니다. 검산도 정합합니다(0.021 µm² + 배열 효율 80.0% = 38.1 Mb/mm²). **두 값은 다른 두 측정이 아니라 추정값과 발표값이었습니다.** IEDM 논문 전문은 미확보이나 이 모음집은 0.021 µm²를 채택하고 항목을 종결합니다 | [01-sram.md](01-sram.md) |
| D1c 세대 다이 분석 공개 | **부분 해소** - TechInsights가 SK하이닉스 D1c 분석을 2026-06-09 공개. **공개 블로그에 수치가 없고 실측값은 유료 보고서 영역이라 `원문 미확인`** | [02-dram.md](02-dram.md), [00-memory-hierarchy.md](00-memory-hierarchy.md) |
| SPHBM4 (JESD330-4)의 핀 속도·등급별 대역폭·지원 단수 | **원문 미확인 유지** - 규격 원문은 여전히 유료입니다. 다만 **JEDEC 공식 문서 페이지가 상대 표현을 제공**합니다: "각 채널 인터페이스는 16비트 DDR 데이터 버스를 유지하며 대응하는 HBM4 채널(64 데이터 비트)보다 **4배 빠르다**". 절대 핀 속도는 여전히 미공개이며, 기술 매체가 인용하는 22.4 – 46.0 GT/s 범위는 **1차 근거 미확인이라 이 모음집이 쓰지 않습니다** | [03-hbm.md](03-hbm.md) |
| SPHBM4 채택 벤더·제품 | **부재 확인** (2026-09-01 공개 검색 범위에서 발표 확인되지 않음). **부재는 등급을 부여할 수 없습니다** - "찾지 못했다"이지 "존재하지 않는다"가 아닙니다 | [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| 삼성 V10 BV-NAND의 공식 면적 밀도와 셀 타입 | **해소 (2026-09-01)** - **삼성 자신의 ISSCC 2025 논문 제목**에 28 Gb/mm²와 3b/cell(TLC)이 들어 있음을 확인(T2). 등급이 T3에서 **T2로 상승**. 동시에 **FMS 2026 보도자료 원문에는 Gb/mm² 표기가 0건**이고 "약 430층"도 없음을 대조 확인 - 이전 판의 유보가 정확했습니다. 남은 유보: 논문(2025-02)과 제품(2026-08)이 동일한지 명시한 자료 없음. 층수는 논문 제목조차 **"4XX"** 로만 표기 | [05-nand.md](05-nand.md) |
| 삼성 V10 양산 여부 | **부분 이동 (2026-09-01)** - 2026-08-31 게재된 개발진 인터뷰에서 **삼성 공식 문서에 처음으로 과거형 양산 표현**이 등장했습니다("양산 단계에서는…", "양산화할 수 있었습니다"). 다만 **같은 글에 공급처·출하·양산 개시 시점·물량이 전혀 없습니다.** 개발 회고 문맥의 과거형은 "양산 준비를 마쳤다"와 "이미 양산 중이다"를 구분하지 않으므로, 상태를 **"공식 문서에 과거형 표현 등장, 시점·물량 미공개"** 로만 옮깁니다. 국내 매체의 "양산해 공급 중"은 여전히 업계 소식통 기반(T3) | [05-nand.md](05-nand.md) |
| HBM4E 양산 시점 | **해소 (2026-09-01)** - 삼성 공식 보도자료가 **"2월 HBM4 양산, 5월 HBM4E 샘플 출하"** 로 두 세대를 명확히 구분(T1). 이 모음집이 추정했던 **HBM4와의 혼동이 원인**이었음이 확인되었습니다. 양산 목표는 SK하이닉스·마이크론이 2027년을 제시하나 삼성은 "고객 일정에 맞춰"로만 적어 **[벤더 목표치]** 로만 기록 | [03-hbm.md](03-hbm.md) |
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

| Hot Chips 2026 발표 내용 (튜토리얼 2026-08-23) | **대폭 해소 (2026-09-01)** - **발표 슬라이드 3종을 확보해 대조했습니다**(SK하이닉스 22장, OXMIQ HBF 23장, 삼성 base die). 대조 결과 **기존 서술 정정 4건**이 나왔습니다(10절 참조). **다만 학회 공식 아카이브 원본이 아니라 매체가 게재한 발표 자료**이며, 확보한 장수가 덱 전체라는 보장이 없습니다. 미확보: Jim Handy 발표, 마이크론 덱 전량, 삼성 덱 1 – 2쪽 | [03-hbm.md](03-hbm.md), [04-hbf.md](04-hbf.md), [appendix-c-industry.md](appendix-c-industry.md) |
| 하이브리드 본딩의 세대별 도입 시점 | **해소 (2026-09-01)** - **상충이 아니었습니다.** 양쪽 기사 본문과 슬라이드를 모두 확보한 결과, **발표자는 세대를 지목하지 않았고** 한 매체가 자기 본문에서 "발표자는 목표 세대를 지목하지 않았다"고 밝히면서 추론을 제목으로 올린 것이었습니다. 슬라이드는 세대가 아니라 **성숙도**로 표기(16단 Development, 20단 이상 Research). 제조사 뉴스룸 기고문도 "HBM4E 또는 HBM5"로 **범위**를 적습니다 | [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| zHBM 이득 수치의 기준선 | **해소 (2026-09-01), 다만 결과가 반대였습니다** - 슬라이드를 확보하니 **한 장 안에서 좌측 차트는 HBM5, 우측 차트는 HBM4E를 기준**으로 쓰고 있었습니다. 다수 매체가 "−70%"에 붙인 HBM4E 기준은 **틀렸습니다.** "약 100 W 절감"과 "+8.3%"는 슬라이드가 두 차트를 화살표로 연결해 **같은 재배분임을 도해**하고 있어 이전 판의 유보가 해소됩니다. 삼성 공식 보도자료는 또 다른 수치 세트(전부 HBM5 대비)를 제시하므로 **세 벌을 섞으면 안 됩니다** | [03-hbm.md](03-hbm.md) |
| HBF 실효 접근 단위 (읽기 64 KB / 쓰기 1 MB) | **해소 (2026-09-01)** - **사양 규정값이 아니라 최대 대역폭용 권고 청크**입니다. 사양이 규정한 접근 단위는 읽기 **64 B – 4 KiB**, 쓰기 **4 KiB**이며, 발표 자료도 둘을 **별개 슬라이드**로 나누어 제시합니다. **다만 문제가 하나 남습니다** - 발표 슬라이드가 64 KB / 1 MB에도 출처를 OCP 사양으로 표기했으나 **사양 130쪽 텍스트 레이어에 "64KB" 문자열이 0회**입니다(그림 55개 내부는 확인 범위 밖) | [04-hbf.md](04-hbf.md) |

**2026-09-01 회차에서 새로 등록된 항목**

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| Hot Chips 2026 공식 슬라이드 아카이브 | **접근 차단 (기한부, 2026-09-26 재확인)** - 슬라이드 PDF 8종과 전체 proceedings zip 모두 여전히 `WWW-Authenticate: Basic realm="Attendees Only"`입니다. 별도 공개 경로(/proceedings/, /slides/)도 404입니다. **공식 FAQ의 2026년 12월 초 공개 예고에 변화 없음.** 2024·2025년 슬라이드는 무료 공개되어 있음을 실측했습니다. **2026-09-26 재확인에서도 두 PDF 모두 401이 유지됩니다.** **2026년 12월에 원본 대조를 다시 해야 합니다** | [03-hbm.md](03-hbm.md), [04-hbf.md](04-hbf.md), [02-dram.md](02-dram.md) |
| iHBM의 기존 설계 적용 가능 여부 | **공식 자료 간 상충 (2026-09-01 확정)** - 양쪽 모두 SK하이닉스 자신의 진술입니다. **2026-05 공식 보도자료(T1)**: "기존 SiP 구조와 높은 **설계 호환성**을 제공해 고객이 **최소한의 설계 조정만으로** 채택할 수 있다". **2026-08 Hot Chips 발표자 직접 인용(T3 보도, 발언 자체는 직접 인용)**: "이미 설계에 들어간 세대에는 적용할 수 없다". 5월 문구가 명시적으로 "설계"를 말하므로 **공정 축과 설계 축으로 나누어 화해시킬 수 없습니다.** 어느 쪽도 채택하지 않았습니다 | [03-hbm.md](03-hbm.md) |
| **(신규)** 16단 HBM4 코어 다이 두께 | **세 값 병존** - 발표 슬라이드는 **상대치 0.9배**로만 적고, 한 매체는 **약 50 µm**, 다른 자료는 **30 µm**를 전합니다. 절대치를 밝힌 1차 근거가 없으므로 이 모음집은 **상대치만 인용**합니다 | [03-hbm.md](03-hbm.md), [06-process.md](06-process.md) |
| d-Matrix 3D DRAM의 적층 구성 | **해소 (2026-09-01)** - **1단(1-Hi)입니다.** 슬라이드 문구 인용("1Hi 32GB 3D-DRAM")과 발표자 직접 인용(다층 계획 질문에 "1단을 동작시키는 것만으로도 벅차다")이 근거이며, "4단"은 매체 한 곳의 서술입니다. 이에 따라 정량값을 본문에 채택했습니다 | [02-dram.md](02-dram.md) |

**2026-09-01 회차(v6.4)에서 새로 등록된 항목**

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| **(신규)** NVHBM의 연산 다이 면적 이득 | **원문 내 불일치** - NVIDIA 기술 블로그의 표는 "최대 25%", 같은 글 본문의 다른 절은 "가용 메인 다이 실리콘 최대 30%", 기업 블로그는 25%입니다. **한 회사가 같은 날 낸 두 글, 그리고 한 글 안에서 값이 다릅니다.** 어느 하나를 확정값으로 쓰지 않고 병기합니다 | [03-hbm.md](03-hbm.md) |
| **(신규)** SK하이닉스 인디애나 팹의 HBM 세대와 양산 분기 | **공식 자료에 없음** - SK하이닉스 공식 발표는 "차세대 HBM"과 "2029년 하반기"까지만 적습니다. 세대명 "HBM4E"와 분기 특정("3분기" 또는 "2분기")은 **매체 보도에만** 있고 매체 간에도 갈립니다 | [appendix-c-industry.md](appendix-c-industry.md) |
| **(신규)** SK하이닉스의 HBM4E base die 인텔 파운드리 위탁 검토 | **보도 단계** - "검토 중(reportedly)" 수준의 전언이며 제조사 확인이 없습니다. 함께 인용된 "TSMC HBM4 base die가 코어 다이의 3 – 4배 비용"도 추정치입니다. **어느 쪽도 본문에 반영하지 않았습니다** | [03-hbm.md](03-hbm.md), [appendix-c-industry.md](appendix-c-industry.md) |
| **(신규)** HBM4 12단 대 8단 출하 비중 | **업계 관측** - 삼성·SK하이닉스가 하반기부터 8단 비중을 늘린다는 보도가 나왔고 근거로 2048 I/O에 따른 발열, 12단 적층 수율, 고객사의 용량 옵션 다변화를 듭니다. **익명 업계 소식통 기반이며 제조사 공식 확인이 없어** 본문에 반영하지 않았습니다 | [03-hbm.md](03-hbm.md) |

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

**2026-09-26 회차(v6.6)에서 새로 등록된 항목**

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| **(신규)** JESD230 NAND 상호운용 규격 본문 | **원문 미확인** - 문서 번호·제목·공동 개발 주체·규정 대상 세 방식은 공표 목록과 초록에서 확인했으나 **본문은 로그인 벽 뒤**입니다. BiCS10이 쓰는 **Toggle DDR6.0의 세부 규정이 이 문서에 있는지 확인하지 못했습니다** - 방식 계열 이름이 같은 것을 버전 일치로 읽으면 안 됩니다 | [05-nand.md](05-nand.md) |
| **(신규)** 마이크론 512 GB RDIMM의 적층 구성 | **[미공개]** - 적층 단수, 다이 개수, 다이 용량, 패키지 높이가 원문에 없습니다. TSV 수직 적층이라는 방식만 공개되었습니다. 양산은 **2027년 하반기 목표([벤더 목표치])** 이며 현재는 **실증 단계**입니다 | [02-dram.md](02-dram.md) |
| **(신규)** 512 GB RDIMM 전력 수치의 측정 조건 | **[미공개]** - 16.0 W와 44.2 W라는 절대값과 용량 정합 기준선은 각주에 있으나, **어떤 워크로드·온도에서 측정했는지가 없습니다.** "1.4배"는 **Spark SVM 한 종목**의 값이라 일반화 근거가 없습니다 | [02-dram.md](02-dram.md) |
| **(신규)** SALT-KV의 정량 성능 | **[미공개]** - 처리량·지연·적중률·용량 절감 수치가 공개 기사에 **한 건도 없고** 논문·기술 문서도 확인하지 못했습니다. **접근 방식의 등장으로만 기록**하며 성능 주장으로 쓸 수 없습니다 | [부록 B](appendix-b-workloads.md) |
| **(신규)** HBF의 동작 제품 존재 여부 | **부재 확인 (2026-09-26)** - 2026-09 AI Infra Summit에서 HBF는 **구조 모형(product mock-up)** 으로 전시되었고, 같은 부스의 PIM·SALT-KV는 동작 하드웨어와 시연이 있었습니다. 6-4절 일정표(샘플 2026년 하반기 전망)와 어긋나지 않으나, **9월 시점에 동작 제품 전시는 확인되지 않았습니다** | [04-hbf.md](04-hbf.md) |
| **(신규)** SK하이닉스 미국 Global AI R&D 센터 | **정성 진술만** - 2026 Global Forum CEO 기조에서 용인 클러스터·인디애나 팹과 함께 "설립"이 언급되었습니다. **위치·시점·투자액·인원이 전혀 없습니다** | [appendix-c-industry.md](appendix-c-industry.md) |

**2026-09-15 회차(v6.5)에서 새로 등록된 항목**

| 항목 | 상태 | 확정 시 갱신할 문서 |
|---|---|---|
| **(신규)** JESD328 SOCAMM2 규격 본문 | **원문 미확인** - 공표 사실·명칭·위원회·용도는 공개 페이지에서 확인했으나, **전송률 규정값·핀 수·최대 용량 구성·기계적 치수는 규격 본문이 등록·로그인 뒤에 있어 확인하지 못했습니다.** 이 모음집이 쓰는 9.6 Gb/s는 **공표 8개월 전 보도자료의 미래형 서술**과 **제조사 제품 발표(T1)** 두 갈래 근거이며 규격 확정값이 아닙니다 | [02-dram.md](02-dram.md) |
| **(신규)** MRCD·MDB 규격 본문 | **원문 미확인** - JESD82-542 / -543 / -553의 서지 정보와 초록까지만 확보했습니다. 전송률·타이밍 등 내부 수치는 인용하지 않습니다 | [02-dram.md](02-dram.md) |
| **(신규)** SOCAMM2 양산 제품의 공표 JESD328 준수 여부 | **확인 실패** - **세 회사 모두 SOCAMM2 제품 발표가 있습니다**(마이크론 샘플 2025-10·2026-03, 삼성 샘플 2025-12, **SK하이닉스 양산 2026-04-20**). 그런데 **SK하이닉스 양산 선언이 JESD328 공표(2026-06)보다 두 달 앞섭니다.** 공표본 준수를 밝힌 제조사 문서가 없으므로 "SOCAMM2 제품 = JESD328 준수"로 쓰지 않습니다 | [02-dram.md](02-dram.md) |
| **(신규)** SOCAMM2 출하 물량과 삼성 제품의 양산 여부 | **[미공개]** - SK하이닉스는 양산을 선언했으나 **물량이 없습니다.** 삼성은 "고객 샘플 공급 중"(2025-12) 이후 양산 발표를 확인하지 못했고 **용량 표기도 없습니다.** 마이크론 두 제품은 샘플 단계 발표입니다 | [02-dram.md](02-dram.md) |
| **(신규)** SOCAMM2 "RDIMM 대비" 수치의 기준선 | **두 회사 미기재, 한 회사는 보도자료마다 다름** - 삼성(55% 감소)·SK하이닉스(75% 효율 개선)는 비교 대상 RDIMM의 용량·수량을 밝히지 않았습니다. 마이크론은 밝혔으나 2025-10은 "128 GB RDIMM 2장", 2026-03은 "64 GB RDIMM 2장"으로 **서로 다릅니다.** 회사 간 비교는 성립하지 않습니다 | [02-dram.md](02-dram.md) |
| **(신규)** 삼성 High-NA EUV의 DRAM 적용 세대·레이어 수 | **[미공개]** - 2026-09-08 발표는 "2028년까지 DRAM 대량 양산에 도입"까지만 적습니다. 세대, 레이어 수, 팹, 12인치 포토마스크 도입 시점이 없습니다. **[벤더 목표치]** | [06-process.md](06-process.md), [02-dram.md](02-dram.md) |
| **(신규)** SK하이닉스 'Full-Stack AI Memory'의 HBF 제품 계획 | **정성 진술만** - 2026-09-08 행사에서 HBF가 3D 적층 DRAM·HBM과 나란히 포트폴리오에 거명되었으나 **용량·대역폭·시점·제품명이 전혀 없습니다.** 같은 글 전체에 정량 수치가 0건입니다. 상태 변화의 근거로만 쓰고 출하 계획으로 읽으면 안 됩니다 | [04-hbf.md](04-hbf.md) |
| **(신규)** OCP HBF 사양의 재현 가능한 직접 URL | **미기록** - 이전 회차가 SHA-256과 접근 경로는 남겼으나 **문서 URL 자체를 기록하지 않았습니다.** 2026-09-11 재조사에서도 복원하지 못했습니다. **다음 회차를 위해 확인된 것만 남깁니다**: (1) OCP 문서의 URL 형식은 `opencompute.org/documents/<슬러그>-pdf` 이며 대조군(`odsa-openhbi-v1-0-spec-rc-final-1-pdf`)이 200 + `application/pdf` 로 응답함을 실측했습니다. (2) 버전은 점이 아니라 하이픈으로 들어갑니다(`v0-7-0`). (3) 제목 기반 슬러그 12종을 시도했으나 전부 404였고, **OCP 사이트 검색과 공개 검색 어느 쪽도 이 문서를 노출하지 않습니다.** 슬러그가 제목과 다르게 붙은 것으로 보입니다 | [04-hbf.md](04-hbf.md), [SOURCES.md](SOURCES.md) |

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

| **2026-09-01** | **v6.3 갱신 (Hot Chips 2026 종료 후 원문 대조).** **이번 회차의 목적은 새 소식 반영이 아니라 v6.2를 원문으로 검증하는 것**이었습니다. v6.2가 학회 진행 중에 작성되어 첫날 보도만을 근거로 삼았기 때문입니다.
**확보한 원문 넷.** (1) **OCP HBF High-Level Base Die Specification v0.7.0** 130쪽(T0) - [04-hbf.md](04-hbf.md) 6-3절을 사양 값으로 재작성하고 6-3-1절 신설. (2) **Hot Chips 발표 슬라이드 3종** - SK하이닉스 22장, OXMIQ 23장, 삼성 base die. (3) **삼성 FMS 2026 보도자료**(T1). (4) **TSMC 공식 리서치 페이지**(T1).
**기존 서술 정정 4건.** ① [03-hbm.md](03-hbm.md) 7-1절 "16단 HBM3E는 칩 두께·갭·범프 피치를 각각 절반으로" → **절반은 갭 높이뿐**이고 나머지는 0.9배. ② 하이브리드 본딩 열저항 감소율의 기준선이 **MR-MUF가 아니라 TC-NCF**(20단 기준 MR-MUF 대비로는 약 25%). ③ "PDN 75% 개선"은 **HBM3 → HBM3E 비교 한정**. ④ EMIB는 **선택지 목록에 등재된 것이지 정량 스트레스 비교 대상이 아님**. 아울러 발표 제목·발표자 소속·튜토리얼 날짜를 학회 공식 프로그램 표기로 정정했습니다(HBF 튜토리얼 발표자 소속이 SanDisk가 아니라 **OXMIQ Labs·PRAXMATI**).
**추적 항목 6건 해소.** HBF 세부 스펙, HBF 실효 접근 단위, 하이브리드 본딩 세대별 도입 시점, zHBM 이득 수치의 기준선, HBM4E 양산 시점, 삼성 V10 면적 밀도·셀 타입. **TSMC N2 비트셀 논쟁도 대폭 해소**(0.021 µm², 이득은 DTCO). **신규 등록 4건**(공식 슬라이드 아카이브 12월 공개, iHBM 적용 가능 여부 상충, 16단 코어 다이 두께 3값, d-Matrix 적층 구성 상충).
**신규 반영.** [00-memory-hierarchy.md](00-memory-hierarchy.md) 1-1절 신설(메모리 월 정량값)과 HBF 휘발성 칸에 조건부 단서. [02-dram.md](02-dram.md) 9-4절 신설(로직을 DRAM 위에). [03-hbm.md](03-hbm.md) 7-2·7-3·7-4절 신설. [07-reliability.md](07-reliability.md)에 Llama 3 필드 데이터(HBM3 17.2%). [appendix-a-cxl.md](appendix-a-cxl.md)에 CXL 4.0과 JEDEC CXL 표준 3종. **v6.2가 반영하지 못한 8월 25일 Memory 세션과 튜토리얼 3개 발표의 존재를 기록했습니다** |

| **2026-09-01** | **v6.4 갱신 (누락 구간 보완과 재확인).** v6.3의 조사가 **오늘 날짜를 2026-08-27로 잘못 잡은 상태에서 수행**되어, 그 이후 발행분이 "미래 날짜"로 걸러졌을 위험이 있었습니다. 2026-08-25 – 09-01 구간을 다시 훑었습니다.
| **2026-09-26** | **v6.6 갱신 (모듈 쪽 신규 발표와 NAND 표준 번호 해소).** 조사 구간은 2026-09-15 – 09-26입니다. **(1) [05-nand.md](05-nand.md) 6절의 공백이 해소되었습니다.** 그 절은 "이 문서의 소스 범위에서 NAND 인터페이스에 대응하는 표준 문서 번호가 확인되지 않았다"고 적어 두었는데, JEDEC 공표 목록에서 **JESD230G.02 "NAND Flash Interface Interoperability"**(2026-09, **JEDEC·ONFI 공동**)를 확인했습니다. 다만 제목이 "Interface"가 아니라 **"Interface Interoperability"** 이므로 소자 규격이 아니라 상호운용 규격이며, 본문은 로그인 벽 뒤라 **Toggle DDR6.0 세부 규정 포함 여부는 미확인**으로 남겼습니다. **(2) 마이크론이 512 GB DDR5 RDIMM을 실증**했습니다(2026-09-15, T1). TSV 수직 적층, 최대 9,200 MT/s, 24슬롯 2소켓에서 12 TB, AMD·인텔 검증 중, 양산 **2027년 하반기 목표**입니다. [02-dram.md](02-dram.md) **6-3-2절을 신설**했습니다. 이 발표는 직전 회차의 반례라 함께 적었습니다 - 전력 각주가 **절대 와트(512 GB 1장 16.0 W 대 128 GB 4장 44.2 W)와 용량이 맞는 기준선**을 제시합니다. 같은 회사의 SOCAMM2 각주가 총용량이 어긋난 비교였던 것과 대비되므로, **판단 대상은 회사가 아니라 각 수치에 붙은 기준선**이라는 점을 6-3-2절에 명시했습니다. **(3) HBF의 전시 상태를 확인했습니다.** AI Infra Summit 2026(09-15 – 17)에서 SK하이닉스가 HBF를 **구조 모형(product mock-up)** 으로만 전시했고, 같은 부스의 PIM·SALT-KV는 동작 시연이 있었습니다. [04-hbf.md](04-hbf.md) 6-4-1절에 보강했습니다. 같은 세션에서 **워크로드 대응**(HBF = long-context, PIM = fast-decoding)이 제조사 입으로 제시되었습니다. **(4) SALT-KV**(Semantic-Aware Lifecycle Tiering for KV Cache)를 [부록 B](appendix-b-workloads.md) 8절에 넣었습니다. KV 캐시를 문맥 구간으로 나눠 HBM·DRAM·SSD에 배치하는 방식이며, **정량 수치가 0건이라 접근 방식의 등장으로만** 기록했습니다. **오인용 함정 5건**을 추가했습니다. **변화 없음:** DDR6·HBM5 JEDEC 문구 불변, **San Diego 합동 위원회 회의는 종료 한 달이 지나도록 공개 발표 없음**, JEDEC 보도자료 최신 항목 여전히 8월자, Hot Chips 공식 슬라이드 2종 여전히 401, CXL 4.0·UCIe 3.0 최신, 삼성 뉴스룸은 이번 구간에 메모리 항목 없음. **확인했으나 채택하지 않은 것:** 삼성의 유리 캐리어 세정 물량·웨이퍼 투입량·HBM4 출하 비중을 담은 국내 집계 글이 있었으나 **1차 출처를 확인하지 못해 쓰지 않았습니다.** SK하이닉스 2026 Global Forum(09-18)은 **정량 수치 0건**인 채용·비전 행사라 본문에 반영하지 않고 미국 Global AI R&D 센터 언급만 9절에 등재했습니다. 마이크론 4분기 실적 발표는 **2026-09-30**으로 이번 구간 밖입니다 |
| **2026-09-15** | **v6.5 갱신 (표준 공표 추적과 빠져 있던 계층 보완).** 조사 구간은 2026-09-01 – 09-15이며, 확인 작업은 **09-11과 09-15 두 차례**에 나누어 했습니다(각주의 확인일이 둘로 갈리는 이유). **이번 회차가 찾아낸 것은 새 소식보다 공백이었습니다.** (1) JEDEC 공표 목록에서 2026년 9월자 **JESD82-542 / -543**(DDR5MRCD02 · MRCD03)을 확인해 [02-dram.md](02-dram.md) 6-3절의 **"MRCD 규격 진행 중"을 정정**했습니다(이전 판 기준일 2026-04). **JESD82-553**(MDB03, 2026-08)도 추가했습니다. (2) 같은 목록에서 이 모음집에 **한 글자도 없던 JESD328 SOCAMM2**(2026-06, JC-45)를 발견해 **6-3-1절을 신설**했습니다. 조사를 이어 가니 **세 회사 모두 제품 발표가 있었고**(마이크론 샘플 2025-10·2026-03, 삼성 샘플 2025-12, **SK하이닉스 양산 2026-04-20** - 표준 공표보다 두 달 앞섬), 세 회사의 **"RDIMM 대비 전력" 수치는 지표도 기준선도 달라** 한 표에서 비교할 수 없음을 원문 각주로 확인했습니다. 마이크론은 두 보도자료에서 RDIMM 쪽 기준선이 "128 GB 2장"과 "64 GB 2장"으로 다르고, 256 GB 제품의 "TTFT 2.3배"는 RDIMM 비교가 아니라 **LPDRAM 2 TB 대 1.5 TB의 예측값**입니다. (3) **삼성이 2028년까지 DRAM 대량 양산에 High-NA EUV를 도입할 계획**을 발표했습니다(2026-09-08, T1). [06-process.md](06-process.md) 3-3절 도입 현황 표에 유일한 T1 행으로 넣고, SK하이닉스의 "첫 설치"(2025-09, T3)와는 **다른 사건**임을 적었습니다. (4) 제조사 뉴스룸 링크를 따라가다 **삼성·브로드컴 MOU**(2026-07-25)를 확인해 [부록 C](appendix-c-industry.md) 2-1절을 신설했습니다. "2,000억 달러 이상"은 **메모리·파운드리 합산, 5년, MOU 추정치**입니다. (5) SK하이닉스 Future Forum(2026-09-08)에서 **HBF가 제조사 포트폴리오 전략에 처음 거명**되어 [04-hbf.md](04-hbf.md) 6-4-1절을 신설하고, "방열·공정 복잡도" 발언으로 [02-dram.md](02-dram.md) 9-4절을 보강했습니다. 그 글에는 **정량 수치가 0건**입니다. **오인용 함정 13건**을 추가했습니다. **정정 2건:** SOURCES 2절·README·[00](00-memory-hierarchy.md)·[04](04-hbf.md) 각주가 OCP 문서를 "Architecture Specification"으로 적고 있었으나 원문 표지는 **"High-Level Base Die Specification"** 입니다(발표 슬라이드의 표기를 인용한 곳은 그대로 둠). 그리고 **작성 중 판단 1건을 공개 전에 뒤집었습니다** - 09-11 작업분이 "삼성·SK하이닉스 SOCAMM2 제품은 부재 확인"으로 적었으나 09-15 재검색에서 SK하이닉스 양산 발표(T1)가 나왔습니다. 9절이 이미 적어 둔 **"부재는 등급을 부여할 수 없다"는 규칙이 그대로 들어맞은 사례**입니다. **변화 없음:** DDR6·HBM5 JEDEC 문구 불변, **San Diego 합동 위원회 회의(08-24 – 28)는 약 3주가 지나도록 공개 발표 없음**, JEDEC 보도자료 최신 항목 여전히 8월자, Hot Chips 공식 슬라이드 2종 여전히 401. **조사 워크플로는 사용량 한도로 세 차례 전부 실패해 이번 회차의 모든 확인은 1차 출처 직접 대조로 이루어졌습니다** |
**정정 1건 (v6.3의 오류).** [03-hbm.md](03-hbm.md) 7-1절이 "SK하이닉스 슬라이드가 삼성 HPB에 온도 30%·열임피던스 16%를 붙였고 삼성 본인의 35%와 어긋난다"고 적었으나, **그 상충은 존재하지 않았습니다.** 확인 가능한 현장 보도 두 건 모두 경쟁사 행에 수치를 붙이지 않고, 유통되는 "16%"는 **엑시노스 2600 모바일 AP용 구리 기반 HPB의 값**입니다. 해당 서술과 추적 항목을 철회했습니다.
**근거 등급 상승 1건.** [00-memory-hierarchy.md](00-memory-hierarchy.md) 1-1절의 메모리 월 수치를 학회 현장 보도(T3)에서 **원 논문(T2, IEEE Micro 2024 "AI and Memory Wall")** 으로 교체했습니다. PDF 원문 대조. 인터커넥트 대역폭 2년 1.4배와 20년 누적(FLOPS 60,000배 / DRAM 100배 / 인터커넥트 30배)이 새로 들어왔고, **인터커넥트 행이 A5를 별도 축으로 세운 근거**가 됩니다.
**추적 항목 3건 정리.** d-Matrix 적층 구성 **해소**(1단 확정), TSMC N2 비트셀 **종결**(0.0175은 발표 전 추정값), 삼성 V10 양산 **부분 이동**(공식 문서에 과거형 표현 등장, 시점 미공개). iHBM 항목은 "발언 상충"에서 **"대조 불가"** 로 재분류했습니다.
**신규 반영.** [03-hbm.md](03-hbm.md) 2-2-1절 신설(**NVHBM** - 고객이 base die를 규정한 첫 사례, T1), 7-4절에 마이크론의 "HBM 비트당 가격 DDR5의 약 5배". [02-dram.md](02-dram.md) 9-4절에 d-Matrix 정량값과 **105°C에서 리텐션 32 ms → 4 ms** 붕괴, LPDDR6 절에 **CXMT 양산 선언**. [appendix-a-cxl.md](appendix-a-cxl.md)에 XCENA MX1. [appendix-c-industry.md](appendix-c-industry.md) 3-6-1·3-7절 신설(인디애나 팹, 키옥시아·샌디스크 일본 투자, 2027년 가격 전망).
**표준은 전부 변화 없음.** DDR6·HBM4E 통합 표준·HBM4E 높이·SPHBM4 채택 벤더·UCIe·CXL·OCP HBF 사양 버전 모두 2026-09-01 재확인까지 그대로입니다. **2026-08-24 – 28 JEDEC 합동 위원회 회의 결과도 공표되지 않았습니다** |

> **검증일 표기 정정 (2026-09-01).** 위 v6.3 항목은 작성 과정에서 한때 **검증일이 2026-08-27로 잘못 기재**되었습니다. 실제 조사·대조 작업은 전부 **2026-09-01**에 이루어졌습니다. 전 문서의 배너와 각주 99곳을 정정했습니다.
>
> **이 모음집에서 이 종류의 오류는 가벼운 것이 아닙니다.** 9절 추적 표의 "재확인까지 변화 없음"이나 각주의 "확인 <날짜>"는 **그 날짜에 실제로 확인했다는 진술**이며, 날짜가 틀리면 진술 자체가 틀립니다. 이 모음집이 앞선 회차에서 "확인하지 않은 항목의 날짜를 올리지 않는다"는 규칙을 세운 것과 같은 이유로, 확인한 날짜를 틀리게 적는 것도 같은 무게로 다룹니다. 정정 사실을 지우지 않고 여기에 남깁니다.

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
| **(v6.3 정정)** zHBM 수치에 기준선을 하나만 붙이기 | **한 장의 슬라이드가 좌우로 다른 기준을 씁니다.** 좌측 전력 차트는 **HBM5** 대비 −70%, 우측 시스템 차트는 **HBM4E** 대비 대역폭 230%·100 W 절감·+8.3%입니다. 다수 매체가 "−70%"에 붙인 HBM4E 기준은 틀렸습니다. 게다가 삼성 공식 보도자료는 **또 다른 세트**(HBM5 대비 성능 8배·밀도 10배·에너지 효율 3배·열저항 절반)를 제시합니다. **세 벌이 있으므로 세대·주체·방향을 반드시 병기하십시오** |
| **(v6.3 정정)** Hot Chips 발표를 매체 기사 제목으로 인용 | v6.2의 이 항목은 "슬라이드 원문이 없다"는 것이었는데, **원문을 확보하고 나니 문제가 다른 곳에 있었습니다.** 매체 기사 제목이 발표 제목과 다르고(삼성 발표의 실제 제목은 "HBM Base Die: How HBM Will Evolve Using Advanced Logic Processes"), 발표자 소속도 다르며(HBF 튜토리얼은 SanDisk가 아니라 **OXMIQ Labs·PRAXMATI**), **한 매체는 기자의 추론을 제목으로 올렸습니다**(하이브리드 본딩 세대). 발표 제목·발표자·소속은 **학회 공식 프로그램**에서 확인하십시오 |
| **(v6.3)** 하이브리드 본딩 열저항 감소율을 "MR-MUF 대비"로 인용 | 슬라이드의 ▼19 / 25 / 30 / 35% 계열은 **TC-NCF 기준**입니다. **MR-MUF 대비로는 20단에서 약 25%** 에 그칩니다. 같은 슬라이드가 코어 다이 두께와 범프 피치에는 "vs MR-MUF"를 명시하면서 열저항만 다른 기준을 쓰므로, **세 수치를 한 문장에 나열하며 기준선을 하나로 뭉뚱그리면 안 됩니다** |
| **(v6.3)** 16단 HBM3E를 "치수를 모두 절반으로 줄였다"로 요약 | 절반이 된 것은 **갭 높이 하나뿐**입니다. 칩 두께와 범프 피치는 0.9배이고 총 패키지 높이는 720 → 775 µm입니다. 네 단을 더 쌓기 위해 깎은 것은 **다이가 아니라 다이 사이의 빈틈**이며, 슬라이드가 적은 난제도 두께 쪽은 Die Warpage, 갭·피치 쪽은 Gap-Fill Quality로 갈립니다 |
| **(v6.3)** HBF를 "리프레시가 필요 없는 비휘발성"으로 서술 | **OCP 사양이 정반대를 규정합니다.** 전원 인가 상태 리텐션이 **85°C에서 24시간**이고, 전원 차단 시에는 "may not retain data … **equivalent to HBM**"이며, 영구 저장에는 SSD를 쓰라고 권고합니다. 게다가 **통상 24 – 48시간마다 호스트가 리프레시**해야 합니다. HBF의 비휘발성을 SSD의 그것과 같은 것으로 옮기면 안 됩니다 |
| **(v6.3)** HBF "읽기 64 KB / 쓰기 1 MB"를 사양 규정값으로 인용 | **규정값은 읽기 64 B – 4 KiB, 쓰기 4 KiB입니다.** 64 KB / 1 MB는 **최대 대역폭을 내려면 이만큼 묶으라는 소프트웨어 권고**이며 발표 자료도 둘을 별개 슬라이드로 나눕니다. "1 MB를 써야 1바이트를 고친다"가 아니라 "1 MB로 묶어야 3 TB/s가 나온다"입니다. **덧붙여 발표 슬라이드가 이 값의 출처를 OCP 사양으로 표기했으나 사양 본문 텍스트에는 없습니다** |
| **(v6.3)** TSMC N2의 SRAM 밀도 개선을 비트셀 축소로 읽기 | TSMC 공식 서술은 "**0.021 µm² 비트셀**을 쓰며 **DTCO를 통해** 밀도를 1.1배 개선"입니다. **비트셀은 N5·N3E와 같은 값이므로 세 노드 연속 제자리**이고, 이득은 셀이 아니라 주변회로·레이아웃에서 나왔습니다. 매크로 밀도 38.1 Mb/mm²를 셀이 줄어든 증거로 쓰면 안 됩니다 |
| **(v6.3)** V10과 V9의 밀도를 셀 타입 없이 비교 | 삼성 V10의 **TLC** 밀도(28 Gb/mm²)와 V9의 **QLC** 밀도(약 28.5)가 거의 같습니다. 셀 타입을 떼면 "한 세대 지나도 밀도가 그대로" 또는 "오히려 낮아졌다"는 정반대 결론이 나오는데, 같은 TLC끼리는 삼성 자신이 밝힌 대로 **약 58% 증가**입니다. v6의 QLC·TLC 함정이 세대 비교에서도 그대로 작동합니다 |
| **(v6.3)** "PDN 75% 개선"을 최근 세대 일반으로 인용 | 이 주석이 붙은 대상은 **HBM3와 HBM3E의 전력 분배망 비교 두 장**입니다. HBM4를 포함한 값이 아닙니다 |
| **(v6.4 정정)** 삼성 HPB의 "열저항 16% 개선"을 HBM 수치로 인용 | **다른 제품의 값입니다.** 16%는 **엑시노스 2600 모바일 AP**에 적용된 구리 기반 HPB의 값이며, HBM용 HPB는 실리콘 기반으로 별도 검토 중입니다. HBM용으로 발표된 값은 **"PHY 면적 50% 이상 덮을 때 피크 온도 35% 초과 감소"** 이고 독립 현장 보도 두 건이 일치합니다. **이 모음집의 직전 판도 이 혼동을 그대로 옮겨 상충으로 등재했다가 철회했습니다** |
| **(v6.4)** TSMC N2 비트셀 0.0175 µm²를 발표값으로 인용 | **발표 전에 나온 추정값입니다.** 그 값을 처음 실은 기사는 IEDM 발표 이전 시점에 "약(around)"을 붙여 **매크로 밀도에서 역산**했고, 같은 매체의 발표 후 보도는 반복하지 않습니다. IEDM 논문 초록에도 비트셀 면적이 없습니다. 발표값은 **0.021 µm²** 입니다 |
| **(v6.4)** NVHBM의 면적 이득을 단일 값으로 인용 | **NVIDIA 자체 자료 안에서 값이 갈립니다.** 기술 블로그의 표는 "연산 다이 면적 최대 25%", 같은 글 본문은 "가용 메인 다이 실리콘 최대 30%"입니다. 또 일부 매체 제목의 **"속도 50%"는 1차 출처에 없습니다**(대역폭은 최대 30%) |
| **(v6.4)** NVHBM을 Hot Chips 2026 발표로 인용 | **학회 발표가 아닙니다.** 2026-08-26 NVIDIA 공식 블로그 2건으로 공개된 것이며, 학회 공식 프로그램의 NVIDIA 발표 목록에 NVHBM 세션이 없습니다 |
| **(v6.4)** 인디애나 팹을 "HBM4E 2029년 3분기 양산"으로 인용 | 제조사 공식 발표는 **"차세대 HBM"** 과 **"2029년 하반기"** 까지입니다. 세대명과 분기는 매체가 붙인 것이며 **매체 간에도 2분기와 3분기로 갈립니다** |
| **(v6.4)** d-Matrix 3D DRAM을 "4단 적층"으로 인용 | **1단(1-Hi)입니다.** 슬라이드 문구가 "1Hi 32GB 3D-DRAM"이고, 발표자는 다층 계획 질문에 "1단을 동작시키는 것만으로도 벅차다"고 답했습니다. "4단"은 매체 한 곳의 서술입니다 |
| **(v6.4)** 키옥시아 기타카미 신규 팹 "1.8조 엔"을 인용 | **회사가 부인한 값입니다.** 이 수치는 기자가 "~로 이해된다"고 단 추정이며, 같은 기사에 키옥시아의 입장이 함께 실려 있습니다. **"이 보도들은 당사나 자회사가 한 발표가 아닙니다."** 공식 발표분은 2032년까지 310억 달러 이상이라는 총액뿐입니다 |
| **(v6.4)** XCENA MX1의 성능으로 "RAG QPS 64배"를 인용 | **다른 발표 주체의 값입니다.** 64배와 에너지 65배는 같은 세션 후반의 **삼성 CXL-PNM** 결과(디바이스 10개 기준)이며 MX1 자체 결과가 아닙니다. MX1 자체 값은 호스트-over-CXL 대비 4.7배, 로컬 DRAM 대비 2배입니다 |
| **(v6.4)** "V10"을 제조사 구분 없이 인용 | **두 회사가 같은 이름을 씁니다.** 삼성 V10은 **400층 이상 BV-NAND**, SK하이닉스 V10은 **375층 4D NAND**입니다. 층수도 구조 명칭도 다르므로 "V10 세대"라고만 적으면 어느 회사인지 사라집니다 |
| **(v6)** HBF 사양 공개를 "스펙 확인 완료"로 취급 | OCP 첫 기술 사양이 공표된 것은 사실이나, 이 모음집은 **사양 원문을 확인하지 못했습니다.** 상태는 `[미공개]`에서 **`원문 미확인`으로 이동**한 것입니다. 쓰기 내구성·전력 프로파일·가격은 여전히 `[미공개]`입니다 |
| **(v6.5)** 마이크론 SOCAMM2의 "RDIMM 대비 전력 2/3 개선"을 192 GB 제품의 값으로 인용 | **각주가 밝힌 계산 근거는 128 GB입니다.** 원문 각주 4: "128 GB 128비트 버스 SOCAMM2 **1장** 대 128 GB 128비트 버스 DDR5 RDIMM **2장**". 발표 주인공은 192 GB인데 비교는 128 GB이고 **모듈 수가 1 대 2**입니다. "모듈당 전력이 1/3"로 옮기면 틀립니다 |
| **(v6.5)** 같은 보도자료의 "TTFT 80% 이상 단축"을 SOCAMM2 모듈 측정값으로 인용 | **모듈을 꽂고 잰 값이 아닙니다.** 각주 1: "마이크론 **내부 테스트**로 검증: **GH200 NVL2**(288 GB HBM3E + **1 TB LPDDR5X**)에서 Llama 3 70B, OSL=128, LMCache 사용". 기성 시스템의 LPDDR5X 구성에서 나온 값이며 측정 주체가 제조사 자신입니다 |
| **(v6.5)** 같은 보도자료의 "전력 효율 20% 이상"과 "2/3 이상"을 같은 줄에 놓고 인용 | **기준선이 다릅니다.** 20%는 각주 2 "마이크론 **이전 세대 LPDDR5X** 대비"이고, 2/3는 **RDIMM 대비**입니다. 두 수치를 더하거나 비교하는 서술은 근거가 없습니다 |
| **(v6.5)** "SOCAMM"과 "SOCAMM2"를 1세대·2세대로 인용 | **범주명과 표준명의 관계입니다.** JESD328 초록 원문: "'SOCAMM', in general language, is used to describe the module category. **SOCAMM2 is the JEDEC standard version.**" NVIDIA가 먼저 쓴 것은 표준화 이전의 독자 사양이며, 이를 "SOCAMM 1세대 표준"으로 부르는 서술은 근거가 없습니다 |
| **(v6.5)** JESD328의 "핀당 9.6 Gb/s"를 규격 확정값으로 인용 | **공표 8개월 전 예고문의 미래형 서술입니다.** 2025-10-20 JEDEC 보도자료는 "**is forecast to support** the full LPDDR5X data rate, including configurations up to 9.6 Gb/s per pin **where platform signal integrity allows**"로 적습니다. 공표된 JESD328의 공개 초록에는 전송률이 없고 규격 본문은 미확인입니다. 제품 층위(마이크론 T1)에서는 같은 값이 확인됩니다 |
| **(v6.5)** MRCD 규격 공개를 "MRDIMM Gen2 확정"으로 인용 | **부품 규격이지 모듈 세대 규격이 아닙니다.** JESD82-542/-543은 레지스터링 클록 드라이버, JESD82-553은 데이터 버퍼의 규격이며, Gen2 로드맵은 2026-09-15 재확인 시점에도 진행 중입니다 |
| **(v6.5)** 삼성·SK하이닉스·마이크론의 SOCAMM2 "RDIMM 대비 전력" 수치를 한 표에서 비교 | **지표도 기준선도 다릅니다.** 삼성은 **소비 전력** "55% 이상 감소", SK하이닉스는 **전력 효율** "75% 이상 개선", 마이크론은 "1/3 소비"(2026-03)와 "효율 2/3 이상 개선"(2025-10)입니다. 효율로 환산하려면 성능이 같아야 하는데 두 회사가 **대역폭 2배**를 함께 주장하므로 환산이 성립하지 않습니다. 삼성·SK하이닉스는 **기준선 자체를 밝히지 않았습니다** |
| **(v6.5)** 마이크론 256 GB SOCAMM2의 "TTFT 2.3배"를 RDIMM 대비 성능으로 인용 | **RDIMM 비교가 아니고 측정값도 아닙니다.** 각주가 "**projected**"라고 적고, 비교는 **CPU당 LPDRAM 2 TB(0.12초) 대 1.5 TB(0.28초)** 입니다. 같은 LPDRAM의 **용량을 늘린 효과의 예측**입니다 |
| **(v6.5)** 마이크론 두 보도자료의 "RDIMM 대비 1/3 전력"을 같은 조건의 값으로 인용 | **기준선이 바뀌었습니다.** 2025-10 각주는 128 GB SOCAMM2 1장 대 "**128 GB** RDIMM 2장", 2026-03 각주는 같은 128 GB SOCAMM2 1장 대 "**64 GB** RDIMM 2장"입니다. 문구대로라면 RDIMM 쪽 총용량이 256 GB와 128 GB로 다르고, 어느 쪽이 오기인지는 원문으로 판정할 수 없습니다 |
| **(v6.5)** SK하이닉스 SOCAMM2 양산 보도자료 영문판의 "추론에서 학습으로 전환"을 인용 | **국문판과 방향이 반대입니다.** 국문 원문은 "AI 시장이 **학습에서 추론 중심으로** 본격 전환되면서"입니다. 영문판 "shifting focus from inference to training"은 번역 과정에서 뒤집힌 것으로 보이며 국문을 원문으로 봅니다 |
| **(v6.5)** SK하이닉스 "첫 High-NA 설치"와 삼성 "업계 최초 High-NA 도입"을 상충으로 인용 | **다른 사건입니다.** SK하이닉스는 2025-09 **장비 설치**(T3 보도), 삼성은 2028년까지 **DRAM 대량 양산 공정 적용 계획**(T1)입니다. 설치와 양산 적용은 단계가 다르므로 두 "최초"는 양립합니다 |
| **(v6.5)** 삼성·브로드컴 MOU의 "2,000억 달러 이상"을 HBM 계약 규모로 인용 | **메모리와 파운드리 합산, 5년 누적, MOU 추정치입니다.** 원문은 "estimated at more than $200 billion **across memory and foundry** over the next five years through 2030"이며 둘의 비중을 나누지 않습니다. HBM 세대도 명시하지 않습니다. 연간 HBM 시장 규모와 나란히 놓으면 단위가 맞지 않습니다 |
| **(v6.6)** 마이크론 512 GB RDIMM을 출하 제품으로 인용 | **실증 단계입니다.** 원문은 "successful demonstration"이며 AMD·인텔이 "검증 진행 중"이고, 양산은 **2027년 하반기 목표**로 "고객 수요에 맞춰"라는 조건이 붙습니다. 9,200 MT/s도 "제공할 것(will deliver)"이라는 미래형입니다 |
| **(v6.6)** 같은 발표의 "1.4배 성능"을 512 GB의 일반 성능 우위로 인용 | **한 워크로드의 값입니다.** 원문은 **Spark SVM 기반 데이터 분석**에서 **256 GB DDR5 구성** 대비 "최대 1.4배"입니다. RocksDB·Redis는 "처리량 개선"이라는 정성 서술만 있고 수치가 없습니다 |
| **(v6.6)** JESD230을 NAND 인터페이스 소자 규격으로 인용 | **상호운용 규격입니다.** 제목이 "NAND Flash Interface **Interoperability**"이고, 초록이 밝힌 목적은 JEDEC 구현과 ONFI 구현이 호환되게 하는 것입니다. JESD270-4나 JESD209-6처럼 소자 자체를 규정하는 문서와 층위가 다릅니다. **Toggle DDR6.0의 세부 규정 포함 여부는 미확인입니다** |
| **(v6.6)** SK하이닉스 AI Infra Summit 전시를 HBF 제품 출시로 인용 | **구조 모형 전시입니다.** 공식 기사가 "HBF structural model", "the product mock-up"으로 적습니다. 같은 부스에서 PIM(AiMX 카드 탑재 서버)과 SALT-KV는 **동작 시연**이 있었으므로, 전시 형태의 차이를 지우고 인용하면 안 됩니다 |
| **(v6.6)** SALT-KV를 성능이 검증된 솔루션으로 인용 | **정량 근거가 0건입니다.** 공개 기사에 처리량·지연·적중률 수치가 없고 논문도 확인되지 않았습니다. 확인되는 것은 동작 방식(KV 캐시를 문맥 구간으로 나눠 HBM·DRAM·SSD에 배치)과 전시 사실까지입니다 |
| **(v6.5)** SK하이닉스 Future Forum 발언을 HBF·3D DRAM의 사양 근거로 인용 | **정량 수치가 한 건도 없는 글입니다.** 방향 진술("Full-Stack AI Memory에 3D 적층 DRAM·HBM·HBF를 조합", "방열과 공정 복잡도가 과제")만 있으며 용량·대역폭·시점·제품명이 없습니다. 상태 변화의 근거로만 쓸 수 있습니다 |

**갱신 규칙**

- 수치를 바꿀 때는 본문·이 인덱스·[assets/IMAGE-MANIFEST.md](assets/IMAGE-MANIFEST.md)의 해당 이미지 유의사항을 **동시에** 갱신합니다.
- 각 문서 상단의 `최종 검증` 배너 날짜를 함께 올립니다.
- 9절의 미확정 항목이 확정되면 해당 행을 10절 갱신 이력으로 옮깁니다.
