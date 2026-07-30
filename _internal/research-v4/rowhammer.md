# Row Hammer와 대응 기법 (TRR·RFM·PRAC)
> 조사일: 2026-07-29 / 상태: 완료

## 0. 로컬 1차 자료 선(先)확인 결과 (중요)

| 확인 항목 | 결과 | 출처 | 등급 | 확인일 |
|---|---|---|---|---|
| jesd79_5.txt 내 "RFM" / "Refresh Management" | **0건 (검색 결과 없음)** | 로컬 `jesd79_5.txt` (DDR5 Full Spec **Draft Rev0.1**, JC42.3 COMMITTEE LETTER BALLOT) | T0(초안) | 2026-07-29 |
| jesd79_5.txt 내 "RAA" / "RAAMMT" / "RAAIMT" | **0건** | 동상 | T0(초안) | 2026-07-29 |
| jesd79_5.txt 내 "hammer" (대소문자 무시) | **0건** | 동상 | T0(초안) | 2026-07-29 |
| jesd79_5.txt 내 "Refresh" | 170건 (일반 REF/REFab/REFsb 문맥) | 동상 | T0(초안) | 2026-07-29 |
| jesd79_4.txt 내 "MAC" / "tMAW" / "TRR" / "Target Row" | **0건** | 로컬 `jesd79_4.txt` | T0 | 2026-07-29 |

**해석(주의):** 로컬 JESD79-5 사본은 **Rev0.1 위원회 회람본(draft ballot)**이며, 최종 비준본 JESD79-5(2020-07) 및 이후 개정판(-5A/-5B/-5C)과 다르다. RFM은 이 Rev0.1 초안 단계에는 **아직 들어 있지 않다.** 따라서 **"DDR5 RFM의 표준 근거"를 로컬 파일로 제시하는 것은 불가능**하며, 본 문서에서 RFM 관련 조항은 모두 웹 출처에 의존한다. 집필 시 로컬 jesd79_5.txt를 RFM 근거로 인용해서는 안 된다.

## 1. 확인된 사실

### 1-A. 임계값 세대별 추이 (MAC / HC_first / N_RH / T_RH)
> 용어 주의: 문헌마다 이름이 다르다. **MAC**(Maximum Activate Count, JEDEC DDR4 모드레지스터 상의 *보장 스펙 값*), **HC_first**(첫 비트플립이 관측된 hammer count, *실측 값*), **N_RH / T_RH**(논문마다 쓰는 rowhammer threshold). **스펙 값과 실측 값을 섞어 쓰면 안 된다.**

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| DDR3 세대(2010–2013 제조 칩) rowhammer 임계 | 약 **69.2K** activations (구형 칩 실측 N_RH) | T2 | ABACuS (Olgun et al., USENIX Security 2024) 인용 문맥, https://www.usenix.org/system/files/sec23winter-prepub-21-olgun.pdf | 실측치. 아래 139K/100K와 값이 다름 → §3 참조 |
| DDR3(2014) rowhammer 임계 | 약 **139K** (T_RH) | T2 | 2차 인용(검색 요약 경유) — **원문 미확인** | §3 상충 |
| DDR3 일반 서술 | "100K 이상의 인접 activation 필요" | T2 | DRAM-Profiler, arXiv:2404.18396 | 근사 서술 |
| DDR4(2019–2020 제조) rowhammer 임계 | **10K** activations | T2 | ABACuS(Olgun et al.) 문맥, USENIX Sec 2024 | 구형 대비 6.9× 감소 |
| LPDDR4(2019–2020 제조) rowhammer 임계 | **4.8K** activations | T2 | 동상 | 구형(69.2K) 대비 **14.4× 감소** |
| 감소 배수 | 69.2K → 10K = 6.9×, 69.2K → 4.8K = **14.4×** | T2 | 동상 | 이 배수는 출처가 명시적으로 제시한 값 |
| DDR5 세대 실측 임계 | **확인 실패** — on-die ECC와 내장 완화 로직 때문에 외부 실측이 어렵다고 명시됨 | T2 | DRAM-Profiler, arXiv:2404.18396 | "assessment is difficult" 취지. **DDR5 구체 수치를 쓰지 말 것** |

### 1-B. PRAC (Per Row Activation Counting) — DDR5
| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 도입 규격 | **JESD79-5C** (DDR5 SDRAM standard) | T0 | JEDEC 보도자료, https://www.jedec.org/news/pressreleases/jedec-updates-jesd79-5c-ddr5-sdram-standard-elevating-performance-and-security | 비준·공개된 정식 개정판 |
| 공표일 | **2024-04-17** (보도자료), 4월 공개 | T0/T3 | JEDEC 보도자료 / StorageNewsletter 2024-04-22 | |
| 기능 명칭 | Per Row Activation Counting (PRAC) | T0 | JEDEC 보도자료 | "DRAM data integrity 향상" 목적으로 소개 |
| 동작 (1) | 각 DRAM row마다 **activation 카운터**를 둠. 추가 DRAM 셀과 센스앰프를 사용하며 해당 row가 activate될 때마다 증가 | T2 | QPRAC, arXiv:2501.18861 | |
| 동작 (2) | **ABO (Alert Back-Off) 프로토콜** — rowhammer 위협 감지 시 DRAM이 호스트에 알려 트래픽을 멈추고 완화(mitigation) 시간을 확보 | T0 + T2 | JEDEC 보도자료(“alerts the system to pause traffic”) + QPRAC arXiv:2501.18861 | |
| 성능 오버헤드 | **확인 실패(정량치 미확보)** — 정성적으로는 precharge 시 카운터 read-modify-write 때문에 tRP·tRC 등 코어 타이밍이 증가한다는 서술만 확보 | T2/T3 | 아래 LPDDR6 항목과 동일 출처 계열 | 구체 %·ns 값 미확보 |

### 1-C. LPDDR6의 per-row activation tracking → **rowhammer 대응 맞음 (확인됨)**
| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| LPDDR6 표준 번호 | **JESD209-6** | T0 | JEDEC(2025-07 공표), 경유: StorageNewsletter 2025-07-10 | |
| 기존 소스 팩 3-2절의 "per-row activation tracking"의 정체 | **PRAC (Per Row Activation Counting)이며 rowhammer 대응 기능이 맞음** | T3(다수 매체 일치) | microcontrollertips.com / eeworldonline.com "What is JESD209-6…", TTI Europe, KitGuru | **JEDEC 원문 T0 직접 인용은 미확보** → 등급 T3 표기 유지 |
| 동작 | row마다 카운터 셀을 두고, precharge 시 read-modify-write로 증가. 그 대가로 tRP·tRC 등 코어 타이밍 증가 | T3 | 상동 | DDR5 PRAC과 동일 계열 메커니즘 |
| 효과(정량) | LPDDR6+PRAC은 LPDDR5X 대비 **약 5배** 많은 공격 횟수가 있어야 완화가 트리거됨 | T3 `단일 출처` | 상동(검색 요약 경유) | **원 논문 미특정. 인용 시 반드시 "단일 출처·원문 미확인" 표기** |

### 1-D. DDR5 RFM (Refresh Management) — RAA 카운터
> **표준 근거 주의**: 아래 값들은 **JESD79-5B** 계열 사양을 인용한 2차 문헌에서 확보한 것이며, **로컬 jesd79_5.txt(Rev0.1 초안)에는 RFM 조항 자체가 없다.** JEDEC 원문(T0) 직접 확인은 하지 못했다.

| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| RAA | Rolling Accumulated ACT — bank별 ACT 횟수 누산 카운터 | T2/T3 | RogueRFM, arXiv:2501.06646 / PROTRR (IEEE S&P 2022), https://comsec.ethz.ch/wp-content/files/protrr_sp22.pdf | |
| **RAAIMT** (RAA Initial Management Threshold) | **32 – 80, 8 단위** | T3 `단일 출처`(2차) | JESD79-5 해설 문헌 경유 | JEDEC 원문 미확인 → 인용 시 "2차 출처" 표기 |
| **RAAMMT** (RAA Maximum Management Threshold) | 벤더 지정. **read-only MR58 opcode bit[7:5]** 에 기록 | T3 `단일 출처`(2차) | 동상 | JEDEC 원문 미확인 |
| RFM 명령 효과 | `RFMab` = 전 bank의 RAA를 RAAIMT만큼 감산(최소 0). `RFMsb` = BA[1:0]로 지정된 bank(전 bank group 공통)만 감산 | T3(2차) | 동상 | |
| 강제 조항 | RAA가 RAAMMT에 도달하면 **REF 또는 RFM으로 카운터를 낮추기 전까지 해당 bank에 추가 ACT 불가** | T3(2차) | 동상 | RFM의 핵심 강제 메커니즘 |
| RFM의 한계(공격면) | RFM 자체가 은닉 채널·서비스 거부(DoS) 공격에 악용될 수 있음 | T2 | RogueRFM, arXiv:2501.06646 | 보안 함의는 §2 말미 한두 문장으로만 |

### 1-E. PRAC 성능 오버헤드 (정량) — **여러 논문이 서로 다른 값을 보고함 → §3 필독**
| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| PRAC 평균 slowdown | **8%** (PRAC), 7.4% (PRAC-Insecure). 이상적 PRAC-Ideal은 0.9% | T2 | Counterpoint (DRAMSec 2025), https://dramsec.ethz.ch/dramsec25-papers/counterpoint-dramsec25.pdf | 원인: 카운터 갱신용 Read-Modify-Write 타이밍 |
| PRAC 평균 slowdown | **6%** (최대 약 20%, SPEC `462.libquantum`) | T2 | PRACtical, arXiv:2507.18581 | precharge 지연 증가가 원인 |
| PRAC slowdown의 속도 의존성 | **3200 MT/s에서 2.2% → 8000 MT/s에서 14%** | T2 `단일 출처` | 검색 경유(PRAC 평가 논문 계열, 개별 논문 미특정) | 고속일수록 tRRD·tFAW가 짧아 ACT 빈도가 올라가며 고정 타이밍 페널티가 자주 노출됨. **논문 특정 실패** |
| QPRAC 계열 오버헤드 | QPRAC-NoOp 12.4%, QPRAC 0.8%, QPRAC+Proactive 계열 사실상 0 | T2 | QPRAC, arXiv:2501.18861 | *제안 기법*의 값이지 JEDEC PRAC 자체 값이 아님 |
| PRAC 타이밍 파라미터 변화 | **tRP 15 ns → 36 ns** (per-row 카운터 RMW 수용 목적) | T2 | PRACtical, arXiv:2507.18581 | 아래 §3 주의 |
| ABO 프로토콜 타이밍 | 경보 후 약 **180 ns**의 pre-recovery 구간, `RFMab` 1회당 복구 **350 ns**, ABO 간격 350 ns – 1500 ns | T2 `단일 출처` | PRACtical, arXiv:2507.18581 | 단일 논문 서술. JEDEC 원문 대조 실패 |

### 1-F. TRR (Target Row Refresh)
| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 성격 | **벤더 독자(proprietary) 구현이며 문서화되어 있지 않음.** "in-DRAM TRR의 어떤 변종도 잘 문서화돼 있지 않다"는 취지 | T2 | TRRespass (Frigo et al., IEEE S&P 2020), arXiv:2004.01807 / https://download.vusec.net/papers/trrespass_sp20.pdf | 벤더별로 서로 다름 |
| 동작 위치 | 최신 구현은 **DRAM 칩 내부에서 전적으로 동작**(호스트가 관여하지 않음) | T2 | 동상 | |
| 우회 원리 | TRR의 **sampler가 추적 가능한 aggressor row 수가 유한**하다는 점을 이용. sampler 테이블을 넘치게 하는 **many-sided hammering**으로 우회 | T2 | 동상 | |
| TRRespass 실험 결과 | **42개 DDR4 모듈 중 13개**가 TRR-aware 패턴에 취약. 3대 벤더(삼성·마이크론·SK하이닉스) 모두 포함 | T2 | 동상 | 논문 PDF 직접 파싱 실패 → 검색 결과 요약 및 다수 2차 인용으로 교차 확인 |
| 필요 aggressor 수 | 사례에 따라 **최대 19개**의 aggressor row 사용 | T2 | 동상 | |

### 1-G. 로컬 표준 문서의 시기적 한계 (직접 확인한 음성 결과)
| 항목 | 값 | 등급 | 출처 | 비고 |
|---|---|---|---|---|
| 로컬 `jesd79_4.txt` 판본 | **JESD79-4, 2012년 9월 원판** | T0 | 로컬 파일 3–8행 헤더 | Kim et al. ISCA 2014보다 **앞선 문서** |
| 그 결과 | 이 판본에는 MAC / tMAW / TRR 조항이 **존재하지 않음**(검색 0건) | T0 | 로컬 grep | MAC은 이후 개정판·SPD Annex L에서 등장 |
| 로컬 `jesd79_5.txt` 판본 | DDR5 Full Spec **Draft Rev0.1** 위원회 회람본 | T0(초안) | 로컬 파일 3–13행 | RFM 조항 **없음**(검색 0건) |

### 1-H. 연구 계보 (서지)
| 논문 | 서지 | 등급 | 확인 경로 |
|---|---|---|---|
| **최초 보고** | Kim, Daly, Kim, Fallin, Lee, Lee, Wilkerson, Lai, Mutlu, "Flipping Bits in Memory Without Accessing Them: An Experimental Study of DRAM Disturbance Errors," **ISCA 2014**. (ACM SIGARCH Computer Architecture News **42(3), 361–372**) | T2 | PRACtical(arXiv:2507.18581) 참고문헌 |
| **TRRespass** | Frigo, Vannacci, Hassan, van der Veen, Mutlu, Giuffrida, Bos, Razavi, "TRRespass: Exploiting the Many Sides of Target Row Refresh," **IEEE S&P 2020, pp. 747–762**. arXiv:**2004.01807** | T2 | PRACtical 참고문헌 + arXiv/ADS |
| **Blacksmith** | Jattke, van der Veen, Frigo, Gunter, Razavi, "BLACKSMITH: Scalable Rowhammering in the Frequency Domain," **IEEE S&P 2022, pp. 716–734**. DOI **10.1109/SP46214.2022.9833772** | T2 | 웹 검색(DOI 명시) |
| **Half-Double** | Kogler, Juffinger, Qazi, Kim, Lipp, Boichat, Shiu, Nissler, Gruss, "Half-Double: Hammering From the Next Row Over," **31st USENIX Security Symposium (2022), pp. 3807–3824**. https://www.usenix.org/conference/usenixsecurity22/presentation/kogler-half-double | T2 | USENIX 공식 페이지 |
| **RowPress** | Luo, Olgun, Yağlıkçı, Tuğrul, Rhyner, Bostancı, Lindegger, Sadrosadati, Mutlu, "RowPress: Amplifying Read Disturbance in Modern DRAM Chips," **ISCA 2023, pp. 1–18**. DOI **10.1145/3579371.3589063**. arXiv:**2306.17061** | T2 | ACM DL + PRACtical 참고문헌 |
| RowHammer 회고 | Mutlu, Kim, "RowHammer: A Retrospective," arXiv:**1904.09724** | T2 | arXiv |

## 2. 구조·메커니즘 서술

### 2-1. 물리적 원인
Row hammer는 하나의 워드라인(aggressor row)을 짧은 시간 안에 반복해서 activate/precharge할 때, 물리적으로 인접한 워드라인(victim row)의 셀 커패시터가 정상 리프레시 주기(tREFI 기반, 통상 64 ms 유지 창) 안에 전하를 잃어 비트가 뒤집히는 현상이다. 핵심은 **셀에 직접 접근하지 않고도 이웃 셀의 데이터를 파괴할 수 있다**는 점이며, 그래서 원 논문 제목이 "Flipping Bits in Memory **Without Accessing Them**"이다 (Kim et al., ISCA 2014, T2).

전하 손실의 물리적 경로로는 (a) 워드라인 전압이 오르내릴 때의 용량성 결합(capacitive coupling)으로 인접 셀의 패스 트랜지스터가 미세하게 열려 누설이 증가하는 것, (b) 워드라인 토글로 발생한 핫캐리어/전자가 기판을 통해 이웃 셀 저장 노드로 이동하는 것 등이 문헌에서 거론된다.
**주의: 이 (a)/(b) 물리 경로 구분은 본 조사에서 T0/T1/T2 원문으로 개별 확정하지 못했다.** 집필 시 특정 메커니즘을 단정하지 말고 "결합·누설 경로가 복합적으로 작용한다"는 수준으로 쓰거나, 별도 근거를 추가로 확보할 것.

핵심 스케일링 논리는 명확하다. 셀 간 간격이 좁아질수록 결합이 강해지고 셀 커패시턴스와 전하 여유가 줄어들어, **비트플립을 일으키는 데 필요한 activation 횟수(임계값)가 세대마다 낮아진다.** §1-A의 69.2K → 10K → 4.8K 추이가 이를 정량적으로 보여준다.

### 2-2. RowPress — row hammer와 구분해야 할 별개 현상
RowPress(Luo et al., ISCA 2023, T2)는 aggressor row를 **오래 열어 두는(keeping the row open longer)** 방식으로 read disturbance를 증폭한다. row hammer가 "얼마나 자주 여닫는가"의 문제라면 RowPress는 "얼마나 오래 열어 두는가"의 문제다. 집필 시 둘을 같은 것으로 뭉뚱그리면 안 된다.

### 2-3. 대응 기법 3세대의 계보
1. **TRR (Target Row Refresh)** — DDR4 시대. DRAM 내부(또는 일부 초기 구현에서는 컨트롤러 측 pTRR)에서 자주 activate되는 row를 **sampler**로 추적하다가, 정규 REF 명령이 들어오는 타이밍에 그 이웃 row를 몰래 추가 리프레시한다. 문제는 **벤더별 독자 구현이고 문서화되지 않았으며 sampler가 추적할 수 있는 aggressor 수가 유한**하다는 것이다. TRRespass(S&P 2020)는 sampler 용량을 넘기는 many-sided 패턴으로 이를 우회했고, 42개 DDR4 모듈 중 13개에서 비트플립을 얻었다. Blacksmith(S&P 2022)는 이를 주파수 영역 퍼징으로 자동화했고, Half-Double(USENIX Sec 2022)은 거리 2(distance-2) row까지 영향이 번지는 것을 보여 "이웃만 리프레시하면 된다"는 TRR의 전제 자체를 깼다.
2. **RFM (Refresh Management)** — DDR5/LPDDR5 시대. TRR의 실패에서 배운 결과, **호스트 컨트롤러가 책임을 분담**한다. DRAM은 bank별로 ACT 횟수를 누산하는 **RAA 카운터**를 유지하고, 컨트롤러는 RAAIMT 임계에 이르면 `RFMab`/`RFMsb` 명령을 발행해야 한다. RFM을 받으면 RAA가 RAAIMT만큼 감산되고, DRAM은 그 시간에 내부적으로 완화 리프레시를 수행한다. RAA가 벤더 지정 상한 **RAAMMT**에 닿으면 **REF/RFM으로 카운터를 낮추기 전까지 해당 bank에 ACT를 더 받지 않는다** — 이것이 강제력의 근원이다. 한계는 여전히 **집합적(aggregate) 카운팅**이라는 점: 어느 row가 몇 번 열렸는지는 모른다.
3. **PRAC (Per Row Activation Counting)** — DDR5 JESD79-5C(2024-04) 및 LPDDR6 JESD209-6(2025-07). **row 하나하나마다 카운터를 둔다.** 카운터는 추가 DRAM 셀과 센스앰프로 구현되고, precharge 시점에 read-modify-write로 갱신된다. 임계를 넘으면 DRAM이 **ABO(Alert Back-Off)** 로 호스트에 알리고, 호스트는 트래픽을 멈춘 뒤 완화용 RFM을 발행한다. 확률적·집합적 추정을 버리고 **정확한 카운트**로 옮겨간 것이 본질적 전환이다. 대가는 성능이다: 카운터 RMW 때문에 precharge 타이밍이 늘어난다(§1-E).

### 2-4. 보안 함의 (여기까지만)
비트플립은 페이지 테이블 엔트리나 권한 관련 자료구조를 겨냥하면 권한 상승으로 이어질 수 있어, row hammer는 신뢰성 문제인 동시에 보안 취약점으로 다뤄진다. 본 문서 모음집은 보안 문서가 아니므로 더 깊이 다루지 않는다.

## 3. 상충·불확실
| 쟁점 | 값 A (출처) | 값 B (출처) | 판단 |
|---|---|---|---|
| DDR3 세대 임계값 | **69.2K** — 2010–2013년 제조 칩 실측 N_RH (ABACuS/Olgun 계열, T2) | **139K–140K** (PRACtical arXiv:2507.18581은 "약 140K", 다른 2차 인용은 "139K", 또 다른 서술은 "100K 이상") | **양쪽 모두 기록할 것.** 차이의 원인은 (i) 측정 대상 칩의 제조 시기·벤더가 다르고 (ii) "첫 비트플립 기준(HC_first)"인지 "특정 비율의 셀 실패 기준"인지 정의가 다르기 때문으로 보이나, **본 조사에서 확정하지 못했다.** 하나만 골라 쓰지 말 것 |
| PRAC 평균 성능 오버헤드 | **8%** (Counterpoint, DRAMSec 2025, T2) | **6%**, 최대 약 20% (PRACtical, arXiv:2507.18581, T2) | 둘 다 T2. 워크로드 셋·시뮬레이터·가정 임계값이 달라 직접 비교 불가. **"논문에 따라 6–8% 수준으로 보고된다"** 식으로 범위 서술 권장 |
| PRAC 오버헤드의 속도 의존 | 3200 MT/s에서 2.2% | 8000 MT/s에서 14% | 상충이 아니라 **같은 논문 내 조건 차이**로 보이나 **출처 논문을 특정하지 못했다.** 인용 시 "출처 미특정" 표기 필수 |
| PRAC 적용 시 코어 타이밍 | tRP 15 ns → **36 ns** (PRACtical Table 1 추출값) | 같은 추출에서 tRAS 32→16 ns, tRC 47→52 ns 도 함께 나왔는데 **tRC = tRAS + tRP 관계가 성립하지 않아 산술적으로 모순** | **tRP 15→36 ns만 조건부로 사용하고, tRAS/tRC 값은 사용 금지.** PDF 텍스트 추출 오류 가능성이 높다. 원문 Table 1 재확인 필요 |
| LPDDR6 PRAC "LPDDR5X 대비 5배" | 기술 매체(T3) 다수가 동일 문구를 반복 | 원 논문·JEDEC 원문 미확인 | **단일 계열 출처. 수치로 인용하지 말고 정성 서술로 낮출 것** 권장 |

## 4. 확인 실패 항목

1. **DDR4 MAC 값 인코딩 표(200K/300K/400K/500K/600K/700K/Unlimited/Untested)의 T0 원문 확인 실패.**
   - 로컬 `jesd79_4.txt`는 2012년 9월 원판이라 MAC 조항이 없다(직접 확인).
   - MAC은 DDR4 **SPD Annex L byte 41**("SDRAM Maximum Active Count (MAC) Value")에 있다는 것까지는 확인했으나(JEDEC 문서 목록 SPD4.1.2.L), **JEDEC 원문이 로그인 벽 뒤라 값 표를 확인하지 못했다.**
   - 어느 모듈이 "pTRR 지원, MAW 64 ms, MAC 400K"로 보고한다는 사례를 메일링 리스트에서 봤으나 **T4급이라 수치 인용 금지.**
   - → **집필 시 구체적 MAC 값 목록을 쓰지 말 것.** 쓰려면 JESD79-4B/SPD Annex L 원문을 별도 입수해야 한다.
2. **DDR5 세대의 실측 rowhammer 임계값 확인 실패.** on-die ECC와 내장 완화 로직 때문에 외부 관측이 어렵다는 서술만 확보(DRAM-Profiler, arXiv:2404.18396, T2). **"DDR5는 N천 회"류 수치를 쓰지 말 것.**
3. **JESD79-5C 원문(T0) 직접 확인 실패.** JEDEC 보도자료 페이지가 HTTP 403, businesswire 미러도 연결 실패. PRAC 관련 T0 근거는 **보도자료를 인용한 T3 매체 경유**로만 확보했다. 조항 번호·MR 비트·정확한 임계 설정 방식은 미확인.
4. **JESD209-6(LPDDR6) 원문(T0) 직접 확인 실패.** LPDDR6의 per-row activation counting이 rowhammer 대응이라는 것은 다수 T3 매체가 일치하나, **JEDEC 원문 문구는 확보하지 못했다.**
5. **RFM의 RAAIMT 32–80(8 단위)·RAAMMT(MR58 opcode 7:5) 값의 T0 확인 실패.** 2차 해설 문헌 경유. JESD79-5B 원문 대조 필요.
6. **arXiv/vusec PDF 직접 파싱 실패**(QPRAC 2501.18861, TRRespass PDF): PDF 스트림이 텍스트로 변환되지 않았다. 해당 논문 수치는 HTML판·검색 요약·교차 인용으로 보완했으며, **verbatim 인용은 하지 않았다.**
7. **삼성/SK하이닉스/마이크론의 벤더별 TRR 구현 세부**(T1 공식 문서) 확인 실패. 벤더들이 공개하지 않는다.
8. **row hammer의 지배적 물리 메커니즘 확정 실패** (§2-1 (a)/(b)).
9. **PRAC의 실제 양산 적용 여부(2026년 시점)** 확인 실패 — 어느 벤더의 어느 제품이 PRAC을 실제로 탑재했는지 T1 근거를 찾지 못했다. **"DDR5가 PRAC을 쓴다"고 단정하지 말 것.** JESD79-5C는 사양이지 탑재 현황이 아니다.

## 5. 기존 소스 팩(v3)과의 충돌
**충돌 없음.**
기존 `C:\Users\MSI\Desktop\내 폴더\코딩\기획\RAM\RAM-source-pack.md`에서 row hammer 관련 서술은 146행 단 한 줄이며, 수치가 없다:
> "…센스앰프 트랜지스터 구조 변경(SK하이닉스는 recessed channel 채택), 게이트 워크펑션 엔지니어링, HKMG, row-hammer 대응이 병행됩니다."

**연결 가능한 공백(중요):** 소스 팩 3-2절에 LPDDR6 스펙 항목으로만 적혀 있던 **"per-row activation tracking"은 PRAC이며 row hammer 대응이 맞다**(§1-C, T3 다수 일치). 즉 소스 팩의 146행(공정 미세화에 따른 row-hammer 대응)과 3-2절(LPDDR6 스펙 항목)은 **같은 주제의 앞뒤**다. 다만 **JEDEC 원문(T0) 확인은 못 했으므로**, 본문에서 연결할 때 등급을 T3로 밝히거나 "업계 보도 기준"이라고 단서를 달아야 한다.

## 6. 집필 시 주의 (서술 규칙 제안)

1. **로컬 `jesd79_5.txt`를 RFM/PRAC 근거로 인용하지 말 것.** Rev0.1 위원회 회람본이며 RFM·PRAC·rowhammer 문자열이 하나도 없다. 이 파일을 "DDR5 표준"이라고만 표기하면 독자를 오도한다. 인용 시 반드시 "**DDR5 Full Spec Draft Rev0.1, JC42.3 위원회 회람본**"이라고 판본을 명시할 것.
2. **로컬 `jesd79_4.txt`도 2012년 9월 원판**이다. MAC/TRR 근거로 쓸 수 없다.
3. **MAC과 HC_first를 섞지 말 것.** MAC은 JEDEC이 정의한 *스펙상 보장 한도*, HC_first/N_RH는 *논문의 실측 값*이다. "MAC이 4.8K로 떨어졌다"는 틀린 문장이다.
4. **임계값에는 반드시 "제조 시기"와 "규격"을 붙일 것.** 4.8K는 **LPDDR4, 2019–2020년 제조 칩**의 실측 최소값이지 "요즘 DRAM 일반"이 아니다. 10K는 **DDR4, 2019–2020년 제조 칩**이다.
5. **DDR3 임계값은 단일 수치로 쓰지 말 것.** 69.2K와 139K–140K가 병존한다(§3). "수만–십수만 회 수준"이라고 범위로 쓰거나 두 값을 병기할 것.
6. **DDR5 임계값은 쓰지 말 것.** 확인 실패다(§4-2).
7. **"JESD79-5C가 PRAC을 도입했다"와 "DDR5 제품이 PRAC을 쓴다"는 다른 문장이다.** 전자만 근거가 있다.
8. **PRAC 오버헤드는 범위로.** "6–8%(논문·워크로드에 따라 다름, 최대 20%대 사례 보고)"가 안전하다. 단일 수치 확정 서술 금지.
9. **TRR을 "실패한 기술"로 단정하는 것은 과하다.** TRRespass가 보인 것은 "42개 중 13개 모듈에서 우회 가능"이지 "TRR이 무용지물"이 아니다. 수치를 정확히 인용할 것.
10. **row hammer와 RowPress를 구분할 것**(§2-2).
11. **보안 서술은 한두 문장으로 제한.** 이 문서 모음집의 목적이 아니다.
12. **PRAC의 tRAS/tRC 변화 수치는 사용 금지**(§3, 산술 모순).

## 7. 출처 목록
| 출처 | 등급 | 제목 | 확인일 |
|---|---|---|---|
| 로컬 `jesd79_5.txt` | T0(**초안**) | JEDEC JC42.3 Committee Letter Ballot, "DDR5 Full Spec Draft Rev0.1" — RFM/PRAC/hammer 조항 **부재** | 2026-07-29 |
| 로컬 `jesd79_4.txt` | T0 | JEDEC STANDARD DDR4 SDRAM, JESD79-4, **September 2012 원판** — MAC/TRR 조항 **부재** | 2026-07-29 |
| 로컬 `RAM-source-pack.md` | — | 기존 소스 팩 v3 (146행에 row-hammer 한 줄) | 2026-07-29 |
| https://www.jedec.org/news/pressreleases/jedec-updates-jesd79-5c-ddr5-sdram-standard-elevating-performance-and-security | T0 | JEDEC 보도자료, "JEDEC Updates JESD79-5C DDR5 SDRAM Standard" (2024-04-17). **직접 fetch는 HTTP 403 — 내용은 T3 매체 경유로만 확보** | 2026-07-29 |
| https://www.storagenewsletter.com/2024/04/22/jedec-published-jesd79-5c-ddr5-sdram-standard/ | T3 | JESD79-5C 공표 보도 | 2026-07-29 |
| https://www.storagenewsletter.com/2025/07/10/jedec-published-jesd209-6-lpddr6-standard-to-enhance-mobile-and-ai-memory-performance/ | T3 | JESD209-6 (LPDDR6) 공표 보도 | 2026-07-29 |
| https://www.microcontrollertips.com/what-is-jesd209-6-and-why-is-it-important-for-edge-ai/ · https://www.eeworldonline.com/what-is-jesd209-6-and-why-is-it-important-for-edge-ai/ | T3 | LPDDR6 PRAC = rowhammer 대응임을 설명 | 2026-07-29 |
| https://www.ttieurope.com/content/ttieurope/en/resources/marketeye/categories/new-technology/me-slovick-20250728.html | T3 | LPDDR6 표준 해설 | 2026-07-29 |
| https://download.vusec.net/papers/trrespass_sp20.pdf (arXiv:2004.01807) | T2 | Frigo et al., "TRRespass: Exploiting the Many Sides of Target Row Refresh," IEEE S&P 2020, pp.747–762. **PDF 파싱 실패 → 검색 요약·교차 인용으로 확보** | 2026-07-29 |
| DOI 10.1109/SP46214.2022.9833772 | T2 | Jattke et al., "BLACKSMITH: Scalable Rowhammering in the Frequency Domain," IEEE S&P 2022, pp.716–734 | 2026-07-29 |
| https://www.usenix.org/conference/usenixsecurity22/presentation/kogler-half-double | T2 | Kogler et al., "Half-Double: Hammering From the Next Row Over," USENIX Security 2022, pp.3807–3824 | 2026-07-29 |
| DOI 10.1145/3579371.3589063 (arXiv:2306.17061) | T2 | Luo et al., "RowPress: Amplifying Read Disturbance in Modern DRAM Chips," ISCA 2023 | 2026-07-29 |
| ISCA 2014 / SIGARCH Comput. Archit. News 42(3):361–372 | T2 | Kim et al., "Flipping Bits in Memory Without Accessing Them" (최초 보고) | 2026-07-29 |
| https://www.usenix.org/system/files/sec23winter-prepub-21-olgun.pdf | T2 | Olgun et al., "ABACuS: All-Bank Activation Counters…," USENIX Security 2024 — 69.2K/10K/4.8K 임계 추이 | 2026-07-29 |
| https://arxiv.org/pdf/2404.18396 | T2 | DRAM-Profiler — DDR3 –100K, DDR4 4.8K, DDR5 평가 곤란 서술 | 2026-07-29 |
| https://arxiv.org/html/2507.18581 | T2 | PRACtical — PRAC 동작·ABO 타이밍·오버헤드 6%(최대 –20%)·tRP 15→36 ns | 2026-07-29 |
| https://dramsec.ethz.ch/dramsec25-papers/counterpoint-dramsec25.pdf | T2 | Counterpoint (DRAMSec 2025) — PRAC 8%, PRAC-Ideal 0.9% | 2026-07-29 |
| https://arxiv.org/pdf/2501.18861 | T2 | QPRAC — PRAC 카운터+ABO 구조, QPRAC 계열 오버헤드. **PDF 파싱 실패, 검색 요약 경유** | 2026-07-29 |
| https://ar5iv.labs.arxiv.org/html/2501.06646 | T2 | RogueRFM — RFM을 이용한 covert-channel/DoS | 2026-07-29 |
| https://comsec.ethz.ch/wp-content/files/protrr_sp22.pdf | T2 | PROTRR: Principled yet Optimal In-DRAM Target Row Refresh, IEEE S&P 2022 | 2026-07-29 |
| https://arxiv.org/pdf/1904.09724 | T2 | Mutlu & Kim, "RowHammer: A Retrospective" | 2026-07-29 |
| https://www.jedec.org/standards-documents/docs/spd412l-4 | T0 | SPD Annex L for DDR4 (byte 41 = MAC). **로그인 벽 — 값 표 미확인** | 2026-07-29 |
