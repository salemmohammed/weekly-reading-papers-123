
# Awesome Asynchronous BFT Consensus

A reading list of important research papers on **fully asynchronous Byzantine Fault Tolerant (BFT) consensus**, Byzantine agreement, and atomic broadcast.

The collection emphasizes foundational algorithms, practical protocols, implementation design choices, and experimental performance evaluation.

## Scope

This list focuses on **permissioned, fully asynchronous Byzantine agreement and atomic broadcast**.

Included topics:
- Randomized Byzantine agreement (ABA)
- Reliable and verifiable broadcast (RBC / VCBC)
- Asynchronous Common Subset (ACS)
- Multivalue Validated Byzantine Agreement (MVBA)
- Common coins and threshold cryptography
- Asynchronous atomic broadcast
- Performance evaluation and benchmarking

**Excluded:** DAG-based consensus, partially synchronous BFT, synchronous BFT, and hybrid protocols using synchronous fast paths.

This is a selected papers, not an exhaustive index.

---

## 1. Must-Read Papers

| Year | Paper | Venue | Main Contribution |
|---|---|---|---|
| 2016 | [HoneyBadgerBFT](https://doi.org/10.1145/2976749.2978399) | **CCS** | Practical asynchronous atomic broadcast using ACS, RBC, ABA, batching, and threshold encryption. |
| 2018 | [BEAT](https://doi.org/10.1145/3243734.3243812) | **CCS** | Five practical asynchronous BFT protocols exploring performance and design trade-offs. |
| 2020 | [Dumbo](https://doi.org/10.1145/3372297.3417262) | **CCS** | Reduces the number of expensive asynchronous agreement instances. |
| 2022 | [Speeding Dumbo](https://doi.org/10.14722/ndss.2022.24385) | **NDSS** | Efficient broadcast and MVBA to reduce communication and agreement latency. |
| 2022 | [DispersedLedger](https://www.usenix.org/system/files/nsdi22-paper-yang_lei.pdf) | **NSDI** | Data dispersal and asynchronous ordering for heterogeneous bandwidth environments. |
| 2022 | [Dumbo-NG](https://doi.org/10.1145/3548606.3559379) | **CCS** | Separates transaction dissemination from agreement to improve throughput and latency. |
| 2023 | [WaterBear](https://www.usenix.org/system/files/usenixsecurity23-zhang-haibin.pdf) | **USENIX Security** | Local-coin-based asynchronous BFT and improved binary agreement mechanisms. |
| 2024 | [Alea-BFT](https://www.usenix.org/system/files/nsdi24-antunes.pdf) | **NSDI** | Pipelined VCBC and one ABA instance per round with rotating proposal selection. |
| 2025 | [TockOwl](https://www.usenix.org/conference/usenixsecurity25/presentation/li-minghang) | **USENIX Security** | Fault-adaptive asynchronous consensus with resilience to crash failures. |

---

## 2. Foundational Theory

| Year | Paper | Contribution |
|---|---|---|
| 1983 | [Another Advantage of Free Choice — Ben-Or](https://doi.org/10.1145/800221.806707) | Foundational randomized asynchronous agreement. |
| 1984 | An Asynchronous [(n−1)/3]-Resilient Consensus Protocol — Bracha and Toueg | Asynchronous Byzantine agreement under the one-third fault threshold. |
| 1985 | [Impossibility of Distributed Consensus with One Faulty Process — FLP](https://doi.org/10.1145/3149.214121) | Establishes deterministic consensus termination impossibility in a fully asynchronous system with a possible crash. |
| 1985 | Asynchronous Consensus and Broadcast Protocols — Bracha and Toueg | Foundational consensus and broadcast techniques. |
| 1993 | [Random Oracles Are Practical — Bellare and Rogaway](https://doi.org/10.1145/168588.168596) | Cryptographic background relevant to randomized cryptographic constructions. |

### Important Building Blocks

1. Asynchronous Binary Agreement (ABA)
2. Reliable Broadcast (RBC)
3. Verifiable Consistent Broadcast (VCBC)
4. Asynchronous Common Subset (ACS)
5. Multivalue Validated Byzantine Agreement (MVBA)
6. Common Coin
7. Threshold Signatures
8. Threshold Encryption
9. Erasure Coding
10. Atomic Broadcast

---

## 3. Research Timeline

```text
1983  Ben-Or randomized agreement
  |
1984  Bracha–Toueg asynchronous agreement
  |
1985  FLP impossibility
  |
  v
2016  HoneyBadgerBFT (CCS)
  |
2018  BEAT (CCS)
  |
2020  Dumbo (CCS)
  |
2022  Speeding Dumbo (NDSS)
      DispersedLedger (NSDI)
      Dumbo-NG (CCS)
  |
2023  WaterBear (USENIX Security)
  |
2024  Alea-BFT (NSDI)
  |
2025  TockOwl (USENIX Security)
```

---

## 4. Protocol Design Choices

| Protocol | Broadcast / Dissemination | Agreement | Main Optimization |
|---|---|---|---|
| HoneyBadgerBFT | RBC | ACS with multiple ABAs | Threshold encryption and batching |
| BEAT | Multiple broadcast and storage designs | Asynchronous agreement variants | Communication, storage, and cryptographic trade-offs |
| Dumbo | RBC and optimized proposal selection | Reduced ABA / MVBA overhead | Agreement efficiency |
| Speeding Dumbo | Cheaper provable broadcast | Optimized MVBA | Communication and latency |
| DispersedLedger | Data dispersal | Asynchronous agreement | Bandwidth heterogeneity |
| Dumbo-NG | Continuous dissemination | Concurrent ordering | Throughput and latency decoupling |
| WaterBear | Protocol-dependent dissemination | Local-coin ABA / RABA | Agreement and security properties |
| Alea-BFT | VCBC | One ABA per round | Pipelined execution |
| TockOwl | Protocol-specific dissemination | Fault-adaptive asynchronous agreement | Resilience to crash faults |

---

## 5. Surveys and Literature Reviews

| Year | Survey | Venue | Focus |
|---|---|---|---|
| 2024 | [A Review of Asynchronous Byzantine Consensus Protocols](https://doi.org/10.3390/s24247927) | Sensors | Asynchronous BFT taxonomy, design mechanisms, and protocol comparison. |
| 2024 | [Reaching Consensus in the Byzantine Empire](https://doi.org/10.1145/3636553) | ACM Computing Surveys | Broad Byzantine consensus taxonomy, complexity, and designs. |
| 2023 | [A Survey of Blockchain Consensus Protocols](https://doi.org/10.1145/3579845) | ACM Computing Surveys | Broad blockchain consensus background. |

**Recommended survey:** A Review of Asynchronous Byzantine Consensus Protocols (2024).

Note: These surveys can discuss DAG and partially synchronous protocols, but only their relevant fully asynchronous, non-DAG material is within this bibliography's scope.

---

## 6. Experimental Evaluation and Benchmarking

The following are important references for developing reproducible evaluations of asynchronous BFT.

| Year | Paper | Type | Why It Matters |
|---|---|---|---|
| 2016 | [BFT-Bench](https://research.spec.org/icpe_proceedings/2016/proceedings/p109.pdf) | Benchmark framework | Fault injection and performance measurement. |
| 2017 | [BLOCKBENCH](https://doi.org/10.1145/3035918.3064033) | Benchmark framework | Repeatable blockchain benchmarking methodology. |
| 2018 | [BEAT](https://doi.org/10.1145/3243734.3243812) | Protocol evaluation | Modular comparison of asynchronous design choices. |
| 2022 | [Speeding Dumbo](https://doi.org/10.14722/ndss.2022.24385) | Protocol evaluation | Component-level broadcast and MVBA benchmarks. |
| 2022 | [DispersedLedger](https://www.usenix.org/system/files/nsdi22-paper-yang_lei.pdf) | Protocol evaluation | Effects of heterogeneous bandwidth. |
| 2022 | [Dumbo-NG](https://doi.org/10.1145/3548606.3559379) | Protocol evaluation | Throughput, latency, and scalability trade-offs. |
| 2023 | [WaterBear](https://www.usenix.org/system/files/usenixsecurity23-zhang-haibin.pdf) | Protocol evaluation | Local-coin agreement and performance trade-offs. |
| 2024 | [Alea-BFT](https://www.usenix.org/system/files/nsdi24-antunes.pdf) | Protocol evaluation | Common-framework comparison, pipelining, and fault performance. |
| 2025 | [TockOwl](https://www.usenix.org/conference/usenixsecurity25/presentation/li-minghang) | Protocol evaluation | Crash faults and adaptive agreement performance. |

**Note:** BFT-Bench and BLOCKBENCH are general benchmarking references, not asynchronous BFT protocols.

---

## 7. Research Direction: Evaluating Asynchronous BFT with PaxiBFT

**Working title:**

*Dissecting Asynchronous Byzantine Fault Tolerance: An Experimental Evaluation of Protocol Design Choices*

**Framework:** [PaxiBFT](https://github.com/salemmohammed/PaxiBFT)

### Objective

Implement selected asynchronous BFT protocols within a common experimental framework and systematically evaluate the effects of protocol and implementation design choices.

### Candidate Protocols

1. HoneyBadgerBFT
2. BEAT
3. Dumbo
4. Speeding Dumbo
5. Dumbo-NG
6. Alea-BFT
7. WaterBear
8. TockOwl

These are research candidates, not claims that the protocols are already implemented in PaxiBFT.

### Design Choices to Evaluate

| Category | Design Choice | Metrics |
|---|---|---|
| Agreement | ABA, ACS, MVBA | Latency, rounds, communication |
| Broadcast | RBC, VCBC, provable broadcast | Bytes, CPU, delivery time |
| Cryptography | Signatures, threshold coins, encryption | CPU, cryptographic latency |
| Batching | Batch sizes and adaptive batching | Throughput, latency |
| Pipelining | Sequential vs. concurrent operations | Latency, throughput |
| Networking | Transport and serialization | CPU, bandwidth, latency |
| Concurrency | Parallel agreement and worker scheduling | CPU, scalability |
| Faults | Crash, omission, Byzantine behavior | Progress, latency, resource use |
| Deployment | LAN, WAN, variable bandwidth | Scalability, performance |
| Resources | Memory, CPU, queue growth | Utilization, bottlenecks |

Protocol variants must preserve their stated correctness assumptions; not every component is interchangeable.

### Main Research Questions

- RQ1: Which components dominate the cost of asynchronous BFT?
- RQ2: How do different broadcast mechanisms affect scalability?
- RQ3: What is the performance cost of common coins and threshold cryptography?
- RQ4: How does concurrent dissemination affect latency and throughput?
- RQ5: How do protocols respond to heterogeneous network conditions?
- RQ6: How do crash and Byzantine faults affect progress?
- RQ7: Which implementation choices most strongly affect performance?
- RQ8: Which design choices offer the best trade-offs under different workloads?

---

## 8. Recommended Reading Order

1. **FLP** — Understand why randomization is necessary.
2. **Bracha and Toueg** — Understand asynchronous agreement and broadcast.
3. **HoneyBadgerBFT** — Understand ACS-based atomic broadcast.
4. **BEAT** — Understand modular design trade-offs.
5. **Dumbo** — Understand agreement optimization.
6. **Speeding Dumbo** — Understand broadcast and MVBA bottlenecks.
7. **DispersedLedger** — Understand bandwidth heterogeneity.
8. **Dumbo-NG** — Understand concurrent dissemination and ordering.
9. **WaterBear** — Understand local coins and alternative agreement constructions.
10. **Alea-BFT** — Understand practical pipelining and streamlined agreement.
11. **TockOwl** — Understand fault-adaptive asynchronous consensus.

---

## Contributing

Contributions are welcome for peer-reviewed, fully asynchronous, non-DAG Byzantine agreement and atomic broadcast research.

Each addition should include:
- Title and authors
- Publication year and venue
- Stable paper URL
- Network and fault model
- Main contribution
- Evaluation methodology
- Source code, if available

Avoid comparing performance numbers from different papers without accounting for their experimental environments.

---

*This is a curated and evolving research bibliography, not an exhaustive systematic review.*
