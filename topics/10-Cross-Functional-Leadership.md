# Topic 10: Cross-Functional Leadership

## Overview
Working effectively with computational biologists, wet-lab scientists, clinicians, ML engineers, and regulatory/quality teams as a BioAI PM.

---

### Q1: How do you build effective working relationships with PhD research scientists who may be skeptical of product management's role or value in a scientifically-driven organization?

**A:**
**Common sources of scientist skepticism toward PM:**
- Past experience with PMs who oversimplified or misrepresented scientific nuance to external stakeholders, damaging scientific credibility
- Perception that "product" pressure pushes toward premature shipping before adequate scientific validation
- Concern that PM prioritization frameworks (designed for typical software features) don't map well onto genuinely uncertain research questions

**Trust-building approach:**
1. **Demonstrate genuine curiosity and technical engagement, not performative interest:** Attending lab meetings, asking substantive follow-up questions, and doing the work to understand the actual scientific bottleneck (not just the product requirement) signals genuine partnership rather than extractive requirement-gathering
2. **Explicitly separate "what's scientifically true/uncertain" from "what we choose to ship now":** A PM who conflates business urgency with scientific validity erodes trust quickly; being explicit that a scoped MVP reflects a deliberate risk/scope trade-off — not a claim that the underlying science is more settled than it is — preserves scientific integrity while still making product progress
3. **Advocate for scientists' concerns upward, visibly:** When a scientist raises a legitimate concern about premature claims or inadequate validation, a PM who visibly carries that concern to leadership/sales (rather than quietly overriding it) builds durable trust, even if the final business decision doesn't fully resolve in the scientist's favor
4. **Translate scientific uncertainty honestly to non-technical stakeholders, and credit the source:** Scientists build trust in a PM who accurately represents their caveats and nuance to executives/customers, rather than a PM who translates "we're 70% confident with these three important caveats" into an unqualified "it works" for a sales deck
5. **Involve scientists early in product decisions that affect their work, not just at review/sign-off:** Retroactive scientist review of an already-formed product plan (vs. early co-design) is a common trust-eroding pattern — even when PM must ultimately make the final call under business constraints, early involvement changes the relationship dynamic substantially

### Q2: Describe how you'd structure a productive working relationship between a PM, an ML engineering lead, and a computational biology lead when their priorities are in tension (e.g., ML wants to invest in model architecture, biology wants more assay/data investment).

**A:**
**Structuring the relationship:**
1. **Establish a shared, quantitative decision framework upfront, not case-by-case negotiation:** As discussed in Topic 02 Q3, running learning-curve/ablation analysis to empirically estimate whether the product is data-limited or architecture-limited gives all three functions a shared evidence base to reason from, rather than each function advocating from their own functional bias (ML engineers naturally gravitate toward architecture work; biologists naturally see data gaps) — the PM's role is often to sponsor and facilitate this analysis, not to unilaterally decide
2. **Create a recurring, structured forum for surfacing and resolving these trade-offs, not just ad hoc escalation:** A regular (e.g., biweekly) cross-functional roadmap review where both leads present their view of the highest-leverage next investment, with the PM synthesizing and making an explicit call, prevents trade-off conversations from only happening reactively during conflict
3. **Make trade-off decisions and their rationale visible and revisitable:** Documenting why a particular quarter prioritized architecture vs. data investment (and what evidence would change that decision) allows both functions to understand they were heard even when the decision didn't fully favor their proposal, and creates accountability to revisit if the assumed rationale turns out to be wrong
4. **Protect focused execution time for both functions once a decision is made:** Constant relitigating of prioritization decisions is often more damaging to velocity than the decision itself — part of the PM's role is absorbing pressure to reopen settled decisions prematurely, while remaining genuinely open to revisiting with new evidence
5. **Recognize that both leads may be structurally biased (in good faith) toward their own function's work, and account for this without dismissing their input:** A mature PM neither defers automatically to whichever function argues more forcefully nor discounts functional expertise — they actively seek disconfirming evidence and outside perspective (e.g., customer/wet-lab outcome data) to ground the decision beyond internal advocacy

### Q3–Q15: (Representative additional topics)
- Working with regulatory/quality teams as genuine product co-designers rather than late-stage gatekeepers
- Managing up to executives who may not have deep biology/ML technical background
- Facilitating productive disagreement between clinical advisors with differing clinical judgment
- Building influence without direct authority over research scientists' time allocation
- Onboarding as a new PM into an established scientific team with existing informal prioritization norms
- Structuring effective sprint/roadmap ceremonies for teams blending software and wet-lab timelines
- Handling situations where a scientific co-founder disagrees with product prioritization decisions
- Communicating technical/scientific trade-offs to the board or investors
- Building a shared glossary/mental model across ML, biology, and clinical functions to reduce miscommunication
- Managing conflicting incentives between a research-publication-motivated scientist and product-shipping-motivated engineering timeline

---

## Summary
Cross-functional leadership in BioAI organizations requires a PM to earn credibility through genuine technical engagement and honest representation of scientific uncertainty, while still driving toward decisive, evidence-grounded prioritization across functions with legitimately different (and sometimes structurally biased) perspectives.
