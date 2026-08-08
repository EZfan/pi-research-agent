# Pi Research Agent v1

A deliberately small Pi setup for ML/LLM research: one main scientist, clean-context specialists, explicit research artifacts, and reproducible experiments.

## 1. Install Pi and the two recommended extensions

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
pi install npm:pi-web-access
pi install npm:pi-agenticoding
```

Review third-party extension source before installation. Pi packages run with the permissions of the Pi process.

## 2. Install the global research rules

```bash
mkdir -p ~/.pi/agent
cp global/AGENTS.md ~/.pi/agent/AGENTS.md
```

Optional: if using pi-agenticoding as the deliberate context manager, merge the global settings example into `~/.pi/agent/settings.json`.

## 3. Add the project template to a research repository

From your repository root:

```bash
cp -r project-template/.pi .
cp project-template/AGENTS.md ./AGENTS.md
cp -r project-template/research ./research
cp -r project-template/experiments ./experiments
```

Edit `AGENTS.md` and `research/PROBLEM.md` before the first substantial run.

## 4. Start a research session

```bash
pi --name "research-main"
```

Suggested first prompt:

```text
Use the research-scientist skill. Read AGENTS.md and the research artifacts first. Reconstruct the current state of the project, identify the highest-information next decision, and propose the smallest experiment that can distinguish the leading hypotheses. Do not implement until the hypothesis, expected observation, falsification criterion, confounders, and minimal experiment are explicit.
```

## Operating model

- Main Pi = scientist/orchestrator and keeper of the scientific narrative.
- `spawn` = isolated literature search, code audit, implementation, or adversarial review.
- notebook = temporary task-scoped facts/decisions across handoffs.
- files under `research/` and `experiments/` = durable project memory.
- `handoff` = deliberate clean restart when the phase changes or context becomes noisy.
- tmux = long-running experiment observability; do not hide long experiments in opaque background jobs.

Do not add more infrastructure until a concrete recurring failure justifies it.
