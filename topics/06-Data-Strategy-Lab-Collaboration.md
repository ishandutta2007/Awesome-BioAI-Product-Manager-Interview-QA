# Topic 06: Data Strategy & Lab Collaboration

## Overview
Data licensing/moats, wet-lab/dry-lab feedback loops, active learning, and the unique data strategy challenges of biological ML products.

---

### Q1: What makes data strategy for BioAI products fundamentally different from typical consumer/enterprise SaaS data strategy, and how should a PM think about building a defensible data moat?

**A:**
**Key differences:**
1. **Data generation is expensive and slow, not free/incidental:** Unlike consumer products where usage generates data as a byproduct, biological training data typically requires deliberate, costly wet-lab experimentation — there's no equivalent of "users clicking around generates useful signal for free"
2. **Data is often small-N and high-dimensional:** Even well-funded discovery programs may generate hundreds to low-thousands of high-quality labeled data points per campaign, not millions — this fundamentally changes what modeling approaches are viable and how much a marginal data point is worth
3. **Batch effects and reproducibility are pervasive:** Biological/experimental data carries systematic noise from assay conditions, reagent lots, and operator variation that has no clean analogue in typical software telemetry data — a naive "more data is better" assumption can be actively wrong if new data introduces uncontrolled batch effects
4. **Proprietary data often carries partner/IP entanglement:** Data generated in partnership with a pharma customer may have contractual restrictions on reuse across other customers, directly constraining the classic SaaS playbook of pooling all customer data to improve a shared model

**Data moat strategy framework:**
1. **Own the data generation loop, not just the data itself:** A defensible moat increasingly comes from owning a proprietary, high-throughput data generation capability (e.g., an automated wet-lab pipeline generating novel training data continuously) rather than a static dataset that competitors could eventually license or replicate
2. **Prioritize data that's expensive/slow for competitors to replicate:** Public datasets and easily-licensed data provide little defensibility; proprietary experimental campaigns targeting genuinely novel chemical/biological space are harder to replicate quickly
3. **Structure partnership data rights deliberately, with the PM at the table:** Data licensing/access terms in customer or partner contracts directly determine whether data can improve a shared platform model or is siloed per-customer — this is a strategic product decision requiring PM involvement in deal structuring, not purely a legal/BD matter
4. **Active learning as a capital-efficiency multiplier, not just a modeling technique:** Since each data point is expensive, prioritizing which experiments to run based on expected model uncertainty reduction (rather than broad/undirected data generation) directly improves the capital efficiency of the data moat-building process — a PM should treat the active learning strategy as core to the data roadmap, not an ML implementation detail

### Q2: Design the feedback loop architecture connecting a computational prediction product to a wet-lab validation process. What product decisions determine whether this loop actually accelerates the model over time?

**A:**
**Core loop:**
```
Model generates ranked predictions/candidates
  → Scientist selects subset for wet-lab testing (real-world selection bias enters here)
  → Wet-lab experiment generates new labeled data (with assay-specific noise/limitations)
  → New data fed back into training set
  → Model retrained/updated
  → Repeat
```

**Product decisions that determine whether this loop actually improves the model:**
1. **Capturing negative/non-selected data, not just wet-lab results:** If only scientist-selected candidates get tested, the model never learns from its false negatives (correctly-scored-low candidates that might have worked) — a well-designed product should periodically inject some model-recommended-low or diverse candidates into the test set specifically to combat this selection bias, even though it's less immediately efficient for the current discovery campaign
2. **Structuring feedback capture to minimize friction for scientists:** If logging wet-lab results back into the system requires manual, tedious re-entry, the feedback loop will leak data and slow down — integration with existing LIMS/ELN systems to auto-capture results (rather than requiring parallel manual logging) is a high-leverage product investment
3. **Explicit versioning and provenance tracking of what model version generated which recommendation:** Without this, it becomes impossible to later attribute wet-lab outcomes to the correct model version for accurate retraining/evaluation — an easy-to-overlook data architecture requirement that a PM should insist on from the start
4. **Batch-aware retraining cadence aligned to real experimental cycles:** Retraining on a continuous/streaming basis doesn't match how wet-lab data actually arrives (in discrete campaign batches) — the product roadmap and infrastructure should be designed around realistic batch cadences (e.g., retrain after each completed assay campaign) rather than over-engineering for a continuous-learning paradigm that doesn't match the actual data generation rhythm
5. **Measuring loop velocity as a product metric:** Track and actively work to reduce the cycle time from "model prediction" to "validated result back in training set" — this cycle time is often the single biggest lever on how fast the product actually improves, and is frequently more tractable to improve through better tooling/integration than through better model architecture

### Q3–Q15: (Representative additional topics)
- Public dataset landscape awareness (ChEMBL, PDB, UniProt, GEO) and their appropriate/inappropriate uses
- Data quality auditing processes for incoming wet-lab data before training set inclusion
- Managing multi-tenant data isolation vs. shared model improvement trade-offs for platform products
- Synthetic data generation strategy and validating its real-world transfer
- Building trust with bench scientists to encourage genuine engagement with AI-suggested experiments
- LIMS/ELN integration architecture and its product prioritization
- Data versioning and reproducibility infrastructure as a product requirement
- Negotiating data rights in pharma partnership/co-development deals
- Handling proprietary competitor data leakage risk in shared/platform data models
- Building internal data literacy/trust among non-technical scientific stakeholders

---

## Summary
Data strategy is arguably the single highest-leverage product decision area in BioAI, given how expensive and slow biological data generation is — PMs who treat data strategy as a core, deliberately-designed product surface (not an ML-team implementation detail) build meaningfully more defensible and faster-improving products.
