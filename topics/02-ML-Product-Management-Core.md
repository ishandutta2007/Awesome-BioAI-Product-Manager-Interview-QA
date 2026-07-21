# Topic 02: ML Product Management Core

## Overview
Model lifecycle management, PRD writing for ML products, eval-driven development, and the unique product management discipline required for probabilistic systems.

---

### Q1: How does writing a PRD for an ML-powered BioAI feature differ from a traditional deterministic software PRD?

**A:**
**Traditional PRD:** Specifies exact expected behavior — given input X, system does Y, testable via binary pass/fail acceptance criteria.

**ML-powered BioAI PRD must additionally specify:**
1. **Performance target with explicit uncertainty bounds:** Not "the model predicts binding affinity" but "the model achieves Spearman correlation ≥0.6 against wet-lab validation on held-out, temporally-split data, with documented performance degradation characterized for out-of-distribution inputs"
2. **Failure mode behavior:** What happens when the model is uncertain or wrong? Does it abstain, flag low confidence, or silently return a point estimate? This is a first-class product decision, not an ML engineering afterthought
3. **Ground truth definition and its limitations:** Explicitly document what "correct" means (which assay, which dataset) and where that ground truth itself is noisy or biased — the PRD should not implicitly treat imperfect labels as ground truth
4. **Human-in-the-loop workflow specification:** For most BioAI products, especially clinical/discovery-critical ones, the PRD must specify exactly where and how a human expert reviews/overrides model output, not just "the model will help scientists"
5. **Retraining/drift monitoring triggers:** Since biological data distributions shift (new assay protocols, new target classes), the PRD should specify what monitoring exists to detect when the shipped model's real-world performance diverges from validation performance
6. **Regulatory classification implications:** For clinical-facing features, the PRD must state upfront whether the feature could be construed as SaMD, since this changes the entire development/validation process required before ship

**Key mindset shift:** A traditional PRD defines what the system does; a BioAI PRD must also define what the system doesn't know it doesn't know, and how that uncertainty surfaces to the user.

### Q2: Describe "eval-driven development" for a BioAI product and how a PM should be involved in building evaluation sets.

**A:** Eval-driven development treats a rigorous, representative evaluation set as a first-class product artifact — built and maintained with the same care as the product itself — rather than an ML-engineering implementation detail assembled late in development.

**PM's role in building evals:**
1. **Define what "good" means in product terms, translated into measurable criteria:** E.g., for a variant pathogenicity classifier, "good" might mean "correctly flags known pathogenic variants from ClinVar at ≥95% sensitivity while keeping VUS-reclassification-triggering false positives below X% " — a PM should drive this translation from user value to measurable target, in partnership with ML/science leads
2. **Ensure eval set represents real deployment distribution, not just convenient benchmark data:** A common failure mode is evaluating on a well-curated academic benchmark that doesn't reflect the messiness (batch effects, missing data, novel chemical space) of actual customer data — PM should push for eval sets sourced from realistic/representative conditions, including adversarial or edge cases customers will actually encounter
3. **Maintain eval set integrity over time:** As the product evolves, ensure the eval set doesn't quietly become "the test the current model happens to pass" (eval set leakage/overfitting to the benchmark) — PMs should sponsor periodic eval set refresh/expansion as a roadmap item, not treat it as one-time setup
4. **Segment evals by customer-relevant strata:** Aggregate metrics hide differential performance — a PM should insist on evals segmented by the dimensions that matter commercially/scientifically (e.g., performance by target class, by data modality, by customer tier) to catch problems aggregate metrics would mask
5. **Tie evals to business/scientific decision thresholds:** Rather than "higher is always better," define the specific performance threshold at which the product becomes commercially/scientifically viable for a given use case, and treat crossing that threshold as the actual ship-readiness gate

### Q3: How do you prioritize a BioAI product roadmap when the biggest lever for improvement is more/better training data rather than model architecture, but data acquisition (wet-lab experiments) is slow and expensive?

**A:**
**Framework:**
1. **Quantify the marginal value of data vs. architecture improvements empirically:** Run learning curve analysis (performance vs. training set size) to estimate whether the product is in a data-limited or architecture-limited regime — this determines whether ML engineering effort or data acquisition investment is the higher-leverage roadmap bet, and should be revisited periodically as both evolve
2. **Active learning / experimental design integration:** Rather than treating data acquisition as an undifferentiated cost, prioritize acquiring the *most informative* data points (uncertainty sampling, diversity sampling) — this is a core product lever a PM should champion, turning "we need more data" into "we need to run the specific 200 experiments that will most reduce model uncertainty in the region customers actually care about"
3. **Data partnership/licensing strategy as a roadmap item:** Evaluate whether externally licensed or partner-generated data (e.g., a pharma partner's proprietary assay data) can substitute for or accelerate internally-generated data, weighing exclusivity/competitive-moat trade-offs
4. **Synthetic/simulation data as a bridge, with explicit validation:** For some domains (e.g., molecular dynamics-derived features), simulation can supplement real data — but the PM must ensure the roadmap includes validating that simulation-augmented performance actually transfers to real wet-lab/clinical outcomes, not just offline benchmark improvement
5. **Sequencing the roadmap around the DMTA cycle cadence:** Since wet-lab data generation happens in discrete batches (not continuously, like user-generated software data), the roadmap should be structured around those batch cycles — e.g., "next model iteration ships after the Q3 assay campaign returns," rather than a continuous-deployment cadence borrowed from typical SaaS PM practice

### Q4–Q16: (Representative additional topics)
- Model versioning and its product/customer communication implications
- Building trust with technical (ML/bio) stakeholders as a PM without a matching technical background
- Feature flagging and gradual rollout strategies for model updates in regulated contexts
- Defining "model performance" SLAs in customer contracts for BioAI products
- Managing model deprecation/sunsetting when a newer model version changes behavior
- A/B testing challenges unique to low-volume, high-stakes BioAI use cases
- Balancing model interpretability requirements against raw predictive performance
- Prioritization frameworks adapted for scientific/clinical impact vs. typical RICE/ICE scoring
- Working with ML engineers on technical debt vs. feature velocity trade-offs in a research-heavy environment
- Translating academic paper claims into realistic product roadmap commitments
- Handling stakeholder pressure to ship model capabilities ahead of adequate validation
- Structuring a minimum viable model (MVM) analogous to MVP for early BioAI product validation

---

## Summary
ML product management for BioAI requires embedding uncertainty, evaluation rigor, and domain-specific data-generation realities into the core PM toolkit — a PRD, roadmap, or prioritization framework borrowed unmodified from typical SaaS product management will systematically underserve the unique demands of probabilistic, biology-grounded products.
