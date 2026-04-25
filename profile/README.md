# EffortlessMetrics

Code is cheap. Trusted change is not.

AI agents write code fast. The bottleneck is knowing whether to merge it. PR count goes up. Confidence doesn't. The tooling, the CI systems, the review infrastructure are all built for a developer writing code in an editor. Developers already moved past that.

We build the infrastructure between code generation and trusted merge. Deterministic checks. Structured evidence at every stage. CI-native gates that tell you what actually passed before a human opens the PR.

---

## The Architecture

We trust receipts, not agents. Including our own.

The governed SDLC separates author from critic. The agent writing code is not the agent deciding if it passed. Every stage produces structured evidence: build receipts, gate results, mutation scores, requirement traceability. The human reviews artifacts, not chat transcripts.

```
Signal → Plan → Build (Author ⇄ Critic) → Review → Gate → Deploy → Wisdom
```

Agents game metrics. They write benchmarks that test struct creation instead of real workloads. They delete tests to stay green. Oppositional validation and mutation-on-diff catch what coverage alone misses. [Where this breaks and what we do about it.](https://effortlesssteven.com/demoswarm)

---

## What We Build

### Code Intelligence and Parser Infrastructure

| Repo | What it does |
|------|-------------|
| [perl-lsp](https://github.com/EffortlessMetrics/perl-lsp) | Rust Perl Language Server + parser toolkit. Built most of a compiler front-end to stay out of the runtime |
| [adze](https://github.com/EffortlessMetrics/adze) | Rust-native grammar toolchain with GLR-capable parsing and typed extraction, tree-sitter interoperable |
| [tokmd](https://github.com/EffortlessMetrics/tokmd) | Code intelligence for humans, machines, and LLMs: receipts, metrics, and insights from your codebase |
| [BitNet-rs](https://github.com/EffortlessMetrics/BitNet-rs) | Rust inference engine for 1-bit BitNet LLMs (GGUF + llama.cpp compatible) |

### Governed SDLC Infrastructure

| Repo | What it does |
|------|-------------|
| [demo-swarm](https://github.com/EffortlessMetrics/demo-swarm) | SDLC template producing review-ready PRs with adversarial build loops and build receipts |
| [flow-studio](https://github.com/EffortlessMetrics/flow-studio) | Runner + UI to execute and visualize swarm runs (flows, receipts, transcripts) with stepwise backends |
| [agent-backplane](https://github.com/EffortlessMetrics/agent-backplane) | Backplane for Agent SDKs |
| [xchecker](https://github.com/EffortlessMetrics/xchecker) | Spec pipelines (requirements → design → tasks) with lockfiles, safe fixups, and versioned receipts |
| [cockpitctl](https://github.com/EffortlessMetrics/cockpitctl) | PR glass cockpit: compiles CI sensor receipts into a deterministic merge surface |
| [rust-as-spec](https://github.com/EffortlessMetrics/Rust-Template) | AC-first, policy-gated, Nix-pinned, ADR-tracked Rust service starter |

### CI Sensors

Small, focused tools. Each one answers a specific question about the change and produces a receipt. `cockpitctl` compiles them into a merge surface.

| Repo | What it checks |
|------|---------------|
| [covguard](https://github.com/EffortlessMetrics/covguard) | Coverage gates with structured output |
| [perfgate](https://github.com/EffortlessMetrics/perfgate) | Perf budgets and baseline diffs for CI/PR bots |
| [lintdiff](https://github.com/EffortlessMetrics/lintdiff) | Diff-scoped lint enforcement |
| [diffguard](https://github.com/EffortlessMetrics/diffguard) | Diff-scoped governance linting for PR automation |
| [depguard](https://github.com/EffortlessMetrics/depguard) | Dependency manifest hygiene for Rust workspaces |
| [semverguard](https://github.com/EffortlessMetrics/semverguard) | Semver checks across workspaces with filtering, scoping, and receipts |
| [buildfix](https://github.com/EffortlessMetrics/buildfix) | Build contract repair |
| [builddiag](https://github.com/EffortlessMetrics/builddiag) | Build contract validation for Rust repos |
| [shipper](https://github.com/EffortlessMetrics/shipper) | Resumable, backoff-aware publishing reliability layer for Rust workspaces |
| [shiplog](https://github.com/EffortlessMetrics/shiplog) | Shipping packet generator: compiles GitHub activity into self-review packets with receipts |

### Legacy and Regulated Data Parsers

Every enterprise AI engagement starts with getting data out of systems built before the architect was born.

| Repo | What it parses |
|------|---------------|
| [copybook-rs](https://github.com/EffortlessMetrics/copybook-rs) | COBOL copybooks: EBCDIC/ASCII to JSON and Parquet with byte-identical round trips |
| [pst-rs](https://github.com/EffortlessMetrics/pst-rs) | Outlook PST/OST: full encryption support, attachment streaming, JSON/EML/MBOX export. Python and C bindings |
| [hl7v2-rs](https://github.com/EffortlessMetrics/hl7v2-rs) | HL7 v2: parser, validator, generator. 18 microcrates, conformance profiles, HTTP/REST with Prometheus metrics |

### Other Projects

| Repo | What it does |
|------|-------------|
| [OpenRacing](https://github.com/EffortlessMetrics/OpenRacing) | Rust 1kHz force-feedback + telemetry stack for sim racing wheels |
| [OpenFlight](https://github.com/EffortlessMetrics/OpenFlight) | Rust real-time input + device layer for flight simulation. 250Hz axis pipeline |
| [slower-whisper](https://github.com/EffortlessMetrics/slower-whisper) | Local-first conversation ETL with streaming, topic segmentation, and schema-versioned JSON |
| [uselesskey](https://github.com/EffortlessMetrics/uselesskey) | Deterministic cryptographic key and certificate fixtures for Rust tests |

---

## Links

- [effortlesssteven.com](https://effortlesssteven.com)
- [Talks and appearances](https://effortlesssteven.com/speaking)
- [crates.io](https://crates.io/users/effortlesssteven)
