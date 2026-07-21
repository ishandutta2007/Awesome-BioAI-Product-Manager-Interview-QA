# Topic 11: Troubleshooting & Failure Modes

## Overview
Diagnosing model drift, silent product failures, and conducting structured postmortems for BioAI product incidents.

---

### Q1: Three months post-launch, a customer reports that a diagnostic model's predictions have become noticeably less reliable, but your offline validation metrics (run on the original test set) still show unchanged performance. Walk through your troubleshooting approach.

**A:**
**Systematic troubleshooting framework:**
1. **Recognize this as a likely distribution shift/drift issue, since static offline metrics can't detect it by definition:** If the original test set is unchanged, unchanged performance on it is expected regardless of real-world drift — this is the core diagnostic trap: the absence of a metric moving doesn't mean the absence of a problem, when the metric can't see the relevant change
2. **Characterize what has changed in the real-world input distribution since launch:** Common culprits include upstream data source changes (e.g., a lab changed assay protocol or equipment, an EHR system upgrade changed how a field is populated), population shift (different patient/sample mix than validation data), or seasonal/temporal effects not represented in the original validation window
3. **Pull a fresh, recent sample of real-world predictions with outcomes (if available) to directly measure current performance:** This is the most direct diagnostic — if recent real-world performance has genuinely degraded relative to the original validation performance, this confirms drift rather than a perception/communication issue
4. **Check for silent input pipeline changes:** A surprisingly common root cause is an upstream data pipeline change (e.g., a unit conversion bug, a schema change in an integrated system) that alters input data in a way the model wasn't trained to handle, without any change to the model itself — differentiate "model drift" from "input pipeline defect," since these require very different fixes
5. **Investigate whether the complaint reflects an actual accuracy problem or a trust/communication problem:** Sometimes "predictions feel less reliable" reflects a user noticing a few salient errors (availability bias) rather than genuine aggregate performance decline — this requires careful, non-dismissive investigation, since both possibilities require different but real responses

**Resolution and prevention:** This scenario is a strong argument for implementing continuous production monitoring (comparing live prediction distributions and, where ground truth eventually becomes available, live accuracy against the validation baseline) rather than relying solely on static pre-launch validation — the product/engineering roadmap should treat drift monitoring as a required post-launch capability, not an optional enhancement.

### Q2: Case study — A generative molecule design tool is found, several months after launch, to be systematically avoiding a specific useful region of chemical space due to a subtle bias in its training data. How do you handle the immediate response and the broader postmortem?

**A:**
**Immediate response:**
1. **Assess real-world impact before broad internal alarm or external communication:** Determine how many active customers/campaigns may have been affected, and whether the bias caused actual missed opportunities (e.g., a customer's target class fell in the avoided region) or was largely inconsequential for current usage patterns — this shapes the urgency and scope of response appropriately rather than reflexive overreaction or underreaction
2. **Communicate proactively and honestly with affected customers, calibrated to actual impact:** If specific customers' campaigns were plausibly affected, a direct, transparent conversation (what was found, likely impact, remediation plan) preserves trust far better than customers discovering it independently or through vague/delayed communication
3. **Implement an interim mitigation while the underlying fix is developed:** This might mean flagging the known-biased region explicitly in the product UI (transparency about the limitation) while a data/retraining fix is in progress, rather than either silently continuing to ship the biased behavior or pulling the entire product unnecessarily if the issue is scoped and manageable

**Broader postmortem (blameless, process-focused):**
1. **Root-cause the bias's origin precisely:** Was this a training data collection gap (certain chemical space simply underrepresented in source data), a labeling/curation bias, or an evaluation gap (the eval set, per Topic 02 Q2, didn't include this region and so couldn't have caught it)? The fix and prevention strategy differ significantly depending on which
2. **Assess why existing evaluation/QA processes didn't catch this before launch:** This is the most important postmortem question — if eval sets are systematically representative of only "well-known" chemical space (a very plausible bias, since well-characterized data is exactly what's easiest to collect and curate), this is a structural gap likely to recur with other products unless the evaluation methodology itself is improved
3. **Distinguish individual accountability from systemic process gaps:** A blameless postmortem culture focuses on "what about our process allowed this to ship undetected" rather than "who missed this" — punitive postmortems discourage the honest reporting needed to catch similar issues earlier next time
4. **Update the eval-set and bias-auditing methodology as a concrete roadmap deliverable, not just a lesson-learned note:** The postmortem should produce a specific, owned action item (e.g., "add systematic chemical-space-coverage analysis as a required pre-launch gate for all future generative chemistry releases"), with a named owner and timeline, not just a retrospective acknowledgment

### Q3–Q15: (Representative additional topics)
- Debugging a sudden unexplained drop in model API latency/throughput affecting customer workflows
- Investigating a customer-reported discrepancy between model output and their own internal validation
- Root-causing a training data leakage issue discovered after a suspiciously high-performing model launch
- Handling a security/data breach incident affecting proprietary customer training data
- Troubleshooting inconsistent model behavior between staging/validation and production environments
- Postmortem for a missed regulatory submission deadline caused by late-discovered validation gaps
- Diagnosing why a well-validated model isn't achieving expected adoption/usage post-launch
- Investigating a partner/customer's claim that the product provided harmful or unsafe guidance
- Root-causing model performance degradation traced to an upstream vendor API/data source change
- Handling public/scientific community criticism of a published model validation claim

---

## Summary
Troubleshooting BioAI product failures requires distinguishing genuine model/data problems from pipeline defects, communication gaps, or perception issues — and treating postmortems as blameless, process-improvement exercises that produce concrete prevention commitments rather than one-off incident reports.
