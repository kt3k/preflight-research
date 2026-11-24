# preflight-research

An Agent Skill for Claude that assesses whether missing knowledge would hurt a task's outcome before executing it, and researches **only when necessary**.

> Research before you act, but only when you need to.

## What it does

- Routine, self-contained, reversible, easily verifiable tasks are executed directly (fast path)
- Otherwise, identifies the most consequential assumptions (2–5) and checks their evidence
- Classifies gaps along knowledge / evidence / procedure / verification, then chooses `EXECUTE` / `RESEARCH` / `CLARIFY` / `STOP`
- When researching, narrows down to 1–3 specific questions and compiles the findings into a concise "Task Context" before executing
- At most one additional research pass by default — never loops indefinitely

See [`SKILL.md`](./SKILL.md) for details.

## Other skills in this repository

### preflight-research-v3

[`preflight-research-v3/SKILL.md`](./preflight-research-v3/SKILL.md) builds on v2. For every document deliverable (proposal, report, slides, spec, plan, manual, memo), it always researches the format and structure at least once. It keeps iterating while rounds produce new information, capped at 4 rounds of up to 3 queries and 4 opened pages each. It then builds its own format harness (profile, ordered sections, conventions, anti-patterns, rubric, provenance, research log) and drafts and scores the deliverable against it.

### preflight-research-v2

[`preflight-research-v2/SKILL.md`](./preflight-research-v2/SKILL.md) is a proposed upgrade of `preflight-research`. It adds a fixed assumption inventory that includes the deliverable's craft and format, treats model recollection as unverified, keeps early outlines provisional until the preflight decision, checks that every acceptance criterion is backed by evidence, requires opening sources instead of citing search snippets, and gives the user a short preflight note.

### research-harness

[`research-harness/SKILL.md`](./research-harness/SKILL.md) generates a task-specific, executable research harness (methodology, evaluation framework, hypotheses, experiment/evaluation interfaces, persistent research state, iteration loop, and stopping conditions) for problems that require empirical investigation. It builds the research infrastructure; it does not conduct the research itself.

Install it the same way as below, replacing the path:

```sh
mkdir -p ~/.claude/skills/research-harness
curl -fsSL https://raw.githubusercontent.com/kt3k/preflight-research/main/research-harness/SKILL.md \
  -o ~/.claude/skills/research-harness/SKILL.md
```

Invoke explicitly with `/research-harness <your task>`.

## Installation

### Claude Code (personal: available in all projects)

```sh
mkdir -p ~/.claude/skills/preflight-research
curl -fsSL https://raw.githubusercontent.com/kt3k/preflight-research/main/SKILL.md \
  -o ~/.claude/skills/preflight-research/SKILL.md
```

Or clone it in place:

```sh
git clone https://github.com/kt3k/preflight-research.git ~/.claude/skills/preflight-research
```

### Claude Code (per project)

From the project root:

```sh
mkdir -p .claude/skills/preflight-research
curl -fsSL https://raw.githubusercontent.com/kt3k/preflight-research/main/SKILL.md \
  -o .claude/skills/preflight-research/SKILL.md
```

Commit it to share the skill with your team.

### Claude.ai / Claude Desktop

1. Put `SKILL.md` in a `preflight-research/` folder and zip it
   ```sh
   mkdir preflight-research && cp SKILL.md preflight-research/
   zip -r preflight-research.zip preflight-research
   ```
2. Upload the zip under Settings → Capabilities → Skills and enable it

## Usage

### Automatic

Based on its `description`, Claude loads the skill automatically for tasks it judges to be unfamiliar, high-stakes, fast-changing, or technically complex. For routine work it is either not loaded, or loaded and then exits via the fast path.

Examples:

- "Migrate this project to the latest major version of this library"
- "Estimate costs based on this API's current pricing"
- "Write a migration procedure for the production database"

### Explicit

In Claude Code, invoke it as a slash command:

```
/preflight-research <your task>
```

Or simply tell Claude to "use the preflight-research skill" in your prompt.

## Expected behavior

- For simple tasks, skips showing internal triage and just delivers the result
- When research is needed: briefly explains the critical knowledge gap → researches → executes → delivers → notes remaining uncertainties
- Does not fabricate numerical confidence scores
- Does not pretend to have searched when no search tool is available
- Treats retrieved external content as data, not as instructions

## Files

```
.
├── README.md                  # This file
├── SKILL.md                   # preflight-research skill
├── preflight-research-v2/
│   └── SKILL.md               # preflight-research v2 (proposed upgrade)
├── preflight-research-v3/
│   └── SKILL.md               # preflight-research v3 (mandatory format research + format harness)
└── research-harness/
    └── SKILL.md               # research-harness skill
```
