# Experiment Matrix Reference

Use this reference when `$experiment-planner` needs to produce a plan, matrix,
or subagent task split. Keep output in chat unless the user asks for a saved
artifact.

## Entry Modes and Continuations

- For a substantial new exploration or design, fill the complete 19-field
  matrix below after the claim and baseline are clear. A small new pilot needs
  only the question, comparison, protocol plus budget, endpoint, and decision.
- For approved execution, load the latest plan and pass receipt when available.
  Reuse
  still-valid claims, controls, metrics, protocol, seed, budget, and decisions.
  An earlier user authorization covers ordinary implementation, local bug
  fixes, queueing in-scope runs, and evaluation, but not a new experiment family,
  dataset, seed policy, or paper-only TODO.
- For acceptance, compare the observed artifacts with the frozen contract and
  report the relevant gate as pass, fail, or inconclusive.
- On a continuation, do not require a fresh grill, literature pass, or all
  matrix fields. Ask only changed or blocking questions and return the delta,
  next decision, or compact pass receipt.

## Matrix Fields

| Field | Required content |
|---|---|
| `research question` | The exact question the experiment answers. |
| `core hypothesis` | The smallest falsifiable claim. |
| `paper claim` | The reviewer-facing claim the completed experiment may support. |
| `storyline` | Why the question matters, what gap exists, and how the method could support a paper story. |
| `literature inspiration` | Known related directions, verified or pending `$research-evidence` checks, and novelty risk. |
| `baseline/control` | The minimal fair comparison or negative control needed to interpret results. |
| `table contract` | Final row/column structure for the main result, ablation, and only the necessary diagnostics; use the in-scope project's explicit missing-value schema until values are accepted. |
| `metric definitions` | Plain definition, unit, direction, aggregation population, and delta reference for every reported metric. |
| `idea validation experiment` | The smallest pilot/smoke/sanity run that can support or falsify the core hypothesis. |
| `expected signal` | What pattern would count as success, including the metric, artifact, or qualitative cue. |
| `failure modes` | How the idea could fail, including dataset leakage, weak baseline, noisy metric, or implementation artifact. |
| `diagnostic checks` | Checks that separate mechanism from bugs, protocol mismatch, or confounds. |
| `follow-up experiments` | Main result, ablation, robustness, efficiency, qualitative, and failure-analysis runs after pilot success. |
| `subagent/task ownership` | Explorer/worker split, write scopes, and which tasks stay with the main session. |
| `compute/resource assumptions` | GPU count, expected runtime, data availability, seed policy, and storage constraints when known. |
| `seed policy` | One fixed seed by default. Mark multi-seed or repeated-seed runs as not scheduled unless the user explicitly requests them. |
| `success gate` | The explicit condition for moving from pilot to full experiment. |
| `claim gate` | The result threshold or comparison pattern required before using stronger paper wording. |
| `next action` | The next concrete step: ask user, search literature, inspect repo, write code, smoke test, launch run, or stop. |

## Run Order

1. For a new design, confirm the problem, motivation, and minimum claim. For a
   continuation, load and reuse the current contract and receipt when available.
2. For a new design or changed novelty claim, check literature or existing
   implementations when novelty or feasibility is uncertain.
3. Identify the baseline/control before designing a method-heavy experiment.
4. For a substantial study or full runs, freeze the final paper/table contract,
   metric definitions, and claim gate. For a small pilot, freeze only the
   endpoint, comparison, protocol plus budget, and decision gate.
5. For execution, reuse the existing project contract and persist only the
   needed pre-run result contract. Update final LaTeX tables only when
   manuscript writing is in scope; otherwise use the existing planning artifact
   or create `experiment-plan.md` only when a saved execution artifact is
   requested. In-chat planning does not mutate files by default.
6. Define the pilot experiment and success gate.
7. Define smoke checks: command starts, config resolves, data loads, first
   batch/output looks plausible, and generated test artifacts can be removed.
8. Only after smoke passes, define the minimum sufficient full runs.
9. Prioritize validation by impact, reuse unchanged passing checks and receipts,
   and do not add endless CPU gates before a feasible authorized GPU pilot.
   Inspect early full-run samples/logs/artifacts, then stop continuous
   monitoring unless the user asks for ongoing monitoring.
10. After results finish, interpret against the frozen claim before planning
   paper writing or additional ablations.

## Result Contract Rules

- Make each main table answer one reviewer question.
- Prefer standard metrics. Introduce a new metric only when existing metrics
  cannot test the claim, and define it before any result is interpreted.
- Keep the main comparison first; make ablations and diagnostics secondary.
- For missing values, follow the in-scope project's explicit schema. If none is
  defined, use `TBD (pending)`, `N/A (inapplicable)`, or
  `unknown (needs user input)` as appropriate; `--` is not mandatory.
- Do not write result claims from placeholders.
- Record one fixed seed and keep compared runs under the same evaluation and
  checkpoint-selection policy.
- Do not add a new experiment family, dataset, multi-seed or repeated-seed
  policy, or other auxiliary run without explicit opt-in. A prior authorization
  covers ordinary implementation, local bug fixes, queueing in-scope runs, and
  evaluation only. Keep the resource and time budget honest; a paper TODO,
  small margin, low cost, idle GPU, reviewer expectation, or venue norm does
  not authorize expansion.
- If an unrequested auxiliary experiment could matter, note it only as an unrun
  option or limitation; keep it out of the active matrix and execution queue.
- Freeze the acceptance rule, primary metric, comparison, and claim boundary
  before inspecting outcomes. Never weaken a gate or redefine the baseline
  after seeing a result.

## Validation and Acceptance

- Validate the highest-impact blocker first and reuse a passing check or receipt
  when code, data, configuration, protocol, relevant environment, and
  dependencies are unchanged.
- A compact pass receipt records the scope, checks/evidence, decision, and next
  action; add a command/run reference or exception only when needed for
  interpretation or recovery.
- Do not use hashes or hash parity as routine validation gates. A minimal
  CPU/configuration smoke check is sufficient before a feasible downstream GPU
  pilot unless a claim-critical check requires more.
- Diagnostic gates test for bugs, confounds, or mechanisms; they are not by
  themselves the complete scientific verdict. State what each gate does and
  what remains untested.

## Failure Taxonomy

Label the relevant failure before choosing the next action:

- `engineering`: command, data, configuration, checkpoint, or artifact contract
  is broken; repair the implementation or protocol.
- `optimization`: the method does not train, converge, or improve the fixed
  target under a fair protocol; report a method or tuning failure.
- `prototype`: a sound, deployable pilot misses its predeclared mechanism
  endpoint, including a negative endpoint despite a plausible mechanism; report
  that measured benchmark endpoint, but do not infer impossibility or
  falsification of the broader mechanism.
- `core-construct`: the predeclared construct-level test contradicts the
  central hypothesis under the frozen protocol; close or narrow that claim.
- `inconclusive/blocked`: noisy or confounded evidence, missing support, an
  invalid protocol, or an unresolvable engineering issue prevents interpreting
  the gate; do not relabel it as a scientific failure.

Do not promote a diagnostic failure into a whole-science conclusion, and do not
relax a gate to rescue an observed outcome.

## Subagent Task Patterns

Use `explorer` for:

- Repo/config/data-path inspection.
- Existing baseline/protocol discovery.
- Dependency, command, or logging investigation.
- Read-only comparison of candidate implementation paths.

Use `worker` for:

- A bounded code or script change with explicit file/module ownership.
- A smoke-test command or runner repair after the main session approves the
  write scope.
- Independent implementation slices that do not overlap with other workers.

Keep in the main session:

- Research claim decisions.
- Whether a pilot result is accepted.
- Whether to launch long experiments.
- Final result interpretation and handoff to writing skills.

## Default Matrix Skeleton (new designs only)

```text
research question:
core hypothesis:
paper claim:
storyline:
literature inspiration:
baseline/control:
table contract:
metric definitions:
idea validation experiment:
expected signal:
failure modes:
diagnostic checks:
follow-up experiments:
subagent/task ownership:
compute/resource assumptions:
seed policy:
success gate:
claim gate:
next action:
```
