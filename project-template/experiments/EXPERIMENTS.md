# Experiment Ledger

## EXP-000 — <short name>

Date: YYYY-MM-DD
Status: planned | running | complete | invalid
Decision role: sanity-check | hypothesis-test | ablation | scale-up

### Question
<What uncertainty does this experiment resolve?>

### Hypotheses and predictions
- H1 predicts: <...>
- H0/H2 predicts: <...>
- Falsification criterion: <...>

### Controls / confounders
- Baseline/control: <...>
- Main confounders checked: <...>

### Reproducibility
- Git commit: <sha>
- Model/checkpoint: <...>
- Dataset/split/version: <...>
- Config: `experiments/configs/<...>`
- Seeds: <...>
- Command:
```bash
<command>
```
- Logs/output: `experiments/results/<...>`

### Results
<Fill only after run. Include uncertainty/variance where relevant.>

### Validity checks
- Baseline reproduced: yes/no
- All intended runs completed: yes/no
- Known anomalies: <...>

### Interpretation
<What the result establishes and does not establish.>

### Decision
GO | NO-GO | INCONCLUSIVE

### Next action
<Only if tied to a specific remaining uncertainty.>
