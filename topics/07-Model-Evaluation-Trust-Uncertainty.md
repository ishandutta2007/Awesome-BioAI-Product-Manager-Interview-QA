# Topic 07: Model Evaluation, Trust & Uncertainty

## Overview
Benchmark design, calibration, uncertainty quantification, and human-in-the-loop product design for building trustworthy BioAI products.

---

### Q1: Why is calibration (not just accuracy/AUC) a critical product requirement for BioAI models, and how would you validate it?

**A:** A model can have excellent discriminative performance (AUC, accuracy) while being poorly calibrated — meaning its predicted probabilities don't match true outcome frequencies (e.g., predictions the model labels "80% confident" are only correct 50% of the time). For BioAI products where users (scientists, clinicians) make resource-allocation or clinical decisions based on stated confidence, calibration failure directly produces bad real-world decisions even when the underlying ranking/discrimination is good.

**Why this matters specifically in BioAI:**
- A discovery scientist deciding which of 20 model-suggested candidates to prioritize for expensive wet-lab testing is implicitly trusting the model's confidence scores to allocate limited experimental budget — miscalibration directly wastes resources
- A clinical risk model's stated probability may directly inform a clinician's or patient's risk communication — a poorly calibrated "70% risk" that's actually a 40% risk has direct patient-communication and trust consequences
- Miscalibration often gets *worse*, not just stays constant, for out-of-distribution inputs — exactly the novel candidates/patients a discovery or diagnostic product is often most valuable for helping with

**Validation approach:**
1. **Reliability diagrams / calibration curves:** Plot predicted probability bins against observed outcome frequency in held-out data — should track the diagonal for well-calibrated models
2. **Expected Calibration Error (ECE) as a tracked product metric:** Not just reported once at model validation, but monitored continuously as part of production model quality dashboards
3. **Stratified calibration checks:** Verify calibration holds not just in aggregate but within relevant subgroups (e.g., by target class, by patient demographic) — a model calibrated in aggregate can still be systematically miscalibrated for specific important subgroups
4. **Recalibration as a lightweight, frequently-deployed fix:** Techniques like Platt scaling or isotonic regression can often correct calibration without full retraining — a PM should ensure the product roadmap includes this as a fast, low-cost lever distinct from the slower full-retraining cycle

### Q2: How do you design a product's uncertainty communication (e.g., confidence scores, prediction intervals) so users calibrate their trust appropriately, rather than either over-trusting or ignoring it entirely?

**A:**
**Core tension:** Users of AI-powered scientific/clinical tools tend toward two failure modes — automation bias (over-trusting model output, especially when it's presented confidently or when the user is under time pressure) or blanket distrust/ignoring (if uncertainty communication is confusing, inconsistent, or the user has been burned by a past overconfident wrong prediction).

**Design principles:**
1. **Match uncertainty presentation format to the user's actual decision, not to what's easiest to compute:** A raw probability score means little to a bench scientist deciding which candidate to synthesize next — translating uncertainty into decision-relevant language (e.g., "similar confidence to compounds that historically validated at a 30% hit rate" vs. "this is genuinely novel territory the model has limited training signal for") is far more actionable than an abstract 0-1 score
2. **Visually and structurally distinguish "novel/out-of-distribution" uncertainty from "inherently noisy but well-characterized" uncertainty:** These require different user responses — the former should probably prompt extra scrutiny or a different validation approach, while the latter is more routine — conflating them into a single uncertainty number loses this actionable distinction
3. **Show uncertainty consistently, not only when it's convenient:** A product that surfaces confidence scores prominently for high-confidence predictions but buries or omits them for low-confidence predictions trains users to associate "no visible score" with implicit trustworthiness — consistency in surfacing uncertainty, even when the answer is "this model doesn't know," is essential for building calibrated trust over time
4. **Instrument and monitor real user behavior against stated confidence, not just assume the UX works:** Track whether users' actual override/acceptance behavior correlates appropriately with model confidence post-launch — if users are accepting low-confidence predictions at the same rate as high-confidence ones, the uncertainty UX has failed regardless of how mathematically correct the underlying calibration is
5. **Periodic deliberate "confidently wrong" surfacing in onboarding/training:** Showing new users real historical examples where the model was confidently incorrect (not just successes) helps calibrate appropriate skepticism from the start, rather than allowing an unearned honeymoon period of over-trust

### Q3: A discovery-stage model shows strong performance on a public benchmark (e.g., a standard molecular property prediction dataset) but customers report it underperforms on their proprietary chemical series. How do you diagnose this as a PM, and what's the product fix?

**A:**
**Diagnosis approach:**
1. **Characterize distributional shift explicitly:** Compare the customer's chemical space (scaffold diversity, property ranges, target class) against the public benchmark's distribution — public benchmarks (e.g., common molecular property datasets) often over-represent well-studied, "drug-like" chemical space relative to the novel, harder chemistry customers are often specifically trying to explore precisely because it's underexplored
2. **This is very likely a fundamental generalization gap, not a bug:** The core issue is usually that public benchmark performance was never a valid proxy for the customer's actual use case distribution — this is a product/evaluation design failure (using an unrepresentative benchmark as the primary success metric) more than a pure ML engineering bug
3. **Request/negotiate access to a small labeled validation sample from the customer's own chemical series:** Directly measuring performance on customer-representative data, even a small sample, is far more diagnostic than further public benchmark analysis

**Product fix directions:**
1. **Re-scope the product's validated claims to be honest about domain applicability:** Rather than a blanket "predicts molecular properties," the product should explicitly communicate the chemical space/target classes where validated performance exists, with appropriate caveats for out-of-domain use — this is a product marketing/positioning fix, not purely technical
2. **Build domain-adaptation/fine-tuning capability into the product as a first-class feature:** If customers routinely work in specialized chemical space, offering a structured few-shot fine-tuning or transfer-learning workflow (using a small amount of customer-labeled data) can be a genuinely differentiated product capability addressing this exact gap, not just a workaround
3. **Update the internal eval-set strategy (per Topic 02, Q2) to include diverse, representative customer-like data going forward**, so this gap is caught pre-launch for future products/versions rather than discovered reactively via customer complaints
4. **Set appropriate expectations in the sales/onboarding process:** A pre-launch pilot period explicitly measuring performance on the specific customer's data, before a full commercial commitment, both protects customer trust and generates exactly the representative validation data needed to close the gap over time

### Q4–Q15: (Representative additional topics)
- Benchmark dataset selection/curation as a product decision with real business consequences
- Out-of-distribution detection as a product feature (not just a research technique)
- Ensemble/multiple-model approaches for uncertainty estimation trade-offs
- Human-in-the-loop workflow design patterns (review, override, escalation)
- A/B testing model versions in low-volume, high-stakes deployment contexts
- Building internal "red team" evaluation processes for BioAI products before launch
- Communicating model limitations honestly to sales/marketing without undermining commercial momentum
- Longitudinal model performance monitoring and drift detection product requirements
- Explainability tooling (SHAP, attention visualization) product integration decisions
- Managing customer expectations when model performance genuinely varies significantly by use case

---

## Summary
Trust and uncertainty communication are not UX polish layered onto a finished model — they are core product design decisions that determine whether users make good decisions with an inherently probabilistic tool, and PMs must treat calibration validation and uncertainty UX with the same rigor as core feature functionality.
