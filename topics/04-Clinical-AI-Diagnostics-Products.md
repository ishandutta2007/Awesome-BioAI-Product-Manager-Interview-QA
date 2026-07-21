# Topic 04: Clinical AI & Diagnostics Products

## Overview
Imaging AI, EHR-based risk models, point-of-care diagnostics, and the unique clinical-workflow-integration demands of patient-facing AI products.

---

### Q1: How do you scope a clinical decision support (CDS) AI product to avoid both "alert fatigue" failure and "clinically useless because too conservative" failure?

**A:** This is a core calibration tension in clinical AI product management — a model tuned to catch every possible case generates excessive false positives that clinicians learn to ignore (alert fatigue, well-documented in EHR CDS literature), while a model tuned for high precision may miss cases that matter or add little value beyond existing clinical judgment.

**Product scoping approach:**
1. **Anchor on the specific clinical decision point and action, not general "risk prediction":** A vague product ("predicts patient risk") is impossible to calibrate correctly; a precisely scoped product ("flags patients for early sepsis workup within a 6-hour actionable window, calibrated against the clinical team's actual capacity to respond") has a concrete precision/recall trade-off that can be reasoned about against real workflow constraints
2. **Involve target clinical users in threshold-setting, not just data scientists:** The "right" sensitivity/specificity trade-off is a clinical workflow and risk-tolerance decision, not a purely statistical one — PMs should facilitate structured elicitation with clinician stakeholders (e.g., "how many false positives per true positive is tolerable given your team's staffing") rather than let the ML team pick a threshold that optimizes an abstract F1 score
3. **Design for alert tiering, not binary alert/no-alert:** Many successful clinical AI products use graduated confidence tiers (e.g., passive dashboard flag vs. interruptive alert) matched to actionability and confidence, rather than a single threshold — this is a product design lever independent of raw model performance that significantly affects real-world adoption
4. **Measure and iterate on real-world alert response rates post-launch, not just pre-launch validation metrics:** Alert fatigue is often only observable after deployment at realistic volume — the product roadmap should include a structured post-launch monitoring period with explicit commitment to threshold recalibration based on observed override/dismissal rates
5. **Explicitly design the override/feedback loop:** Every alert dismissal is a data point — product architecture should capture clinician override reasons (structured, not just a dismiss button) to enable both model improvement and threshold recalibration over time

### Q2: What's the difference between a clinical AI product that requires FDA clearance as SaMD and one that doesn't, and how does this shape product scoping decisions early?

**A:** The FDA's Clinical Decision Support (CDS) software guidance (following the 21st Century Cures Act's CDS carve-out) distinguishes non-device CDS from regulated SaMD based on four criteria — a product must meet ALL of them to qualify for the non-device exemption:

1. Does not acquire, process, or analyze a medical image or signal from an in vitro diagnostic device or pattern from a signal acquisition system (i.e., not analyzing raw physiological signals/images)
2. Displays, analyzes, or prints medical information about a patient or other medical information
3. Provides recommendations to a clinician, rather than specific directive outputs
4. Enables the clinician to independently review the basis for the recommendation (i.e., the clinician can understand and evaluate the underlying rationale, not just receive a black-box output)

**Product scoping implications:**
- A product analyzing raw imaging/signal data (e.g., detecting abnormalities in a chest X-ray) almost always falls under SaMD regulation regardless of the other criteria — this triggers the full FDA clearance pathway (510(k)/De Novo/PMA depending on risk classification) before commercial launch
- A product summarizing/displaying existing structured EHR data with transparent, clinician-reviewable logic (e.g., a rules-based or simply-interpretable risk score with visible contributing factors) has a plausible path to non-device CDS status — but PMs should not assume this without formal regulatory consultation, since the "independently review the basis" criterion is often the crux of borderline cases
- **Black-box deep learning models are structurally disadvantaged for non-device CDS status** under criterion 4 — if a PM wants to avoid the SaMD regulatory pathway, this is a strong argument for architecting toward inherently interpretable models or robust explainability tooling from the start, not as a retrofit
- **Early regulatory classification determines the entire development timeline and validation rigor required** — a PM who scopes a product assuming non-device status, only to have regulatory/legal determine SaMD applies well into development, faces a costly and often product-redefining pivot; regulatory classification should be assessed at the concept stage, not after building

### Q3: How do you design a rollout/validation strategy for a clinical AI product across health systems with very different EHR configurations and clinical workflows?

**A:**
**Core challenge:** Unlike typical B2B SaaS where a product mostly works uniformly across customers, clinical AI models trained/validated on one health system's data (with its specific patient population, EHR configuration, documentation patterns, and lab reference ranges) frequently underperform when deployed to a different health system — a well-documented generalization failure mode in clinical ML literature.

**Rollout strategy:**
1. **Local validation before full deployment at each new site, not just initial validation:** Product rollout plan should include a defined local validation period (silent/shadow mode, comparing model output against actual outcomes without clinical action) at each new health system before the model influences care — this should be budgeted into the go-to-market timeline as a required step, not an optional nice-to-have
2. **Explicit EHR/data harmonization requirements as part of onboarding:** Since input data (lab units, coding systems, documentation templates) varies across EHR instances (even the same EHR vendor's product configured differently by different health systems), the product's technical onboarding process must include a data mapping/harmonization step, with a PM-owned checklist ensuring this isn't skipped under deployment time pressure
3. **Site-specific performance monitoring dashboards, not just aggregate multi-site metrics:** Post-launch monitoring should be able to detect a specific site's performance degrading even if aggregate performance across all sites looks acceptable — this is essential for catching site-specific integration or population-mismatch issues early
4. **Design for local recalibration, not just retraining:** Lightweight recalibration (e.g., adjusting decision thresholds to local population base rates) is often more practical and faster to validate than full model retraining per site — the product architecture should support this as a first-class deployment capability
5. **Clear escalation/rollback criteria defined before rollout, not improvised during a crisis:** Define in advance what performance degradation threshold triggers automatic rollback to shadow mode or full deactivation at a given site, so this decision isn't made reactively under pressure when a real-world issue surfaces

### Q4–Q15: (Representative additional topics)
- Imaging AI product design (radiology, pathology) and PACS/workflow integration
- Reimbursement/CPT coding strategy as a product go-to-market dependency
- Clinical validation study design for a diagnostic AI product (retrospective vs. prospective)
- Health equity/bias auditing as a required product development gate, not an afterthought
- Explainability UX design for clinician-facing AI outputs (SHAP visualizations, natural language rationale)
- Point-of-care diagnostic AI product constraints (edge deployment, connectivity, CLIA waiver considerations)
- Clinical workflow mapping methodology (shadowing, time-motion studies) before product design
- Post-market surveillance product requirements for deployed clinical AI (adverse event monitoring)
- Multi-stakeholder buying process navigation (CMIO, clinical champions, procurement, IT security)
- Designing for clinician trust calibration (avoiding both over-reliance/automation bias and under-utilization)

---

## Summary
Clinical AI product management requires treating regulatory classification, cross-site generalization, and clinician trust calibration as core product design constraints from day one — these are not compliance checkboxes layered on afterward but fundamental shapers of what the product can credibly promise and how it must be built.
