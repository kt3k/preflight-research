---
name: research-harness
description: >
  Generate a task-specific research harness for problems that
  require empirical investigation, experimentation, custom
  evaluation, and iterative improvement. Design the research
  methodology, hypotheses, experimental environment, evaluation
  framework, iteration loop, and stopping criteria. Produce
  executable research infrastructure rather than conducting
  the research itself. Use when a task requires discovering
  or validating an approach rather than simply implementing
  a known solution.
---

# Research Harness

Generate a task-specific, executable research harness that enables
an AI agent to systematically investigate a problem through
hypothesis generation, experimentation, evaluation, and iteration.

Your responsibility is to **design and implement the research
system**, not to conduct the research or claim experimental results.

The generated harness should enable another agent to perform
the research with minimal additional instructions.

## Core Principles

1. **Task-specific methodology**
   Do not impose a universal research methodology.
   Derive the research process from the task's characteristics.

2. **Empirical grounding**
   Prefer measurable evidence over intuition or model confidence.

3. **Evaluation-first design**
   Define what constitutes success before designing experiments.

4. **Falsifiability**
   Every major hypothesis must have an observable condition
   under which it would be rejected.

5. **Reproducibility**
   Experiments should be reproducible, auditable, and resumable.

6. **Adaptive experimentation**
   The research loop should adapt based on observed results.

7. **Bounded autonomy**
   Define explicit resource budgets, safety constraints,
   approval boundaries, and stopping conditions.

8. **Separation of concerns**
   Separate hypothesis generation, experiment execution,
   evaluation, and research coordination.

9. **No fabricated evidence**
   Never invent experimental results, measurements, citations,
   or claims of validation.

## Workflow

### Phase 1: Analyze the Research Task

Analyze the user's task and identify:

- The underlying research question
- The desired outcome or decision
- The unknowns preventing a reliable solution
- Existing knowledge that can be reused
- Relevant disciplines and technical domains
- Available data, tools, infrastructure, and constraints
- The expected cost of incorrect conclusions
- Whether the research involves external systems or people

Distinguish among:

- Knowledge gaps resolvable through literature review
- Engineering gaps resolvable through implementation
- Empirical uncertainties requiring experiments
- Fundamental uncertainties that may remain unresolved

Do not assume that every task requires a complex research loop.

If a simpler methodology can answer the research question,
design the simpler methodology.

### Phase 2: Select the Research Methodology

Choose the methodology based on the task.

Possible methodologies include:

**Software Engineering**
- Unit and integration testing
- Property-based testing
- Differential testing
- Performance benchmarking
- Fuzzing
- Formal verification

**Machine Learning and AI**
- Benchmark construction
- Model comparison
- Ablation studies
- Human evaluation
- LLM-as-a-Judge
- Error analysis
- Hyperparameter optimization

**Data Science**
- Statistical hypothesis testing
- Cross-validation
- Causal inference
- Backtesting
- Sensitivity analysis
- Simulation

**Systems Research**
- Load testing
- Fault injection
- Reliability testing
- Resource profiling
- Distributed systems simulation

**Product and UX**
- Usability studies
- Controlled experiments
- Behavioral analysis
- Qualitative coding
- User interviews

**Scientific Research**
- Controlled experiments
- Computational modeling
- Simulation
- Literature synthesis
- Replication studies

**Mathematics and Formal Methods**
- Automated theorem proving
- Counterexample search
- Model checking
- Proof assistant integration

These are examples, not an exhaustive list.

Combine methodologies when necessary.

Explain why the selected methods are appropriate and what
their limitations are.

### Phase 3: Define the Evaluation Framework

Design the evaluation framework before the experiment loop.

Specify:

1. Primary success metric
2. Secondary metrics
3. Baseline or control
4. Evaluation dataset or experimental conditions
5. Measurement procedure
6. Acceptance criteria
7. Failure criteria
8. Sources of bias and uncertainty

Metrics must be operationally defined.

Avoid vague objectives such as:

- "Improve quality"
- "Make it more robust"
- "Find the best solution"

Translate them into measurable or inspectable outcomes.

For qualitative objectives, define structured rubrics,
independent review procedures, or other defensible
evaluation methods.

If reliable evaluation cannot yet be defined, make
evaluation design the first research milestone.

#### Evaluation Integrity

Prevent evaluation overfitting.

- Separate development evaluation from final evaluation.
- Keep final evaluation data isolated when possible.
- Freeze primary success criteria before optimization.
- Track all evaluation changes.
- Avoid selecting only favorable examples.
- Use independent evaluators when practical.
- Require human review for subjective or high-stakes claims.
- Treat LLM-as-a-Judge as an imperfect measurement instrument.

Do not allow the optimization agent to silently modify
the final evaluation criteria.

### Phase 4: Generate Research Hypotheses

Create an initial set of competing hypotheses.

Each hypothesis should contain:

- Unique identifier
- Proposed explanation or approach
- Supporting rationale
- Falsifiable prediction
- Required experiment
- Expected observation if correct
- Rejection criteria
- Estimated cost
- Dependencies

Include a baseline hypothesis whenever applicable.

Prefer hypotheses that distinguish between competing
explanations rather than merely demonstrate feasibility.

Avoid generating large numbers of speculative hypotheses
without a mechanism for prioritization.

### Phase 5: Design the Experimental Environment

Determine the infrastructure needed to execute experiments.

Possible components:

- Experiment runner
- Evaluation runner
- Dataset loader
- Metrics collector
- Artifact storage
- Research journal
- Hypothesis registry
- Configuration manager
- Result comparison utility
- Research coordinator

Generate only components justified by the task.

Prefer existing project tools and conventions.

Do not introduce unnecessary dependencies or infrastructure.

For each component, define:

- Responsibility
- Inputs
- Outputs
- Dependencies
- Failure handling
- Reproducibility requirements

### Phase 6: Design the Research Loop

Define an explicit iterative research process.

The default loop is:

1. Inspect current evidence and unresolved questions.
2. Generate or revise hypotheses.
3. Select the most informative feasible experiment.
4. Validate experimental prerequisites.
5. Execute the experiment.
6. Collect observations and artifacts.
7. Evaluate results using predefined criteria.
8. Compare results with the baseline and prior experiments.
9. Update the research state.
10. Continue, revise direction, or terminate.

Experiment selection should consider:

- Expected information gain
- Potential improvement
- Cost
- Risk
- Dependencies
- Uncertainty
- Reproducibility

Do not optimize only for the highest observed metric.

Prefer experiments that reduce important uncertainty.

#### Negative Results

Negative results are valuable evidence.

Record:

- Failed hypotheses
- Invalid assumptions
- Inconclusive experiments
- Unexpected observations
- Known dead ends

Do not repeatedly retry failed approaches without
new evidence or a meaningful change in conditions.

### Phase 7: Define Stopping Conditions

Every generated harness must have explicit stopping rules.

Include applicable limits on:

- Maximum experiment count
- Wall-clock time
- Token consumption
- API or compute cost
- Storage consumption
- External requests
- Consecutive unsuccessful experiments

Also define scientific stopping conditions:

- Success criteria satisfied
- No meaningful improvement
- Insufficient evidence
- Invalid experimental assumptions
- Exhausted promising hypotheses
- Unacceptable uncertainty
- Safety or authorization boundary reached

The harness must not run indefinitely.

Do not interpret reaching a resource limit as scientific
success or failure.

### Phase 8: Implement the Harness

Create actual files and executable infrastructure when
filesystem and execution tools are available.

Use the existing project's language, runtime, package
manager, and conventions where possible.

A typical structure is:

```
research/
  README.md
  RESEARCH.md
  config/
    research.yaml
  hypotheses/
    registry.json
  experiments/
    runner.*
  eval/
    evaluator.*
  results/
  state/
    research-state.json
```

This is an example, not a mandatory structure.

Adapt the structure to the task.

At minimum, generate:

**Research specification**

A document describing:

- Research question
- Methodology
- Hypotheses
- Evaluation criteria
- Experimental design
- Resource limits
- Stopping conditions

**Experiment interface**

A defined mechanism to:

- Submit an experiment
- Execute or simulate it
- Capture observations
- Record failures
- Preserve artifacts

**Evaluation interface**

A mechanism to:

- Evaluate experimental outputs
- Compare against baselines
- Produce structured results
- Record uncertainty

**Research state**

A persistent representation of:

- Current hypotheses
- Completed experiments
- Pending experiments
- Results and observations
- Best validated result
- Remaining uncertainties
- Resource consumption

**Research loop instructions**

Instructions another agent can follow to execute,
resume, and terminate the research.

When implementation is not possible, provide complete
file contents and clearly label unimplemented interfaces.

Never describe pseudocode as executable code.

### Phase 9: Validate the Generated Harness

Validate the harness infrastructure without performing
the substantive research.

Where practical:

- Check configuration syntax.
- Check file references and dependencies.
- Run static analysis.
- Run unit tests for harness components.
- Execute a synthetic or mocked experiment.
- Verify evaluation output schemas.
- Verify state persistence and recovery.
- Verify budget and stopping enforcement.

Use synthetic inputs rather than real research data.

A successful harness smoke test does not imply that
the research hypothesis is correct.

Clearly distinguish:

- Infrastructure validation
- Evaluation validity
- Experimental findings

### Phase 10: Produce the Handoff

Provide:

1. Generated files and their locations
2. Research question and selected methodology
3. Evaluation strategy
4. Initial hypotheses
5. Instructions for running the research
6. Resource and approval requirements
7. Known limitations
8. What was actually validated

The harness should be usable by a separate agent
without reconstructing the design from conversation history.

## Agent Roles

Use logical role separation even when only one model
or agent is available.

### Research Coordinator

Maintains research state, prioritizes experiments,
enforces budgets, and decides when to stop.

### Hypothesis Generator

Proposes competing explanations and experiments.

### Experiment Executor

Implements and runs experiments without changing
the predefined success criteria.

### Evaluator

Measures results and identifies errors, uncertainty,
and methodological weaknesses.

### Research Critic

Challenges assumptions, experimental validity,
and unsupported conclusions.

These roles do not require separate agents.

Use separate agents only when their independence
or specialization justifies the additional cost.

## Research State Requirements

Persist enough information to resume after interruption.

Each experiment record should include:

- Experiment ID
- Hypothesis ID
- Configuration
- Code or artifact version
- Dataset or input version
- Random seed, when applicable
- Start and completion status
- Metrics
- Observations
- Errors
- Artifact locations
- Evaluation version
- Resource consumption

Prefer structured, machine-readable records.

Use append-only experiment logs when practical.

Never overwrite historical results merely because
a newer experiment performs better.

## Safety and Authorization

Do not assume permission to:

- Spend money
- Access private datasets
- Modify production systems
- Conduct experiments on real users
- Contact external parties
- Perform disruptive testing
- Execute destructive operations

Build approval gates into the harness where needed.

Use safe local or simulated experiments by default.

Respect applicable policies, licenses, privacy
requirements, and higher-priority instructions.

## Output Rules

The output of this skill is the research harness itself.

Do not stop after describing a possible research plan
when implementation tools are available.

Do not begin the substantive research loop unless the
user explicitly requests its execution.

Do not claim that a hypothesis is validated merely
because the harness was generated successfully.

If required information is missing, make reasonable,
explicit assumptions where safe.

Ask the user only when missing information prevents
a meaningful or safe harness design.

## Definition of Done

The skill is complete when:

- The research question is operationally defined.
- An appropriate methodology is selected.
- Success and failure are evaluable.
- Initial hypotheses are specified.
- Experiments can be executed through defined interfaces.
- Results can be evaluated and persisted.
- The research loop can resume after interruption.
- Budgets and stopping conditions are enforced.
- The generated infrastructure passes available
  validation checks.
- Another agent can begin the research without
  redesigning the methodology.

## Core Principle

**Do not merely research the problem. Build the system
that can systematically discover, test, and validate
solutions to the problem.**
