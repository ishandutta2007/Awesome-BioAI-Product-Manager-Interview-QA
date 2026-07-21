# Topic 03: Drug Discovery & Computational Biology

## Overview
Target identification, protein structure/design, generative chemistry, and how AI intersects with the therapeutic discovery pipeline.

---

### Q1: Explain how AlphaFold-class structure prediction changed the drug discovery product landscape, and what product opportunities/limits remain.

**A:** Before AlphaFold2 (2020-2021), experimentally determining a protein structure (X-ray crystallography, cryo-EM, NMR) was slow (months) and expensive, and many therapeutically relevant proteins (especially membrane proteins, intrinsically disordered regions) resisted experimental structure determination entirely. AlphaFold2 and successors made high-confidence structure prediction for most single-chain proteins essentially instant and free.

**Product opportunities unlocked:**
1. **Structure-based drug design at scale:** Virtual screening/docking products could target proteins previously lacking any structural data, dramatically expanding addressable target space
2. **Downstream tool ecosystem:** Products built on top of predicted structures (binding site prediction, druggability scoring, protein-protein interaction prediction) proliferated once structure was no longer the bottleneck
3. **Protein design/engineering products:** Inverse-folding and generative design tools (e.g., RFdiffusion-class approaches) became viable product categories once reliable structure prediction/validation existed as a foundation

**Remaining limits a PM must understand:**
1. **Confidence metrics (pLDDT, PAE) are not accuracy guarantees for downstream tasks:** A high-confidence predicted structure is not the same as a structure proven correct for the specific therapeutic question (e.g., binding site conformation in a specific ligand-bound state) — product claims must carefully distinguish "confident structure prediction" from "validated for drug design purposes"
2. **Complex/dynamic biology remains hard:** Multi-state conformational ensembles, protein-protein complexes (especially transient ones), and intrinsically disordered regions are still substantially less reliable than single-chain static structure prediction — a PM must scope product claims to what's actually validated for these harder cases
3. **Structure is necessary but not sufficient for discovery success:** Even a perfectly correct structure doesn't guarantee a designed molecule will bind, be selective, be synthesizable, or have acceptable ADMET properties — product roadmaps that imply "solve structure = solve discovery" oversell the actual bottleneck, which has shifted downstream

### Q2: How would you scope and prioritize a generative chemistry product (e.g., de novo molecule generation for a target) given the gap between "generates valid molecules" and "generates molecules a medicinal chemist will actually synthesize and test"?

**A:**
**Core scoping challenge:** Generative models can trivially achieve high scores on naive metrics (chemical validity, novelty, predicted binding affinity) while producing molecules that are synthetically inaccessible, chemically unstable, or simply implausible to an experienced chemist — a classic case where the offline metric diverges sharply from real product value.

**Prioritization framework:**
1. **Anchor the core metric on synthesizability-adjusted quality, not raw generative metrics:** Integrate a synthesizability/retrosynthesis-feasibility score (e.g., SAScore or a learned retrosynthesis-based metric) as a hard filter or joint optimization objective from the start, not a post-hoc filter bolted on later
2. **Design the product around chemist review, not autonomous generation:** Frame the MVP as a chemist-in-the-loop ideation accelerant (e.g., "generate 50 candidates ranked by multi-objective score, chemist selects and refines 5") rather than an autonomous pipeline — this is both more honest about current model reliability and more aligned with how medicinal chemists actually want to work
3. **Instrument the DMTA-cycle feedback loop as the core product metric:** Track what fraction of AI-suggested molecules actually get synthesized (chemist trust/uptake) and what fraction of synthesized molecules hit target potency/selectivity bars, not just generative model offline benchmarks — this becomes the product's real north-star metric
4. **Multi-objective optimization transparency:** Since real drug design requires balancing potency, selectivity, solubility, synthetic accessibility, and IP novelty simultaneously, the product should expose these trade-offs explicitly (e.g., a Pareto frontier view) rather than collapsing to a single opaque "AI score" that hides which objectives are being traded off
5. **Sequence toward increasing autonomy only as trust is earned:** Roadmap progression from "chemist-reviewed suggestions" → "AI pre-filters most promising 5% for chemist review" → (much later, if ever) "AI-driven autonomous design-make-test loops" — resist pressure to over-promise autonomy before the trust and validation data exist to support it

### Q3–Q16: (Representative additional topics)
- Target identification/validation product workflows (genetic evidence integration, Open Targets-style platforms)
- Virtual screening product design (docking, ML-based scoring functions, active learning for screening)
- ADMET prediction products and their role in de-risking candidate selection
- Antibody/biologics design products vs. small-molecule design product differences
- Multi-omics integration for target discovery product strategy (see Precision Medicine repo overlap)
- Chemical space representation choices (SMILES, graphs, 3D) and their product implications
- Retrosynthesis prediction products and synthesis planning tool integration
- Building products around uncertain/sparse experimental training data (low-N regimes)
- Competitive landscape: platform biotechs (Recursion, Insitro, Isomorphic) vs. tool vendors vs. big pharma internal builds
- IP and freedom-to-operate considerations in AI-generated molecule products
- Benchmark datasets in computational biology (and their known limitations/biases)
- Explaining model predictions to medicinal chemists in chemically meaningful terms

---

## Summary
Drug discovery BioAI products succeed or fail based on how well the PM scopes claims against the true bottleneck in the discovery pipeline — structure/generation is rarely the limiting step; synthesizability, experimental validation throughput, and chemist trust typically are.
