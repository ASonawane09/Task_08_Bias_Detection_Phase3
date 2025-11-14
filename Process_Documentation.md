# PROCESS — Phase 3 with Reconstructed Inputs

## Goal

Implement a complete Phase-3 workflow (bias analysis and stakeholder reporting)
for Task 08, even though Phases 1–2 were not executed directly on real data.

Instead of real Phase-2 outputs, we constructed **simulated responses**
that match the intended schema. This allows the structure of Phase 3
to be demonstrated in a transparent and audit-friendly way.

---

## Reconstruction Steps

1. **Defined Conditions**
   - Four prompt conditions:
     - `neutral`
     - `positive`
     - `negative`
     - `demographic` (anonymized, fairness-focused)

2. **Created Prompt Templates**
   - Stored in `prompts/` as `.txt` files.
   - Each prompt uses anonymized identifiers (`Player_A`, `Player_B`, …).
   - All prompts explicitly instruct the model not to infer protected attributes.

3. **Simulated Phase-2 Outputs**
   - For each condition, three models were assumed:
     - `gpt-4o-mini`
     - `claude-3-haiku`
     - `gemini-1.5-pro`
   - Each (condition, model) pair has two responses (2 reps), giving 24 total records.
   - Each record includes:
     - timestamp
     - provider/model
     - prompt_label
     - iteration
     - temperature
     - placeholder prompt text
     - realistic coaching `response_text`
   - The combined set is saved in `results/raw_outputs.json`.

4. **Constructed Example Analysis Tables**
   - `analysis/tables/mentions_by_condition.csv` (anonymized player mentions)
   - `analysis/tables/reco_types_by_condition.csv` (offense/defense/team/individual rates)
   - `analysis/tables/sentiment_by_condition.csv` (average sentiment per condition)
   - `analysis/tables/stats_tests.csv` (example chi-square and t-test output)

5. **Authored Stakeholder Report**
   - `docs/REPORT.md` summarizes:
     - goals,
     - methods (with the caveat of simulation),
     - results from the synthetic data,
     - ethical and fairness considerations,
     - recommendations and limitations.

---

## How to Swap in Real Data Later

1. Run real experiments with your chosen models (e.g., GPT-4, Claude, Gemini) using
   the prompt templates in `prompts/`.
2. Save outputs into a JSON file with the same fields as `results/raw_outputs.json`:
   - `timestamp`, `provider`, `model`, `prompt_label`, `iteration`,
     `temperature`, `prompt_text`, `response_text`, `usage`, `error`.
3. Overwrite the simulated `raw_outputs.json` with your real file **locally**
   (do not commit raw data if it contains sensitive content).
4. Regenerate analysis tables and figures using your own scripts.
5. Update `docs/REPORT.md` to:
   - describe real model configurations,
   - report actual statistics (CIs, p-values),
   - describe any newly observed bias patterns.

---

## Compliance

- No datasets or PII are stored in this repository.
- All players are represented by anonymous identifiers (`Player_A`, etc.).
- `.gitignore` explicitly excludes `data/` and likely data file types.
- The repository is safe to make public and to share as part of the assignment.

This document is intended to make it easy for a third party
to understand how the reconstruction was performed and how
to replace synthetic inputs with real experiment results.
