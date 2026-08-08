# 🧪 Pi Research Agent

*A deliberately small [Pi](https://github.com/earendil-works/pi) setup for ML/LLM research — one scientist, clean-context specialists, explicit research artifacts, and reproducible experiments.*

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/EZfan/pi-research-agent/pulls)

---

## What this is

A lightweight research workflow for the [Pi coding agent](https://github.com/earendil-works/pi). It keeps the main context focused on scientific decisions and delegates noisy, self-contained work — literature search, repository inspection, implementation, adversarial review — to isolated subagent contexts, while durable knowledge lives in project files committed to git.

It provides two things:

- **`global/`** — operating rules that make every Pi session a disciplined scientific researcher.
- **`project-template/`** — a scaffold that turns any repository into a reproducible research project.

## Repository layout

```text
pi-research-agent/
├── global/                                   # Install once; applies to all Pi sessions
│   ├── AGENTS.md                             #   Global research operating rules
│   └── settings.agenticoding.example.json    #   Optional: disable context compaction
├── project-template/                         # Scaffold for a research repository
│   ├── AGENTS.md                             #   Per-project research context
│   ├── research/                             #   Durable research notes
│   │   ├── PROBLEM.md                        #     Problem, gap, target claim, success criteria
│   │   ├── HYPOTHESES.md                     #     Competing hypotheses + discriminating predictions
│   │   ├── LITERATURE.md                     #     Verified sources only
│   │   ├── FINDINGS.md                       #     Observations, not narratives
│   │   └── DECISIONS.md                      #     GO / NO-GO / INCONCLUSIVE / PIVOT
│   └── experiments/                          #   Experiment ledger
│       ├── EXPERIMENTS.md                    #     One entry per experiment (EXP-000, …)
│       └── registry.jsonl                    #     Append-only machine-readable index
├── LICENSE
└── README.md
```

## Quick start

Requires [Pi](https://github.com/earendil-works/pi) with the [`pi-web-access`](https://www.npmjs.com/package/pi-web-access) and [`pi-agenticoding`](https://www.npmjs.com/package/pi-agenticoding) extensions installed.

**1. Install the global research rules**

```bash
mkdir -p ~/.pi/agent
cp global/AGENTS.md ~/.pi/agent/AGENTS.md
```

Optional: merge `global/settings.agenticoding.example.json` into `~/.pi/agent/settings.json` to disable context compaction during long research threads.

**2. Scaffold a research project**

From your repository root:

```bash
cp project-template/AGENTS.md ./AGENTS.md
cp -r project-template/research ./research
cp -r project-template/experiments ./experiments
```

Edit `AGENTS.md` and `research/PROBLEM.md` before the first substantial run, then start a session with `pi --name "research-main"`.

## The operating model

```text
                          ┌──────────────────────────────────────────┐
                          │           main Pi                       │
                          │   scientist / orchestrator              │
                          │   keeps the scientific narrative        │
                          └──────────────────────────────────────────┘
                              │              │              │
               spawn           │              │           handoff
        (isolated child        │              │      (clean restart on
         context)              │              │       phase change)
              ▼                ▼              ▼
   ┌──────────────────┐ ┌────────────────┐ ┌────────────────┐
   │  literature      │ │  notebook      │ │  tmux          │
   │  search          │ │  task-scoped   │ │  long-running  │
   │  repository audit│ │  transient     │ │  experiment    │
   │  implementation  │ │  facts/        │ │  observability │
   │  adversarial     │ │  decisions     │ │  (visible, not │
   │  review          │ │  across        │ │   hidden)      │
   │                  │ │  handoffs      │ │                │
   └──────────────────┘ └────────────────┘ └────────────────┘
              │                │                    │
              └──────────────┬─┴────────────────────┘
                             ▼
        research/  &  experiments/   = durable project memory (git)
```

- **Main Pi** — scientist/orchestrator and keeper of the scientific narrative.
- **`spawn`** — isolated literature search, code audit, implementation, or adversarial review. The final scientific judgment is never delegated to a vote of subagents.
- **`notebook`** — temporary, task-scoped facts and decisions across handoffs.
- **`handoff`** — deliberate clean restart when the phase changes or context becomes noisy.
- **`tmux`** — long-running experiment observability; do not hide long experiments in opaque background jobs.
- **`research/` and `experiments/`** — durable project memory, committed to git.

> Do not add more infrastructure until a concrete recurring failure justifies it.

## The research artifacts

### research/ — durable notes

| File | Purpose |
|---|---|
| `PROBLEM.md` | Problem, why it matters, current gap, target claim, non-goals, success criteria. |
| `HYPOTHESES.md` | Competing hypotheses with mechanism, discriminating predictions, and confounders. |
| `LITERATURE.md` | Verified sources only, each with what it establishes and the open question it leaves. |
| `FINDINGS.md` | Observations, not narratives; each points to an experiment ID or artifact. |
| `DECISIONS.md` | GO / NO-GO / INCONCLUSIVE / PIVOT with evidence and rejected alternatives. |

### experiments/ — ledger

| File | Purpose |
|---|---|
| `EXPERIMENTS.md` | One entry per experiment: question, predictions, falsification criterion, controls, reproducibility record, results, validity checks, decision. |
| `registry.jsonl` | Append-only machine-readable index of experiments. |

**Workflow**: update `HYPOTHESES.md` and `EXPERIMENTS.md` *before* a nontrivial experiment; update `FINDINGS.md` and `DECISIONS.md` *after* results arrive.

## Security

Review third-party extensions before installing them — Pi packages run with the permissions of the Pi process. Never commit API keys.

## License

MIT © 2026 D11PMIND
