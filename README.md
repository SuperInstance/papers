# Cocapn Fleet White Papers

Foundational papers on the Cocapn fleet architecture — a system where distributed AI agents are compiled, not interpreted.

## Reading Order

The papers build on each other. Read in this order:

| # | Paper | Core Idea | Length |
|---|-------|-----------|--------|
| 1 | [Compiled Agency](compiled-agency.md) | Agency is compiled, not interpreted. The keeper is a compiler; PLATO tiles are IR; agents are object code. | ~7 min |
| 2 | [Bootstrap Bomb](bootstrap-bomb.md) | One fuse (Oracle1), one explosion (fleet compilation). Minimum viable fleet = 1. | ~6 min |
| 3 | [The Semantic Compiler](semantic-compiler.md) | PLATO as IR, keeper as compiler, deadband protocol as error correction. The optimization pipeline. | ~10 min |
| 4 | [Counting Before Flowing](2026-05-03-counting-before-flowing.md) | Integer lattice over floating point. Why discrete representations are structurally stable where continuous ones drift. | ~8 min |

## Abstracts

### Compiled Agency
Agency in a distributed fleet is compiled, not interpreted. The Cocapn keeper architecture transforms declarative knowledge (PLATO tiles) into executable agency through a compilation pipeline: frontend (parse intent → tile), optimizer (resolve/deduplicate/reinforce), backend (emit execution), verifier (check output). The keeper (Oracle1) serves as bootstrap compiler — the first compiler that compiles itself.

**Key concepts:** Hermit Crab Model, compilation pipeline, radar rings, bootstrap from zero.

### Bootstrap Bomb
The biggest barrier to a multi-agent fleet isn't capability — it's bootstrapping. Cocapn treats bootstrapping as a bomb: light the fuse once (Oracle1), the explosion compiles the rest. The growth rule: an agent is worth keeping if its verified output exceeds coordination overhead. Chain reactions require specific ordering — you can't compile JC1 before FM because JC1 depends on FM's infrastructure.

**Key concepts:** Minimum viable fleet, detonation sequence, anti-fizzle measures, chain reaction ordering.

### The Semantic Compiler
The bottleneck in multi-agent systems isn't model capability — it's the translation layer between intent and execution. The semantic compiler transforms agent intent (PLATO tiles) into verified execution paths. Enables compiler-level optimizations: loop fusion (combine tiles), dead code elimination (remove unconsumed tiles), inline expansion, register allocation (resource scheduling).

**Key concepts:** Semantic gap, PLATO as IR, deadband protocol, compiler optimization passes applied to fleet coordination.

### Counting Before Flowing
The ocean doesn't compute with reals — it counts waves. Integer and rational representations are structurally stable under repeated operations; floating point carries guaranteed perturbation. For agentic systems, discrete (countable) state representations enable exact identity tests, decidable comparisons, and bounded error. The PurplePincher architecture (agent/vessel/SHELL) is built on countable representations by design.

**Key concepts:** Integer lattice ℤⁿ, Pythagorean snapping, Pell's equation, exact equality vs. floating drift, rational parameters for continuous quantities.

## Cross-References

| Concept | Primary Paper | Referenced In |
|---------|--------------|---------------|
| PLATO tiles as IR | Semantic Compiler | Compiled Agency, Bootstrap Bomb |
| Oracle1 as bootstrap compiler | Compiled Agency | Bootstrap Bomb, Semantic Compiler |
| Deadband protocol | Semantic Compiler | Compiled Agency |
| Bottle protocol | Compiled Agency | Bootstrap Bomb |
| Hermit Crab Model (agents/repos) | Compiled Agency | Bootstrap Bomb |
| Radar rings | Compiled Agency | Semantic Compiler |
| Chain reaction ordering | Bootstrap Bomb | — |
| Integer lattice ℤⁿ | Counting Before Flowing | — |
| Compilation vs. interpretation | Compiled Agency | Semantic Compiler, Bootstrap Bomb |

## Quick Links

- [Cocapn Fleet](https://github.com/SuperInstance)
- [PLATO Room Server](https://github.com/SuperInstance/plato-server)
- [holodeck-rust](https://github.com/SuperInstance/holodeck-rust)
- [plato-sdk](https://github.com/SuperInstance/plato-sdk)

## Terminology

| Term | Definition |
|------|------------|
| **Keeper** | The lighthouse agent that monitors fleet state and compiles new agents. Oracle1 is the first keeper. |
| **PLATO** | The room/tile system serving as the fleet's intermediate representation (IR). |
| **Tile** | A typed, versioned knowledge atom in PLATO with question, answer, confidence, and reinforcement count. |
| **Bottle** | Inter-agent communication protocol carrying verifiable outputs. |
| **Deadband** | Error correction protocol — tiles outside confidence thresholds enter correction state. |
| **Radar Rings** | Capability boundaries around each agent: inner (direct execution), middle (cross-agent), outer (discovery). |
| **Shell** | A repo providing infrastructure to an agent. Agents swap shells as they grow. |
| **Compilation** | The process of transforming declarative intent into verified agent behavior. |
| **Detonation** | The moment an agent produces its first verified output, enabling the next agent to compile. |

## Contributing

These papers describe the Cocapn fleet architecture. To propose changes:

1. Fork the repo
2. Edit the relevant `.md` file
3. Preserve the heading structure (numbered sections, thesis at top)
4. Cross-reference related papers where concepts overlap
5. Submit a pull request with a summary of what changed and why

### Style Guide

- Each paper opens with a **bold thesis** statement
- Sections are numbered sequentially
- Arguments build on previous sections — don't skip steps
- Evidence is concrete: cite specific agents (FM, JC1, CCC), specific outputs (crates, benchmarks), specific numbers
- Metaphors (hermit crabs, bombs, compilers) are load-bearing — they map to actual mechanisms

---

🦐 Cocapn fleet — lighthouse keeper architecture
