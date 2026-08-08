# Project Research Context

## Project

Name: <PROJECT_NAME>
One-sentence goal: <WHAT SCIENTIFIC QUESTION THIS PROJECT ANSWERS>

## Current research question

<QUESTION>

## Current status

- Stage: exploration | hypothesis-test | implementation | scaling | paper-writing
- Strongest current evidence: <...>
- Main unresolved uncertainty: <...>
- Current leading hypothesis: <...>
- Current strongest alternative explanation: <...>

## Repository map

- Core implementation: `<PATH>`
- Training/inference entrypoint: `<PATH OR COMMAND>`
- Evaluation entrypoint: `<PATH OR COMMAND>`
- Experiment configs: `experiments/configs/`
- Experiment outputs: `experiments/results/`
- Durable research notes: `research/`

## Environment

- Python/env: <e.g. conda env / uv / poetry>
- GPU assumptions: <...>
- Dataset locations: <...>
- Model/checkpoint locations: <...>
- Tracking: <W&B / TensorBoard / files>

## Known-good baseline

Command:
```bash
<BASELINE COMMAND>
```

Expected key metrics:
- <metric>: <value/range>

Do not intentionally break this baseline without preserving a reproducible route back to it.

## Project-specific constraints

- <compute constraint>
- <deadline or benchmark constraint>
- <do-not-touch paths / shared server constraints>

## Required workflow

Before a nontrivial new experiment, update `research/HYPOTHESES.md` and create/update an entry in `experiments/EXPERIMENTS.md`.
After results arrive, update `research/FINDINGS.md` and `research/DECISIONS.md` before starting the next conceptual iteration.

If repository facts conflict with this file, inspect the repository and update this file rather than pretending the conflict does not exist.
