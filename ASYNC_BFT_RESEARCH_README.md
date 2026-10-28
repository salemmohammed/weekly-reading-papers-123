# Awesome Asynchronous BFT Consensus 📚

> A curated, chronological reading list of **asynchronous Byzantine fault-tolerant (BFT) consensus**, major surveys, and experimental evaluation papers. **Updated: October 2026.**

**Scope.** Emphasis is on permissioned asynchronous Byzantine agreement and atomic broadcast, with DAG protocols and hybrid/partially synchronous designs included for comparison. This is a **selected bibliography**, not an exhaustive index of every paper.

## Contents

- [Start here](#start-here)
- [Key terminology](#key-terminology)
- [Research timeline](#research-timeline)
- [Protocol papers](#protocol-papers)
- [DAG-based and hybrid research](#dag-based-and-hybrid-research)
- [High-quality surveys](#high-quality-surveys)
- [Benchmarking and evaluation](#benchmarking-and-evaluation)
- [Open-source implementations](#open-source-implementations)
- [Suggested comparative research](#suggested-comparative-research)

## Start here

| Recommendation | Paper | Why read it? |
|---|---|---|
| **Foundational practical asynchronous BFT** | [HoneyBadgerBFT (CCS 2016)](https://doi.org/10.1145/2976749.2978399) | Introduced a practical asynchronous atomic broadcast design. |
| **High-throughput asynchronous BFT** | [Dumbo-NG (CCS 2022)](https://doi.org/10.1145/3548606.3559379) | Concurrent dissemination and ordering; throughput/latency tradeoffs. |
| **DAG-based architecture** | [Narwhal and Tusk (EuroSys 2022)](https://arxiv.org/abs/2105.11827) | Separates data dissemination from consensus ordering. |
| **Adaptation to faults and networks** | [TockOwl / TockOwl+ (USENIX Security 2025)](https://www.usenix.org/conference/usenixsecurity25/presentation/li-minghang) | Adaptive performance under crash faults and different network conditions. |
| **Focused survey** | [A Review of Asynchronous Byzantine Consensus Protocols (Sensors 2024)](https://doi.org/10.3390/s24247927) | ACS- versus DAG-based taxonomy. |
| **Broad, high-profile BFT survey** | [Reaching Consensus in the Byzantine Empire (ACM CSUR 2024)](https://doi.org/10.1145/3636553) | Algorithm-level comparison, complexity and protocol figures. |

## Key terminology

- **Asynchronous:** No fixed upper bound on message delays is required by the network model. Termination of randomized asynchronous consensus can be probabilistic.
- **Partially synchronous:** Liveness relies on eventual timing assumptions. **PBFT and HotStuff are not fully asynchronous liveness baselines.**
- **ACS:** Asynchronous Common Subset, used in HoneyBadger-style atomic broadcast.
- **DAG:** Directed acyclic graph of proposals/certificates or events; DAG membership and ordering can be separated.
- **Hybrid / fast-path:** A protocol can use a fast mode under favorable conditions and fall back to an asynchronous mode. Check the exact guarantees of each component.

## Research timeline

```text
1983–1988  Randomized consensus, FLP, asynchronous Byzantine agreement,
           and partial synchrony foundations
    |
2016       HoneyBadgerBFT
    |
2018       BEAT
    |
2020       Dumbo
    |
2021       DAG-Rider
    |
2022       Speeding Dumbo / DispersedLedger / Dumbo-NG
           Narwhal & Tusk / Bullshark / Bolt-Dumbo Transformer
    |
2023       ParBFT / WaterBear / further DAG systems
    |
2024       Mysticeti / Mahi-Mahi / modern DAG refinements
    |
2025       TockOwl and TockOwl+ (fault/network adaptation)
    |
2026       AionBFT (Blockchain: Research and Applications) / TD (Future Internet)
```

### Foundational theory

| Year | Paper | Why it matters |
|---|---|---|
| 1983 | [Another Advantage of Free Choice — Ben-Or](https://doi.org/10.1145/800221.806707) | Randomized agreement. |
| 1985 | [Impossibility of Distributed Consensus with One Faulty Process — Fischer, Lynch, Paterson](https://doi.org/10.1145/3149.214121) | FLP impossibility: deterministic consensus cannot guarantee termination in a fully asynchronous setting with even one crash. |
| 1984 | *An Asynchronous [(n−1)/3]-Resilient Consensus Protocol* — Bracha and Toueg | Fundamental Byzantine asynchronous agreement. |
| 1985 | *Asynchronous Consensus and Broadcast Protocols* — Bracha and Toueg | Consensus and broadcast building blocks. |
| 1988 | *Consensus in the Presence of Partial Synchrony* — Dwork, Lynch, Stockmeyer | Distinguishes partial synchrony from full asynchrony. |
| 1996 | *Unreliable Failure Detectors for Reliable Distributed Systems* — Chandra and Toueg | Failure-detector perspective on consensus. |

## Protocol papers

### ACS-based and related practical asynchronous BFT

| Year | Paper | Venue | Main idea |
|---|---|---|---|
| 2016 | [The Honey Badger of BFT Protocols](https://doi.org/10.1145/2976749.2978399) | ACM CCS | Practical asynchronous atomic broadcast using ACS, threshold encryption, and batching. |
| 2018 | [BEAT: Asynchronous BFT Made Practical](https://dl.acm.org/doi/10.1145/3243734.3243812) | ACM CCS | More practical asynchronous BFT variants. |
| 2020 | [Dumbo: Faster Asynchronous BFT Protocols](https://eprint.iacr.org/2020/841) | ACM CCS | More efficient asynchronous agreement, including Dumbo variants. |
| 2022 | [Speeding Dumbo: Pushing Asynchronous BFT Closer to Practice](https://www.ndss-symposium.org/ndss-paper/auto-draft-256/) | NDSS | Reduced latency and agreement overhead. |
| 2022 | [DispersedLedger](https://www.usenix.org/system/files/nsdi22-paper-yang_lei.pdf) | USENIX NSDI | Separates data dispersal from agreement, tolerating bandwidth heterogeneity. |
| 2022 | [Dumbo-NG: Fast Asynchronous BFT Consensus with Throughput-Oblivious Latency](https://doi.org/10.1145/3548606.3559379) | ACM CCS | Concurrent transaction dissemination and ordering. |
| 2022 | *Bolt-Dumbo Transformer* | ACM CCS | Optimistic fast path and asynchronous fallback. |
| 2023 | *ParBFT: Faster Asynchronous BFT Consensus with a Parallel Optimistic Path* | ACM CCS | Parallel optimistic execution. |
| 2023 | [WaterBear](https://www.usenix.org/system/files/usenixsecurity23-zhang-haibin.pdf) | USENIX Security | New asynchronous BFT paradigm and security/performance improvements. |
| 2025 | [TockOwl: Asynchronous Consensus with Fault and Network Adaptability](https://www.usenix.org/conference/usenixsecurity25/presentation/li-minghang) | USENIX Security | Fault-adaptive TockOwl and network-adaptive TockOwl+. |
| 2026 | [AionBFT: High-Throughput Asynchronous BFT Consensus with Even Faster Confirmation](https://doi.org/10.1016/j.bcra.2026.100467) | Blockchain: Research and Applications | Network-aware fast path with fully asynchronous fallback. |
| 2026 | [TD: Faster Asynchronous BFT Protocol Minimizing Throughput–Latency Tension](https://www.mdpi.com/1999-5903/18/9/460) | Future Internet | Throughput–latency optimization. |

> **Warning:** A paper's claimed speedup is based on its own experimental settings. Do not combine throughput/latency figures from different papers as if they came from the same testbed.

## DAG-based and hybrid research

Not all papers here prove liveness under the same *fully asynchronous* model; classify network assumptions individually before making comparisons.

| Year | Paper | Venue / type | Main idea |
|---|---|---|---|
| 2021 | [DAG-Rider: All You Need Is DAG](https://arxiv.org/abs/2102.08325) | ACM PODC | DAG-based asynchronous atomic broadcast. |
| 2022 | [Narwhal and Tusk: A DAG-based Mempool and Efficient BFT Consensus](https://arxiv.org/abs/2105.11827) | ACM EuroSys | Separate mempool dissemination from ordering. |
| 2022 | [Bullshark: DAG BFT Protocols Made Practical](https://arxiv.org/abs/2201.05677) | ACM CCS | Efficient DAG-based ordering, including an asynchronous design. |
| 2023 | *Cordial Miners* | Research paper | DAG-based ordering. |
| 2023 | *Shoal* | Research work | Leader performance for DAG designs. |
| 2024 | [Mysticeti: Reaching the Limits of Latency with Uncertified DAGs](https://arxiv.org/abs/2310.14821) | Research publication | Low-latency DAG design; review exact synchrony assumptions. |
| 2024 | *Mahi-Mahi* | Research work | DAG ordering refinements. |

## High-quality surveys

**Venue prestige and scope are separate considerations:** ACM Computing Surveys is well suited to broad related-work reviews, while the Sensors article is more directly targeted to asynchronous BFT.

| Year | Survey | Venue | Use |
|---|---|---|---|
| 2023 | [A Survey of Blockchain Consensus Protocols](https://doi.org/10.1145/3579845) | **ACM Computing Surveys** | Blockchain consensus background and taxonomy. |
| 2024 | [Reaching Consensus in the Byzantine Empire: A Comprehensive Review of BFT Consensus Algorithms](https://doi.org/10.1145/3636553) | **ACM Computing Surveys** | Broad BFT protocol comparison and message/time complexity. |
| 2024 | [A Review of Asynchronous Byzantine Consensus Protocols](https://doi.org/10.3390/s24247927) | **Sensors** | Direct focus on ACS- and DAG-based asynchronous protocols. |

## Benchmarking and evaluation

Dedicated evaluation frameworks are distinguished from **protocol papers that include benchmark experiments**.

| Year | Paper or artifact | Type | Why it is useful |
|---|---|---|---|
| 2016 | [BFT-Bench: A Framework to Evaluate BFT Protocols](https://research.spec.org/icpe_proceedings/2016/proceedings/p109.pdf) | **Benchmark framework**, ICPE work-in-progress | Fault injection, metrics, and repeatable testing scenarios; not exclusive to asynchronous protocols. |
| 2017 | [BLOCKBENCH: A Framework for Analyzing Private Blockchains](https://doi.org/10.1145/3035918.3064033) | **Benchmark framework**, SIGMOD | System-level blockchain performance benchmarking. |
| 2022 | [DispersedLedger](https://www.usenix.org/system/files/nsdi22-paper-yang_lei.pdf) | **Protocol evaluation**, NSDI | Performance under bandwidth heterogeneity and geo-distribution. |
| 2022 | [Dumbo-NG](https://doi.org/10.1145/3548606.3559379) | **Protocol evaluation**, CCS | Throughput–latency tradeoffs and comparisons against asynchronous baselines. |
| 2025 | [TockOwl](https://www.usenix.org/conference/usenixsecurity25/presentation/li-minghang) | **Protocol evaluation**, USENIX Security | Crash faults, fast/slow tracks, and network variability. |
| 2025 | [Asynchronous BFT Consensus Made Wireless](https://arxiv.org/abs/2503.21279) | **Preprint + implementation** | Wireless constraints and batching effects. |
| 2026 | [TD](https://www.mdpi.com/1999-5903/18/9/460) | **Protocol evaluation**, Future Internet | Throughput/latency tradeoffs across scales. |

### Evaluation checklist

- [ ] Same hardware, operating systems, and CPU allocations
- [ ] Same number of replicas and Byzantine-fault threshold
- [ ] Transaction payload size, batching, and workload arrival rate
- [ ] LAN vs. WAN, injected RTT, jitter, bandwidth, loss and asymmetry
- [ ] Throughput in committed **transactions/second**
- [ ] End-to-end latency p50, p95, p99 (define start/end timestamps)
- [ ] Communication bytes/transaction and messages/decision
- [ ] CPU, memory, and cryptographic overhead
- [ ] Crash, Byzantine, and network-degradation scenarios
- [ ] Recovery time and effect of changing conditions
- [ ] Repeatability: code revisions, configs, seeds, traces, confidence intervals

## Open-source implementations

- [TockOwl experimental repository](https://github.com/yrdsm666/tockowl) — includes TockOwl, TockOwl+, TockCat, BKR, Speeding-Dumbo, ParBFT and Dumbo-NG implementations in a common codebase. Useful for fairer experiments, subject to configuration equivalence.
- [ConsensusBatcher](https://github.com/ConsensusBatcher/ConsensusBatcher) — HoneyBadger, BEAT and Dumbo variants for wireless networks.

> Open-source availability does not imply maintained, production-ready, or directly comparable implementations. Audit licensing, dependencies, commits, and experiment configurations.

## Suggested comparative research

**Working question:** *How do asynchronous BFT protocols respond to variable delay, asymmetric bandwidth, crash faults, and changing workload, and when does adaptive selection improve performance?*

**Initial comparison set:**

1. HoneyBadgerBFT — foundational ACS baseline.
2. Dumbo — improved agreement.
3. DispersedLedger — bandwidth heterogeneity.
4. Dumbo-NG — concurrent dissemination and consensus.
5. Bullshark / Tusk — DAG-based architecture (with explicit network-model caveats).
6. TockOwl+ — fault/network adaptability.

**Potential extension:** A situation-aware experimental controller that *measures* RTT, latency distribution, throughput, backlog, CPU, and replica failures. Compare fixed implementations first; only consider switching consensus mechanisms after a rigorous argument that safety, state transfer, and quorum-intersection invariants are preserved.

### Recommended reading order

`FLP → Bracha/Toueg → HoneyBadger → Dumbo → DispersedLedger → Dumbo-NG → Narwhal/Tusk → Bullshark → TockOwl`

---

### Contributing

PRs welcome for papers with **title, authors, year, peer-reviewed venue or preprint status, stable URL/DOI, network model, primary contribution, and code link**. Avoid unqualified “best performance” claims across unrelated benchmarks.

*This is a living research bibliography, not a systematic review or an exhaustive inventory.*
