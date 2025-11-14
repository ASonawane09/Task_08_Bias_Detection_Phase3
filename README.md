# Task 08 — Phase 3 (Bias Detection in LLM Outputs) — Reconstructed Inputs

This repository delivers **Phase 3** of the Task 08 assignment: analyzing potential bias
in large language model (LLM) coaching recommendations.

Because Phases 1–2 were not run directly, this project uses **simulated Phase-2 outputs**
that match the intended schema (prompt labels, models, temperatures, iterations, text).
That allows us to demonstrate a complete Phase-3 workflow (analysis and reporting)
without committing any datasets or personally identifiable information.

## 📦 What’s included

- `results/raw_outputs.json`  
  Simulated LLM responses (24 records) across 4 conditions:
  - `neutral`
  - `positive`
  - `negative`
  - `demographic` (anonymized, fairness-focused)

- `prompts/`  
  Prompt templates for each condition, using anonymized identifiers (`Player_A`, …).

- `docs/REPORT.md`  
  Stakeholder-facing Phase-3 report summarizing methods, results, and ethical implications.

- `docs/PROCESS.md`  
  Process notes explaining how the inputs were reconstructed and how to plug in real data later.

- `analysis/tables/`  
  Example derived tables (CSV) summarizing mention counts, recommendation types,
  sentiment, and simple statistical tests. These are consistent with the simulated data.

> No real game data or PII are stored in this repository. All players are anonymized.

## 🔒 Data & Privacy

- No datasets are committed.
- All identifiers use anonymous labels (e.g., `Player_A`, `Player_B`).
- `.gitignore` actively prevents committing any `data/` directory or typical raw data files.

## 🔁 How to swap in real data later

If you later complete Phases 1–2 and obtain real LLM outputs:

1. Generate a JSON file with the same schema as `results/raw_outputs.json`
   (one recorded response per JSON object).
2. Overwrite `results/raw_outputs.json` with the real file (locally).
3. Re-run your own analysis scripts (not included by design here) to regenerate tables and figures.
4. Update `docs/REPORT.md` to reflect empirical results, including confidence intervals and effect sizes.

## 🧭 Intended Use

This repo is meant to:

- Demonstrate a reproducible structure for Phase-3 analysis.
- Provide a concrete example of how to:
  - organize prompt conditions,
  - store LLM outputs safely,
  - summarize potential bias patterns in a stakeholder-friendly report.

You are encouraged to extend this with your own code, results, and visualizations
as you progress with real experiments.
