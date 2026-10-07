# SDDA Empirical Validation & Falsification Framework

**A Scientific Protocol for Evaluating Agent-Operated Software Architectures**  
*Testing Efficiency, Architectural Attractor Dynamics, and Mechanical Self-Repair across Autonomous Maintenance Sequences.*

---

## 1. Executive Summary & Research Question

Most architectural benchmarks evaluate human ergonomics, runtime throughput, or single-turn code generation on isolated functions. SDDA makes a fundamentally different proposition:

> **Core Thesis:**  
> When autonomous AI agents act as the primary authors and maintainers of a codebase, software architecture must not function merely as a stylistic guideline for humans. It must function as a **machine-checkable constraint system** that maximizes repository retrieval locality, minimizes hidden state exploration, and acts as a **stable architectural attractor** over longitudinal code evolution.

### The Central Research Question
> **Can an architecture grounded in explicit dataflow, progressive type lineage, pure decision cores, and mechanically enforced boundaries reduce the operational cost of autonomous maintenance while preventing the structural degradation (architectural drift) typically caused by repeated LLM-generated modifications?**

This framework specifies the formal hypotheses, baseline requirements, metric definitions, and longitudinal testing protocols required to empirically validate or falsify this proposition.

---

## 2. The Three Core Hypotheses

To avoid vague claims regarding model cognition, the SDDA evaluation is decomposed into three mutually independent, falsifiable hypotheses:

```text
┌────────────────────────────────────────────────────────────────────────┐
│ H1: Operational Efficiency (Per-Task Performance)                      │
│ Agents solve tasks faster, cheaper, and with fewer retrieval misses.   │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
┌──────────────────────────────────▼─────────────────────────────────────┐
│ H2: Longitudinal Stability (The Architectural Attractor)               │
│ Repositories resist structural entropy across 50–100 consecutive tasks.│
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
┌──────────────────────────────────▼─────────────────────────────────────┐
│ H3: Mechanical Self-Repair (Constraint Convergence)                    │
│ AST linters guide agents back to valid shapes without human prompting. │
└────────────────────────────────────────────────────────────────────────┘
```

### Hypothesis 1: Operational Efficiency (H1)
* **Statement:** An autonomous agent will resolve maintenance and feature tasks with lower context retrieval overhead, fewer token expenditures, fewer tool calls, and fewer repair iterations on an SDDA codebase than on a functionally identical conventional codebase.
* **Falsification Condition (Null Hypothesis $H_{1,0}$):** Across a statistically significant suite of tasks ($N \ge 50$), the mean token consumption, time-to-green, or repair iterations on SDDA are equal to or greater than those on the conventional baseline ($p \ge 0.05$).

### Hypothesis 2: Architectural Stability / The Attractor Effect (H2)
* **Statement:** As an autonomous agent sequentially implements tasks over time without human intervention, an SDDA codebase will maintain architectural invariants, whereas a conventional codebase will exhibit compounding architectural drift (leaked boundaries, ad-hoc abstractions, increased dependency depth, and duplicate logic).
* **Falsification Condition (Null Hypothesis $H_{2,0}$):** After a sequence of $K \ge 50$ consecutive unassisted agent tasks, the rate of architectural debt accumulation in the SDDA repository is statistically indistinguishable from the conventional baseline.

### Hypothesis 3: Mechanical Constraint Convergence (H3)
* **Statement:** When an agent produces code that violates an architectural invariant, deterministic AST linter failures in the CI loop provide sufficient gradient for the agent to autonomously converge back to a compliant implementation without human prompting.
* **Falsification Condition (Null Hypothesis $H_{3,0}$):** When an agent is rejected solely by an SDDA mechanical linter (and not by a runtime functional test), it enters an unrecoverable repair loop or fails to produce a compliant patch in $\ge 30\%$ of cases.

---

## 3. Experimental Design: The Longitudinal Twin Protocol

Single-task evaluations evaluate static snapshots. They fail to test how architectures degrade under compounding agent edits. The SDDA validation protocol mandates a **Longitudinal Twin Experiment**.

```text
                           Identical Agent Configuration
                       (Model, Temperature, Tool Budget)
                                      │
                   ┌──────────────────┴──────────────────┐
                   ▼                                     ▼
      Repository A: Canonical SDDA          Repository B: Conventional Baseline
     ┌──────────────────────────────┐      ┌──────────────────────────────┐
     │ • Constructive Schema Gate   │      │ • Clean Architecture / DDD   │
     │ • Referential Domain Core    │      │ • Dependency Injection       │
     │ • Imperative Shell / Outbox  │      │ • Repositories & Services    │
     │ • AST Linters Enforced in CI │      │ • Mock-Based Unit Tests      │
     └──────────────┬───────────────┘      └──────────────┬───────────────┘
                    │                                     │
                    └──────────────────┬──────────────────┘
                                       ▼
                       Sequential Execution Loop (Task 1 → N)
                          • Identical task requirements
                          • No human intervention between tasks
                          • Git commit persisted after every pass
                                       │
                    ┌──────────────────┴──────────────────┐
                    ▼                                     ▼
        Operational Evaluation               Structural Evaluation
     (Tokens, Tool Calls, Time)            (Architectural Drift Score)
```

### Phase 1: Twin Baseline Construction
Two repositories are implemented to provide identical business functionality:

1. **Common Ground:**
   * Same programming language and runtime version.
   * Same relational datastore schema and transactional guarantees.
   * Same external APIs, network contracts, and public HTTP endpoints.
   * Same acceptance test suite (black-box API end-to-end integration tests).
   * Approximately equal initial Lines of Code ($\pm 10\%$).

2. **Repository A (SDDA):**
   * Implemented strictly according to the SDDA specification.
   * Pure domain core, explicit context, progressive type lineage, outbox persistence.
   * AST linters installed in CI to mechanically reject I/O in the core.

3. **Repository B (Conventional Baseline):**
   * Must represent idiomatic, high-quality enterprise engineering: Clean Architecture / DDD with Dependency Injection, Interface Segregation, Domain Services, Repositories, and Mocked Unit Tests.
   * *Rationale:* Beating poorly written code is trivial; proving that SDDA outperforms respected enterprise paradigms provides real architectural value.

### Phase 2: Autonomous Sequential Maintenance Loop
A suite of 50 to 100 realistic engineering backlog items is fed sequentially to the autonomous agent.

* **Task Composition:**
  * 40% Feature Extensions (e.g., "Add partial refund support with tiered penalty calculations").
  * 30% Bug Fixes (e.g., "Fix race condition in concurrent inventory allocation").
  * 20% Policy Modifications (e.g., "Update tax calculation rules based on seasonal regional codes").
  * 10% Cross-Cutting Additions (e.g., "Track diagnostic audit events for failed authorizations").
* **Execution Rules:**
  * The agent receives only the task description and the current repository state.
  * The agent runs autonomously until the test suite passes and git commit is generated, or until it exhausts its tool/turn budget.
  * **Zero Human Intervention:** No prompt tweaking, no manual file pointers, and no reset of the repository between tasks. Task $N+1$ operates directly on the output of Task $N$.

---

## 4. Dual Measurement Framework

Evaluation requires two distinct observation lenses: **Operational Efficiency** and **Architectural Conformance**.

### Dimension A: Operational & Efficiency Metrics (Per-Task)

| Metric | Symbol | Description | Data Collection Method |
| :--- | :--- | :--- | :--- |
| **Functional Success Rate** | $R_{\text{success}}$ | Percentage of tasks where all black-box acceptance tests pass. | CI test runner status. |
| **Context Acquisition Efficiency** | $E_{\text{context}}$ | Ratio of *relevant files inspected* to *total files inspected* before first edit. | Tool-call execution logs (`read_file`, `grep`, `find`). |
| **Repository Exploration Breadth** | $B_{\text{files}}$ | Total number of unique source files loaded into context. | Tool-call execution logs. |
| **Inference Token Expenditure** | $T_{\text{total}}$ | Total input, output, and cache-read tokens consumed per task. | Model provider telemetry. |
| **Time-to-Green** | $t_{\text{green}}$ | Wall-clock execution time until successful patch completion. | CI/Runner execution timestamps. |
| **Repair Loop Iterations** | $I_{\text{repair}}$ | Number of failed compile/test/lint cycles before a successful commit. | Git commit and test invocation history. |
| **Regression Rate** | $R_{\text{regress}}$ | Percentage of tasks that break previously passing functionality. | Full regression suite execution after each task. |

---

### Dimension B: Architectural Conformance & Drift Metrics (Longitudinal)

| Metric | Symbol | Description | Data Collection Method |
| :--- | :--- | :--- | :--- |
| **Mechanical Invariant Violations** | $V_{\text{invar}}$ | Number of SDDA AST rule violations attempted or committed. | Static AST analysis on patch diffs. |
| **Dependency Graph Depth** | $D_{\text{graph}}$ | Maximum call-chain depth from entry point to persistent effect. | Static call-graph analysis. |
| **Cross-Module Coupling** | $C_{\text{module}}$ | Number of import edges crossing feature/module boundaries. | Static dependency matrix analyzer. |
| **Cognitive Indirection Index** | $I_{\text{indir}}$ | Count of interfaces, abstract classes, and proxy adapters added per feature. | AST symbol extractor. |
| **Duplication Delta** | $\Delta_{\text{dup}}$ | Growth in duplicate logic blocks across distinct services. | Token-based duplicate code detection. |

---

## 5. The Architectural Drift Score (ADS)

To quantify the degradation of a codebase across sequential tasks, we define the **Architectural Drift Score (ADS)**. 

For any given task patch $k$, the marginal drift $\delta_k$ is computed as:

$$\delta_k = w_1 \cdot \Delta \text{Indirection} + w_2 \cdot \Delta \text{Coupling} + w_3 \cdot \Delta \text{Depth} + w_4 \cdot \text{Violations}$$

Where:
* $\Delta \text{Indirection}$: Number of new interfaces, abstract classes, or factories introduced with only a single concrete implementation.
* $\Delta \text{Coupling}$: Number of new cross-boundary dependencies bypassing architectural strata.
* $\Delta \text{Depth}$: Increase in call-stack hops between raw ingress and persistent egress.
* $\text{Violations}$: Count of bypassed schema parsers, hidden ambient state accesses, or leaked side effects.

### The Cumulative Drift Metric
The Cumulative Architectural Drift across an $N$-task sequence is:

$$\text{ADS}_N = \sum_{k=1}^{N} \delta_k$$

```text
Hypothesized Longitudinal Behavior:
Architectural Drift (ADS)
│
│                                      Conventional Baseline (Compounding Debt)
│                                     /
│                                   /
│                                 /
│                               /
│                             /
│ SDDA (Bounded Attractor)  /
│ ─────────────────────────
│
└─────────────────────────────────────────────────── Task Count (1 → N)
```

* **Target Outcome for SDDA:** $\lim_{N \to \infty} \frac{\text{ADS}_N}{N} \approx 0$ (The architecture enforces a bounded state).
* **Observed Tendency in Baselines:** $\frac{\text{ADS}_N}{N} > 0$ (Agents take progressive shortcuts, duplicate logic, and accumulate indirection).

---

## 6. Mechanical Enforcement: The CI Linter as an Architectural Oracle

To isolate the architecture from prompt obedience, boundaries are enforced mechanically via static analysis gates within the inner feedback loop.

```text
                   ┌───────────────────────────────┐
                   │      Backlog Task Input       │
                   └──────────────┬────────────────┘
                                  ▼
                   ┌───────────────────────────────┐
                   │    Agent Generates Patch      │
                   └──────────────┬────────────────┘
                                  ▼
                   ┌───────────────────────────────┐
                   │    Compiler / Syntax Check    │
                   └──────┬─────────────────▲──────┘
                     Fail │                 │ Error Feedback
                          └─────────┬───────┘
                               Pass │
                                    ▼
                   ┌───────────────────────────────┐
                   │     SDDA AST Linter Gate      │
                   └──────┬─────────────────▲──────┘
                Violation │                 │ Linter Rule Violation
                          └─────────┬───────┘
                               Pass │
                                    ▼
                   ┌───────────────────────────────┐
                   │   Unit & Acceptance Tests     │
                   └──────┬─────────────────▲──────┘
                     Fail │                 │ Test Failure Output
                          └─────────┬───────┘
                               Pass │
                                    ▼
                   ┌───────────────────────────────┐
                   │ Task Complete & Git Commit    │
                   └───────────────────────────────┘
```

### Mandatory AST Linter Gates (Core Purity Engine)
The following rules run as hard CI failures on any file within the designated `core/` path:

1. **`SDDA001_NO_IO_IN_CORE`:** Prohibits imports of HTTP clients, database drivers, filesystem modules, or network sockets inside domain core paths.
2. **`SDDA002_NO_AMBIENT_STATE`:** Prohibits calls to ambient runtime clocks (`Date.now()`, `time.time()`), environment variables, or global state variables.
3. **`SDDA003_NO_DIRECT_MUTATION`:** Flags in-place object mutations across function boundaries; mandates frozen or immutable data records.
4. **`SDDA004_LINEAGE_GATE_ENFORCEMENT`:** Enforces that functions typed to accept `ValidatedCommand` cannot receive raw or unparsed payload objects.
5. **`SDDA005_EXPLICIT_DECISION_RETURN`:** Mandates that core orchestration functions return an explicit algebraic sum type or tagged union (`Decision`), prohibiting untyped `void` mutations.

---

## 7. The Stress Test: Inducing Artificial Violations (H3 Verification)

To explicitly test Hypothesis 3 (Mechanical Constraint Convergence), the benchmark includes a specialized **Controlled Perturbation Test**.

### The Perturbation Protocol
1. Take a clean, passing SDDA repository.
2. Programmatically inject an anti-SDDA implementation of a new feature:
   ```typescript
   export class BookingService {
     async execute(rawInput: any) {
       const user = await db.loadUser(rawInput.userId); // Leaked I/O
       if (user.isBlocked) throw new Error("Blocked");  // Hidden exception
       return db.saveBooking(rawInput);                 // Leaked side effect
     }
   }
   ```
3. Run the CI pipeline. The SDDA AST Linter halts execution:
   ```text
   ERROR [SDDA001]: Direct I/O detected in core path at booking_service.ts:3.
   ERROR [SDDA004]: Raw untyped payload consumed without passing through Schema Gate.
   ERROR [SDDA005]: Function execute() does not return a pure algebraic Decision.
   ```
4. Hand the repository and the compiler/linter error output to the agent with zero human guidance.
5. **Measure the Recovery:**
   * Does the agent refactor the code into the canonical four strata (`Schema Gate` $\to$ `Context Projection` $\to$ `Pure Core` $\to$ `Atomic State Commit + Outbox`)?
   * How many repair turns are required to achieve compliance?
   * Does the agent attempt to modify the linter configuration or disable rules (an evasion failure)?

---

## 8. Threats to Validity & Mitigation Protocols

| Threat to Validity | Potential Bias | Benchmark Mitigation Protocol |
| :--- | :--- | :--- |
| **Strawman Baseline Bias** | Comparing SDDA against poorly written, unrealistic legacy code. | Implement the baseline using idiomatic, production-grade enterprise patterns (DDD, Clean Architecture, Dependency Injection) adhering to official community guidelines. |
| **Training Set Memorization** | Models have seen millions of standard OOP examples, potentially biasing performance toward familiar patterns. | Use synthetic, proprietary domain requirements (e.g., custom financial clearing instruments) with non-standard naming and business invariants. |
| **Prompt Engineering Asymmetry** | Providing detailed instructions to the SDDA agent while starving the baseline agent. | Use standardized, minimal tool harness prompts for both repositories. Only structural repository context and CI error logs are provided. |
| **Evaluation Non-Determinism** | LLM sampling variability creating noisy benchmark passes. | Run all tasks across multiple random seeds ($k \ge 5$) at a fixed inference temperature ($T = 0.2$), reporting mean and standard deviations. |
| **Linter Evasion** | The agent modifies the CI script, deletes tests, or disables linter rules to get a green build. | The benchmarking test harness locks `.github/workflows/`, test runner configs, and linter configuration files in read-only volumes. Any attempt to modify them results in immediate task failure. |

---

## 9. Reporting Standard: The Architectural Benchmark Card

Every published SDDA evaluation run must report its results using the following standardized scorecard:

```text
================================================================================
SDDA ARCHITECTURAL BENCHMARK SCORECARD
Model Evaluated: [Model Name & Version]
Harness / Agent System: [e.g., SWE-agent, OpenHands, Custom]
Tasks Executed: [Number, e.g., 50 Sequential Tasks]
================================================================================
OPERATIONAL EFFICIENCY (H1)          BASELINE (Clean/OOP)   SDDA (Dataflow)   DELTA
--------------------------------------------------------------------------------
Task Completion Rate (%):            [XX.X]%               [XX.X]%           [+/-]%
Median Tokens per Task:              [XXX,XXX]             [XXX,XXX]         [-XX.X]%
Median Files Inspected per Task:     [XX]                  [XX]              [-XX.X]%
Context Retrieval Precision (%):     [XX.X]%               [XX.X]%           [+XX.X]%
Median Repair Turns:                 [X.X]                 [X.X]             [-XX.X]%
Regression Rate (%):                 [X.X]%                [X.X]%            [-XX.X]%

LONGITUDINAL STABILITY (H2)          BASELINE (Clean/OOP)   SDDA (Dataflow)   DELTA
--------------------------------------------------------------------------------
Initial Architectural Violations:    0                     0                 0
Final Architectural Violations:      [XX]                  [X]               [-XX.X]%
Cumulative Architectural Drift (ADS):[XXX.X]               [XX.X]            [-XX.X]%
Max Call-Graph Depth Growth:         [+X]                  [+0]              [-XX.X]%
Cross-Module Import Growth:          [+XX]                 [+X]              [-XX.X]%

CONSTRAINT CONVERGENCE (H3)                                SDDA VALUE
--------------------------------------------------------------------------------
Autonomous Self-Repair Success (%):                        [XX.X]%
Mean Turns to Resolve Linter Violations:                   [X.X] turns
Linter Evasion Attempt Rate (%):                           [X.X]%
================================================================================
CONCLUSION: [HYPOTHESIS VALIDATED / FALSIFIED]
================================================================================
```

---

## 10. Summary: The Core Realization

This benchmark does not ask: *"Can an LLM write a functional program?"*  
It asks: **"Can an architecture structurally protect a codebase from the entropy of continuous, autonomous machine modification?"**

By testing efficiency, longitudinal drift, and mechanical constraint convergence against an idiomatic enterprise baseline, this protocol provides the empirical rigor necessary to establish SDDA as an authoritative, machine-operable software engineering standard.
