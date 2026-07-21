# Topic 09: Product Case Studies & Prioritization

## Overview
Roadmapping frameworks, 0-to-1 launch strategy, and applied trade-off scenarios common in BioAI PM case-study interview rounds.

---

### Q1: Case study — You're the PM for a protein structure prediction tool used by a biotech's structural biology team. Usage is declining despite the model's accuracy improving with each release. How do you diagnose and respond?

**A:**
**Diagnostic approach:**
1. **Separate "model quality" from "product value" as distinct hypotheses:** Improving accuracy doesn't help if usage decline stems from a different root cause — workflow friction, a competing tool with better integration, or the underlying scientific need shifting (e.g., team's focus moved from single-structure prediction to complex/multi-state prediction the tool doesn't handle well)
2. **Talk to actual users and recently-churned users directly:** Quantitative usage dashboards show *what* is declining, not *why* — direct structured interviews with both active and lapsed users are essential before proposing a fix; a common failure mode is jumping to a technical fix based on a plausible-sounding hypothesis without this grounding
3. **Check for workflow substitution, not just competitor substitution:** Investigate whether users have found an internal workaround (e.g., using a public tool directly, or a colleague's script) that's "good enough" and lower-friction than the product — this is a distinct failure mode from losing to a named competitor and requires a different response
4. **Examine usage patterns by user segment/use case:** Aggregate decline can mask a bifurcated reality — e.g., steady usage for simple single-chain prediction but complete abandonment for complex-assembly use cases where user needs have outgrown the product's capability

**Response framework (contingent on diagnosis):**
- If workflow friction: prioritize integration/UX fixes (e.g., direct integration into their existing structural biology software) over further accuracy improvements
- If capability gap (team's needs evolved beyond single-structure prediction): this may require a genuine roadmap pivot toward complex/multi-state prediction, a much larger investment decision requiring validation that this reflects a broader market shift, not just one account's idiosyncratic need
- If accuracy improvements aren't being communicated/trusted: the issue may be a trust/credibility gap (Topic 07) rather than an actual capability gap — solution is validation transparency, not further model work

**Key interview signal:** A strong answer resists jumping directly to "ship more accuracy" and instead demonstrates structured diagnostic thinking that could lead to several different, non-obvious root causes and correspondingly different roadmap responses.

### Q2: Case study — You have capacity to build exactly one of two features next quarter: (A) a well-scoped improvement to model accuracy for your core existing use case, validated to meaningfully reduce wet-lab false-positive rate, or (B) a new capability opening up an adjacent use case with a large potential new customer segment, but requiring substantial new data collection and unproven demand. How do you decide?

**A:**
**This is intentionally a "it depends" case study — a strong answer surfaces the actual decision-relevant questions rather than picking a side reflexively:**

**Key questions to resolve before deciding:**
1. **What's the actual business stage and runway?** An early-stage company under pressure to prove a wedge use case works decisively should likely favor (A) — deepening proven value with existing customers reduces churn risk and builds the reference customers needed for the next funding/growth stage. A company with an established core product and pressure to expand TAM might reasonably favor (B).
2. **How validated is the "adjacent use case" demand, really?** "Large potential new customer segment" is a claim requiring evidence — has this been validated via customer discovery interviews, or is it an internally-generated hypothesis? Weak validation is a strong argument against betting a full quarter on (B) without a smaller validation step first
3. **What's the true opportunity cost of NOT doing (A)?** If competitors are closing the accuracy/false-positive gap that (A) would address, delaying it may cost more than the case study prompt implies — this requires understanding competitive dynamics, not just the two options in isolation
4. **Can (B) be de-risked with a smaller investment before committing the full quarter?** A strong answer often proposes a third path — a scoped discovery spike or customer validation sprint for (B) (e.g., 2 weeks of customer interviews/landing-page-style demand testing) before committing full quarterly capacity, rather than treating the choice as fully binary with no cheaper validation option
5. **What does "meaningfully reduce wet-lab false-positive rate" actually mean for customer retention/expansion revenue?** If (A)'s benefit is quantifiable in terms of customer-relevant value (e.g., cost savings from fewer wasted wet-lab experiments), this should be weighed concretely against (B)'s speculative TAM expansion, not compared as an apples-to-oranges gut call

**What interviewers are evaluating:** Not which option is "correct" (the prompt is deliberately ambiguous), but whether the candidate demonstrates structured prioritization reasoning, appropriately questions unstated assumptions in the prompt, and considers de-risking options rather than treating it as a forced binary choice.

### Q3–Q15: (Representative additional topics)
- 0-to-1 case study: launching a new BioAI product category with no established market comparables
- Prioritization framework case study: balancing a major pharma partner's custom feature request against platform roadmap coherence
- Case study: responding to a competitor's surprise product launch with overlapping claims
- Resource allocation case study: splitting a small ML team's capacity across model improvement vs. new feature development
- Metrics case study: defining a north-star metric for a platform serving multiple, divergent customer segments
- Stakeholder conflict case study: clinical/scientific team wants more validation rigor before launch; sales wants to ship now
- Roadmap sequencing case study: regulatory-gated feature vs. faster-to-ship non-regulated feature
- Pricing case study: transitioning from a per-seat model to outcome-based pricing for a discovery platform
- Build vs. partner case study: evaluating whether to build a capability in-house or partner/license a specialized vendor
- Crisis case study: a validated model is found post-launch to have a significant blind spot for an important subpopulation

---

## Summary
BioAI product case-study interviews reward structured diagnostic reasoning, willingness to surface and question unstated assumptions, and explicit consideration of de-risking/validation steps over reflexive, single-answer decisiveness — the specific "right answer" matters far less than the quality and rigor of the reasoning process demonstrated.
