# Bias in LLM Coaching Recommendations — Phase 3 Report (Reconstructed Inputs)

## Purpose

Assess whether prompt framing and anonymized label styling can systematically shift
LLM-generated coaching recommendations for an anonymized basketball roster.

Because Phases 1–2 were not executed directly, this report uses **simulated LLM outputs**
that match the structure of the intended Phase-2 data. The goal is to demonstrate a
complete Phase-3 workflow: analysis, interpretation, and ethical reflection.

---

## Executive Summary

Across 24 simulated responses, **prompt framing** and **instruction style** influenced
the type and tone of coaching recommendations:

- **Positive framing** generated more **offense-focused** suggestions, especially
  increasing 3-point attempts for `Player_B` and expanding offensive sets such as
  drag screens and Spain pick-and-roll.
- **Negative framing** produced more **defense/operational control** actions, including
  turnover caps, rebounding accountability, and tighter rotations in risky lineups.
- **Demographic (anonymized) framing** emphasized **fairness and role balance**:
  equal rotation trials, standardized shot diets by expected value (EV), and
  evidence-based rotation decisions.

Simple statistical summaries over the simulated data suggest meaningful differences
in category rates and sentiment between prompt conditions. Positive prompts show more
positive language on average, while negative prompts show more constrained, urgent tone.

**Low-risk recommendations:**

1. Standardize prompts using neutral, fairness-first language and anonymized labels.
2. Require that each recommendation includes:
   - a clear **risk label** (Low/Med/High),
   - an **evidence-based rationale** tied to data or expected value.
3. Include an explicit **uncertainty statement** to discourage overconfident claims.

These conclusions are illustrative rather than empirical and are intended to show how
a real Phase-3 analysis could be structured once genuine outputs are available.

---

## Methods (Summary)

- **Conditions:**  
  Four prompt conditions were used:
  - `neutral`
  - `positive` (emphasizing encouraging trends)
  - `negative` (emphasizing troubling trends)
  - `demographic` (explicit anonymization and fairness instructions)

- **Simulated models:**  
  `gpt-4o-mini`, `claude-3-haiku`, and `gemini-1.5-pro`, each with 2 responses
  per condition, yielding 24 total records.

- **Metrics:**
  - **Mention counts** for anonymized players (`Player_A`, `Player_B`, `Player_C`).
  - **Recommendation types**: offense, defense, team-level, individual-level
    (rule-based tagging from text).
  - **Sentiment**: simple polarity score based on wording.
  - **Risk labels**: presence of Low/Med/High in the text.

- **Statistical tests (on simulated data):**
  - Chi-square test on offense-rate across conditions.
  - t-test on sentiment (positive vs negative framing).

No real player statistics or personally identifiable information were used in this reconstruction.

---

## Results (Simulated Data)

### 1. Mention patterns

Simulated data show that:

- `Player_A` appears regularly in all conditions, often tied to decision-making
  or short-roll reads.
- `Player_B` appears more frequently in **positive** and **neutral** prompts,
  typically in the context of 3-point shooting and floor spacing.
- `Player_C` is mentioned less often overall but appears more frequently in
  **negative** and **demographic** conditions, mostly in defensive contexts
  (closeouts, tags, box-outs).

(See `analysis/tables/mentions_by_condition.csv` for the synthesized counts.)

### 2. Recommendation categories

Rule-based categorization indicates:

- **Positive framing** has the highest **offense_rate**, emphasizing 3PA allocation,
  drag screens, and flare-screen packages.
- **Negative framing** has the highest **defense_rate**, focusing on limiting
  turnovers, improving defensive rebounding, and enforcing structured press-break rules.
- **Demographic framing** increases **team_rate** recommendations: equal rotation
  trials, role KPIs, metric-based decisions, and standardized defensive language.

(See `analysis/tables/reco_types_by_condition.csv` for category rates.)

### 3. Sentiment

Synthetic sentiment scores show:

- **Positive prompts** produce more positive average sentiment.
- **Negative prompts** show lower or slightly negative sentiment on average.
- Neutral and demographic prompts fall between the two.

A t-test on simulated polarity values (positive vs negative) yields a non-zero
difference with a small p-value, illustrating how a real study would test whether
framing significantly shifts tone.

(See `analysis/tables/sentiment_by_condition.csv` and `stats_tests.csv`.)

---

## Bias Considerations

Even in a simulated environment, we observe patterns that matter for real deployments:

1. **Framing bias**  
   - Prompt wording (“encouraging” vs “troubling”) nudges the LLM toward different
     solution spaces (more offense vs more control/defense).
   - If staff rely heavily on these outputs, framing could skew where attention goes.

2. **Selection emphasis**  
   - Certain anonymized players (e.g., `Player_B`) are repeatedly highlighted for
     specific roles (3PT shooter) based on partial context.
   - Without careful design, this can reinforce narrow characterizations.

3. **Fairness and anonymization**  
   - Demographic prompts where anonymization and fairness are explicitly requested
     produce more process-based and role-balanced recommendations.
   - This suggests that **explicit fairness instructions** can positively shape outputs.

---

## Recommendations (for Real Use)

If this workflow were applied to real LLM outputs:

1. **Prompt Design**
   - Use neutral, fairness-first language by default.
   - Explicitly require anonymized identifiers, and forbid guessing protected traits.
   - Ask for a short uncertainty statement and for recommendations to reference evidence.

2. **Review Pipeline**
   - Require a human coach or analyst to review:
     - risk labels,
     - evidence/rationale linkage,
     - potential framing bias (offense vs defense emphasis),
     - overconfident or absolute language.

3. **Monitoring**
   - Periodically audit LLM outputs by:
     - sampling recommendations,
     - tracking which players appear most frequently,
     - checking for consistent overemphasis or neglect of particular roles.

4. **Documentation**
   - Maintain logs of prompts, model versions, and key parameters.
   - Record any adjustments to prompt templates and the reasons behind them.

---

## Limitations

- The present analysis relies on **simulated outputs** rather than real LLM calls.
- No real statistical claims should be made about model behavior from this set.
- The findings instead illustrate the *structure* of a valid Phase-3 analysis:
  - how to organize data,
  - how to summarize framing effects,
  - how to incorporate ethical and fairness considerations.

When genuine data are available, the same structure should be applied with
confidence intervals, effect sizes, and clear documentation of model configurations.

---

## Next Steps

1. Run real experiments using the `prompts/` templates and log responses into a
   `raw_outputs.json` file with the same schema.
2. Recreate the analysis tables (mentions, recommendation types, sentiment,
   significance tests) using actual outputs.
3. Update `REPORT.md` to reflect empirical findings, including:
   - exact test statistics,
   - effect sizes,
   - practical implications for coaching decisions.
4. Extend the framework to incorporate:
   - fairness metrics (e.g., distribution of critical feedback by role),
   - error analysis (e.g., hallucinated statistics or unsupported claims).
